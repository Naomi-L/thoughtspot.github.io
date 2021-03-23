---
title: ["Free Trial Release Notes"]
keywords: "free trial"
last_updated: 03/23/2021
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
This release includes the following features.

{: id="auto-worksheet"}

Starting with the March 2021 Free Trial release, you can auto-generate a Worksheet during onboarding. When setting up a Worksheet through the Setup tab, you can view suggested joins, and take advantage of data modeling best practices, making your data easier to search.

## About Worksheets

Users are often unfamiliar with tables and how they relate to one another. A Worksheet groups multiple related tables together in a logical way. Using Worksheets has the following advantages:

* Pre-join multiple tables together.
* Give a user or group access to only part of the underlying data.
* Include a derived column using a formula.
* Rename columns to make the data easier to search.
* Build in a specific filter or aggregation.
* Give users a filtered set of data to search.

Typically, you create one Worksheet for each set of fact and dimension tables. For example, you may have a sales fact table and an inventory fact table. Each of these fact tables shares common dimensions like date, region, and store. In this scenario, you would create two Worksheets: sales and inventory. The following diagram depicts the workflow for creating the sales Worksheet.

![]({{ site.baseurl }}/images/workflow_create_worksheet.png "Create worksheet")

## Generating Worksheets

To generate a Worksheet through the Setup tab, follow these steps:

1. Complete Step 1 of Setup, <a href="{{ site.baseurl }}admin/ts-cloud/connect-data.html">setting up your connection</a>.

2. Click Step 2, *Model data and create a Worksheet.* Select *Create Worksheet* in the lower left corner. A list of the available fact tables from your connection appears.

3. The first fact table alphabetically will be selected by default. Choose the fact table from which you would like to create your Worksheet by selecting the box to the left of its name.

   {% include note.html content="After the Worksheet is created, you will have the option to add more fact tables to its schema."%}

4. Click *Next* in the upper right corner. A list of the available dimension tables from your connection appears.

5. Choose the dimension table(s) to join to your fact table and click *Next*. You can choose up to four dimension tables.

6. The joins interface appears, showing a join based on a column of data both tables contain. You can proceed with the suggested join, or click the column names to change the join.

   {% include note.html content="The default join type is Inner, which will yield all search results with matching values from the fact table and the dimension table. You can click the Venn diagram icon to change the join type."%}

7. Click *Next*. The columns view of your Worksheet appears. You may notice that the column names have been changed to make them more easily searchable (for example, underscores may be replaced with spaces).

8. [Optional] Click *My Worksheet* to change the name of your Worksheet.

9. [Optional] Click the column titles to change the names of your searchable columns. You can also click the blue check-box next to a column name to remove it from your Worksheet.

10. [Optional] Click the data type under *Type* to change the recorded data type. For example, you can change a data type like Zipcode from ‘Measure’ to ‘Attribute’.

11. Click *Save worksheet*. Your Worksheet is now available to search and share.

   {% include note.html content="Joins created in the setup of a Worksheet are inherited at the table level. To remake your auto-generated Worksheet through the Setup tab, you must first delete the Worksheet, then delete the joins at the table level."%}
