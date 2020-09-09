---
title: [Set up AWS for ThoughtSpot]
keywords: AWS, AMI
last_updated: 1/21/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---

After you've determined your configuration options, you must set up your virtual machines (VMs) on AWS using a ThoughtSpot Amazon Machine Image (AMI). Please read further for next steps.

## Overview of ThoughtSpot setup in AWS
The high-level process for setting up ThoughtSpot in AWS is the following:
1. Gain access to ThoughtSpot AMIs.
2. Choose a VM instance configuration recommended by ThoughtSpot.
3. Work with ThoughtSpot to set up your ThoughtSpot cluster.
4. Open the required network ports for communication for the nodes in your cluster and end users.
5. [Deploy your AWS instance using CloudFormation CLI.]({{ site.baseurl }}/appliance/aws/deploy-aws-cloud-formation.html)

## About the ThoughtSpot AMI

The ThoughtSpot AMI comes provisioned with the custom ThoughtSpot image to make deploying simple. An Amazon Machine image (AMI) is a preconfigured template that provides the information required to launch an instance. You must specify an AMI when you launch an instance in AWS. An AMI includes the following:

-   A template for the root volume for the instance (for example, an operating system, an appliance server, and applications).
-   Launch permissions that control which AWS accounts can use the AMI to launch instances.
-   A block device mapping that specifics the volumes to attach to the instance when it’s launch.

The ThoughtSpot AMI has specific applications on a CentOS base image. The EBS volumes required to install ThoughtSpot in AWS are included in the AMI. When you launch an EC2 instance from this image, the EBS volumes are automatically sized and provisioned.

##  Prerequisites

ThoughtSpot instances on AWS need AWS EC2 instances to be provisioned in the AWS account before ThoughtSpot can be installed and launched. Please make sure you follow the guidelines below for setting up your EC2 details:
- Sign in to your AWS account from the [AWS Amazon sign in page](https://console.aws.amazon.com/console/home).
- Copy the suitable ThoughtSpot public AMI which has been made available in N. California region to your AWS region. Details for the default AMI are:  
**AMI Name**: thoughtspot-image-20190614-0123e58511a-prod-2tb-ebs  
**AMI ID**: ami-0e8118e34275009d1  
**Region**: N. California
- Default AMI has 2x1 TB attached EBS storage volumes to support the maximum capacity of 250 GB data per ThoughtSpot node.
- For customers with smaller data sets, a custom AMI (Name = thoughtspot-image-20190614-0123e58511a-prod-800gb-ebs, ID = ami-0b1a0f31eb913e45b) has also been made available. VMs based on this configuration will suffice for data sizes up to 800 GB/node.
- Choose the appropriate EC2 instance type: See [ThoughtSpot cloud instance types]({{ site.baseurl }}/appliance/cloud.html#thoughtspot-cloud-instance-types) for supported instance types.
- Networking requirements: 10 GbE network bandwidth is needed between the VMs. This is the default for the VM type recommended by ThoughtSpot.
- Security: The VMs that are part of a cluster need to be accessible by each other, which means they need to be on the same Amazon Virtual Private Cloud (VPC) and subnetwork. Additional external access may be required to bring data in/out of the VMs to your network.
- Number of EC2 instances needed: Based on the datasets, this number will vary. Please check [ThoughtSpot cloud instance types]({{ site.baseurl }}/appliance/cloud.html#thoughtspot-cloud-instance-types) for recommended nodes for a given data size.
- Staging larger datasets (> 50 GB per VM), may require provisioning additional attached EBS volumes that are SSD (gp2).

## Setting up your ThoughtSpot cluster in AWS

The examples/screenshots below are for N. California region. Your own region may be different.

To set up a ThoughtSpot cluster in AWS, do the following:

1. Navigate to the EC2 service dashboard by clicking **Services**, then **EC2**.

     ![]({{ site.baseurl }}/images/navigate_to_ec2_dashboard.png "Navigate to the EC2 Dashboard")

2. Make sure your selected region is correct in the top right corner of the dashboard.
   If not, select a different region you would like to launch your instance in.

     ![]({{ site.baseurl }}/images/select_region.png "Select a region to launch your instance in")

3. Start the process of launching a VM by clicking **Launch Instance**.

     ![]({{ site.baseurl }}/images/launch_instance.png "Launch an instance")

4. Click the **My AMIs** tab, find the ThoughtSpot AMI from the list, and click **Select**.

     ![]({{ site.baseurl }}/images/select_the%20ami.png "Select the AMI")

5. On the Choose an Instance Type page, select a ThoughtSpot-supported instance type.
   (See [ThoughtSpot cloud instance types]({{ site.baseurl }}/appliance/cloud.html#thoughtspot-cloud-instance-types) )        
6. Click **Next: Configure Instance Details**.
7. Configure the instances by choosing the number of EC2 instances you need.
   The instances must be on the same VPC and subnetwork. ThoughtSpot will set up the instances to be in the same ThoughtSpot cluster.
8. Click **Next: Add Storage**.
    The default storage specified by the ThoughtSpot AMI should be populated. Optionally, you can add extra storage. Based on the dataset size requirement, you might need to provision and prepare (formatting/file system placement) an extra storage of 400 GB per VM that is SSD gp2 provisioned.
9. When you are done modifying the storage size, Click **Next: Add Tags**.
10. Set a name for tagging your instances and click **Next: Configure Security Group**.
11. Select an existing security group to attach new security groups to so that it meets the security requirements for ThoughtSpot.

    {{site.data.alerts.tip}} <b>Security setting for ThoughtSpot</b><ul><li>The VMs need intragroup security, i.e. every VM in a cluster must be accessible from one another. For easier configuration, ThoughtSpot recommends that you enable full access between VMs in a cluster.</li> <li>Additionally, more ports must be opened on the VM to provide data staging capabilities to your network. Check <a href="https://docs.thoughtspot.com/5.2/appliance/firewall-ports.html">Network policies</a> to determine the minimum required ports that must be opened for your ThoughtSpot appliance.</li></ul>
    {{site.data.alerts.end}}

12.  Click **Review and Launch**. After you have reviewed your instance launch details, click **Launch**.
13.  Choose a key pair.
      A key pair consists of a public and private key used to encrypt and decrypt login information. If you don’t have a key pair, you must create one, otherwise you won’t be able to SSH into the AWS instance later on.
14.  Click **Launch Instance**. Wait a few minutes for it to fully start up. Once it has started up, it will show up on the EC2 console.
15.  Contact ThoughtSpot Support to complete your ThoughtSpot installation.
     They will set up the VM instances to be part of the cluster.
16.  When the setup is complete, you can load data into ThoughtSpot for search analytics.    

## Open the required network ports

See [Network policies]({{ site.baseurl }}/appliance/firewall-ports.html) for a complete list of network ports that must be open for traffic from end users as well as between ThoughtSpot nodes in a cluster.

These are the minimum ports required for operations and debugging:

|Port|Protocol|Service|
|----|--------|------------|
|22|SSH|Secure Shell access|
|443|HTTPS|Secure Web access|
|12345|TCP|ODBC and JDBC drivers access|

## Additional resources
As you develop your expertise in AWS VM creation, we recommend the following ThoughtSpot U course:
* [Node Configuration: AWS](https://training.thoughtspot.com/node-network-configuration/484851){:target="_blank"}

See other training resources at <br/>
<a href="https://training.thoughtspot.com/" target="_blank"><img src="{{ "/images/ts-u.png" | prepend: site.baseurl  }}" alt="ThoughtSpot U"></a>

## Related information  

[EC2 Best Practices](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html)
[Loading data from an AWS S3 bucket]({{site.baseurl }}/admin/loading/use-data-importer.html#loading-data-from-an-aws-s3-bucket)
