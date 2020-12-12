<h2>Possible Joins</h2>
<dl>
<dlentry id="join-worksheet">
    <dt>Origin: Worksheet</dt>
    <dd>Destination: Tables uploaded through the UI</dd>
    <dd>Necessary permissions: <strong>Can edit</strong> permission on source Worksheet</dd>
</dlentry>
<dlentry id="join-view">
    <dt>Origin: View</dt>
    <dd>Destination: other Views, Materialized Views, tables imported through the UI, tables uploaded from backend (tsload) or through DataFlow</dd>
    <dd>Necessary permissions: <strong>Can edit</strong> permission on source View</dd>
</dlentry>
<dlentry id="join-materialized-view">
    <dt>Origin: Materialized View</dt>
    <dd>Destination: Views, other Materialized Views, tables imported through the UI, and tables uploaded from backend (tsload) or through DataFlow</dd>
    <dd>Necessary permissions: <strong>Can edit</strong> permission on source Materialized View</dd>
    <dd>Note: For tables loaded from backend, it is best practice to create the join through ThoughtSpot UI, rather than using TQL.</dd>
</dlentry>
<dlentry id="join-imported-table">
    <dt>Origin: Imported table (UI)</dt>
    <dd>Destination: Worksheets, Views, Materialized Views, tables imported through the UI, tables uploaded from backend (tsload) or through DataFlow</dd>
    <dd>Necessary permissions: <strong>Can edit</strong> permission on source table</dd>
</dlentry>
<dlentry id="join-tsload-table">
    <dt>Origin: Table uploaded from backend (tsload) or through DataFlow</dt>
    <dd>Destination: Views, Materialized Views, tables imported through the UI, tables uploaded from backend (tsload) or through DataFlow</dd>
    <dd>Necessary permissions: <strong>Can edit</strong> permission on source table</dd>
    <dd>Note: For joins from tables uploaded through tsloard to Materialized Views and other tables uploaded through tsload, it is best practice to create the join through ThoughtSpot UI, rather than using TQL.</dd>
</dlentry>
<dlentry id="join-table-embrace">
      <dt>Origin: Table uploaded through Embrace</dt>
      <dd>Destination: other tables uploaded through Embrace, Views on top of tables uploaded through Embrace</dd>
      <dd>Necessary permissions: <strong>Can edit</strong> permission on source table, and <strong>can manage data</strong> permission</dd>
      <dd>Note: The join must be created between two tables or a table and a View from the same connection.</dd>
</dlentry>
<dlentry id="join-view-embrace">
      <dt>Origin: View on top of a table uploaded through Embrace</dt>
      <dd>Destination: Tables uploaded through Embrace, other Views on top of tables uploaded through Embrace</dd>
      <dd>Necessary permissions: <strong>Can edit</strong> permission on source View</dd>
      <dd>Note: The join must be created between two Views or a table and a View from the same connection.</dd>
</dlentry>
</dl>
