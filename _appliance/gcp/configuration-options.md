---
title: [GCP configuration options]
keywords: GCP, configuration
tags: [performance]
last_updated: 3/18/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
ThoughtSpot has performed extensive testing on various Google Cloud Platform
(GCP) configurations for best performance, load balancing, scalability, and
reliability.

You can find information here on which configuration of memory, CPU, storage,
and networking capacity you should be running for your instances.

## ThoughtSpot GCP instance types

<table width="853">
    <colgroup>
      <col width="110" />
      <col width="110" />
      <col width="110" />
      <col width="105" />
      <col width="140" />
      <col width="95" />
    </colgroup>
	<tr>
      <td><br /></td>
      <td colspan="2"><p dir="ltr"><center><strong>Use case</strong></center></p></td>
      <td><br /></td>
      <td><br /></td>
      <td><br /></td>
      <td><br /></td>
    </tr>
    <tr>
      <td><p dir="ltr"><strong>Data shape</strong></p></td>
      <td><p dir="ltr"><strong>Total cluster <BR>data size</strong></p></td>
      <td><p dir="ltr"><strong>Per VM <BR>Data capacity</strong></p></td>
      <td><p dir="ltr"><strong>Recommended <BR>Instance type</strong></p></td>
      <td><p dir="ltr"><strong>vCPU/RAM</strong></p></td>
	  <td><p dir="ltr"><strong>Boot disk</strong></p></td>
	  <td><p dir="ltr"><strong>Data volumes</strong></p></td>
    </tr>
    <tr>
      <td><p dir="ltr">Standard</p>
        <p dir="ltr">(1KB/row)</p></td>
      <td><p dir="ltr">Up to 3 TB </p></td>
      <td><p dir="ltr">208 GB</p></td>
      <td><p dir="ltr">n1-highmem-64</p></td>
      <td><p dir="ltr">64/416</p></td>
		<td><p dir="ltr">250 GB for each ndoe</p></td>
		<td><p dir="ltr">2X 1 TB</p></td>
    </tr>
    <tr>
      <td><br /></td>

      <td><p dir="ltr">&gt;3 TB</p></td>
      <td><p dir="ltr">312 GB</p></td>
      <td><p dir="ltr">n1-highmem-96</p></td>
      <td><p dir="ltr">96/624</p></td>
		<td><p dir="ltr">250 GB for each node</p></td>
		<td><p dir="ltr">2X 1.5 TB</p></td>
    </tr>
    <tr>
      <td><br /></td>

      <td><p dir="ltr">Up to 100 GB</p></td>
      <td><p dir="ltr">100 GB</p></td>
      <td><p dir="ltr">n1-highmem-32<sup>b</sup></p></td>
      <td><p dir="ltr">32/208</p></td>
		<td><p dir="ltr">250 GB for each node</p></td>
		<td><p dir="ltr">2X 400 GB</p></td>
    </tr>
    <tr>
      <td><br /></td>

      <td><p dir="ltr">Up to 20 GB</p></td>
      <td><p dir="ltr">20 GB</p></td>
      <td><p dir="ltr">n1-highmem-16<sup>b</sup></p></td>
      <td><p dir="ltr">16/122</p></td>
		<td><p dir="ltr">250 GB for each node</p></td>
		<td><p dir="ltr">2X 400 GB</p></td>
    </tr>
    <tr>

      <td><p dir="ltr">Thin rows</p>
        <p dir="ltr">(&lt;300 bytes/row)</p></td>
      <td><p dir="ltr">Any</p></td>
      <td><p dir="ltr">180 GB</p></td>
      <td><p dir="ltr">n1-standard-96</p></td>
      <td><p dir="ltr">96/360</p></td>
		<td><p dir="ltr">250 GB for each node</p></td>
		<td><p dir="ltr">2X 1 TB</p></td>
    </tr>
	<tr>

      <td colspan="6"><p dir="ltr">(a) Use the sizing calculators on each cloud provider to plug in expected customer discounts to arrive at the proper recommended cloud instance type.</p><p>(b) Use the small and medium instance-type configuration. Refer to: <a href="/5.2/appliance/cloud.html#use-small-and-medium-instance-types">Use small and medium instance types.</a></p>
       </td>
    </tr>
  </table>

GCP provides several storage types and media options. ThoughtSpot requires [attached storage](https://cloud.google.com/compute/docs/disks/) and persistent disks.        |

ThoughtSpot uses only persistent storage options. Instance storage (also known
as "local storage") is not used for ThoughtSpot deployments on GCP.

For most instances, the per VM recommended user data capacity is set at 50% of the available RAM on the instance. However, in the case of our 16CPU/122GB RAM and 32CPU/208GB RAM instances, we support user data sizes below those numbers to budget for application overhead.
