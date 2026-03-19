# Azure Redis Inventory - Python

This tool pulls usage statistics for Azure Cache for Redis instances. It interacts with Azure Monitor to retrieve metrics over a specified period (default 7-30 days).

## Purpose
Use this script when you need detailed usage data (Operations/Sec, Used Memory, Connections) to assess the workload. This helps in right-sizing for migration.

## Prerequisites
- **Python 3.11+** (Python 3.11 and 3.12 are tested and supported)
- **Azure CLI** installed and logged in (`az login`)
- Permissions to read **Monitoring Metrics** on the target subscriptions/resources.

## Installation

```bash
# Clone the repository
git clone https://github.com/AzureManagedRedis/migrate-to-amr-accelerator.git
cd migrate-to-amr-accelerator

# Recommended: Create a virtual environment
python -m venv venv
# Windows
.\venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# Install dependencies
python -m pip install -r requirements.txt
```

## Usage

Navigate to the script directory and run the script.

```bash
cd inventory/python
python pullAzureCacheForRedisStats.py
```

### Output
- Generates an Excel file `AzureStats.xlsx` in the current directory (or specified output dir).
- Columns include:
  - Subscription, RG, Region
  - SKU Details
  - **Avg Ops/Sec**
  - **Used Memory**
  - **Max Connections**

## Notes
- Includes both **Azure Cache for Redis** and **Redis Enterprise** instances by default.
