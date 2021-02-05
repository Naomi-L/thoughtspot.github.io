---
title: [Pinboard Download API]
summary: "You can download a Pinboard, or specific visualizations from the Pinboard, as a PDF."
last_updated: 2/4/2021
sidebar: mydoc_sidebar
redirect_from:
permalink: /:collection/:path.html
---

This API enables you to programmatically download Pinboards or certain visualizations from the Pinboards as a PDF.

You can also [download an embedded Pinboard with unsaved changes](#embed).

This feature is the API version of the [download a Pinboard as a PDF]({{ site.baseurl }}/end-user/pinboards/download-pinboard-pdf.html) UI feature. The API parameters refer to options in the UI. To see these options in the UI, refer to [Download a Pinboard as a PDF]({{ site.baseurl }}/end-user/pinboards/download-pinboard-pdf.html).

## Resource URL

<code class="api-method-post">post</code> /tspublic/v1/export/pinboard/pdf

## Request Parameters

<table>
   <colgroup>
      <col style="width:20%" />
      <col style="width:15%" />
      <col style="width:45%" />
      <col style="width:10%" />
      <col style="width:10%" />
   </colgroup>
   <thead>
      <tr>
         <th>Form Parameter</th>
         <th>Data Type</th>
         <th>Description</th>
         <th>Mandatory?</th>
         <th>Default</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td><code>id</code></td>
         <td>string</td>
         <td>ID (GUID) of the Pinboard to download</td>
         <td>Yes, unless using the <code>transient_pinboard_content</code> parameter.</td>
         <td>None</td>
      </tr>
     <tr>
         <td><code>layout_type</code></td>
         <td>string [PINBOARD/VISUALIZATION]</td>
         <td>For <code>PINBOARD</code>, the PDF looks like the Pinboard does in the UI. For <code>VISUALIZATION</code>, the PDF has one visualization for each page.</td>
         <td>Yes</td>
         <td>PINBOARD</td>
      </tr>
      <tr>
         <td><code>orientation</code></td>
         <td>string [PORTRAIT/LANDSCAPE]</td>
         <td>Specifies portrait or landscape mode.</td>
         <td>Yes</td>
         <td>LANDSCAPE</td>
      </tr>
      <tr>
      <td><code>truncate_tables</code></td>
      <td>boolean</td>
      <td>If set to true, displays only the first page of the tables. Only applicable in Visualization layout.</td>
      <td>Yes, if <code>layoutType</code> is <code>VISUALIZATION</code></td>
      <td>false</td>
         </tr>
     <tr>
     <td><code>visualization_ids</code></td>
     <td>string</td>
     <td>Only select specific visualizations to include. Only applicable in Visualization layout.</td>
     <td>Yes, if <code>layoutType</code> is <code>VISUALIZATION</code></td>
     <td>none</td>
      </tr>
      <tr>
      <td><code>include_logo</code></td>
      <td>boolean</td>
      <td>Include customized wide logo if available in the footer</td>
      <td>Yes</td>
      <td>true</td>
      </tr>
      <tr>
      <td><code>footer_text</code></td>
      <td>string</td>
      <td>Any footer text to be included in the footer of each page of the PDF</td>
      <td>No</td>
      <td>none</td>
      </tr>
      <tr>
      <td><code>include_page_number</code></td>
      <td>boolean</td>
      <td>Whether to include a footer with the page number</td>
      <td>Yes</td>
      <td>true</td>
      </tr>
      <tr>
      <td><code>include_cover_page</code></td>
      <td>boolean</td>
      <td>Whether to inclue a cover page displaying the Pinboard title</td>
      <td>Yes</td>
      <td>true</td>
      </tr>
      <tr>
      <td><code>include_filter_page</code></td>
      <td>boolean</td>
      <td>Whether to include a second page with a list of all applied filters</td>
      <td>Yes</td>
      <td>true</td>
      </tr>
      <tr>
      <td><code>transient_pinboard_content</code></td>
      <td>string</td>
      <td>For use when embedding ThoughtSpot. If the Pinboard has unsaved changes, pass this parameter, and use the <a href="{{ site.baseurl }}/reference/api/about-JS-API.html">JavaScript API</a>.</td>
      <td>Yes, unless using the <code>id</code> parameter.</td>
      <td>none</td>
      </tr>       
   </tbody>
</table>

## Request Example

##### cURL

```

curl --location --request POST 'http://<instance>/callosum/v1/tspublic/v1/export/pinboard/pdf' \
--header 'Accept: application/octet-stream' \
--header 'X-Requested-By: ThoughtSpot' \
--header 'Cookie: JSESSIONID=71cc2672-7ead-4480-be7d-b6ad52023e98; userGUID=59481331-ee53-42be-a548-bd87be6ddd4a; Callosum-Download-Initiated=false' \
--form 'id="061457a2-27bc-43a9-9754-0cd873691bf0"' \
--form 'layout_type="PINBOARD"' \
--form 'orientation="LANDSCAPE"' \
--form 'truncate_tables="false"' \
--form 'include_logo="true"' \
--form 'include_page_number="true"' \
--form 'include_filter_page="true"' \
--form 'include_cover_page="true"'
```

{% include note.html content="You must send the <code>X-Requested-By</code> header in your request. Without it, the request fails." %}

##### Request URL

```
https://<instance>/callosum/v1/tspublic/v1/export/pinboard/pdf
```

## Response Example
The response appears in the form of a raw pdf file. The response type is `application/octet-stream`.

## Runtime filters
You can modify the API's output by appending runtime filters at the end of the resource URL, with a specific syntax. For example:

```
https://<instance>/callosum/v1/tspublic/v1/export/pinboard/pdf?col1=COL_NAME1&op1=OP_TYPE1&val1=VALUE1&coln=COL_NAMEn&opn=OP_TYPEn&valn=VALUEn
```

You can add more than one filter by specifying `col2`, `op2`, `val2`, and so on.

| Parameter | Definition |
| --- | --- |
| col*n* | Name of the column to filter on |
| op*n* | {IN, EQ, NE, LT, LE...} |
| val*n* | Value of the column to filter on. |

{% include note.html content="These parameters are case-insensitive. <code>EQ</code>, <code>eq</code>, and <code>eQ</code>, for example, have the same result." %}

### Runtime filter operators

|Operator|Description|Number of Values|
|--------|-----------|----------------|
|`EQ`|equals|1|
|`NE`|does not equal|1|
|`LT`|less than|1|
|`LE`|less than or equal to|1|
|`GT`|greater than|1|
|`GE`|greater than or equal to|1|
|`CONTAINS`|contains|1|
|`BEGINS_WITH`|begins with|1|
|`ENDS_WITH`|ends with|1|
|`BW_INC_MAX`|between inclusive of the higher value|2|
|`BW_INC_MIN`|between inclusive of the lower value|2|
|`BW_INC`|between inclusive|2|
|`BW`|between non-inclusive|2|
|`IN`|is included in this list of values|multiple|

{: id="embed"}
## Embedded Pinboard with unsaved changes
If your ThoughtSpot environment is embedded, and you want to download Pinboards with unsaved changes as PDFs, you must use the [JavaScript API]({{ site.baseurl }}/reference/api/about-JS-API.html) and pass the <code>transient_pinboard_content</code> parameter in the browser fetch request, using the `getExportRequestForCurrentPinboard` method.

The signature for this API method is as follows:

```
function getExportRequestForCurrentPinboard(frame: HTMLIframeElement): Promise<string>;
```

The promise returned resolves with a string that contains, encoded as JSON, the transient pinboard content which to send to the `/callosum/v1/tspublic/v1/export/pinboard/pdf` endpoint under the key `transient_pinboard_content`. This content resembles the current Pinboard as is, including any changes, saved or not.

### Sample browser fetch request
```
<iframe src="http://ts_host:port/" id="ts-embed"></iframe>
<script src="/path/to/ts-api.js"></script>
<script>
const tsFrame = document.getElementById("ts-embed");
async function downloadPDF() {
  const transientPinboardContent = await thoughtspot.getExportRequestForCurrentPinboard(tsFrame);
  const pdfResponse = await fetch("http://ts_host:port/callosum/v1/tspublic/v1/export/pinboard/pdf", {
    method: "POST",
    body: createFormDataObjectWith({
      "layout_type": "PINBOARD",
      "transient_pinboard_content": transientPinboardContent,
    }),
  });
  // Do something with pdfResponse.blob()
}
</script>
```

### Response Example
The response appears in the form of a raw pdf file. The response type is `application/octet-stream`.

## HTTP status codes
You may receive the following status codes in your output. These HTTP status codes have the following meanings:

| Status code | Meaning |
| --- | --- |
| 200	| Streaming output for pinboard pdf |
| 400	| Invalid parameter values |
| 403	| No read access for pinboard |
| 404	| Object not found |
