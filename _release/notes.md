---
title: ["5.2 Release Notes"]
toc: false
keywords: "release notes"
last_updated: 04/09/20
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---

ThoughtSpot version 5.2.3 is now available. These release notes include information about new and enhanced features.

For a complete list of issues that we fixed in this release, see [Fixed issues]({{ site.baseurl }}/release/fixed.html).

* [Supported Upgrade Paths](#supported-upgrade-paths)
* [Mobile App](#mobile-app)
* [5.2 New Features](#52-new)

## Supported Upgrade Paths

If you are running one of the following versions, you can upgrade to the 5.2.3 release
directly:

* 5.0.x to 5.2.3
* 5.1.x to 5.2.3

This includes any hotfixes or customer patches on these branches.

If you are running a different version, you must do a multiple pass upgrade.
First, upgrade to one of the above versions, and then to the 5.2.3 release.

## Mobile App

ThoughtSpot mobile version 1.1.2 now supports auto-redirect Single Sign-On (SSO) for configured clusters.

For more information, see [Mobile]({{ site.baseurl }}/admin/mobile/use-mobile.html).

{: id="52-new"}
## 5.2 New Features and Functionality

For a complete list of issues that we fixed in this release, see [5.2 Fixed issues]({{ site.baseurl }}/release/fixed.html#5-2).

### ThoughtSpot mobile beta

Our brand new mobile app is now available in beta on iOS devices for customers with ThoughtSpot 5.1 or later. If you want to try it, fill out this form: <a href="https://docs.google.com/forms/d/e/1FAIpQLSfs8SyPeXdiL5lpcp8tulPLLoaXbNJcpNgIuFcU6pr34vOx6A/viewform" target="_blank">ThoughtSpot Mobile App Beta Access.</a>

### Favorites

If you frequently go back to look at certain Answers or Pinboards, you can now use Favorites to find them faster than ever before. Click the Favorite icon ![Favorite icon]({{ site.baseurl }}/images/icon-favorite.png){: .inline} of an Answer or Pinboard, and it will be added to the Favorites list on the Answers and Pinboard pages, as well as the ThoughtSpot home page.

### Custom calendars

You can now add a custom fiscal calendar for your company. This is important if your company has a fiscal year that is different than the calendar year. With your custom calendar, you can be sure when you search for ‘last quarter’ that you will get results that reflect your company's last fiscal quarter. For details refer to [Create a custom calendar]({{ site.baseurl }}/admin/setup/set-custom-calendar.html#creating-a-custom-calendar).

### Ask an expert

Sometimes making a data-based decision is so challenging that you need an expert opinion from someone else. This is what the 'Ask an expert' feature is all about. Below the results of a Search or Answer, click **Ask an expert** to write a question to the ThoughtSpot users in your organization who are very familiar with the data set used for that search.  When you send your question, you automatically provide the search terms and the results. With this information, an expert in your organization will have the context they need to provide clarification and updated search terms, if necessary. For details refer to [Ask an expert]({{ site.baseurl }}/end-user/search/ask-an-expert.html).

### IN subquery for filtering

With the IN subquery feature, you can now combine two queries into one without ever leaving the Search bar. For example, you could do a query like this: `What were the sales this month from my top 10 stores in terms of net margin last month`. That’s actually two queries. The first one searches for the top 10 stores in terms of net margin last month, and the second one searches for the sales of those stores this month.  Before the IN subquery, you would need to save a View to get this answer. For details refer to [Using the in keyword for nested searches]({{ site.baseurl }}/complex-search/in-keyword-searches.html).

### Support for small and medium cloud instance types

One size does not fit all when it comes to the cloud. You need flexibility to choose the right cloud instance type for your ThoughtSpot deployment. If you are deploying an instance with lower data sizes (<=100 GB), ThoughtSpot now supports “small” (20 GB data) and “medium” (100 GB data) instance types to help reduce the costs of cloud infrastructure. These are instances with lower CPU/RAM sizes (16/32 vCPU and 128 GB/256 RAM). For details refer to [ThoughtSpot cloud instance types]({{ site.baseurl }}/appliance/cloud.html#thoughtspot-cloud-instance-types).

### Cluster shutdown and restart to save infrastructure costs

If you don't need your ThoughtSpot cluster up and running 24/7, you can shut it down and restart it during normal usage hours. This allows you to save on the infrastructure costs of running ThoughtSpot VM instances in cloud environments. For details refer to [Shut down and restart your cluster]({{ site.baseurl }}/appliance/cloud.html#reducing-your-cloud-infrastructure-costs).

### Ability to upload .CSV data from an AWS S3 bucket

If you have data in .csv format stored in an AWS bucket, you can now load it directly into ThoughtSpot, using the **tsload** command. For details, refer to: [Loading data from an AWS S3 bucket]({{ site.baseurl }}/admin/loading/use-data-importer.html#loading-data-from-an-aws-s3-bucket).

### Allow users to sign up for ThoughtSpot

You can now allow people in your organization to sign up for ThoughtSpot by clicking a button on the sign-in page. When a person clicks the sign-up button, they go to a sign-up page that you’ve already set up outside of ThoughtSpot. This can be any page you want to use for registering new users.
For details, refer to: [Allow users to sign up]({{ site.baseurl }}/admin/users-groups/sign-up.html).

### Improved Japanese date keywords

Japanese-language users now have a more natural way of expressing date phrases in their queries.
For details, refer to: [Japanese (日本語) date keyword reference]({{ site.baseurl }}/reference/keywords-ja-JP.html).

### New languages

ThoughtSpot now supports seven new languages, available in the Profile page:
* Danish
* Norwegian
* Swedish
* Finnish
* Portuguese (Portugal)
* Spanish (Spain)
* Italian
* English (Australia)

### One-to-one joins in worksheets

When editing joins within a worksheet, you can now specify a join cardinality of One to One, as well as Many to One.
