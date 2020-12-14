To create a table join through the Web interface:
1. Click **Data** in the top menu, and choose **Tables**.
2. Find your table through browsing, Search, or selecting the appropriate Tag(s).
3. To select the table for adding joins, click its name in the list.
You will see the **Columns** view of the table.
4. Click the **Joins** tab. The list of existing joins from the table appears.
![]({{ site.baseurl }}/images/table-add-join.png "Add a join to a table")
5. Click **+Add join**.
The **Create Join** page appears.
![]({{ site.baseurl }}/images/table-create-join.png "Create a join from a table")
<table>
    <tr>
      <th>Legend</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>1.</td>
      <td>Select the data source of your table, either <em>Embrace</em>, or <em>Falcon</em>.</td>
    </tr>
    <tr>
      <td>2.</td>
      <td>Choose your connection from the dropdown <em>Connection</em> menu. You can only create joins between data sources uploaded through the same connection.</td>
    </tr>
    <tr>
      <td>3.</td>
      <td>Click <em> Enter join name</em> to name your join. Note that ThoughtSpot automatically names joins using the following syntax: [OriginDataSourceName]_to_[DestinationDataSourceName]. You can always enter a more meaningful join name, either when creating, or when editing the join.</td>
    </tr>
  </table>
6. Under **Table 1**, choose the table you want to create a join from (origin table).
7. Under **Table 2**, choose the destination table or View for the other end of the join.
8. Choose the matching columns under each table. These columns must use the same data type. [Optional] You can select multiple columns for the same join. To add another pair of matching columns to the join definition, click **+Add columns**.
9. Specify the join type; see (Join types).
10. Specify the join cardinality; see (Cardinality).
11. Click **Create join**.
