---
title: [Cloud overview]
keywords: setup,cluster,cloud,aws,azure,gcp
last_updated: 6/16/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
ThoughtSpot currently supports the following cloud deployments:

- [Amazon Web Services (AWS) EC2]({{ site.baseurl }}/appliance/aws/about-aws.html)
- [Microsoft Azure]({{ site.baseurl }}/appliance/azure/about-azure.html)
- [Google Cloud Platform (GCP)]({{ site.baseurl }}/appliance/gcp/about-gcp.html)

This page provides recommendations and best practices for ThoughtSpot cloud deployments, including how to set up your ThoughtSpot instance and how to reduce infrastructure costs.

## ThoughtSpot cloud instance types

Refer to the following guidelines for how to set up ThoughtSpot on each cloud service:

- [AWS instance types]({{ site.baseurl }}/appliance/aws/configuration-options.html)
- [Azure instance types]({{ site.baseurl }}/appliance/azure/configuration-options.html)
- [GCP instance types]({{ site.baseurl }}/appliance/gcp/configuration-options.html)

## Reducing your cloud infrastructure costs

ThoughtSpot recommends following these guidelines to help reduce the cost of your cloud deployment.  

### Use small and medium instance types

For ThoughtSpot customers who are deploying their instance with lower data sizes (<=100 GB), ThoughtSpot supports “small” (20 GB data) and “medium” (100 GB data) instance types, as provided at the links above, to help reduce the costs of cloud infrastructure. These are instances with lower CPU/RAM sizes (16/32 vCPU and 128 GB/256 RAM). Additional configuration is required before any data can be loaded onto these instances.

Please contact ThoughtSpot support for assistance with this configuration.

### Shut down and restart your cluster

If you do not need your ThoughtSpot cluster to be up and running 24/7, you can shut down your cluster and restart it during normal usage hours to save on the infrastructure costs of running ThoughtSpot instances in cloud provider environments.

To shut down and restart your cluster, do the following in the tscli:

1. Ensure there are no issues with the cluster by running: `$ tscli cluster check`

   The above command should return no failure messages.

2. Stop the cluster by running: `$ tscli cluster stop`

   Wait until you see the message: “Done stopping cluster”

3. Go to your cloud provider's console and shut down all of the ThoughtSpot VMs in your cluster.

4. When you are ready to use ThoughtSpot again, start up your node VMs.

5. Restart your cluster by running:
	`$ tscli cluster start`

   You should see the message: ”Started pre-existing cluster”

   Depending on the size of your cluster, you may need to wait several minutes before the system is fully usable again. For massive clusters with hundreds of GBs of data, this time to readiness may be several hours. Assess time to readiness on a per-cluster basis. Make sure you budget for this startup time to ensure that the system is fully operational before advertising it as ready and usable.

6. Ensure that your cluster is ready for use by running:
	`$ tscli cluster status`

	The following messages are displayed to indicate your cluster is up and running: <br> 	
  `...`
  `Cluster: RUNNING` <br>
  `Database: READY` <br>
  `Search Engine: READY`
