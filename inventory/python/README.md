# Azure Redis Inventory - Python

This tool pulls usage statistics for Azure Cache for Redis instances. It interacts with Azure Monitor to retrieve metrics over a specified period (default 7-30 days).

## Purpose
Use this script when you need detailed usage data (Operations/Sec, Used Memory, Connections) to assess the workload. This helps in right-sizing for migration.

## Prerequisites
- **Python 3.8+**
- **Azure CLI** installed and logged in (`az login`)
- Permissions to read **Monitoring Metrics** on the target subscriptions/resources.

## Installation

```bash
# Recommended: Create a virtual environment
python -m venv venv
# Windows
.\venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# Install dependencies
pip install -r ../../requirements.txt
```

## Usage

Run the script from the root or this directory (adjusting paths).

```bash
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
