# Lab 5: Copy Pipeline

In this lab you will create a Data Pipeline that orchestrates all the
ingestion activities you have created in the previous labs into a single
automated workflow.

Instead of running each item manually, the pipeline will trigger all
three in sequence:

1. The Copy Job — imports Orders and Customers from Azure SQL
2. Dataflow Gen2 SalesPerson — imports salesperson data
3. Dataflow Gen2 Territory — imports territory data

---

## Task 1: Create a Data Pipeline

1. Go to your workspace and click **+ New Item**.

2. In the search box, type **Pipeline** and select **Data Pipeline**
   from the results.

   ![New item — Data Pipeline selection](/images/lab05/Image1.png)

3. Name your pipeline:
   `Gear_Co_Pipeline_{your student number}`
   Click **Create**.

   ![New pipeline naming screen](/images/lab05/Image2.png)

4. You are now in the pipeline canvas.

   ![Pipeline canvas — empty](/images/lab05/Image3.png)

---

## Task 2: Add the Copy Job Activity

1. Click **Add activity** and select **Copy activity** from the list.

2. In the **General** tab rename the activity to:
   `Ingest_from_AZDB`

   ![General tab — activity renamed](/images/lab05/Image4.png)

3. In the **Settings** tab, connect this activity to your existing
   Copy Job:
   `Gear_Co_AZDBCopy_{your student number}`

   ![Settings tab — Copy Job selected](/images/lab05/Image5.png)

4. Click **Save**.

---

## Task 3: Add the Dataflow Gen2 Activities

1. Click **Add activity** and this time select **Dataflow**.

2. In the **General** tab rename the activity to:
   `Dataflow_SalesPerson`

   ![General tab — Dataflow_SalesPerson renamed](/images/lab05/Image6.png)

3. In the **Settings** tab, select your Dataflow Gen2:
   `Dataflow_SalesPerson_{your student number}`

   ![Settings tab — SalesPerson Dataflow selected](/images/lab05/Image7.png)

4. Connect the two activities by hovering over the
   **Ingest_from_AZDB** box until you see a small arrow on its
   right edge. Drag that arrow to the **Dataflow_SalesPerson** box.
   A green arrow (Success dependency) should appear between them.

   ![Success dependency arrow between activities](/images/lab05/Image10.png)

5. Click **Add activity** again and select **Dataflow**.

6. In the **General** tab rename the activity to:
   `Dataflow_Territory`

   ![General tab — Dataflow_Territory renamed](/images/lab05/Image8.png)

7. In the **Settings** tab, select your Dataflow Gen2:
   `Dataflow_Territory_{your student number}`

8. Connect **Dataflow_SalesPerson** to **Dataflow_Territory** using
   the same drag method.
   A green arrow should appear between them.

   ![SalesPerson to Territory connection](/images/lab05/Image11.png)

   ![Pipeline with all 3 activities connected](/images/lab05/Image12.png)

9. Click **Save**.

---

## Task 4: Run the Pipeline

1. Click **Run** in the top menu to trigger the pipeline manually.

   ![Pipeline run triggered](/images/lab05/Image13.png)

2. Watch the status at the bottom of the screen. All three activities
   should turn green.

   ![Pipeline run succeded](/images/lab05/Image14.png)

   > If any activity fails, click on it to read the error message
   > and diagnose the issue.

4. Go back to your Lakehouse and confirm all tables are present:
   - `DimCustomers`
   - `FactOrders`
   - `DimSalesPerson`
   - `DimTerritory`

---

[Previous: Lab Stretch — Dataflow Gen2](04-stretch-dataflow.md) | [Next: Lab 6 — Materialized Lake Views](06-mlv.md)
