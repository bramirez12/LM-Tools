# LM Tools

Standalone Windows desktop tools for LogicMonitor administrators. Each tool is a self-contained `.exe` — no installation, no stored credentials, no external dependencies beyond a JRE.

## Tools

| Tool | Purpose |
|---|---|
| **LM SDT Export** | Exports all active/scheduled Scheduled Downtimes (SDTs) to an Excel workbook, split into per-customer tabs plus a summary sheet (by customer, type, and admin). |
| **LM Datasource Threshold Report** | Reports on datasources, instances, and datapoints for a device group (optionally recursive), including current values, global vs. instance-level threshold overrides, alerting/collection status, poll interval, and polls-to-alert. |

## Prerequisites

- Java Runtime Environment **11 or later** installed on the machine running the tool
- A LogicMonitor **Bearer token** for your user (Settings → Users and Roles → your user → API Tokens, in the LM portal)

## Installation

1. Download the `.exe` for the tool you need
2. Extract it from the zip, if applicable
3. Right-click the `.exe` → **Properties** → check **Unblock** → **OK**
   (Windows flags downloaded executables from the internet by default; this step removes that block so the tool will run)
4. Double-click to run

No installer, no admin rights, and nothing is written outside the report location you choose.

## Usage

1. Launch the tool
2. Enter your **portal name** (e.g. `yourcompany` — the tool appends `.logicmonitor.com` automatically)
3. Enter your **Bearer token**
4. Fill in any tool-specific fields (see below)
5. Run the report and choose where to save the resulting `.xlsx`

Credentials are used only for the duration of the report run and are never written to disk.

### LM Datasource Threshold Report — additional fields

| Field | Notes |
|---|---|
| Device group ID | The numeric ID of the LogicMonitor device group to report on |
| Recursive | Include devices in sub-groups |
| Datasource filter | Optional — filters to a single datasource |

> **Important:** When filtering by datasource, use the DataSource **name**, not the **label**. These are frequently different in LogicMonitor — the label is what's shown in the UI, while the name is the internal identifier the API expects. You can confirm the correct name from the datasource's properties in the LogicModule Exchange or via **Settings → DataSources → (your datasource) → Info**.

## Output

Both tools produce a standard `.xlsx` workbook that opens in Excel or any compatible spreadsheet application — no macros, no external formatting dependencies.

## Troubleshooting

| Symptom | Cause / Fix |
|---|---|
| Windows SmartScreen warning on first run | Expected for an unsigned `.exe` — click **More info → Run anyway**, or complete the Unblock step above first |
| Tool won't launch | Confirm JRE 11+ is installed and on your `PATH` (`java -version` in a command prompt) |
| "Instance Threshold Override: Yes" on datapoints you never touched | Fixed in current builds — update if you're on an older version; this was caused by LM's API returning a record for every datapoint regardless of customization |
| Report is empty or errors on export | Verify the Bearer token is valid and the portal name doesn't include `.logicmonitor.com` (it's added automatically) |

## Notes

- These tools use the LogicMonitor REST API v3 with Bearer token authentication.
- No credentials, tokens, or customer data are transmitted anywhere other than your LogicMonitor portal.
