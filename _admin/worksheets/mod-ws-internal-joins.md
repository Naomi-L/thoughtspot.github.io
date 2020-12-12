---
title: [Modify joins within a worksheet]
last_updated: 11/18/2019
summary: "Learn how to change the join type between the tables within a worksheet."
toc: true
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---

When you create a worksheet, you select a [join rule]({{ site.baseurl }}/admin/worksheets/progressive-joins.html). The join rule works together with the joins defined within the worksheet determine how the tables that make up the worksheet are joined, and how those joins behave when searching on the worksheet.

Starting with ThoughtSpot version 5.0, you are not limited to just one join rule for the entire worksheet. You can define different types of joins for each join between tables in a worksheet. Be default, each of these individual table joins uses an inner join. But you can override this at the individual join level.

You must have either the **Can administer ThoughtSpot** privilege or the **Can manage data** privilege to modify joins within worksheets.

## Modify a join

To modify the join types within a worksheet, follow these steps:

1. Click the **Data** tab in the top menu.  

2. Under **Data Objects**, select **Worksheets**.

3. Click the name of the Worksheet. Here, we selected the worksheet _West Regional Sales_.

4. At the top of the Worksheet, click **Joins**.

5. The join information and the schema for the worksheet appear.
   -  The schema representation includes the join type.  
   -  You can see the list of _Joins within the worksheet_, which include all joins between the underlying tables, both [created using TQL]({{ site.baseurl }}/admin/loading/constraints.html) and [created in the browser]({{ site.baseurl }}/admin/data-modeling/create-new-relationship.html).
   -  The fact table is always on the left side of the join, and it appears on the left side.

   ![]({{ site.baseurl }}/images/worksheet-join-schema-view.png "View join and schema")

   Note the available actions for the join view.  

   <table>
     <tr>
       <th>Legend</th>
       <th>Action</th>
     </tr>
     <tr>
       <td>1.</td>
       <td>See either <em>Join within this Worksheet (Default)</em>, or <em>Joins from this Worksheet</em>.</td>
     </tr>
     <tr>
       <td>2.</td>
       <td>Click the pencil icon to edit the join.</td>
     </tr>
     <tr>
       <td>3.</td>
       <td>Click the up arrow icon to collapse the join detail.</td>
     </tr>
   </table>

7. Select the join you plan to modify, and click the **Edit** \(pencil\) icon next to it.

8. In the **Edit Join** window modal, make the necessary changes:  

   ![]({{ site.baseurl }}/images/change-join.png "Select join type and cardinality")

    -  Under **Join Type**, select one of _Inner Join_, _Left Outer Join_, _Right Outer Join_, or _Full Outer Join_.
    - Under **Join Cardinality**, select either _Many to One_, or _One to One_.

   Click **Save**.

## Related Information

-   [Join rule]({{ site.baseurl }}/admin/worksheets/progressive-joins.html)
-   [Create joins using TQL]({{ site.baseurl }}/admin/loading/constraints.html)
-   [Create join relationships in the browser]({{ site.baseurl }}/admin/data-modeling/create-new-relationship.html)
