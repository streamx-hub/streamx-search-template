# StreamX Search

This repository provides a Search project built on StreamX, designed to quickly deliver a fully functional full-text and faceted search powered by a microservices-based mesh architecture.

The project is complemented by the [StreamX Search UI](https://github.com/streamx-hub/streamx-search-ui) frontend library, which provides ready-to-use components for building search experiences in websites and web applications.

Together, **StreamX Search** and **StreamX Search UI** provide an end-to-end solution that makes it easy to add search capabilities to a website—from indexing and querying content to presenting search results, filters, and facets in the user interface.

---

# Data Ingestion & Custom Sources

## Ingesting Data Using StreamX CLI

You can use the StreamX CLI to ingest data from the files.

### 1. Install StreamX CLI

```bash
brew install streamx-com/tap/streamx
```

### 2. Configure ingestion endpoint

1. Go to **Gateways** in the StreamX Console
2. Copy the **REST Ingestion URL**
3. Set it in CLI:

```bash
streamx settings set streamx.ingestion.url <INGESTION_URL>
```

### 3. Configure authentication

1. Go to **Sources** tab in the StreamX Console
2. Copy the **pages token**
3. Set it in CLI:

```bash
streamx settings set streamx.ingestion.auth-token <TOKEN>
```

### 4. Publish data

Use [publish commands](https://streamx-com.github.io/streamx-cli/latest/commands/publish/) to ingest pages which you want to index in search. e.g.:
```bash
streamx publish event page.published <path_to_html_file> <page_path>
```

### 5. Query the search

1. Go to **Gateways** in the StreamX Console
2. Open the URL for:
    ```
    opensearch-sink
    ```
3. Ensure `/search/pages?query=<query_text>` in URL. Where `<query_text>` is the text that you are seraching for.
---

## Connecting Your Own Data Source

To integrate your own data (e.g. EDS or AEM):

* Use one of the available **StreamX connectors**, or
* Build a **custom connector**

### How integration works

Integration with external systems follows the same pattern as CLI ingestion:

* You need to provide:

    * **Ingestion URL**
    * **Authentication token**

These should be configured inside your connector instead of the CLI.

Your connector is responsible for:

* Fetching data from your external system
* Transforming it into StreamX-compatible events
* Sending it to the ingestion endpoint