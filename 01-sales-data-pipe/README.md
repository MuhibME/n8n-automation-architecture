## 📊 Project 1: Multi-Branch Enterprise Sales Data Pipeline
<img width="1568" height="756" alt="image" src="https://github.com/user-attachments/assets/bd7cc393-ff40-49a0-8b8f-2cbf10d53c57" />

### 🔍 Project Overview
In enterprise environments, different departments require distinct outputs from a single primary data snapshot. Running duplicate API requests for separate workflows is highly inefficient and risks data discrepancies. 

This project establishes a production-grade data processing engine that connects securely to a remote data warehouse via header authentication, transforms flat array payloads into isolated objects, and branches out to serve three distinct operational requirements simultaneously:
1. **Operations Branch:** Aggregates and pushes all 50 verified individual orders into the fulfillment queue.
2. **Finance Branch:** Filters out incomplete orders, groups data by region, runs statistical summaries (Sum, Count, Average), and publishes analytics updates.
3. **Management Branch:** Generates a formatted binary CSV report containing critical metadata and execution timestamps for executive review.

---

### 🗺️ System Architecture & Node Routing
The workflow is designed deterministically using functional node naming conventions to ensure clarity, debuggability, and maintainability across engineering teams:

*   **Ingestion:** `TriggerManual` ➔ `GetSalesData` (HTTP Request utilizing secure token header authentication mapping)
*   **Transformation:** `SplitOrders` (Splits high-level payload array into individual processing loops) ➔ `SetOrderTotals` (Edit Fields node executing mathematical evaluation: `quantity * unit_price`)
*   **Operations Flow:** `AggregateOrders` (Compiles data back into a structured object list) ➔ `SendOrders` (POST request to operations endpoint)
*   **Analytics Flow:** `FilterDelivered` (IF node status validation switch) ➔ `SummarizeByRegion` (Data breakdown matrix calculation) ➔ `UpdateFieldNames` (Key renaming array mapping) ➔ `AggregateRegions` ➔ `SendAnalysis` (POST request to validation engine)
*   **Reporting Flow:** `SetReportMetadata` (Appends system execution context using `$now.format`) ➔ `ConvertToCSV` (Converts raw JSON items into an independent binary file stream) ➔ `SendReport` (Multi-part binary file HTTP upload)

---

### 🛠️ Technical Stack & Skills Verified
*   **Data Serialization:** JSON object syntax structure mapping, array separation, and key-value pair injections.
*   **Security & Auth:** Header-based API Authentication (`X-Assessment-ID`) moving away from insecure URL query parameters.
*   **Flow Engineering:** Data pinning, conditional routing logic arrays, data aggregation steps, and asynchronous sub-flow setups.
*   **File Management:** Converting abstract JSON data frames into local binary file buffers (CSV) and passing binary streams over HTTP POST requests.

---

### 🚀 How to Import and Run
1. Download the `project1-sales-data-pipeline.json` file from this repository.
2. Open your local or cloud-hosted n8n instance interface.
3. Create a blank workflow, click the top-right menu icon, select **Import from File**, and upload the JSON payload.
4. Configure your unique credentials inside the HTTP Request credential manager containers to clear authorization gates.
