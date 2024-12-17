# Lab 06: Visualize data with Power BI

## Lab scenario
In this lab, you'll use Microsoft Power BI Desktop to create a data model and a report containing interactive data visualizations.

## Lab objectives

In this lab, you will perform the following tasks:

+ Task 1: Import data
+ Task 2: Explore a data model
+ Task 3: Create a report
  
## Estimated timing: 30 minutes

## Architecture diagram

![](images/sc900module6.png)

## Exercise 1: Visualize data with Power BI

### Task 1: Import data

1.  Open Power BI Desktop. The application interface should look similar to this, select **Get Started**, if it is asking for the Email, select Cancel :
    
    ![The Power BI Desktop start screen](images/power-bi-start-1.png)
    
    Now you're ready to import the data for your report.

2.  On the Power BI Desktop welcome screen, select  **Get data**, and then in the list of data sources, select  **Web**  and then select  **Connect**.
    
    ![Selecting the web data source](images/web-source.png)
    
3.  In the  **From web**  dialog box, enter the following URL and then select  **OK**:
    

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    
    ```
    
4.  Verify that the URL opens a dataset containing customer data, as shown below. Then select  **Load**  to load the data into the data model for your report.
    
    ![A dataset of customer data](images/customers.png)
    
5.  In the main Power BI Desktop window, in the  **Get data**  menu, select  **Web**:
    
    ![The Get data menu](images/get-data.png)
    
6.  In the  **From web**  dialog box, enter the following URL and then select  **OK**:
    

    
    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    
    ```
    
7.  Load the product data in this file into the data model.
    
8.  Repeat the previous three steps to import a third dataset containing order data from the following URL:
    

    
    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    
    ```
    
### Task 2 : Explore a data model

The three tables of data you've imported have been loaded into a data model, which you'll now explore and refine.

1.  In Power BI Desktop, on the left-side edge, select the  **Model**  tab, and then arrange the tables in the model so you can see them (you can hide the panes on the right side by using the  **>>**  icons):
    
    ![The Model tab](images/model-tab.png)
    
2.  In the  **orders**  table, select the  **Revenue**  field and then in the  **Properties**  pane, set its  **Format**  property to  **Currency**:
    
    ![Setting the Revenue format to Currency](images/revenue-currency.png)
    
    This will ensure that revenue values are displayed as currency in report visualizations.
    
3.  In the products table, right-click the  **Category**  field (or open its  **⋮**  menu) and select  **Create hierarchy**. This creates a hierarchy named  **Category Hierarchy**  (you may need to expand or scroll in the  **products**  table to see this - you can also see it in the  **Fields**  pane)
    
    ![Adding the Category Hierarchy](images/category-hierarchy.png)
    
4.  In the products table, right-click the  **ProductName**  field (or open its  **⋮**  menu) and select  **Add to hierarchy**  >  **Category Hierarchy**. This adds the  **ProductName**  field to the hierarchy you created previously.
    
5.  In the  **Fields**  pane, right-click  **Category Hierarchy**  (or open its  **...**  menu) and select  **Rename**. The hierarchy will be renamed to  **Categorized Product**.
    
    ![Renaming the hierarchy](images/rename-hierarchy.png)
    
6.   On the left-side edge, select the **Table view** tab, and then in the **Data** pane, select the **customers** table.
    
7.  Select the  **City**  column header, and then set its  **Data Category**  property to  **City**:
    
    ![Setting a data category](images/data-category.png)
    
    This will ensure that the values in this column are interpreted as city names, which can be useful if you intend to include map visualizations.
    

### Task 3 : Create a report

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1.  On the  **File**  menu, select  **Options and Settings**. Then select  **Options**, and in the  **Security**  section, ensure that  **Use Map and Filled Map visuals**  is enabled and select  **OK**.
    
    ![Setting options](images/set-options.png)
    
    This ensures that you can include map visualizations in reports.
    
2.  On the left-side edge, select the  **Report**  tab and view the report design interface.
    
    ![The report tab](images/report-tab.png)
    
3.  In the ribbon, above the report design surface, select  **Text Box**  and add a text box containing the text  **Sales Report**  to the report. Format the text to make it bold with a font size of 32.
    
    ![A text box](images/text-box.png)
    
4.  Select any empty area on the report to de-select the text box. Then in the  **Fields**  pane, expand  **Products**  and select the  **Categorized Products**  field. This adds a table to the report.
    
    ![A table of categorized products in a report](images/categorized-products-table.png)
    
5.  With the table still selected, in the  **Fields**  pane, expand  **Orders**  and select  **Revenue**. A Revenue column is added to the table (you may need to expand the size of the table to see it).
    
    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the  **Model**  or  **Data**  tab and change the decimal places if you wish!
    
    ![A table of categorized products with revenue in a report](images/revenue-column.png)
    
6.  With the table still selected, in the  **Visualizations**  pane, select the  **Stacked column chart**  visualization. The table is changed to a column chart showing revenue by category.
    
    ![A stacked column chart of categorized products with revenue in a report](images/stacked-column-chart.png)
    
7.  Hover on the selected column chart, then click on more options(...), select **sort axis** then select  **↓ sort ascending**  icon to turn on drill-down. Then in the chart, select the second column (_Road Bikes_) to drill down and see the revenue for the individual products in this category. This capability is possible because you defined a hierarchy of categories and products.
    
    ![A column chart drilled down to see products within a category](images/drill-down.png)
    
8.  Use the  **↓ sort ascending**  icon to drill back up to the category level. Then select the  **(**↓ sort descending**)**  icon to turn off the drill-down feature.
    
9.  Select a blank area of the report, and then in the  **Fields**  pane, select the  **Quantity**  field in the  **orders**  table and the  **Category**  field in the  **products**  table. This results in another column chart showing sales quantity by product category.
    
10.  With the new column chart selected, in the  **Visualizations**  pane, select  **Pie chart**  and then resize the chart and position it next to the revenue by category column chart.
    
     ![A pie chart shows sales quantity by category](images/category-pie-chart.png)
    
11.  Select a blank area of the report, and then in the  **Fields**  pane, select the  **City**  field in the  **customers**  table and then select the  **Revenue**  field in the  **orders**  table. This results in a map showing sales revenue by city (rearrange and resize the visualizations as needed):
    
     ![A map shows revenue by city](images/revenue-map.png)
    
12.  In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.
    
     ![A map shows revenue by city highlighting data for the selected city](images/selected-data.png)
    
13.  On the  **File**  menu, select  **Save**. Make sure to save it in the Documents folder. Then save the file with chart-<inject key="DeploymentID" enableCopy="false" />.pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

     >**Note**: In this exercise, you have used Power BI Desktop to ingest data, create a data model, and use interactive visualizations to create a report. If you have a  [Power BI service](https://www.powerbi.com/)  subscription, you can sign into your account and publish the report to a Power BI workspace.

  > **Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

   <validation step="9bcb34ed-c80a-479b-add9-231776c2e3df" />

## Review
In this lab, you have completed:
- Import data
- Explore a data model
- Create a report
  
## You have successfully completed this lab

