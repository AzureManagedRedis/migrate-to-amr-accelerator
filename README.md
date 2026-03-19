# Azure Redis Migration Accelerator

This repository provides a set of tools to **Discover** your Azure Redis estate and collect **Inventory & Usage Statistics** to assist with migration planning (e.g., migrating to Azure Managed Redis).

## 🚀 Getting Started

The workflow is split into two phases: **Discovery** and **Inventory (Assessment)**.

### Phase 1: Discovery (What do I have?)
Use the **Discovery Tool** for a lightweight, rapid scan of your environment.
- **Goal:** Identify all Redis resources, their SKUs, configurations, and *provisioned* capacity (vCPU/Memory).
- **Use when:** You just want a list of servers and what you are paying for, without waiting for metrics API calls.
- **Tool:** [Discovery Script (Python)](discovery/README.md) or [REDIS_DISCOVERY_GUIDE.md](discovery/REDIS_DISCOVERY_GUIDE.md)

### Phase 2: Inventory & Assessment (How is it used?)
Use the **Inventory Tools** to deep-dive into the workload.
- **Goal:** Collect detailed usage metrics (Operations Per Second, Used Memory, Connections) to understand the actual load.
- **Use when:** You are planning a migration and need to "right-size" the target cache based on actual consumption, not just provisioned size.
- **Tools:** Choose the version that fits your environment:
    - [Python Metric Collector](inventory/python/README.md) (Recommended)
    - [PowerShell Metric Collector](inventory/PowerShell/README.md)
    - [Bash / Cloud Shell Script](inventory/bash/README.md)
    - [Azure Resource Graph Query](inventory/AzureResourceGraph/README.md) (For simple high-level listing)

---

## 🔒 Security & Privacy

We understand that running scripts against production environments requires trust. Here is exactly what these tools do and do not do.

### 🛡️ Required Permissions
These tools operate entirely with **Read-Only** permissions. No write, contributor, or admin access is required.
- **Discovery:** Requires `Reader` role (specifically `Microsoft.Cache/*/read`).
- **Inventory:** Requires `Monitoring Reader` or `Reader` to access Azure Monitor metrics (`Microsoft.Insights/metrics/read`).

### What is collected?
- **Resource Metadata:** Subscription IDs, Resource Group names, Redis Cache Names, Regions, Tier/SKU information.
- **Configuration:** Shard counts, HA status, Version.
- **Usage Metrics (Inventory Phase only):**
    - `operationsPerSecond` (Average/Max)
    - `usedMemory`
    - `connectedClients`

### What is NOT collected?
- ❌ **NO Data values:** Use of `GET`/`SET` commands is never performed. No keys or values are read from the cache.
- ❌ **NO Connection Strings/Keys:** Access keys are not retrieved or exported.
- ❌ **NO PII:** No personal identifiable information is scanned.

### How it runs
- **Client-Side Execution:** All scripts run locally on your machine (or in your Cloud Shell).
- **Authentication:** Uses your local Azure CLI credentials (`az login` or `Connect-AzAccount`).
- **Data Destination:** Output is written to a local file (Excel `xlsx` or CSV) on your machine. **No data is sent to Microsoft or any third party automatically.** You choose who to share the output file with.

---

## Prerequisites
- **Azure CLI** or **Azure PowerShell Module**
- Python 3.11+ (for Python scripts)
- Read access to the Azure Subscriptions you wish to scan.
    - *Discovery*: Reader
    - *Inventory*: Monitoring Reader (to access metrics)

## License
MIT License - Copyright (c) Microsoft Corporation.

## Support

This project is provided "as-is" and is not officially supported by Microsoft. 

We welcome your feedback and contributions! If you encounter issues or have questions, please:
1. **Search** existing issues to see if your problem has already been reported.
2. **Open a new issue** in this repository if your problem is unique.

_Note: This code is for specific accelerator purposes and comes with no warranties or Service Level Agreements (SLAs)._
