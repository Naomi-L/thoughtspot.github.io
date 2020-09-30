---
title: [How to view a data schema]
keywords: schema viewer, relationships, keys, worksheet
last_updated: 12/13/2018
tags: [Modeling]
toc: true
summary: "Use the schema viewer to see tables and worksheets and their relationships. "
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
ThoughtSpot offers a schema viewer that lets you see your database schema in the
web browser. The Schema Viewer is interactive, so you can configure it to show
just what you want to see.

You need **Admin** privileges to use the **Schema Viewer**.

## Bringing up the Schema Viewer

You can bring up the Schema Viewer from the **Data** screen. Click the ellipses icon
(3 dots) ![more options menu icon]({{ site.baseurl }}/images/icon-ellipses.png){: .inline},
and select **View Schema**.

 ![]({{ site.baseurl }}/images/access_schema_viewer.png "Access the Schema
 Viewer")

When viewing the schema, you can filter the tables shown similarly to how you
filter data sources. The list of tables, worksheets, and imported data on the
left includes only those objects you want to see. Clicking on one of the objects
brings it to the middle of the viewer and highlights it. You can drag the
objects around in the viewer.

 ![]({{ site.baseurl }}/images/schema_viewer.png "Schema Viewer filters")

## Why to use the Schema Viewer

You can use the Schema Viewer to find out information like:

-   What is the relationship between two tables? What tables make up this
-   worksheet, and how are they joined?

The schema viewer shows joins between tables, join directionality, and join type
(whether they are Foreign Key to Primary Key, relationship joins, or joins
defined by users through the web interface). Use the **Table** list to find a
specific table or worksheet.

## How the Schema Viewer shows joins

You can use the Schema Viewer to review your schema and ensure that it was
modeled using best practices. For example, joins appear in different colors to distinguish their type:

* Generic relationships are in **red**
* Primary key/ foreign key joins are in **green**

When viewing a worksheet, you can also see what joins connect the tables: the inner, left outer, right outer, or full outer joins.

{% include note.html content="Defining a generic relationship in the UI rather than using a primary key/ foreign key join through TQL has no impact on performance. However, when creating relationships in the UI, you must ensure that you create it in the right direction: many to one. To create many-to-many joins, or to create joins using >, <, >=, or <=, use TQL." %}

## Worksheet view

Worksheets are often based on more than one table. The worksheet schema will
show schemas for the tables behind the worksheet, as well as the joins between
tables _that were created as a part of the worksheet_.

Click on a worksheet, to see it in the Schema Viewer. If the schema view is not showing the schema behind the worksheet, double click the tab on the top right of the worksheet object.

![]({{ site.baseurl }}/images/worksheet_viewer_schema.png "Worksheet schema example")


The worksheet view shows the following information:

-   All tables in the worksheet, and the relationships between these tables.
-   Source columns for all columns of a worksheet.

-   Keys and definitions for each relationship, as well as join paths and types.

-   Columns that are derived from formulas.

-   Correct join paths for newly created chasm trap worksheets. Existing chasm
-   trap worksheets created prior to ThoughtSpot version 4.4 will not show the correct join paths.

 ![]({{ site.baseurl }}/images/worksheet_viewer.png "Worksheet view example")

## Related Information

-   [Worksheet joins]({{ site.baseurl }}/admin/worksheets/add-joins.html)
-   [Change the schema using TQL]({{ site.baseurl }}/admin/loading/change-schema.html)
-   [Constraints]({{ site.baseurl }}/admin/loading/constraints.html)
