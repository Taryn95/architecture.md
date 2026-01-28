```mermaid
flowchart LR

subgraph Source_Systems["Operational Source Systems (Data Silos)"]
    Sage["Sage X3 ERP\n(Orders, Invoices, Costs)"]
    Freshdesk["Freshdesk\n(Quotes, Tickets, Partner Interactions)"]
    OrderEasi["OrderEasi\n(Partner Quotes, Carts)"]
    PricingMod["Pricing Modulator\n(Pricing Rules, Margins)"]
end

subgraph Ingestion["Data Ingestion Layer"]
    API["APIs / Connectors"]
    Batch["Batch & Scheduled Loads"]
    Events["Event / Change Data Capture"]
end

Sage --> API
Freshdesk --> API
OrderEasi --> API
PricingMod --> Batch

subgraph Data_Foundation["Unified Data Foundation"]
    Lake["Enterprise Data Lake / Lakehouse\n(Raw → Cleansed → Curated)"]
    Dictionary["Enterprise Data Dictionary\n+ Business Glossary\n+ KPI Definitions"]
    Lineage["Metadata & Lineage"]
end

API --> Lake
Batch --> Lake
Events --> Lake

Lake --> Dictionary
Lake --> Lineage

subgraph Consumption["Analytics & Consumption"]
    BI["BI & Dashboards"]
    Analytics["Advanced Analytics & Forecasting"]
    Apps["Operational Apps"]
end

Dictionary --> BI
Lake --> BI
Lake --> Analytics
Dictionary --> Analytics
Lake --> Apps

subgraph AgentMesh["AI Agent Mesh"]
    PricingAgent["Pricing Agent"]
    SalesAgent["Sales Insight Agent"]
    SupportAgent["Partner Support Agent"]
    FinanceAgent["Finance & GP Agent"]
end

Dictionary --> PricingAgent
Dictionary --> SalesAgent
Dictionary --> SupportAgent
Dictionary --> FinanceAgent

Lake --> PricingAgent
Lake --> SalesAgent
Lake --> FinanceAgent

PricingAgent --> PricingMod
SalesAgent --> Freshdesk
SupportAgent --> Freshdesk
FinanceAgent --> Sage

