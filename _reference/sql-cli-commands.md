---
title: [TQL reference]
summary: Learn the TQL commands.
last_updated: 12/11/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
TQL is the ThoughtSpot language for entering SQL commands. This reference lists
TQL commands you can use to do things like creating a schema or verifying a data
load.

## About using TQL

You can use TQL either [through the ThoughtSpot application's web interface]({{
site.baseurl }}/admin/loading/upload-sql-script.html#) or the [command line
interface]({{ site.baseurl }}/reference/sql-cli-commands.html#) in the Linux
shell.

Use  `--query_results_apply_top_row_count <number>` flag to limit the number of
result rows returned by a query. For example:

`$ tql --query_results_apply_top_row_count 100`


As a best practice, you should enclose object names (database, schema, table,
and column) in double quotes, and column values in single quotes.
 When referring to objects using fully qualified object names, the syntax is:

```
"database"."schema"."table"
```

To get help on SQL when using TQL,  enter `help` on the command line.

You can use TQL to view and modify schemas and data in tables. Remember to add a
semicolon after each command. Commands are not case sensitive but are
capitalized here for readability.

{% include note.html content="Worksheets and pinboards in ThoughtSpot are
dependent upon the data in the underlying tables. Use caution when modifying
tables directly. If you change or remove a schema on which those objects rely,
the objects could become invalid." %}


## View schemas and data

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:75%">
   </colgroup>
   <thead >
      <tr>
         <th>Syntax</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <code>SHOW DATABASES</code>
         </td>
         <td>Lists all available databases.

         <p>Examples:</p>
            <p><code>SHOW DATABASES;</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>USE &lt;database&gt;</code></p>
         </td>
         <td>Switches the context to the specified database. This is required if queries
            do not use fully qualified names (database.schema.table) for specifying
            tables.
         <p>Examples:</p>
            <p><code>USE "fruit_database";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <code>SHOW SCHEMAS</code>
         </td>
         <td><p>Lists all schemas within the current database. For example:</p>
            <p><code>SHOW SCHEMAS;</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SHOW TABLES</code></p>
         </td>
         <td><p>Lists all tables within the current database by schema. For example:</p>
            <p><code>SHOW TABLES;</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SHOW TABLE &lt;table&gt;</code></p>
         </td>
         <td><p>Lists all the columns for a table. For example:</p>
            <p><code>SHOW TABLE "locations";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SCRIPT SERVER</code></p>
         </td>
         <td><p>Generates the TQL schema for all tables in all databases on the
            server. For example:</p>
            <p><code>SCRIPT SERVER;</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SCRIPT DATABASE &lt;database&gt;</code></p>
         </td>
         <td><p>Generates the TQL schema for all tables in a database. For example:</p>
            <p><code>SCRIPT DATABASE "fruit_database";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SCRIPT TABLE &lt;table&gt;</code></p>
         </td>
         <td><p>Generates the TQL schema for a table. For example:</p>
            <p><code>SCRIPT TABLE "vendor";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>SELECT
   &lt;cols_or_expr&gt;
   FROM &lt;table_list&gt;
   [WHERE &lt;predicates&gt;]
   [GROUP BY &lt;expr&gt;]
   [ORDER BY &lt;expr&gt;]</code></p>
         </td>
         <td>
            Shows specified set of table data.
            <p>If you do not specify the TOP number of
               rows to select, the top 50 rows will be returned by default. The number of rows
               to return can be set using the <span class="ph">TQL</span> command line flag:
            </p>
            <p><code>--query_results apply_top_row_count</code></p>
            <p>You can use the following aggregation functions:</p>
            <ul>
               <li><code>sum</code></li>
               <li><code>count</code></li>
               <li><code>count distinct</code></li>
               <li><code>stddev</code></li>
               <li><code>avg</code></li>
               <li><code>variance</code></li>
               <li><code>min</code></li>
               <li><code>max</code></li>
            </ul>
            <div>
               You can use the following date functions:
               <ul>
                  <li><code>absyear</code></li>
                  <li><code>absmonth</code></li>
                  <li><code>absday</code></li>
                  <li><code>absquarter</code></li>
                  <li><code>date</code></li>
                  <li><code>time</code></li>
               </ul>
            </div>
          <p>For example:</p>
<p><code>SELECT TOP 10 "quantity" FROM "sales_fact";</code></p>
<p><code>SELECT COUNT(&#42;) FROM "vendor";</code></p>
<p><code>SELECT "vendor", SUM("quantity") FROM "sales_fact" GROUP BY "vendor";</code></p>
<p><code>SELECT "vendor", SUM("amount") FROM "vendor", "sales_fact"
     WHERE "sales_fact"."vendorid" = "vendor"."vendorid"
     AND "amount" &gt; 100 GROUP BY "vendor" ORDER BY "amount" DESC;</code></p>
<p><code>SELECT "vendor", SUM("quantity") FROM "sales_fact"
GROUP BY "vendor" LIMIT 10;</code></p>
         </td>
      </tr>
   </tbody>
</table>

## Schema creation

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:75%">
   </colgroup>
   <thead >
      <tr>
         <th>Syntax</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <p><code>CREATE DATABASE
            &lt;database&gt;</code></p>
         </td>
         <td>
            <p>Creates a database. For example:</p>
            <p><code>CREATE DATABASE "fruit_database";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>CREATE SCHEMA &lt;schema&gt;</code></p>
         </td>
         <td>
            <p>Creates a schema within the current database. For example:</p>
            <p><code>CREATE SCHEMA "fruit_schema";</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>CREATE TABLE &lt;table&gt; (&lt;column_definitions&gt;
            [&lt;constraints&gt;]) [PARTITION BY HASH (&lt;number&gt;) [KEY
            ("&lt;column&gt;")]])</code></p>
         </td>
         <td>
            <p>Creates a table with the specified column definitions and constraints.</p>
            <p>
            Use <code>PARTITION BY HASH</code> to shard a table across all nodes. If no <code>KEY</code> is specified, the table will be randomly sharded.
            </p>
            <p>
               Do not specify relationship constraints (<code>FOREIGN KEY</code>
               or <code>RELATIONSHIP</code>) in the <code>CREATE TABLE</code>
               statement. Instead, define these using <code>ALTER TABLE</code>
               statements at the end of your TQL script, after
               creating your tables. This method guarantees that tables are created
               before they are referenced in the constraint definitions. For example:
            </p>
            <p><code>CREATE TABLE "vendor" ("vendorid" int, "name" varchar(255));</code></p>
<p><code>CREATE TABLE "sales_fact" ("saleid" int, "locationid" int, "vendorid" int,
"quantity" int, "sale_amount" double, "fruitid" int,
CONSTRAINT PRIMARY KEY("saleid")) PARTITION BY HASH(96) KEY ("saleid");</code></p>
         </td>
      </tr>
   </tbody>
</table>

## Schema modification

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:75%">
   </colgroup>
   <thead>
      <tr>
         <th>Syntax</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
   <tr>
      <td>
         <p><code>DROP DATABASE
         &lt;database&gt;</code></p>
      </td>
      <td><p>Drops a database and all of its schemas and tables. For example:</p>
         <p><code>DROP DATABASE "fruit_database";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code>DROP SCHEMA &lt;schema&gt;</code></p>
      </td>
      <td><p>Drops a schema within the current database, and drops all of the tables in
         the schema. For example:</p>
         <p><code>DROP SCHEMA "fruit_schema";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code>DROP TABLE &lt;table&gt;</code></p>
      </td>
      <td><p>Drops a table. For example:</p>
         <p><code>DROP TABLE "location";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <code>TRUNCATE TABLE
         &lt;table&gt;</code>
      </td>
      <td>
         <p>Removes all data from a table, but preserves its metadata, including all
         GUIDs, relationships, etc. This can be used to force a new schema for a table
         without losing the metadata.</p>
         <p>However, this operation removes all existing data
            from the table and must be used with caution. You must reload the data following
            a <code>TRUNCATE</code>, or all dependent objects (worksheets and pinboards) in <span class="ph">ThoughtSpot</span> will become invalid. For example:
         </p>
         <p><code>TRUNCATE TABLE "location";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code>ALTER TABLE &lt;table&gt; ADD|DROP|RENAME COLUMN
         &lt;column&gt;</code></p>
      </td>
      <td>
         Alters a table to add, drop, or rename a column.
         <p>When you add a column to
            an existing table, you must provide a default value to use for existing
            rows. For example:</p>
<p><code>ALTER TABLE "cart" ADD COLUMN "nickname" varchar(255) DEFAULT 'no
nickname';</code></p>
<p><code>ALTER TABLE "cart" DROP COLUMN "nickname";</code></p>
<p><code>ALTER TABLE "cart" RENAME COLUMN "nickname" TO "shortname";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code>ALTER TABLE &lt;table&gt; DROP CONSTRAINT PRIMARY KEY;</code></p>
      </td>
      <td>
        <p> Drops the primary key from a table.</p>
         <p>Note that if you then add a new
            primary key, the same upsert behavior will be applied as with adding any primary
            key. This can result in data deletion, so make sure you understand how the
            upsert will affect your data ahead of time.
            For example:
         </p>
         <p><code>ALTER TABLE "sales" DROP CONSTRAINT PRIMARY KEY;</code></p>
         <p><code>ALTER TABLE "sales" ADD CONSTRAINT PRIMARY KEY ("PO_number");</code></p>

      </td>
   </tr>
   <tr>
      <td>
         <p><code>ALTER TABLE &lt;table&gt; DROP [CONSTRAINT | RELATIONSHIP]
       &lt;name&gt;;</code></p>
      </td>
      <td><p>Drops the named foreign key or relationship between two tables. For example:</p>
         <p><code>ALTER TABLE "sales_fact" DROP CONSTRAINT "FK_PO_number";</code></p>
        <p><code>ALTER TABLE "fruit_dim" DROP RELATIONSHIP "REL_dates";</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code>ALTER TABLE &lt;table&gt; [SET DIMENSION | SET FACT [PARTITION BY
         HASH [(&lt;shards&gt;)] [KEY(&lt;column&gt;)]]]</code></p>
      </td>
      <td>
         <div>
            <p>Changes the partitioning on a table by doing one of:</p>
            <ul class="ul" id="reference_cbc_fx4_j4__ul_egx_4jg_wv">
               <li>re-sharding a sharded table</li>
               <li>changing a replicated table to a sharded table</li>
               <li>changing a sharded table to a replicated (unsharded) table</li>
            </ul>
            <p>By default, ThoughtSpot does not shard dimension tables.</p>
         </div>
         <p>To change the partitioning on a table, or to change a dimension table to a
            sharded table, use <code>ALTER TABLE...SET FACT PARTITION BY HASH...;</code>
         </p>
         <p>To make a sharded table into a dimension table (replicated on every node),  use
            <code>ALTER TABLE...SET DIMENSION;</code> command.  
         </p>
         <p>Examples of this statement:</p>
         <p><code>ALTER TABLE "sales_fact" SET FACT PARTITION BY HASH (96) KEY
         ("PO_number");
         ALTER TABLE "fruit_dim" SET DIMENSION;</code></p>
      </td>
   </tr>
   <tr>
      <td>
         <p><code align="left">ALTER TABLE &lt;table&gt; MODIFY COLUMN &lt;column&gt;
&lt;new_data_type&gt;;</code></p>
      </td>
      <td>
         <p>Changes the data type of a column. This can have implications on sharding and
            primary key behavior. See <a href="{{"/admin/loading/about-data-type-conversion.html#concept_u2t_clg_wv" | prepend: site.baseurl}}"> About data type conversion</a>. For example:
         </p>
         <p><code>ALTER TABLE fact100 MODIFY COLUMN product_id int;</code></p>
      </td>
   </tr>

   </tbody>
</table>


## Modify data

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:75%">
   </colgroup>
   <thead >
      <tr>
         <th>Syntax</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
            <p><code>INSERT INTO &lt;table&gt; VALUES ...</code></p>
         </td>
         <td><p>Inserts values into a table. Only use this for testing. Do not use <code>INSERT</code> on
            a production system. For example:</p>

            <p><code>INSERT INTO "vendor" VALUES ('helen rose', 'jacob norse', 'eileen ruff',
'manny gates');</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code align="left">ALTER TABLE &lt;table&gt; SET LOAD PRIORITY &lt;value&gt;
   &lt;new_data_type&gt;;</code></p>
         </td>
         <td>
            <p>Sets the load priority for a table. Load priority determines the order in which a table is loaded on a cluster restart. You can set any value from <code>1-100</code>. The system default for all tables is <code>50</code>. For example:
            </p>
            <p><code>ALTER TABLE 'sales_facts' SET LOAD PRIORITY 1;</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>UPDATE &lt;table&gt; ... SET ... [WHERE ...]</code></p>
         </td>
         <td><p>Updates rows in a table that match optionally provided predicates. Predicates
            have the form <code>column = value</code> connected by the <code>AND</code> keyword. Sets the column values
            to the specified values. For example:</p>
            <p><code>
UPDATE "location" SET "borough" = 'staten island', "city" = 'new york'
WHERE "borough" = 'staten isl' AND city = 'NY';</code></p>
         </td>
      </tr>
      <tr>
         <td>
            <p><code>DELETE FROM &lt;table&gt; [WHERE...]</code></p>
         </td>
         <td><p>Deletes rows from a table that match optionally provided predicates.
            Predicates have the form <code>column = value</code> connected by the <code>AND</code> keyword. When specifying dates, use <a href="https://www.epochconverter.com/">epoch values</a>. Other date formats can result in error and unwanted deletion of data from the table.
         For example.</p>

<p><code>DELETE FROM "vendor" WHERE "name" = 'Joey Smith' AND "vendorid" =
'19463';</code></p>
         </td>
      </tr>
   </tbody>
</table>

## Constraints and relationships

Constraints and relationships in ThoughtSpot are used to define the
relationships between tables (how they can be joined). However, constraints
are not enforced, as they would be in a transactional database. You can define
the following constraints when creating a table with <code>CREATE TABLE</code>, or add them
to an existing table using the <code>ADD CONSTRAINT</code> syntax:

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:75%">
   </colgroup>
   <thead >
      <tr>
         <th>Syntax</th>
         <th>Description</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>PRIMARY KEY</td>
         <td>
            Designates a unique, non-null value as the primary key for a table. This can
            be one column or a combination of columns. If values are not unique, an upsert
               will be performed if a row includes a primary key that is already present in the
               data. Some examples:
            </p>
<p><code>CREATE TABLE "schools" ( "schoolID" varchar(15), "schoolName"
varchar(255), "schoolCity" varchar(55), "schoolState" varchar(55), "schoolNick"
varchar(55), CONSTRAINT PRIMARY KEY ("schoolID") ) ;</code></p>
<p><code>ALTER TABLE "cart" ADD CONSTRAINT PRIMARY KEY ("cart_id");</code></p>
<p><code>ALTER TABLE "cart" DROP CONSTRAINT PRIMARY KEY "cart_id";</code></p>
         </td>
      </tr>
      <tr>
         <td>FOREIGN KEY</td>
         <td>
            <p>Defines a relationship where the value(s) in the table are used to join to a
            second table. Uses an equality operator. The foreign key must match the primary
            key of the table that is referenced in number, column type, and order of
            columns.</p>
            <p>When creating a foreign key, give it a name. You can reference the
               foreign key name later, if you want to remove it.
            </p>
<p>Examples of this statement:</p>
<p><code>ALTER TABLE "batting" ADD CONSTRAINT "FK_player" FOREIGN KEY ("playerID")
REFERENCES "players" ("playerID");</code></p>

<p><code>ALTER TABLE "batting" ADD CONSTRAINT "FK_lg_team" FOREIGN KEY ("lgID" ,"teamID")
REFERENCES "teams" ("lgID" ,"teamID");</code></p>

<p><code>ALTER TABLE "shipment" ADD CONSTRAINT "FK_PO_vendor" FOREIGN KEY ("po_number",
"vendor") REFERENCES "orders" ("po_number", "vendor");</code></p>

<p><code>ALTER TABLE "shipment" DROP CONSTRAINT "FK_PO_vendor";</code></p>
         </td>
      </tr>
      <tr>
         <td>RELATIONSHIP</td>
         <td>
            <p>Defines a relationship where the value(s) in the table can be used to join to
            a second table, using an equality condition (required) and one or more range
            conditions (optional). These conditions act like a WHERE clause when the two
            tables are joined. They are applied using AND logic, such that all conditions must
            be met for a row to be included.</p>
            <p>You may add multiple relationships between
               tables. When creating a relationship, give it a name. You can reference
               the relationship name later, if you want to remove it.
            </p>
            <p>Examples of this statement:</p>
            <p><code>ALTER TABLE "wholesale_buys" ADD RELATIONSHIP "REL_fruit" WITH
"retail_sales" AS "wholesale_buys"."fruit" = "retail_sales"."fruit" AND
("wholesale_buys"."date_order" &lt; "retail_sales"."date_sold" AND
"retail_sales"."date_sold" &lt; "wholesale_buys"."expire_date");</code></p>

<p><code>ALTER TABLE "wholesale_buys" DROP RELATIONSHIP "REL_fruit";</code></p>
         </td>
      </tr>
      <tr>
      <td>

      </td>
      </tr>
   </tbody>
</table>

### Permitted joins and necessary permissions

See this matrix for information about which joins you can create, and what permissions these joins require.

{% include content/joins-definition-list.md %}

## Data types

ThoughtSpot supports a simplified list of data types:

<table>
   <colgroup>
      <col style="width:25%">
      <col style="width:25%">
      <col style="width:50%">
   </colgroup>
   <thead >
      <tr>
         <th>Syntax</th>
         <th>Description</th>
         <th>Examples</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>Character</td>
         <td>
            <ul class="ul" id="reference_cbc_fx4_j4__d109e35">
               <li>VARCHAR(<em class="ph i">n</em>)</li>
            </ul>
         </td>
         <td>Specify the maximum number of characters, as in VARCHAR(255). The size limit is 64MB for
            VARCHAR values.
         </td>
      </tr>
      <tr>
         <td>Floating point</td>
         <td>
            <ul class="ul" id="reference_cbc_fx4_j4__d109e47">
               <li>DOUBLE</li>
               <li>FLOAT</li>
            </ul>
         </td>
         <td>DOUBLE is recommended.</td>
      </tr>
      <tr>
         <td>Boolean</td>
         <td>
            <ul class="ul" id="reference_cbc_fx4_j4__d109e58">
               <li>BOOL</li>
            </ul>
         </td>
         <td>Can be <code class="ph codeph">true</code> or <code class="ph codeph">false</code>.</td>
      </tr>
      <tr>
         <td>Integer</td>
         <td>
            <ul class="ul" id="reference_cbc_fx4_j4__d109e73">
               <li>INT</li>
               <li>BIGINT</li>
            </ul>
         </td>
         <td>
            INT holds 32 bits.
            <p>BIGINT holds 64 bits.</p>
         </td>
      </tr>
      <tr>
         <td>Date or time</td>
         <td>
            <ul class="ul" id="reference_cbc_fx4_j4__d109e86">
               <li>DATE</li>
               <li>DATETIME</li>
               <li>TIMESTAMP</li>
               <li>TIME</li>
            </ul>
         </td>
         <td>
            <p>DATETIME, TIMESTAMP, and TIME are stored at the granularity of seconds</p>.
            <p>TIMESTAMP is
               identical to DATETIME, but is included for syntax
               compatibility.
            </p>
         </td>
      </tr>
   </tbody>
</table>
