---
title: OpenStack
date: 2021-09-23T09:33:00+08:00
draft: false
---

```bash
# Create initial CVL Stack
openstack --os-cloud nimbus-cvl stack create -e env.yaml -t stack.yaml cvl

# Update Stack on changes
openstack --os-cloud nimbus-cvl stack update -e env.yaml -t stack.yaml cvl
```

* Example Environment file

{{< render-code file="/static/openstack/env.yaml" language="yaml" >}}

* Heat Orchestration Template (HOT)

{{< render-code file="/static/openstack/server.yaml" language="yaml" >}}

{{< render-code file="/static/openstack/stack.yaml" language="yaml" >}}
