---
title: [SpotApps]
last_updated: 12/11/2020
summary: "SpotApps, ThoughtSpot's scriptable applications, allow you to migrate multiple objects to and from clusters."
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
SpotApps take advantage of [Scriptability]({{ site.baseurl }}/admin/ts-cloud/scriptability.html), ThoughtSpot's solution for exporting, enhancing, and migrating ThoughtSpot objects, to provide you with scriptable applications you can use in multiple clusters.   

Once you connect to your data, you can work with your ThoughtSpot contacts to deploy ThoughtSpot's scriptable applications, or SpotApps, which provide an easy way for you to start getting value from your data.

ThoughtSpot offers [pre-built SpotApps](#pre-built-spotapps), which leverage your data in Snowflake, Amazon Redshift, Google BigQuery, or Azure Synapse to provide pre-built Pinboards, Answers, Views, Tables, and Worksheets. You can also [create your own custom SpotApps](#create-spotapps) that satisfy your specific business needs.

{: id="pre-built-spotapps"}
## Pre-built SpotApps
ThoughtSpot offers 3 pre-built SpotApps: Salesforce, procurement, and accounts receivable. These applications leverage your data in Snowflake, Amazon Redshift, Google BigQuery, or Azure Synapse to provide pre-built Pinboards, Answers, Views, Tables and Worksheets.

For example, if you choose to use the Procurement SpotApp, the **Search** page contains a Worksheet for your users to query on, called "Procurement Analytics Solution."

![Procurement Worksheet Search]({{ site.baseurl }}/images/scriptable-app-procurement-search.png "Procurement Worksheet Search")

Your users may want to understand what Answers and Pinboards are before they start searching, or they may only want to gain insights from pre-built objects. They can view any of the pre-existing objects, such as this Exec Summary Pinboard:

![Exec summary]({{ site.baseurl }}/images/exec-summary-pinboard.png "Exec summary")

When you are ready to move to a production environment, you can migrate these Pinboards, Answers, Views, Tables, and Worksheets to your new environment using [Scriptability]({{ site.baseurl }}/admin/ts-cloud/scriptability.html), ThoughtSpot's flat-file editing and migration system for ThoughtSpot objects.

{: id="create-spotapps"}
## Create and export SpotApps
You can create your own custom SpotApps from the **SpotApps** page. Alternatively, ThoughtSpot automatically creates SpotApps for you when you export more than one object of the same type at a time, or when you export an object and its dependents.

To create and export your own custom SpotApps, follow these steps.

1. Navigate to the **SpotApps** page: **Data > SpotApps**.

2. Select **Export SpotApps**.

3. In the **Export** interface, select the Pinboards, Answers, Views, Tables, and Worksheets that you would like to include in your SpotApp. For example, for a Marketing SpotApp, you might choose a *Marketing* Worksheet, a *Campaigns* Worksheet, a *Pipeline* Pinboard, and a few Answers your Chief Marketing Officer created.

4. Click **Export selected files**.

5. The **Choose what to Export** modal appears. Choose whether to export only the selected objects, or the selected objects and their underlying data sources (Worksheets, tables, and Views).

6. Click **Export**.

7. Open the downloaded `TML` zip file. The SpotApp zip file contains a document called the `Manifest` file, which defines the objects you exported, their underlying data sources, and any export errors. It also contains the `joins.tml` file, which defines the joins each object uses. If an individual export fails, you can find an error message in the `Manifest` file. The zip file still exports, even if an individual object's export fails.

See [Scriptability]({{ site.baseurl }}/admin/ts-cloud/scriptability.html) for more information on exporting and importing objects.

### Import SpotApps
You can import SpotApps from the SpotApps page, under **Data > SpotApps**.

1. From the **SpotApps** page under the **Data** tab, click **Import**.

    ![Import SpotApps]({{ site.baseurl }}/images/scriptability-spotapps-import.png "Import SpotApps")

2. In the **Import** interface, click **Select TML or .zip files to upload**.

6. In your file system, find and select the .zip file for the SpotApp.

8. If you constructed the file correctly, the **Import** interface displays a *Validation successful* message, and shows you which objects are validated. You can now import the objects. The <code>GUID</code> parameter in an object's TML file allows ThoughtSpot to recognize pre-existing GUIDs, and determine if you are updating an existing object, or creating a new one. If you are updating an existing object, the system asks if you would like to create a new object, or update the existing one.

9. You can unselect any files in the `.zip` file you do not want to upload.

10. Click **Import selected files**.

11. The **Import Status** screen displays the status of the objects you imported. You can open the object(s) that you imported, or click **Done** to return to the main object page.

    ![Go to object]({{ site.baseurl }}/images/scriptability-migrate-answers-created.png "Go to object")

### Limitations
You cannot import manually compressed .zip files. You can only import .zip files that you exported from ThoughtSpot: a custom SpotApp, an object and its associated data sources, or multiple objects of the same type that you exported from the object list page.
