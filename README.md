# Azure KeyVault Insights
The 'Azure Key Vault Insights' workbook offers a comprehensive view of your Azure Key Vault resources.

This workbook enables teams to centrally monitor Azure Key Vault inventory, configuration, metrics, and logs, and to identify and troubleshoot issues (401/403/429, etc.) across multiple vaults.

## Introduction
The comprehensive view of Azure Key Vaults resources, allowing teams to review Permission model (`RBAC` or `Access Policy`) and network configurations (`Public Network Access` and `Private Endpoint Connections`), including whether vaults are accessible from the internet. By leveraging metrics and logs, teams can easily monitor Key Vault usage, identify trends, and quickly detect errors across multiple vaults.

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/ae176ff7-b3bd-4afb-b2ba-b696b61eef24" />

## How to use

Importing this Workbook to your Azure environment is quite simple.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdolevshor%2FAzure-KeyVault-Insights%2Frefs%2Fheads%2Fmain%2FWokbook%2FAzure%2520Key%2520Vault%2520Insights.json)

### Manual deploy

Import to Workbook Gallery
- Open **Azure Monitor → Workbooks**
- Click **New** → **Advanced editor**
- Paste the workbook content (Click **Copy Raw file**)
  - For [Gallery Template](https://github.com/dolevshor/Azure-KeyVault-Insights/blob/main/Wokbook/Azure%20Key%20Vault%20Insights.workbook)
  - For [ARM Template](https://github.com/dolevshor/Azure-KeyVault-Insights/blob/main/Wokbook/Azure%20Key%20Vault%20Insights.json)
- Click **Apply**
- Click **Save**

## Structure and Views 

### Structure

This workbook includes three main sections:
- **Overview** - Holistic view of Azure Key Vault resources
- **Monitor** - Holistic view of Azure Key Vault resources Metrics
- **Insights** - Holistic view of Azure Key Vault resources Logs
  - Requires Diagnostic Settings enabled and connected to a Log Analytics workspace

<img width="1303" height="1384" alt="image" src="https://github.com/user-attachments/assets/85e09a2b-e54a-4095-9522-e3b9fd7e94f0" />

### Views

Types of views this workbook includes:

- **Overview**
  - Azure Key Vault Resources by
    - SubscriptionId
    - Resource Group
    - Location
    - Permission model
    - Public Network Access
    - Private Network Access
  - All Azure Key Vault Resources

> The information displayed uses [KQL](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/) queries to query the [Azure Resource Graph](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview).

> [!TIP]
> This view shows a simple way to identify Key Vaults without RBAC permissions and Key Vaults that are accessible from the internet:

<img width="1302" height="357" alt="image" src="https://github.com/user-attachments/assets/530eeea6-ac2a-41af-81d1-06d7a05b93c3" />

- **Monitor**
  - Overview
    - Total Requests
    - Average latency
    - Saturation
    - Availability
  - Status Code
    - Successes (2xx)
    - Failures (4xx)
    - Unauthorized (401)
    - Forbidden (403)
    - Not Found (404)
    - Throttling (429)
    - Others
  - Activity
    - Requests
    - Requests timeline
    - Requests Successes
    - Requests failures
    - Average Latency

> The information displayed uses Azure Key Vault Platform Metrics.

- **Insights**
  - Overview
    - Requests
      - by Resource
      - by ResultSignature
      - by OperationName
      - by CallerIPAddress
  - All Logs

## Diagnostic logs (required for *Insights*)
To use the **Insights** tab, enable Key Vault [diagnostic settings](https://learn.microsoft.com/en-us/azure/azure-monitor/platform/diagnostic-settings?tabs=portal) and send logs to a **Log Analytics Workspace**:
- Azure Key Vault diagnostic settings → send to Log Analytics

> If you only want Inventory + Metrics, you can still use the workbook without Log Analytics, but Insights will be empty.


## Permissions

- Reader role (or higher) on the subscriptions containing Key Vaults (for Resource Graph + Metrics)
- Access to the Log Analytics workspace used for diagnostics (for Insights)
