---
title: [GCP configuration options]


last_updated: 3/17/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
ThoughtSpot can be deployed in your GCP environment by deploying compute (VM) instances in your VPC as well as an underlying persistent storage infrastructure. Currently we support Zonal SSD persistent disk for persistent storage. For more information, see [Zonal Persistent SSD disks](https://cloud.google.com/compute/docs/disks/#pdspecs){:target="_blank"} in Google's Cloud documentation.

All GCP VMs (nodes) in a ThoughtSpot cluster must be in the same zone
(and, therefore, also in the same region). ThoughtSpot does not support deploying VMs (nodes) of the same cluster across zones. For more information, see [Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/){:target="_blank"} in Google's Cloud documentation.

## ThoughtSpot GCP instance types

| Per VM user data capacity | Instance type | CPU/RAM | Recommended per-VM <br>Zonal Persistent SSD Disk volume | Required root volume capacity |
| --- | --- | --- |--- | --- |
| 208 GB | n1-highmem-64 | 64/416 | 2x 1 TB | 200 GB for each node |
| 312 GB | n1-highmem-96 | 96/624 | 2x 1.5 TB | 200 GB for each node |
| 100 GB | n1-highmem-32 | 32/208 | 2X 400 GB | 200 GB for each node |
| 20 GB | n1-highmem-16 | 16/122 | 2X 400 GB | 200 GB for each node |
| 180 GB | n1-standard-96 | 96/330 | 2X 1 TB | 200 GB for each node |


For most instances, the per VM recommended user data capacity is set at 50% of the available RAM on the instance. However, in the case of our 16CPU/122GB RAM and 32CPU/208GB RAM instances, we support user data sizes below those numbers to budget for application overhead.
