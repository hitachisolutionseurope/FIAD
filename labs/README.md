# Microsoft Fabric in a Day — Lab Manual

---

## Context

Adventure Gear Co. is a company that specializes in selling outdoor 
equipment, including bicycles, tents, hiking gear, and fitness 
accessories. Their mission is to inspire a love for the outdoors by 
providing high-quality products for all adventure enthusiasts.

In 2023, Adventure Gear Co. experienced growth but also faced challenges 
with market competition. The marketing team wants to segment their customer 
base to better target promotional efforts and increase customer retention.

---

## Marketing Goals

1. Identify high-value customers who frequently purchase high-end gear
2. Understand demographic and geographic patterns to tailor marketing strategies
3. Boost sales among dormant or infrequent customers by re-engaging them 
   with personalized campaigns

---

## Your Work

Your work will consist in a 3-step process:

1. Bring data into a Lakehouse in Fabric
2. Make relevant changes to existing tables in the Lakehouse
3. Create a Power BI report to cover the marketing director requests

---

## Architecture

![New item — Architecture diagram](/images/prelab/Image1.jpg)

---

## Labs

| Lab | Title |
|---|---|
| Pre-lab | Connecting to Fabric |
| Lab 1 | Bring data into a Lakehouse |
| Lab 2 | Data Transformation |
| Lab 3 | Data Modelling, Reporting & Visualization |
| Lab 4 | Dataflow Gen2 |
| Lab 5 | Pipeline & Monitoring|
| Lab 6 | Materialized Lake Views |

---

## Navigation

- [Pre-lab — Connecting to Fabric](labs/00-pre-lab.md)
- [Lab 1 — Bring data into a Lakehouse](labs/01-ingestion.md)
- [Lab 2 — Data Transformation](labs/02-transformation.md)
- [Lab 3 — Data Modelling, Reporting & Visualization](labs/03-reporting.md)
- [Lab 4 — Dataflow Gen2](labs/04-dataflow.md)
- [Lab 5 — Pipeline & Monitoring](labs/05-pipeline.md)
- [Lab 6 — Materialized Lake Views](labs/06-mlv.md)


---

## Naming Conventions

| Resource | Name format |
|---|---|
| Lakehouse | `Lakehouse_Gear_Co_{student number}` |
| Copy Job | `Gear_Co_AZDBCopy_{student number}` |
| Notebook | `Gear_co_Transformation` |
| Dataflow | `Dataflow_SalesPerson_{student number}` |
| Semantic Model | `Mrkt_analysis` |
| Report | `Gear_co_marketing` |

