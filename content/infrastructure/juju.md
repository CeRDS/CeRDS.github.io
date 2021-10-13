---
title: Juju
---

[JAAS](https://jaas.ai/)

## Client setup

```console
sudo snap install juju --classic
```

## Simplestreams

```console
$ openstack image list
$ cd $(mktemp -d)
$ mkdir simplestreams

$ juju metadata generate-image -a amd64 -d ./simplestreams -i 90303547-6dd7-42f8-a173-fe4f5902ed30 -r RegionOne -s focal -u https://nimbus.pawsey.org.au:5000/v3
$ juju metadata generate-image -a amd64 -d ./simplestreams -i 3a0daf62-69f0-42fd-90ff-e8fea01f7531 -r RegionOne -s bionic -u https://nimbus.pawsey.org.au:5000/v3
Image metadata files have been written to:
/tmp/tmp.GTcJ2OUBed/simplestreams/images/streams/v1.
For Juju to use this metadata, the files need to be put into the
image metadata search path. There are 2 options:

1. For local access, use the --metadata-source parameter when bootstrapping:
   juju bootstrap --metadata-source /tmp/tmp.GTcJ2OUBed/simplestreams [...]

2. For remote access, use image-metadata-url attribute for model configuration.
To set it as a default for any model or for the controller model,
it needs to be supplied as part of --model-default to 'juju bootstrap' command.
See 'bootstrap' help for more details.
For configuration for a particular model, set it as --image-metadata-url on
'juju model-config'. See 'model-config' help for more details.
Regardless of where this attribute is used, it expects a reachable URL.
You need to configure a http server to serve the contents of
/tmp/tmp.GTcJ2OUBed/simplestreams
and set the value of image-metadata-url accordingly.

$ cd simplestreams
$ mc mb store/simplestreams
$ mc cp -r * store/simplestreams
$ mc policy set download store/simplestreams

$ cd $(mktemp -d)
$ mc mirror store/simplestreams
$ juju metadata generate-image -a amd64 -d . -i f210c2f1-2d03-4e07-80ab-cf606d550d69 -r RegionOne -s bionic -u https://nimbus.pawsey.org.au:5000/v3
$ mc mirror . store/simplesreams --overrite
```
Can be accessed via the url https://store.s3.cerds.org.au/simplestreams

## Bootstrap controller

```console
$ juju bootstrap --bootstrap-series=focal --image-metadata-url="https://store.s3.cerds.org.au/simplestreams"
```

## Image convert to RAW

```console
$ wget https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64-disk-kvm.img
$ sha256sum focal-server-cloudimg-amd64-disk-kvm.img | grep 93631c31efe4dbe104ef10ef1b33a8358a444523a5c741294c6e51ce6193cab4
$ qemu-img convert -Oraw focal-server-cloudimg-amd64-disk-kvm.img focal-server-cloudimg.raw
$ openstack image create --container-format bare --disk-format raw --min-disk 3 --min-ram 500 --file focal-server-cloudimg.raw --shared focal-server-cloudimg
```

Download the kvm qcow2 disk images from the official Ubuntu cloud image repository. Nimbus uses Ceph storage as the backing medium for their OpenStack service, for performance/snapshot functionality the image needs to be converted from QCOW2 to RAW before being uploaded to the OpenStack image service within the Project.

## Kubernetes

References

```console
wget https://api.jujucharms.com/charmstore/v5/charmed-kubernetes-545/archive/bundle.yaml
wget https://raw.githubusercontent.com/charmed-kubernetes/bundle/master/overlays/calico-overlay.yaml
wget https://raw.githubusercontent.com/charmed-kubernetes/bundle/master/overlays/openstack-overlay.yaml
```

```console
juju add-model k8s
juju deploy cs:~containers/charmed-kubernetes-545 --overlay overlay.yaml --overlay calico-overlay.yaml --overlay openstack-overlay.yaml --trust
```

overlay.yaml

```YAML
applications:
  easyrsa:
    to: ["lxd:kubernetes-master"]
  etcd:
    to: ["lxd:kubernetes-master"]
  kubernetes-master:
    constraints: cores=4 mem=4G root-disk=16G
    num_units: 3
  kubernetes-worker:
    constraints: cores=8 mem=4G root-disk=16G
    num_units: 3
```

calico-overlay.yaml

```YAML
description: Charmed Kubernetes overlay to add Calico CNI.
applications:
  calico:
    annotations:
      gui-x: '480'
      gui-y: '750'
    charm: cs:~containers/calico
    options:
      cidr: "10.1.0.0/16"
      disable-vxlan-tx-checksumming: false
      ignore-loose-rpf: true
      ipip: "Never"
      manage-pools: true
      nat-outgoing: true
      node-to-node-mesh: true
      veth-mtu: 1500
      vxlan: "Always"
  flannel:
relations:
- - calico:etcd
  - etcd:db
- - calico:cni
  - kubernetes-master:cni
- - calico:cni
  - kubernetes-worker:cni
```

openstack-overlay.yaml

```YAML
description: Charmed Kubernetes overlay to add native OpenStack support.
applications:
  openstack-integrator:
    annotations:
      gui-x: "600"
      gui-y: "300"
    charm: cs:~containers/openstack-integrator
    num_units: 1
    options:
      bs-version: "auto"
      ignore-volume-az: false
      trust-device-path: false
    to: ["lxd:kubernetes-master"]
    trust: true
relations:
  - ['openstack-integrator', 'kubernetes-master:openstack']
  - ['openstack-integrator', 'kubernetes-worker:openstack']
```
