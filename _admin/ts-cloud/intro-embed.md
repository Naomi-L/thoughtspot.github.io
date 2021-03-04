---
title: [ThoughtSpot embedding solution]
last_updated: 3/3/2021
summary: "The ThoughtSpot embedding solution provides SDK and APIs for embedding search, visualizations, pinboards, and the full ThoughtSpot application in a third-party product or business solution."
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
The ThoughtSpot embedding solution enables you to integrate ThoughtSpot functionality and infuse search-driven data and insights into your application, website, portal, product, or business solution. With ThoughtSpot embedding, you can enrich your applications with ThoughtSpot capabilities and provide context-driven analytics with a seamless experience for your application users.

ThoughtSpot provides a suite of APIs, SDK, and developer tools to programmatically embed search analytics, pinboards, visualizations, and even the entire ThoughtSpot application. The embedding solution also provides UI-based functions for customizing and rebranding the embedded ThoughtSpot components.

## Types of embedding

ThoughtSpot supports embedding the full application or its individual components into your business solution.
Based on your business needs and integration environment, you can use one of the following embedding approaches:

**Full application embedding**
You can embed the entire ThoughtSpot application into your host application or portal. Your application users can navigate to the ThoughtSpot UI through a tab or a link. 

**Page-level embedding**
You can embed a ThoughtSpot page and hide the navigation bar, help, and profile links. The host application can allow page-to-page navigation.

**Object-level embedding**
You can embed a specific ThoughtSpot component such as the search functionality, pinboards, or charts.

## ThoughtSpot SpotDev portal

To facilitate faster application integration and assist developer users, ThoughtSpot offers the SpotDev portal.
The SpotDev portal includes a playground for application developers to learn, explore, and interact with the Visual Embed APIs, and build sample content.
The portal also allows developers to customize the ThoughtSpot UI and configure custom actions.

You can access the SpotDev portal from either the ThoughtSpot website, or the **SpotDev** tab in the ThoughtSpot application. To access the **SpotDev** tab in the ThoughtSpot application, you must have administrator or developer user privileges.

For more information, see [ThoughtSpot SpotDev portal]({{ site.baseurl }}/admin/ts-cloud/spotdev-portal.html).

## Embedding methods

You can use one of the following methods to embed a ThoughtSpot functionality or the full application into your host application:

**Using the Visual Embed SDK**  
Using this method, you can install the Visual Embed SDK, import the Javascript library, and programmatically integrate ThoughtSpot application and its components.
The Visual Embed SDK includes separate libraries for embedding ThoughtSpot content, such as the search bar, visualizations, pinboards, and the full application.
For more information, see [Embed content using Visual Embed SDK]({{ site.baseurl }}/admin/ts-cloud/visual-embed-sdk.html).

**Using REST APIs**  
Using this method, you can use the REST APIs to programmatically fetch, embed, and customize data from the ThoughtSpot application.

For more information, see [Embed data using REST APIs]({{ site.baseurl }}/admin/ts-cloud/about-rest-apis.html).

## UI customization and rebranding

If you have embedded the ThoughtSpot application in your host application, you can customize the look and feel of ThoughSpot UI to match your organization’s branding guidelines.

You can customize the ThoughtSpot application UI either from the **Admin** console, or by using the style customization settings in the SpotDev portal.

For more information, see [Customize embedded content]({{ site.baseurl }}/admin/ts-cloud/customize-style-spotdev.html).

## Custom actions

The ThoughtSpot embedding solution allows you to build additional actions to the embedded pinboards and visualizations.

For example, if you want to email a pinboard, you can create a custom action and add it to your menu component on the Pinboards page.

For more information, see [Add custom actions]({{ site.baseurl }}/admin/ts-cloud/customize-actions-spotdev.html).
