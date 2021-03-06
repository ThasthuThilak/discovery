---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-27"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:gif: data-image-type='gif'}

# Smart Document Understanding
{: #sdu}

Smart Document Understanding (SDU) trains {{site.data.keyword.discoveryfull}} to extract custom fields in your documents. Customizing how your documents are indexed into {{site.data.keyword.discoveryshort}} improves the answers that your application returns.

With SDU, you annotate fields within your documents to train custom conversion models. As you annotate, Watson is learning and starts to predict annotations. SDU models can be exported and used on other collections. 

## Supported document types and browsers
{: #doctypes}

Supported document types for Smart Document Understanding: 
-  Lite plans: PDF, Word, PowerPoint, Excel, JSON\*, HTML\*
-  Advanced plans: PDF, Word, PowerPoint, Excel, PNG\*\*, TIFF\*\*, JPG\*\*, JSON\*, HTML\* 

\* JSON and HTML documents are supported by {{site.data.keyword.discoveryfull}}, but can not be edited using the SDU editor. To change the configuration of HTML and JSON docs, you need to use the API. For more information, see the [API reference](https://{DomainName}/apidocs/discovery/){: external}.

\*\* Individual image files (PNG, TIFF, JPG) are scanned and the text (if any) is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned and the text, if any, is extracted.

## Using the Smart Document Understanding editor
{: #annotate}

<!-- Learn more topic WDS -->
The SDU editor is only available for collections that contain supported document types and do not have the Element Classification enrichment applied. If you do not want to use the SDU editor, you can set up your configuration using the API, see the [API reference](https://{DomainName}/apidocs/discovery/){: external}.
{: important}

The SDU editor functions are only available in the {{site.data.keyword.discoveryshort}} tooling, they are not available in the API.
{: note}

Navigating the Smart Document Understanding editor:

If you did not yet create a {{site.data.keyword.discoveryshort}} instance and environment, see [Getting started](/docs/discovery?topic=discovery-getting-started) for instructions.
{: tip}

1. On the **Manage Data** screen, click the **Upload your own data** button and create a new Private collection in {{site.data.keyword.discoveryshort}}.
1. If you wish, drag and drop documents into your collection, or click **browse from computer** to upload documents. After the upload is complete, this information displays:
   -  The fields identified from your documents.
   -  Enrichments applied to your documents. The Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging enrichments are automatically applied to the `text` field by {{site.data.keyword.discoveryshort}} (unless you are importing documents using a connector). You can add (or remove) additional enrichments to the `text` (and other) fields.
   -  Pre-built queries you can run immediately.
1. Click **Configure data** on the upper right. On the **Configure data** screen, there are three tabs: **Identify fields**, **Manage fields**, and **Enrich fields**.

   - **Identify fields** contains the SDU editor. 
   - **Manage fields** lists all indexed fields (all fields are indexed by default). Switch off any fields you do not want to index. For example, your PDFs might contain a running header or footer that does not contain useful information, so you can exclude those fields from the index. You can also split documents here, based on fields, see [Splitting documents](/docs/discovery?topic=discovery-sdu#splitting).
   - **Enrich fields** is identical to the **Enrich** tab on the original screen. For more information about enrichments, see [Adding enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments). The **Upload sample documents** option is not available with SDU collections.

   If you did not upload any documents earlier, return to the **Overview** screen by clicking the name of your collection in the upper left, or click the ![Manage Data](/images/icon_yourData.png) icon and choose your collection. Drag and drop documents into your collection, or click **browse from computer**. After you initially upload your documents, the **Upload documents** button displays on the upper right.
   {: important}

1. Open the **Identify fields** tab. A maximum of twenty (20) documents from your collection automatically loads in the Smart Document Understanding editor.

You can use the toolbar at the top to complete the following actions:
- Choose a document to annotate
- Navigate the document displayed
- Adjust the page view (`single page view`, `zoom in`, `zoom out`), `clear changes`, and `export/import models`. Click on `single page view` to toggle the display - you can view your annotations and document separately, or together.

You can also crawl various data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling. Click the **Connect a data source** button and see [Connecting to data sources](/docs/discovery?topic=discovery-sources) for more information. 
{: tip}

## How to annotate a document
{: #documents}

See [Best practices for annotating documents](/docs/discovery?topic=discovery-sdu#bestpractices) before you begin annotating.

1. A default set of fields appears to the right of your document. The available fields are `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, `title`, `image`, and `table`. If you would like to create one or more new custom field labels, click **Create new**. You are limited to the following number of custom labels: Lite plans - `0`, Advanced plans - `10`, Premium plans - `100`.
1. Click on a field label on the right to activate it.
1. Click on the content representing that field in the SDU editor. The content highlights with the corresponding field label color.
   - Alternately, you can select a field label on the right, and drag it to the content in the SDU editor.
   - To clear a change, click the **Clear change** button on the toolbar.
1. Click **Submit**.
   
   As you annotate, Watson is learning and starts to predict annotations. Continue annotating, until Watson correctly and consistently identifies fields.
   {: note}

1. After you finish annotating, click **Apply changes to collection.** The **Upload your documents** screen opens. Re-upload the documents in your collection. After uploading is complete, you are redirected to the **Overview** screen.

Field | Definition  
------ | ------ 
answer | In a Q/A pair (often in an FAQ), the answer to the question.
author | Name of author (or authors).
footer | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the bottom of the page.
header | Use this tag to denote meta-information about the document that appears at the top of the page.
question | In a Q/A pair (often in an FAQ), the question.
subtitle | The secondary title of the document being annotated. 
table_of_contents | Use this tag on listings in the document table of contents.
text | Use this tag for standard copy text, including paragraphs, definitions, or any set of words that is not a title, part of a table, answer, author, subtitle, header, or a footer. 
title | The main title of the document being annotated.
table |	Use this tag to annotate tables in your document.
image |	Use this tag to annotate images and diagrams in your document.

## Splitting documents
{: #splitting}

<!-- Learn more topic WDS -->
The **Manage fields** tab contains the option to **Improve query results by splitting your documents**. This option allows you to split your documents into segments based on a field name. After the document splits, each segment is a separate document that is enriched, indexed, and returned as a separate query result.

Documents are split based on a single field name, for example: `title`, `author`, `question`. 

Considerations:

  - The number of segments per document is limited to `250`. Any document content remaining after `249` segments are stored within segment `250`.

  - Each segment counts towards the document limit of your plan. {{site.data.keyword.discoveryshort}} indexes segments, until the plan limit is reached. For document limits, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans).

  - PDF and Word metadata, as well as any custom metadata, is extracted and included in the index with each segment. Every segment of a document includes identical metadata.

  - If a split document is updated and needs to be re-uploaded, it is recommended that you replace the document, using the [Update document](https://{DomainName}/apidocs/discovery#update-a-document){: external} method. It is recommended that you upload the document, using the POST method of the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API, specifying the contents of the `parent_id` field of one of the current segments as the `{document_id}` path variable. All segments are overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments remain in the index and can be individually deleted, using the API. For details, see the [API Reference](https://{DomainName}/apidocs/discovery#delete-a-document){: external}.

## Importing and exporting models
{: #import}

After you define a model with the SDU editor, you can save it and reuse it on other collections.

You can import or export your completed SDU model using the toolbar at the top of the editor. Click the last icon and choose `Import model` or `Export model`.

Exported models have the file extension of `.sdumodel`.

An imported model is intended to be used without any further annotations. If you continue annotating after importing it, the model is overwritten. If you plan to import a model into a new collection, it is a good best practice to create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.

## Best practices for annotating documents
{: #bestpractices}

- Follow all guidelines and use consistent labeling on all documents
- Do not label whitespace
- Use the `image` labels on images and diagrams
- Do not treat **bold**, _italic_, or underlined text differently. Label based on the context, not the style.
- When labeling a document, work from the first page to the last.
- If you incorrectly label an item, choose another label for the item to overwrite the first.
- Pages can be submitted at any time. Ensure that all appropriate labeling is complete before submitting.
- Documents that appear to have text overlaying other text are considered “double overlaid” and cannot be annotated. Report these documents to your administrator.
- Documents that contain multiple columns of text on a single page cannot be annotated. Report these documents to your administrator.
- It is recommended that you only label footnotes when they appear at the bottom of the page and are referenced in the main body of text in the document.
- It is recommended that you label notes that appear within sections or lists, for example, explicitly called out as “Notes,” as `text`.
- When annotating a table, make sure to select the entire table before applying the `table` label.