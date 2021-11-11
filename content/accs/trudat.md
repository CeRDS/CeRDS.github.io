---
name: TruDat
title: TruDat (MyTARDIS) data store
draft: false
---
Data management for scientific instruments

TruDat is a branded deployment of [MyTardis](http://www.mytardis.org/) for the storage and pre-processing
of instrumentation data. Located within Pawsey infrastructure the data is in close proximity to
Cloud and HPC infrastructure as well as the Characterisation Virtual Laboratory (CVL) instance it cohabits with.

## Great care is taken with your data

Example nightly backup report (NB: numbers would not depict current storage state)
```
Number of files: 329,566 (reg: 197,234, dir: 132,331, link: 1)
Number of created files: 58 (reg: 39, dir: 19)
Number of deleted files: 0
Number of regular files transferred: 39
Total file size: 8,477,695,618,674 bytes
Total transferred file size: 3,624,131,266 bytes
Literal data: 3,624,131,266 bytes
Matched data: 0 bytes
File list size: 2,075,091
File list generation time: 0.001 seconds
File list transfer time: 0.000 seconds
Total bytes sent: 532,329
Total bytes received: 1,947,358,526

sent 532,329 bytes  received 1,947,358,526 bytes  1,848,970.91 bytes/sec
total size is 8,477,695,618,674  speedup is 4,352.24
Runtime (mins): 17
0m0.000s 0m0.005s
0m42.104s 0m29.418s

Filesystem                                Size  Used Avail Use% Mounted on
//drive.irds.uwa.edu.au/SCI-MYTARDIS-001  9.9T  9.0T  871G  92% /Volumes/drive.irds.uwa.edu.au/SCI-MYTARDIS-001
```

The above report example is sent to the CeRDS team to ensure that the daily backup has been completed and is 
always in a healthy state.

Other stuff that may interest you...

The TruDat service and in fact Pawsey infrastructure has no access to the backup service at all and the process is triggered
via a pull operation from within the UWA security context. The process and data communication is within a virtual private network (VPN)
verifying the endpoints and encrypting the transfer. The transfer incorporates integrity checks to ensure data consistency and 
the connection from the backup service to the IRDS storage volume is protected via Kerberos. Once in IRDS your data enteres the 
CentralIT controlled backup process.

In short, your data is verified, backed up, has security issolation at both infrastructural and technical team levels. Please feel
free to make contact if you wish for any further details or have any concerns.
