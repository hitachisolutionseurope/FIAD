# Lab 1: Bring data into a Lakehouse in Fabric

For this activity, you will need 4 tables from 2 data sources:

1. The Lakehouse maintained by the data engineering team
2. The Sales Database

## Your Tasks

- Create a Lakehouse
- Create a copy job to import data from the Azure SQL Database
- Create shortcuts to the Lakehouse tables

---

## Task 1: Create a Lakehouse

A Lakehouse is essential because it serves as a centralized repository 
for all types of data, structured or unstructured. It enables efficient 
data management and analysis, forming the backbone of any data-driven 
operation.

1. Go to home screen of your Fabric Workspace

2. In your student workspace, click **+ New Item** and then click the 
   **Lakehouse** box.

   ![New item — Lakehouse selection](/images/lab01/Image1.png)

3. Name your Lakehouse:

   `Lakehouse_Gear_Co_{your student number}`

   A clear name helps in organizing and managing your data projects, 
   especially when working with multiple datasets or collaboratively.

   Once you have given the Lakehouse a name, click **Create**.

   <p align="center">
      <img src="/images/lab01/Image2.png" width="48%" />
      <img src="/images/lab01/Image3.png" width="48%" />
   </p>
---

## Task 2: Create a Copy Job to import data from the Azure SQL Database

The Copy job is a simplified process that enables users to perform data 
ingestion tasks more efficiently and with less complexity.

1. Inside your Lakehouse, under Get data in your lakehouse, click the New copy job tile.
   **+ New Item**. Type **copy job** in the search box.

   ![New item — Copy job selection](/images/lab01/Image4.png)

2. Name your copy job:

   `Gear_Co_AZDBCopy_{your student number}`

   Then click **Create**.

   ![New copy job naming screen](/images/lab01/Image5.png)

3. In the new source section, choose **Onelake-catalog**. From the 
   Onelake-catalog section, select **FIAD-wwi-sample-sqldb**. Accept 
   any defaults and click **Next**.

   ![Onelake-catalog source selection*](/images/lab01/Image6.png)

   ![FIAD-wwi-sample-sqldb connection settings](/images/lab01/Image7.png)
   ![Connextion setting](/images/lab01/Image8.png)

4. In the search box type **sales** and choose the following 2 tables:
   - **Sales.allCustomers**
   - **Sales.allOrders**

   Click **Next**.

   ![Table selection](/images/lab01/Image9.png)

5. We want to copy all the data from the source. To do this, ensure that 
   the **Full copy** option is checked

6. Ensure that **Tables** is checked as destination type.


   ![Full copy option selected](/images/lab01/Image10.png)

   In the **Destination** column change the table names as follows:

   | From | To |
   |---|---|
   | Sales.allCustomers | Sales.DimCustomers |
   | Sales.allOrders | Sales.FactOrders |

   Click **Next**.

   ![Table mapping](/images/lab01/Image11.png)

7. In the next window, click **Save + Run**.

   ![Review and save screen](/images/lab01/Image12.png)


8. You will be able to see the loading status of the two tables. The 
   extract process will take some time, eventually turning to **Succeeded**.

   ![Copy job run status — Succeeded](/images/lab01/Image13.png)

   Return to your Lakehouse (`Lakehouse_Gear_Co_{your student number}`).

   In the Lakehouse, go to the **Tables** section and check that you have 
   the **DimCustomers** and **FactOrders** tables added.

   > If you see undefined or no tables, refresh your web page using **Ctrl+F5**.

   ![Lakehouse Tables section](/images/lab01/Image14.png)

---

## Task 3: Create Shortcuts in the Lakehouse

1. To add a table shortcut in the Lakehouse you previously created, expand 
   the **Tables** section and then click the **...** next to the **Sales schema**.

   ![Tables section](/images/lab01/Image15.png)
   

2. In the options list, choose **New table shortcut**.

   ![Tables section shortcut](/images/lab01/Image16.png)

3. Choose **Microsoft OneLake**.

   ![Select data source type](/images/lab01/Image17.png)

4. Choose **Gear_sales_engineering_team** and click **Next**.

   ![data source type](/images/lab01/Image18.png)

5. Expand the **Tables** section and check the **Calendar** and **Products** 
   items, then click **Next** followed by **Create**.

   ![Calendar and Products selected](/images/lab01/Image19.png)

6. Rename the tables as follows:

   | From | To |
   |---|---|
   | Calendar | DimCalendar |
   | Products | DimProducts |

   On each row, click the tick (✓) to validate your change, then click **Create**.

   ![Shortcut rename](/images/lab01/Image20.png)
   ![Shortcut rename validate](/images/lab01/Image21.png)
   ![Shortcut rename](/images/lab01/Image22.png)


7. The Tables section should now have 4 tables; if not, refresh your web 
   page (**Ctrl+F5**).

   ![Lakehouse Explorer](/images/lab01/Image23.png)

---

[Previous: Pre-lab — Connecting to Fabric](00-pre-lab.md) | [Next: Lab 2 — Data Transformation](02-transformation.md)
