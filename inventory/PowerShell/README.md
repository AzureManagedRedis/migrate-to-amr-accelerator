# Azure Redis Inventory - PowerShell

This script retrieves usage statistics for Azure Cache for Redis instances using the Azure PowerShell module.

## Purpose
Use this script if you prefer a PowerShell environment to collect workload metrics (Ops/Sec, Memory, Connections) for assessment and right-sizing.

## Prerequisites
- **PowerShell 5.1+** or **PowerShell Core 7+**
- **Az PowerShell Module** (`Install-Module -Name Az`)
- Authenticated session (`Connect-AzAccount`)

## Usage

```powershell
.\Pull-Azure-Cache-For-Redis-Stats.ps1
```

### Output
- Generates a CSV file `AzureStats.csv` in the current directory.
- Includes details for all shards in clustered instances.

## Notes
- Automatically detects and includes **Azure Cache for Redis Enterprise** instances.
