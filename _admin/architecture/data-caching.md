---
title: [Data Use Strategies]
last_updated: 04/26/2021
summary: "ThoughtSpot does all analysis against data in memory to help achieve
fast results across millions and billions of records of data."
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
ThoughtSpot caches data as relational tables in memory. You can
source tables from different data sources and join them together. ThoughtSpot has several approaches for getting data into the cluster.

![]({{ site.baseurl }}/images/data-caching-architecture.png)

{% include note.html content="For cases where your company stores data externally, use Embrace to access and query your data. To cache your data within ThoughtSpot, you can load it directly using DataFlow, or the <code>tsload</code> command line utility. JDBC and ODBC drivers are also available."%}

## ThoughtSpot Embrace ##
If your company stores source data externally in data warehouses, you can use [ThoughtSpot Embrace]({{ site.baseurl }}/data-integrate/embrace/embrace-intro.html) to directly query that data and use ThoughtSpot's analysis and visualization features, without moving the data into ThoughtSpot. While Embrace caches metadata, it *does not* cache the data itself within ThoughtSpot.

Embrace supports the following external databases:
<ul>
<li>Snowflake</li>
<li>Amazon Redshift</li>
<li>Google BigQuery</li>
<li>Microsoft Azure Synapse</li>
<li>Teradata</li>
<li>SAP HANA</li>
</ul>

## ThoughtSpot DataFlow ##
[DataFlow]({{ site.baseurl }}/data-integrate/dataflow/dataflow.html) is a capability in ThoughtSpot through which users can easily ingest data into ThoughtSpot from dozens of the most common databases, data warehouses, file sources, and applications. If your company maintains large sources of data externally, you can use DataFlow to easily ingest the relevant information, and use ThoughtSpot’s analysis and visualization features. After you configure the scheduled refresh, your analysis visuals are always up to date. DataFlow supports a large number of [databases]({{ site.baseurl }}/data-integrate/dataflow/dataflow-databases.html), [applications]({{ site.baseurl }}/data-integrate/dataflow/dataflow-applications.html), and [file systems]({{ site.baseurl }}/data-integrate/dataflow/dataflow-filesystems.html).

DataFlow is recommended for large amounts of data, and for scheduled refresh. Many times the source data could have many years of data and it becomes infeasible to load all that data on a daily basis. Through DataFlow you can specify the filter conditions to get only the latest data.

## JDBC and ODBC Drivers ##
ThoughtSpot provides a [JDBC]({{ site.baseurl }}/data-integrate/clients/about-jdbc.html) and [ODBC]({{ site.baseurl }}/data-integrate/clients/about-odbc.html) driver that can be used to write data to ThoughtSpot. This is useful for customers who already have an existing ETL process or tool, and want to extend it to populate the ThoughtSpot cache.

JDBC and ODBC drivers are appropriate under the following circumstances:
<ul>
<li>have an ETL load, such as Informatica, SSIS, and so on</li>
<li>have available resources to create and manage ETL</li>
<li>have smaller daily loads</li>
</ul>

## tsload ##
You can use the [<code>tsload</code>]({{ site.baseurl }}/admin/loading/use-data-importer.html) command line tool to bulk load delimited data with very
high throughput. Finally, individual users can upload smaller (< 50MB)
spreadsheets or delimited files.

We recommend the tsload approach in the following cases:
<ul>
<li>initial data load</li>
<li>JDBC or ODBC drivers are not available</li>
<li>there are large recurring daily loads</li>
<li>for higher throughput; this can add I/O costs</li>
</ul>


## Choosing a Data Use Strategy ##

The approach you choose depends on your environment and data needs. There are, of course, tradeoffs between different data caching options.

Many implementations use a variety of approaches. For example, a solution with a large amount of initial data and smaller daily increments might use <code>tsload</code> to load the initial data, and then use the JDBC driver with an ETL tool for incremental loads.

### Related information: ###
<ul>
<li>[ThoughtSpot Embrace]({{ site.baseurl }}/data-integrate/embrace/embrace-intro.html)</li>
<li>[ThoughtSpot DataFlow]({{ site.baseurl }}/data-integrate/dataflow/dataflow.html)</li>
<li>[ThoughtSpot with ODBC]({{ site.baseurl }}/data-integrate/clients/about-odbc.html)</li>
<li>[ThoughtSpot with JDBC]({{ site.baseurl }}/data-integrate/clients/about-jdbc.html)</li>
<li>[ThoughtSpot <code>tsload</code>]({{ site.baseurl }}/admin/loading/use-data-importer.html)</li>
<li>[<code>tscli</code> command reference]({{ site.baseurl }}/reference/tscli-command-ref.html)</li>
<li>[<code>tsload</code> flag reference]({{ site.baseurl }}/reference/data-importer-ref.html)</li>
</ul>
