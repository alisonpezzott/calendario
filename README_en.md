# Calendar Dimension Table

> [!IMPORTANT]  
Before you begin, make sure you have at least the January 2025 version of Power BI Desktop installed.  
Enable the option at File > Options and settings > Options > Preview features > ✅ TMDL View

## 1. Local Mode Directly in Power BI Desktop with TMDL

> This method is intended for those who want an independent calendar dimension table for each semantic model.  
> This is the only method that does not require any licensing.

Pros:
- Independence from other items such as dataflows, lakehouses, and warehouses.

Cons:
- Longer refresh time.
- More data volume in Power BI Service.
- Possible discrepancies between models.

Instructions:
- Create or import any table into Power BI Desktop;
- Click the `TMDL` button on the left sidebar;
- Copy the code for your desired language from [TMDLDesktop](./TMDLDesktop/) and paste it into the code area.
- Click `Apply` and then, in the alert above, click `Refresh now`.

## 2. Dataflow gen1 Import (PRO)

> This method is recommended for those who want a single calendar dimension table for the entire organization using dataflows gen1.  
> This is the most recommended method for PRO license users.

Pros:
- Single date source for the organization;
- Standardization;
- Performance;
- Reusability.

Cons:
- More steps for initial setup.

Instructions:
- Create a new dataflow gen1;
- Create a blank query;
- Copy the code for your desired language from [PowerQueryOrDataflow](./PowerQueryOrDataflow/) and paste it into the advanced editor of the blank query;
- Rename your table to DimCalendar;
- Click `Save and close`;
- Save the dataflow and name it DfwCalendar;
- Refresh the dataflow;
- Set up automatic refresh daily at 00:00 according to your time zone;
- Open a blank file in Power BI Desktop;
- On the `Home` tab, click `Get Data` and then `Dataflows`;
- If prompted, log in with your account and password;
- Find the Workspace and the Dataflow `FlwCalendar`, check the table `dCalendar`, and click `Load`;
- Click the `TMDL` button on the left sidebar;
- Drag the DimCalendar table from the Tables tab on the right to the code field of Script1;
- Create Script2 by clicking `+` on the bottom tab;
- Copy the code for the corresponding language from [TMDLAfterDataflow](./TMDLAfterDataflow/) and paste it into Script2. Do not apply yet!;
- Return to Script1, scroll to the end of the code, and copy from 'partition' to the end;
- Go to Script2, scroll to the end, and paste over from 'partition' to the end;
- Click `Apply`.

### 3. Direct Lake Mode (Fabric Users)

> This mode is recommended for those using semantic models in Fabric's Direct Lake.  
> The code is updated via Dataflows gen2 and can be allocated in both Lakehouses and Warehouses.  
> For demonstration, the load will be in a Warehouse simulating the gold layer of our project.

Pros:
- Single date source for the organization;
- Standardization;
- Performance;
- Reusability.

Cons:
- More steps for initial setup.

Instructions:
- Create a Workspace and configure it for a Fabric Capacity (or Trial);
- Create a new Warehouse;
- Name the Warehouse as DW_Gold;
- Inside the Warehouse, click `Get Data` and then choose `New Dataflow Gen2`;
- Name it DfwCalendar and check the option `Enable Git integration...` and click `Create`;
- Create a blank query;
- Copy the code for your desired language from [PowerQueryOrDataflow](./PowerQueryOrDataflow/) and paste it into the advanced editor of the blank query;
- Rename your table to DimCalendar;
- Save the dataflow and close;
- Wait for the initial publish and refresh. If it does not occur, force a refresh;
- Set up automatic refresh daily at 00:00 according to your time zone via scheduling or Data Pipelines;
- Open the warehouse, click `Reports` then `New semantic model`;
- Choose the table `dCalendar` and other desired tables for your model;
- Name it `SMGold` and save;
- Open Power BI Desktop and on the `Home` tab click OneLake catalog and then `Power BI Semantic Models`;
- Click the `SMGold` model but do not click the connect button, instead click the arrow next to it and then `Edit`;
- Click the `TMDL` button on the left sidebar;
- Drag the DimCalendar table from the Tables tab on the right to the code field of Script1;
- Create Script2 by clicking `+` on the bottom tab;
- Copy the code for the corresponding language from [TMDLDirectLake](./TMDLDirectLake/) and paste it into Script2. Do not apply yet!;
- Return to Script1, scroll to the end of the code, and copy from 'partition' to the end;
- Go to Script2, scroll to the end, and paste over from 'partition' to the end;
- Apply and refresh;
- Click `Apply`.