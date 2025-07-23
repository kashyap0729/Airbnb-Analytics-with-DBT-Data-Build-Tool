
# 🏡 Airbnb Data Pipeline: Ingestion, Transformation, Visualization & MCP Integration

This project demonstrates an end-to-end modern data stack solution to ingest, transform, and visualize Airbnb data, with cutting-edge **MCP (Model Context Protocol)** integration for AI-driven insights and automation.

---

## 🧱 Components Overview

### 1. **Data Ingestion**

* **Source**: Raw Airbnb listings data.
* **Storage**: Stored in **Amazon S3** for scalable, cost-effective storage.

### 2. **Data Transformation**

* **Warehouse**: **Snowflake** used to store, clean, and process data.
* **dbt**:

  * Models raw Airbnb data into views, tables, and incremental models.
  * Implements **SCD Type 2** using dbt snapshots.
  * Tracks **data freshness** and quality with tests and expectations.
  * Applies **custom/generic testing** using macros.
  * Documents models via **dbt Exposures**.
  * Manages permissions with dbt hooks.

### 3. **Orchestration**

* **Dagster** automates the pipeline with:

  * Partitioned + incremental model runs.
  * Scheduled workflows and backfills.

### 4. **Visualization**

* **Preset** provides interactive dashboards and exploration for stakeholders.

---

## 🔌 5. MCP Integration (Model Context Protocol)

MCP (Model Context Protocol) enables **secure and structured communication between AI tools and your dbt project**, unlocking:

* Model discovery
* Trusted metric querying
* Job execution (run/test/build)

### 🔎 Capabilities via MCP:

* `get_all_models` – list dbt models.
* `get_model_details`, `get_model_parents` – model metadata & lineage.
* `list_metrics`, `get_dimensions`, `query_metrics` – semantic metrics access.
* `dbt run`, `dbt build`, `dbt test` – execute dbt CLI commands safely via LLMs or agents.

### 🔧 Example Use Cases

* Ask: *“What are all the fact tables and their dependencies?”* → Uses `get_model_parents`
* Ask: *“Get the total listings in June with max, min, average”* → `query_metrics`
* Ask: *“Run freshness tests for the staging models”* → `dbt test`

### 🛠 MCP Setup

```bash
# Clone and set up dbt MCP server
git clone https://github.com/dbt-labs/dbt-mcp
cd dbt-mcp
pip install -r requirements.txt

# Set environment for dbt Core project
export DBT_PROJECT_DIR=../your_dbt_project
export DBT_CLI_PATH=$(which dbt)

# Start MCP server
mcp-server start
```

You can now use tools like **Claude Desktop, Cursor, VS Code** to chat with your dbt project via this interface.

---

## 🗺 Project Workflow

```
            ┌────────────┐
            │ Airbnb Raw │
            │    Data    │
            └─────┬──────┘
                  ↓
           ┌────────────┐
           │   Amazon   │
           │     S3     │
           └─────┬──────┘
                 ↓
        ┌────────────────┐
        │  Snowflake DB  │
        └─────┬────┬─────┘
              ↓    ↓
       ┌────────┐ ┌────────┐
       │   dbt  │ │   MCP  │
       └────┬───┘ └────┬───┘
            ↓          ↓
        ┌────────┐  ┌─────────────┐
        │ Dagster│  │ AI/LLM Tool │
        └────┬───┘  └────┬────────┘
             ↓           ↓
        ┌────────────────────┐
        │     Preset         │
        │  Dashboards (UI)   │
        └────────────────────┘
```

---

## 🚀 Quick Start

1. **Upload Data to S3**
2. **Run dbt models**

   ```bash
   dbt run
   ```
3. **Schedule via Dagster**
4. **Start MCP server**
5. **Open Preset dashboard or connect AI tool**

---

## 🧪 Testing & Validation

* dbt tests: uniqueness, null checks, referential integrity
* Custom macros: advanced rule enforcement
* dbt expectations framework: behavioral testing
* MCP-triggered tests via LLM for automated QA

---

## 📊 Dashboard Example

<img width="1867" height="967" alt="ConnectingDBTMCP" src="https://github.com/user-attachments/assets/22a00573-c00e-448e-855a-9fae590b4215" />


* **Key Metrics**:

  * Avg Listings (June): `114.57`
  * Max: `154`, Min: `91`
* **Weekend Avg**: `141.3` vs Weekday Avg: `101.2`
* **Insights**:

  * Weekends show higher availability
  * Listings fluctuate heavily mid-month

---

## 📚 Resources

* [dbt Official Docs](https://docs.getdbt.com/)
* [dbt + Snowflake Guide](https://www.getdbt.com/data-platforms/snowflake)
* [MCP Intro](https://docs.getdbt.com/blog/introducing-dbt-mcp-server)
* [MCP Spec (Anthropic)](https://en.wikipedia.org/wiki/Model_Context_Protocol)
