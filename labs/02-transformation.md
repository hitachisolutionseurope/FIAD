# Lab 2: Data Transformation

All the data transformation and logic will happen in a Fabric notebook, 
using available Apache Spark capabilities.

| Order to Order_Silver | Customer to Customer_Silver |
|---|---|
| Add column Total Amount | Add a column GlobalCustomers |
| Change OrderDate column type | UPPER CASE for territory |

---

## Task 1: Create the FactOrder_Silver table

1. In your workspace click **+ New Item** then in the search box type 
   **Notebook**. Click the **Notebook** box.

   ![New item — Notebook selection](/images/lab02/Image1.png)

2. Rename the notebook to **Gear_co_Transformation** and click **Create**.

   ![New Notebook naming screen](/images/lab02/Image2.png)

3. Delete the existing code to clear your notebook to start fresh.

   ![Clear notebook](/images/lab02/Image3.png)

4. Add a title to your notebook by clicking **+ Markdown**.

   ![Add Markdown cell](/images/lab02/Image4.png)

5. Enter the following into the markdown area to give your notebook a title:
   Creation of FactOrder_silver table

   ![Markdown title rendered](/images/lab02/Image5.png)

6. Before proceeding, you need to connect your notebook to a data source.
   This is achieved by clicking on **Add data items** followed by 
   **From OneLake catalog**.

   ![Add data items — From OneLake catalog](/images/lab02/Image6.png)

7. Choose the Lakehouse you created (named 
   `Lakehouse_gear_co_{your student number}`), then click **Add**.

   ![Select lakehouse](/images/lab02/Image7.png)

8. You should now see all the tables that are in your Lakehouse.

   ![Notebook Explorer — all tables visible](/images/lab02/Image8.png)

9. Right click the **FactOrders** table. In the option list, click 
   **Load data** and choose **Spark**.

   ![Load data Spark](/images/lab02/Image9.png)

   A code block will appear under your previously entered markdown.

   Go to that code, remove **LIMIT 1000** and then execute the code 
   cell by clicking ▷.

   ![FactOrders — Load data Spark code generated](/images/lab02/Image10.png)

   ![Code executed — results displayed](/images/lab02/Image11.png)

10. Below the results table, click **+ Code** to add a new code cell.

    A new code section will be added.

    ![Add code cell below](/images/lab02/Image12.png)

11. In the created cell, copy the following code to add a calculated 
    column called **TotalAmount**. Execute the code by clicking ▷.

    ```python
    df_with_total_amount=df.withColumn("TotalAmount",df.Quantity*df.UnitPrice)
    display(df_with_total_amount)
    ```

12. Below the code (and above the data table returned from the code), click **Data Wrangler** to open the data wrangler tool.

    ![Data Wrangler button](/images/lab02/Image13.png)

    This allows you to explore data with little to no python knowledge — here you can define actions, and they will be translated in python code.

    Our first action is to add a Date column in our Order table using the data wrangler operation **new column by example**.

13. The column date is in a type of **object**; **New column by example** does not apply to this type of column. So, we will change the data type of the column date from **object** to **datetime**.

    Click the **...** on the **OrderDate** column, then select **Change column type**:

    ![Change column type menu](/images/lab02/Image14.png)

    - **Target columns:** OrderDate
    - **New type:** datetime64[ns]

    When done, click **Apply**.

    <p align="center">
      <img src="/images/lab02/Image15.png" width="48%" />
      <img src="/images/lab02/Image16.png" width="48%" />
    </p>

    The OrderDate column is now converted to datetime format:

    ![OrderDate converted to datetime](/images/lab02/Image17.png)

14. In the **Operations** area, type the word **example** and click on 
    **New column by example**:
    - **Target Column:** Order Date
    - **Derived column name:** OrderDateID

    ![New column by example — OrderDateID](/images/lab02/Image18.png)

    Now go to the green column named **OrderDateID**, in the first row 
    type the year, the month and the day — following this example, for 
    the date 2013-01-01 00:00:00 type **20130101** and wait a few seconds.

    ![New column — OrderDateID](/images/lab02/Image19.png)

    Shortly after, you will see the other lines filled based on that model 
    — check the accuracy of the operation and, if everything is ok, click 
    **Apply** in the Operations section.

    ![New column by example — OrderDateID applied](/images/lab02/Image20.png)

15. Click the **...** on the **OrderDateID** column, then select 
    **Change column type**:
    - **Target columns:** OrderDateID
    - **New type:** int32

    When done, click **Apply**.

    ![Change column type — OrderDateID to int32](/images/lab02/Image21.png)

    ![Change column type applied](/images/lab02/Image22.png)

16. The steps you added for your transformation were all translated into 
    python code. To bring this into your notebook, click 
    **+ Add code to notebook** and then click **Add** in the subsequent 
    prompt that you see.

    ![Add code to notebook](/images/lab02/Image23.png)

    ![Add code to notebook confirmation](/images/lab02/Image24.png)

17. Now you will slightly change the python code generated:
    - **Delete the last row:** `display(df_with_total_amount_clean)`
    - **Add the following line** — this code creates a table 
      **FactOrders_silver** in the Lakehouse with the data that you 
      have in the dataset:

    ```python
    df_with_total_amount_clean.write.mode("overwrite").format("delta").saveAsTable("FactOrders_Silver")
    ```

18. Execute the code by clicking ▷.

    ![Code executed — FactOrders_Silver saved](/images/lab02/Image25.png)

---

## Task 2: Create the DimCustomer_Silver table

1. Below the results cell, click + Markdown to add a new markdown cell.

   Enter the following into the markdown area to give your section a title:
   Creation of customer_silver table

   ![Markdown title rendered text](/images/lab02/Image26.png)

2. Hover over the table **DimCustomers** and click on the three dots 
   next to the table name **...**. In the option list, click **Load data** 
   and choose **Spark**.

   ![DimCustomers — Load data Spark](/images/lab02/Image27.png)

3. Go to that code, remove **LIMIT 1000** , change the data frame variable name,
   from **df** to  **Dim_customer_silver**and then execute the code 
   cell by clicking ▷.

   ![return](/images/lab02/Image28.png)

5. The dataset Dimcustomers_silver is displayed on your screen. Click 
   **Data Wrangler** to open the data wrangler tool.

   ![Data wrangler tool](/images/lab02/Image30.png) 


6. In the **Operations** area, type the word **example** and click on 
   **New column by example**:
   
   ![new by example](/images/lab02/Image31.png)  

   - **Target Column:** CustomerName
   - **Derived column name:** GlobalCustomerName

   In the green column, on the first line type **Tailspin Toys**, then 
   click the second line.

   ![New column by example — GlobalCustomerName](/images/lab02/Image32.png) 

   Go back to the operations section and click **Apply**.
   
   ![Apply — GlobalCustomerName](/images/lab02/Image33.png) 
   

7. The steps you added for your transformation were all translated into 
   python code. To bring this into your notebook, click 
   **+ Add code to notebook** and then click **Add** in the subsequent 
   prompt that you see.

   ![Add code to notebook](/images/lab02/Image34.png) 

8. Now you will slightly change the python code generated:
   - **Delete the last row:** `display(Dim_customer_silver_clean)`
   - **Add the following line** — this code creates a table 
     **DimCustomers_silver** in the lakehouse with the data that you 
     have in the dataset:

   ```python
   DimCustomers_silver_clean.write.mode("overwrite").format("delta").saveAsTable("DimCustomers_silver")
   ```

9. Execute the code by clicking ▷.

    ![Code executed — DimCustomers_silver saved](/images/lab02/Image35.png) 

---

[Previous: Lab 1 — Bring data into a Lakehouse](01-ingestion.md) | [Next: Lab 3 — Data Modelling, Reporting & Visualization](03-reporting.md)