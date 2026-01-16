# Azure Redis Inventory - Azure Resource Graph (KQL)

This folder contains Kusto Query Language (KQL) queries for performing a high-level inventory of your Redis estate using Azure Resource Graph.

## Purpose
Use this query when you need a **fast, instant list** of all Redis resources across your entire tenant/management group, without waiting for metric collection. This is useful for:
- Identifying all Azure Cache for Redis assets.
- Checking SKU distribution.
- verifying Provisioning State.

## Usage

1. Go to the **Azure Portal**.
2. Search for **"Resource Graph Explorer"**.
3. Copy the content of `pull-AzureCacheforRedis.kql`.
4. Paste it into the query window.
5. Click **Run Query**.
6. (Optional) "Export to CSV" to save the results.

## Output
A table containing:
- Resource ID, Subscription, Region, SKU Name, Capacity.
- Normalized Shard Counts (for clustered instances).
- Does **not** include usage metrics (Ops/Sec, Memory Used).
