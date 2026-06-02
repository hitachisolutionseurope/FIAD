# Lab 3: Data Modelling, Reporting & Visualization

Now that your tables are ready, you need to create a data model to put 
all these tables together. You will create relationships between tables 
and create a semantic model. All this will happen in the Lakehouse.

After creating the semantic model, you will use Copilot to help you 
create a Power BI report.

---

## Task 1: Create a Semantic Model

1. Go to your workspace and open the Lakehouse you have previously created.

   Choose the Lakehouse you created named 
   `Lakehouse_gear_co_{your student number}`.

   ![Lakehouse Explorer view](/images/lab03/Image1.png)

2. Click **New semantic model**.

   You will be asked to **Upgrade to a paid Power BI license**. On the 
   window that appears, click the **Try free** button to get a Power BI 
   license for the duration of the session.

   ![Upgrade to paid Power BI license prompt](/images/lab03/Image2.png)

3. Enter the following details:
   - **Direct Lake semantic model name:** `Mrkt_analysis`
   - **Workspace:** the workspace you are working with

4. Go to **dbo**, expand the table list and select:
   - DimCalendar
   - DimProducts
   - dimcustomer_silver
   - factorders_silver

   Click **Confirm** to proceed.

   ![new semantic model — table selection](/images/lab03/Image3.png)

5. To establish relationships, drag the **customerID** column from the 
   **Dimcustomers_silver** table and drop it onto the **customerID** 
   column in the **Factorder_silver** table.

   ![table selection](/images/lab03/Image4.png)

   
6. Ensure that the cardinality is **One to many** and then **Save**.

   ![Relationship drag and drop — customerID](/images/lab03/Image5.png)


7. Repeat this for the other tables following the table below:

   | Dim tables | Dim table columns | FactOrders Columns | Cardinality |
   |---|---|---|---|
   | DimCustomers_silver | CustomerID | CustomerID | Many to one(*:1) |
   | DimProducts | StockItemID | StockItemID | Many to one(*:1) |
   | DimCalendar | DateID | OrderDateID | Many to one(*:1) |

8. At the end of these operations, your model should appear as follows:

   ![Completed data model](/images/lab03/Image6.png)

9. Define Calendar as the date table, click the 3 dots **...** at the 
   top of the **DimCalendar** table, then click **Mark as date table**.

   ![Mark as date table — DimCalendar](/images/lab03/Image7.png)

10. In the **DimCalendar** table, click the **month_year** column. In 
    the properties pane, go to **Advanced** and set the sort by column 
    to **Month_ID**.

    ![Sort by column — Month_ID](/images/lab03/Image8.png)

11. You will now create four measures that will be used for the report.

12. To achieve this, click the **FactOrder_silver** table. Go to Home 
    page menu and click **New measure**.

     ![New measure — FactOrder_silver selected](/images/lab03/Image9.png)
     ![New measure2 — FactOrder_silver selected](/images/lab03/Image10.png)

13. Copy and paste the following DAX formula for each measure:
```
    Revenue=SUM(factorders_silver[TotalAmount])
```
```
    Total quantity = sum(factorders_silver[Quantity])
```
```
    % revenue growth =
    VAR SalesAmount = [Revenue]
    VAR TotalSalesTransactions =
        FILTER (
            ALL ( factorders_silver ),
            RELATED (DimCalendar[Year]) IN VALUES ( DimCalendar[Year])
        )
    VAR AllSalesAmount =
        SUMX (
            TotalSalesTransactions,
            factorders_silver[TotalAmount]
        )
    VAR Result = DIVIDE ( [Revenue], AllSalesAmount)
    RETURN
        Result
```
```
% quantity growth =
VAR quantity = sum(factorders_silver[Quantity])
VAR TotalSalesTransactions =
    FILTER (
        ALL ( factorders_silver ),
        RELATED (DimCalendar[Year]) IN VALUES ( DimCalendar[Year])
    )
VAR AllSalesAmount =
    SUMX (
        TotalSalesTransactions,
        factorders_silver[Quantity]
    )
VAR Result = DIVIDE ( quantity, AllSalesAmount)
RETURN
    Result
```
   

   ![Measures created in FactOrder_silver](/images/lab03/Image11.png)

---

## Task 2: Create a Power BI Report and Explore your Data using Copilot

You will now create a Power BI report using the semantic model that was 
developed by data engineers and create an executive summary using Fabric 
Copilot.

The executive summary will highlight the numbers available in the report 
pointing the visuals used so that you can integrate these in the version 
you can share with the board.

1. Go back to your workspace and click **+ New Item**.

2. Choose **Report**.

   ![New item — Report selection](/images/lab03/Image12.png)

3. Choose **Pick a published semantic model**.

   ![Build your first report — Pick a published semantic model](/images/lab03/Image13.png)

4. Choose the semantic model named:
   **Mrkt_analysis**, Owner: Angela Messina, Location: Fiad_Copilot.

   ![Semantic model selection — Mrkt_analysis](/images/lab03/Image14.png)

5. Click **Auto-create report**.

   ![Auto-create report](/images/lab03/Image15.png)

6. Edit the report.

   ![Auto-created report — edit view](/images/lab03/Image16.png)


7. Open the Copilot prompt to explore your data.

  ![Copilot prompt opened](/images/lab03/Image17.png)

8. In the prompt choose **Suggest content for a new report page**.

   ![Copilot — Suggest content for a new report page](/images/lab03/Image18.png)

   Continue exploring Copilot's capabilities by asking questions.

---

[Previous: Lab 2 — Data Transformation](02-transformation.md) | [Next: Lab 4 — Dataflow Gen2](04-dataflow.md)



