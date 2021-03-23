---
title: ["ThoughtSpot Cloud Release Notes"]
toc: false
last_updated: 3/9/2021
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---

ThoughtSpot 7 Cloud March version (ts7.mar.cl)  is now available.

These release notes include information about new and enhanced features.

To see what's new in Free Trial, read <a href="{{ site.baseurl }}release/free-trial.html">Free Trial Release Notes</a>.

{: id="new"}
## New Features and Functionality

{% include content/new-features-cloud-release.md %}

{: id="2020-february"}
## ThoughtSpot 7 Cloud February Release (ts7.feb.cl)

<ul>
<li><a href="{{ site.baseurl }}#feb-cloud-analyst">For the Analyst</a></li>
<li><a href="{{ site.baseurl }}#feb-cloud-business-user">For the Business User</a></li>
<li><a href="{{ site.baseurl }}#feb-cloud-data-engineer">For the Data Engineer</a></li>
<li><a href="{{ site.baseurl }}#feb-cloud-it-ops-engineer">For the IT Ops Engineer</a></li>
</ul>

<h3><a id="feb-cloud-analyst"></a>For the Analyst</h3>

<dl>
  <dlentry id="scriptability">
    <dt>Scriptability</dt>
    <dd><ul><li><p>You can now create and edit joins at the table level using TML, including range and generic joins. You must edit these joins from the source table, not the destination table. Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/tml.html#syntax-tables">ThoughtSpot Modeling Language</a>.</p>
    <p>This feature is in Beta. To enable it, <a href="{{ site.baseurl }}/admin/misc/contact.html">contact ThoughtSpot Support</a>.</p></li>
    <li><strong>Export custom SpotApps</strong>: Support for custom SpotApp export is now GA and on by default. You can now export your own custom SpotApps, or collections of Scriptable ThoughtSpot Answers, Pinboards, Views, tables, and Worksheets, packaged together as a zip file. Simply navigate to <strong>Data > SpotApps</strong> and choose the objects you would like to include in a custom SpotApp. Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/app-templates.html">SpotApps</a>.</li></ul>
</dd></dlentry>

 <dlentry id="simplified-join-creation">
  <dt>Simplified join creation</dt>
  <dd>This release makes creating and editing joins from a table more flexible and intuitive. Our new joins interface allows you to define and edit the join type and cardinality at the table level, where previously this was only possible at the Worksheet level. Refer to <a href="{{ site.baseurl }}/admin/worksheets/add-joins.html#table-join">Table joins</a>.
</dd></dlentry>

<dlentry id="pinboard-download-api">
  <dt>Pinboard Download API</dt>
  <dd>Use the new Pinboard Download API to programmatically download Pinboards, or specific visualizations from the Pinboards, as PDFs. Refer to <a href="{{ site.baseurl }}/reference/api/pinboard-download-api.html">Pinboard Download API</a>.
</dd></dlentry>

<dlentry id="spotiq-analyze">
  <dt>Support for SpotIQ Analyze</dt>
  <dd><p>In this release, ThoughtSpot Cloud adds support for SpotIQ analyze. Now you can analyze any answer, pinboard visualization, or data source to generate instant insights, by clicking the SpotIQ analyze button <img src="{{ site.baseurl }}/images/icon-lightbulb.png" alt="SpotIQ analyze icon" class="inline"/>. For more information, see <a href="{{ site.baseurl }}/spotiq/customization.html">Custom SpotIQ analysis</a>.</p></dd></dlentry>

</dl>

<h3><a id="feb-cloud-business-user"></a>For the Business User</h3>

<dl>
<dlentry id="home-page-shortcuts">
<dt>Home page shortcuts</dt>
<dd><p>You can now create and access quick links to your most-used Answers and Pinboards from the ThoughtSpot One home page. Refer to <a href="{{ site.baseurl }}/end-user/thoughtspot-one/thoughtspot-one-homepage.html#quick-links">Home page shortcuts</a>.</p>
<p>ThoughtSpot One may be off in your environment. To enable ThoughtSpot One, <a href="{{ site.baseurl }}/admin/misc/contact.html">contact ThoughtSpot Support.</a></p></dd>
</dlentry>

<dlentry id="internet-explorer">
  <dt>Deprecation of Internet Explorer</dt>
<dd>ThoughtSpot browser support for Internet Explorer is now deprecated. Refer to <a href="{{ site.baseurl }}/end-user/accessing.html">ThoughtSpot browser access</a> for a list of supported browsers.</dd>
</dlentry>

</dl>

<h3><a id="feb-cloud-data-engineer"></a>For the Data Engineer</h3>

<dl>
<dlentry id="embrace">
<dt>Embrace</dt>
<dd>Embrace now supports security passthrough for Snowflake and Google BigQuery using OAuth for authentication and authorization. For more information, see <a href="{{ site.baseurl }}/admin/ts-cloud/ts-cloud-embrace-snowflake-add-connection.html">Snowflake</a>, and <a href="{{ site.baseurl }}/admin/ts-cloud/ts-cloud-embrace-gbq-add-connection.html">Google BigQuery</a>.</dd>
<dd>Embrace passthrough functions are available for Snowflake. Passthrough functions allow you to send custom SQL expressions directly to your Snowflake database without being interpreted by ThoughtSpot. For more information, see <a href="{{ site.baseurl }}/admin/ts-cloud/ts-cloud-embrace-snowflake-passthrough.html">Passthrough functions for Snowflake</a>.</dd>
<dd>Embrace now supports Oracle Autonomous Database <span class="label label-beta">Beta</span>. This feature is in beta and disabled by default. To enable this feature, contact <a href="{{ site.baseurl }}/admin/misc/contact.html">ThoughtSpot Support</a>.</dd>
</dlentry>
</dl>

<h3><a id="feb-cloud-it-ops-engineer"></a>For the IT Ops Engineer</h3>

<dl>
<dlentry id="new-region-support">
<dt>New region support</dt>
<dd>ThoughtSpot Cloud is now available in the following 2 regions, in addition to US East and West, Sydney, and Ireland:
<ul><li>Frankfurt</li>
<li>Singapore</li></ul></dd></dlentry>

<dlentry id="search-answers-pinboard">
<dt>Search on Answers Pinboard</dt>
<dd>There are several changes to the behavior of the <a href="{{ site.baseurl }}/admin/thoughtspot-one/query-intelligence-pinboard.html">Stats and Trends for Search on Answers Pinboard</a>:
<ul>
<li>The Pinboard and its underlying Worksheet, <strong>Discover Monitoring Data</strong>, are now accessible only to admins by default. Admins can share the Pinboard and Worksheet with anyone else who might need this information.</li>
<li>The Pinboard is populated with your users' Search on Answers data by default. You do not need to contact ThoughtSpot Support to see your users' Search on Answers data in the Pinboard.</li></ul></dd>
</dlentry>

<dlentry id="pinboard-download-control">
<dt>Pinboard download control</dt>
<dd><p>You can now limit or remove the options ThoughtSpot provides for downloading Pinboards and their visualizations. You can allow users to only download Pinboard visualizations in a specific format (such as .csv), or you can restrict access to downloading Pinboards and their visualizations altogether.</p>
<p>This is a cluster-level feature. You cannot configure permissions for specific users.</p>
<p>This is an embed-only feature. To enable this functionality, <a href="{{ site.baseurl }}/admin/misc/contact.html">contact ThoughtSpot Support</a>.</p></dd>
</dlentry>

<dlentry id="consumption-based-pricing">
<dt>Consumption-based pricing</dt>
<dd>ThoughtSpot now offers consumption, or usage, based pricing. Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/consumption-pricing.html">Consumption-based pricing</a> and the <a href="{{ site.baseurl }}/admin/ts-cloud/consumption-pricing-faq.html">Consumption pricing FAQ</a>. To compare consumption- and capacity-based pricing, refer to <a href="https://www.thoughtspot.com/pricing" target="_blank">ThoughtSpot pricing</a>.</dd>
</dlentry>
</dl>

{: id="2020-december"}
## ThoughtSpot 6 Cloud December Release (ts6.dec.cl)

<h3>Scriptability</h3>
There are several new features for Scriptability:
<ul>
<li><p><strong>Export custom SpotApps</strong>: You can now export your own custom SpotApps, or collections of Scriptable ThoughtSpot Answers, Pinboards, Views, tables, and Worksheets, packaged together as a zip file. Simply navigate to <strong>Data > SpotApps</strong> and choose the objects you would like to include in a custom SpotApp. Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/app-templates.html">SpotApps</a>.</p>
<p>This feature is in Beta. To enable it, <a href="{{ site.baseurl }}/admin/misc/contact.html">contact ThoughtSpot Support</a>.</p></li>
<li><strong>GUID handling</strong>: ThoughtSpot now recognizes pre-existing GUIDs upon import and asks if you would like to update the existing object or create a new one. Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/scriptability.html">Scriptability</a>.</li>
<li>ThoughtSpot Scripting Language is now called ThoughtSpot Modeling Language.</li></ul>

<h3>Information Center</h3>
ThoughtSpot has a new Information Center, accessible from the help icon <strong>?</strong> next to your profile on the top navigation bar. This new help menu contains many useful resources, including a navigation overview, several training videos, and links to more help across the ThoughtSpot product, community, training, and documentation. Refer to <a href="{{ site.baseurl }}/end-user/help-center/what-you-can-find-in-the-help-center.html">More help and support</a>.

<h3>Embrace passthrough functions</h3>
Embrace now supports passthrough functions which allow you to send SQL expressions directly to the database, without being interpreted by ThoughtSpot. If you have custom database functions that ThoughtSpot doesn't support, you can use these new passthrough functions in the ThoughtSpot Formula Assistant to call your custom functions. Refer to <a href="{{ site.baseurl }}/reference/formula-reference.html#passthrough-functions">Embrace passthrough functions</a>.

<h3>New language support</h3>

Starting in the December Cloud release, ThoughtSpot supports the following new locale, including support for language keywords that can be used in the search bar:

<ul>
<li> English (India) </li>
</ul>

To set locale to English (India), click the user icon in the top right corner to navigate to the <strong>Profile</strong> page, and select locale under <strong>Preferences</strong>.

{: id="2020-october"}
## ThoughtSpot 6 Cloud October Release (ts6.oct.cl)

<h3>New Home page</h3>

The ThoughtSpot <a href="{{ site.baseurl }}/end-user/thoughtspot-one/thoughtspot-one-homepage.html">Home page</a> allows you to access all your essential actions as a business user. You can:

<ul>
<li>Search across existing Answers and Pinboards</li>
<li>Search your data to create new Answers and Pinboards</li>
<li>View objects you viewed recently</li>
<li>View trending Pinboards and Answers</li>
<li>Filter existing objects by favorite, author, tag, or type of object</li>
<li>Sort existing objects by author, views, or most recently viewed</li>
<li>Bulk mark objects as favorites</li>
</ul>

<h3>Search existing Answers</h3>
In addition to the existing Search over data, this release gives business users easy <a href="{{ site.baseurl }}/end-user/search/search-answers.html">Search over existing Answers and Pinboards</a>. This  meets the users' information needs by making Answers searchable, sortable, and applying filters on relevance, recency, number of views, authorship, metrics used, and so on.

<h3>Stats and Trends for Search on Answers Pinboard</h3>
Use this default <a href="{{ site.baseurl }}/admin/thoughtspot-one/query-intelligence-pinboard.html">Pinboard</a> to analyze how users are searching your existing Answers and Pinboards, so you can determine what objects are the most popular and what assets you may need to create.

<h3>Disable Answer Search for specific Worksheets</h3>
When users search for existing Answers and Pinboards, the default experience is to search across all Worksheets that they have access to. You may not want users to search for existing Answer and Pinboards built on certain Worksheets that are works in progress or deprecated. You can disable searching for Answers on specific Worksheets. Refer to <a href="{{ site.baseurl }}/admin/thoughtspot-one/disable-discover-for-worksheet.html">Disable Answer Search</a>.

<h3>Linked Pinboard filters</h3>
You can now create one filter that filters visualizations based on multiple Worksheets by linking the Worksheet columns, at the Pinboard level. This is useful when you have a Pinboard built on multiple Worksheets, and you would like to filter on columns that are functionally the same, but exist in multiple Worksheets.<br><br>

Refer to <a href="{{ site.baseurl }}/complex-search/linked-filters.html">Linked Pinboard filters</a>.<br>

<h3>Selective Pinboard filters</h3>
You can now configure Pinboard filters to apply to specific visualizations that you choose. This is useful when you would like to filter some, but not all, visualizations in a Pinboard.<br><br>

Refer to <a href="{{ site.baseurl }}/complex-search/selective-filters.html">Selective Pinboard filters</a>.

<!--<h3>Enhanced data modeling capabilities</h3>
This release enables new data modeling capabilities. You can now:
<ul>
<li>Join a View to a table</li>
<li>Build a Worksheet on top of a View</li>
</ul>-->

<h3>Geomaps</h3>
ThoughtSpot's Geomaps now have more detailed geographic and infrastructural boundaries by default. This includes road names, cities, and so on.<br>

ThoughtSpot supports maps of many countries. See the complete list in the <a href="{{ site.baseurl }}/reference/geomap-reference.html">Geo Map Reference</a>.

<h3>Customize ThoughtSpot Help</h3>
You can now tailor the ThoughtSpot Help menu to your organization by customizing it from the Admin Console. When you configure these Help settings, you set system-wide defaults for all your users.

Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/customize-help.html">Customize ThoughtSpot Help</a>.

<h3>User Adoption Pinboard</h3>
The <a href="{{ site.baseurl }}/admin/ts-cloud/user-adoption.html">User Adoption Pinboard</a> is now accessible from the Admin Console.

{: id="2020-september"}
## ThoughtSpot Cloud September Release (tscloud.5)

<h3>Scriptability</h3>
Scriptability contains the following new features:
<ul>
  <li>Export and update logical tables</li>
  <li>Edit, validate, and publish objects using the TML editor</li>
  <li>Import multiple objects from the <strong>SpotApps</strong> page, or from the object list page</li>
  <li>Update Views</li>
  <li>GUID handling: a new <code>GUID</code> parameter in an object's .tml file allows ThoughtSpot to recognize pre-existing GUIDs, and determine if you are updating an existing object, or creating a new one</li>

</ul>

See <a href="{{ site.baseurl }}/admin/ts-cloud/scriptability.html">Scriptability</a>.

<h3>Style Customization</h3>
You can now customize the ThoughtSpot application from the Admin Console. With style customization, you can change the fonts, chart color palettes, footer text, application logo, and background colors in your embedded ThoughtSpot instance.<br><br>

Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/style-customization.html">Style customization</a>.

<h3>In-app acceptance of ThoughtSpot's use agreement</h3>
You can now sign ThoughtSpot's end-user use agreement from the application itself. Even if you previously signed a paper copy of the use agreement, an admin must sign the agreement in the application, within 30 days of ThoughtSpot upgrading your cluster to Cloud 5.<br><br>

Refer to <a href="{{ site.baseurl }}/admin/ts-cloud/use-agreement.html">ThoughtSpot use agreement</a>.

<h3>User adoption and performance Pinboards</h3>
This release of ThoughtSpot Cloud contains two new default Pinboards for administrators. Use the <a href="{{ site.baseurl }}/admin/ts-cloud/user-adoption.html">User Adoption Pinboard</a> to understand how your ThoughtSpot users are interacting with ThoughtSpot, and how your user adoption is changing over time. Use the <a href="{{ site.baseurl }}/admin/ts-cloud/performance-tracking.html">Performance Tracking Pinboard</a> to understand how your ThoughtSpot cluster is performing.<br><br>

See <a href="{{ site.baseurl }}/admin/ts-cloud/user-adoption.html">User Adoption Pinboard</a> and <a href="{{ site.baseurl }}/admin/ts-cloud/performance-tracking.html">Performance Tracking Pinboard</a>.
