# Get-started-with-Real-Time-Intelligence-in-Microsoft-Fabric
# Real-Time Intelligence Lab with Microsoft Fabric

This repository provides a concise walkthrough for implementing Real-Time Intelligence in Microsoft Fabric. You will ingest, analyze, and visualize a live stream of stock market data using Fabric’s eventstream and eventhouse capabilities.

## Lab Objectives

1. **Create a Workspace**  
   - Set up a Microsoft Fabric workspace with real-time capacity enabled.

2. **Create an Eventstream**  
   - Connect to the Stock Market sample data source.
   - Name the eventstream `stock-data-stream`.

3. **Create an Eventhouse**  
   - Provision an Eventhouse for real-time data storage.
   - Capture streaming data into a KQL table named `stock`.

4. **Query Captured Data**  
   - Use Kusto Query Language (KQL) to:
     - Retrieve the latest 100 records.
     - Compute average bid price per symbol over the last 5 minutes.

5. **Create a Real-Time Dashboard**  
   - Pin the average price query to a new dashboard (`Stock Dashboard`).
   - Edit the tile to display a Column chart of average prices.

6. **Create an Alert**  
   - Configure an Activator alert to notify via email when `avgPrice` increases by 100.
   - Run the alert query every 5 minutes, grouped by `symbol`.

7. **Clean Up Resources**  
   - Delete the workspace to remove all lab artifacts.

---

## Example KQL Queries

```kql
// Retrieve latest 100 records
stock
| take 100

// Average bid price per symbol in last 5 minutes
stock
| where ["time"] > ago(5m)
| summarize avgPrice = avg(todecimal(bidPrice)) by symbol
| project symbol, avgPrice
```

---

## Alert Configuration

- **Run query every**: 5 minutes  
- **Grouped by**: `symbol`  
- **Condition**: `avgPrice` increases by 100  
- **Action**: Send email notification  

---

© Microsoft Learn | Real-Time Intelligence Lab
