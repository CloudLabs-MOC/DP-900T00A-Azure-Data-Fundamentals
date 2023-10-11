# Module 05c: Explore real-time analytics in Microsoft Fabric

## Lab scenario
In this exercise you'll explore real-time analytics in Microsoft Fabric.

> **Note**: You'll need a Microsoft Fabric license to complete this exercise. See [Getting started with Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) for details of how to enable a free Fabric trial license. You will need a Microsoft *school* or *work* account to do this. If you don't have one, you can [sign up for a trial of Microsoft Office 365 E3 or higher](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Lab objective

In this lab, you will perform:

+ Exercise 1: Select the workspace
+ Exercise 2: Create a KQL database
+ Exercise 3: Create an eventstream
+ Exercise 4: Query real-time data in a KQL database

## Estimated timing: 25 minutes

## Architecture diagram

![](images/dp900-2.png)

## Exercise 1: Select the workspace

Before working with data in Fabric, create a workspace with the Fabric trial enabled.

1. Open an Edge browser, sign into [Microsoft Fabric](https://app.fabric.microsoft.com). Enter the username <inject key="AzureAdUserEmail"></inject>, and password enter <inject key="AzureAdUserPassword"></inject>. Then on the **Microsoft Fabric**, select **Power BI**.

    >**Note:** If you are getting popup **save password**, then select **Save & Turn on** option.
   > In the pop-up for *Help us protect your account*, select **Skip for now (14 days until this is required)**.
   > If you see the pop-up **Stay Signed in?**, click Yes
    
    >**Note:** If **You've selected Microsoft Fabric free** page appears, then select **Continue**. In **Business phone number** provide any number, and select **Get Started**.

     ![](images//msfabric.png)

2. In the menu bar on the left, select **My workspaces**.

## Exercise 2: Create a KQL database

Now that you have a workspace, you can create a KQL database to store real-time data.

1. At the bottom left of the portal, switch to the **Real Time Analytics** experience.

    ![Screenshot of the experience switcher menu.](./images/fabric-real-time.png)

    >**Note:** The real time analytics home page includes tiles to create commonly used assets for real-time data analyis

2. In the real time analytics home page, select **KQL Database (Preview)**, and create a new **KQL Database** with a name of your choice.

    After a minute or so, a new KQL database will be created:

    ![Screenshot of a new KQL database.](./images/kql-database.png)

    >**Note:**  on the **Successfully upgraded to a free Microsoft Fabric (preview) trial** page, select **OK**.

    Currently, there are no tables in the database.

## Exercise 3: Create an eventstream

Eventstreams provide a scalable and flexible way to ingest real-time data from a streaming source.

1. In the menu bar on the left, select the **Home** page for the real-time analytics experience.

1. On the home page, select **Eventstream (Preview)**, and create a new **Eventstream** with a name of your choice.

    After a short time, the visual designer for your eventstream is displayed.

    ![Screenshot of the Eventstream designer.](./images/eventstream-designer.png)

    The visual designer canvas shows a source that connects to your eventstream, which in turn is connected to a destination.

1. On the designer canvas, select the **New source** drop-downlist, select **Sample data**. Then in the **Sample data** pane, specify the following configurations,

   - Source name: **taxis** 
   - Sample data: **Yellow Taxi**
   - Select **Add**.

1. Beneath the designer canvas, select the **Data preview** tab to preview the data being streamed from the source:

    ![Screenshot of the Eventstream data preview.](./images/eventstream-preview.png)

1. On the designer canvas, select **New destination** drop-down, select **KQL database**. Then in the **KQL database** pane, specify the following configurations,
   
   - Destination name: **taxi-data**
   - Workspace: Select your workspace
   - KQL Database: Select your KQL database
   - Select **Create and configure**.

1. In the **Ingest data** wizard, on the **Destination** page, select **New table** and enter the table name **taxi-data**. Then select **Next: Source**.

1. On the **Source** page, review the default data connection name, and then select **Next: Schema**.

1. On the **Schema** page, change the **Data format** from TXT to **JSON**, and view the preview to verify that this format results in multiple columns of data. Then select **Next: Summary**.

1. On the **Summary** page, wait for continuous ingestion to be established, and then select **Close**.

1. Verify that your completed eventstream looks like this:

    ![Screenshot of a completed Eventstream.](./images/complete-eventstream.png)

## Exercise 4: Query real-time data in a KQL database

Your eventstream continuously populates a table in your KQL database, enabling you to query the real-time data.

1. In the menu hub on the left, select your KQL database (or select your workspace and find your KQL database there).
1. Hover on **taxi-data** table, and select **...** menu, select **Query table > Records ingested in the last 24 hours**.

    ![Screenshot of the Query table menu in a KQL database.](./images/kql-query.png)

1. View the results of the query, which should be a KQL query like this:

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    The results show all taxi records ingested from the streaming source in the last 24 hours.

1. Replace all of the KQL query code in the top half of the query editor with the following code:

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(tpep_pickup_datetime, 1h)
    ```

1. Use the **&#9655; Run** button to run the query and review the results, which show the number of taxi pickups for each hour.

## Review
In this lab, you have completed:
- Selected the workspace
- Created a KQL database
- Created an eventstream
- Queried real-time data in a KQL database
  
## You have successfully completed this lab
