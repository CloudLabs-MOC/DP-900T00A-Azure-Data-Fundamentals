# Lab 05: Explore Azure Stream Analytics

## Lab scenario
In this lab, you'll provision an Azure Stream Analytics job in your Azure subscription, and use it to process a stream of real-time data.
Before starting the exercise on Microsoft Learn, you'll need to prepare a cloud shell environment for your Azure subscription.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create Azure resources
+ Task 2: Explore the Azure resources
+ Task 3: Use the resources to analyze streaming data
  
## Estimated timing: 15 minutes

## Architecture diagram

![](images/dp900module(5).png)  

## Exercise 1: Analyze streaming data

### Task 1: Create Azure resources

1.  Inside Azure Portal, use the  **[>_]**  button to the right of the search bar at the top of the page to create a new Cloud Shell, if prompted to select either Bash or PowerShell, select **Bash** and if you get **You have no storage mounted** click on **create storage**.The cloud shell provides a command line interface in a pane at the bottom of the Azure portal, as shown here:
     
    ![Azure portal with a cloud shell pane](images/cloud-shell(1).png)

1.  In the Azure Cloud Shell, enter the following command to download the files you'll need for this exercise.
    

    ```
    git clone https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals dp-900
    
    ```
    
1.  Wait for the command to complete, and then enter the following command to change the current directory to the folder containing the files for this exercise.
    

    
    ```
    cd dp-900/streaming
    
    ```
    
1.  Enter the following command to run a script that creates the Azure resources you will need in this exercise.
    

    
    ```
    bash setup.sh
    
    ```
    
    Wait as the script runs and performs the following actions:
    
    1.  Installs the Azure CLI extensions needed to create resources (_you can ignore any warnings about experimental extensions_)
    2.  Identifies the Azure resource group provided for this exercise, which will have a name similar to  **learn-_xxxxxxxxxxxxxxxxx..._**.
    3.  Creates an  _Azure IoT Hub_  resource, which will be used to receive a stream of data from a simulated device.
    4.  Creates a  _Azure Storage Account_, which will be used to store processed data.
    5.  Creates a  _Azure Stream Analytics_  job, which will process the incoming device data in real-time, and write the results to the storage account.

### Task 2: Explore the Azure resources

1.  In the  [Azure portal](https://portal.azure.com/), on the home page, select  **Resource groups**  to see the resource groups in your subscription. This should include the  ****learnxxxxxxxxxxxxxxxxx...**** resource group identified by the setup script.
    
2.  Select the  ****learnxxxxxxxxxxxxxxxxx...****  resource group, and review the resources it contains, which should include:
    
    -   An  _IoT Hub_  named  **iothubxxxxxxxxxxxxx**, which is used to receive incoming device data.
    -   A  _Storage account_  named  **storexxxxxxxxxxxx**, to which the data processing results will be written.
    -   A  _Stream Analytics job_  named  **streamxxxxxxxxxxxxx**, which will be used to process streaming data.
    
    If all three of these resources are not listed, click the  **↻ Refresh**  button until they appear.
    
3.  Select the **streamxxxxxxxxxxxxx**  Stream Analytics job and view the information on its  **Overview**  page, note the following details:
    
    -   The job has one  _input_ (Select **Inputs** under Job topology on the left hand pane)  named  **iotinput**, and one  _output_ (Select **Outputs** under Job topology on the left hand pane) named  **bloboutput**. These reference the IoT Hub and Storage account created by the setup script.
    -   The job has a  _query_(Select **Query** under Job topology on the left hand pane), which reads data from the  **iotinput**  input, and aggregates it by counting the number of messages processed every 10 seconds; writing the results to the  **bloboutput**  output.

### Task 3:  Use the resources to analyze streaming data

1.  At the top of the  **Overview**  page of the Stream Analytics job, select the  **▷ Start**  button, and then in the  **Start job**  pane, select  **Start**  to start the job.
    
2.  Wait for a notification that the streaming job started successfully.
    
3.  Switch back to the Azure Cloud Shell, and enter the following command to simulate a device that sends data to the IoT Hub.
    
    ```
    bash iotdevice.sh
    
    ```  
    
4.  Wait for the simulation to start, which will be indicated by output like this:
     
    ```
    Device simulation in progress: 6%|#    | 7/120 [00:08<02:21, 1.26s/it]
    
    ```
      
5.  While the simulation is running, back in the Azure portal, return to the page for the  **learn*xxxxxxxxxxxxxxxxx...***  resource group, and select the  **store*xxxxxxxxxxxx***  storage account.
    
6.  In the pane on the left of the storage account blade, select the  **Containers**  tab.
    
7.  Open the  **data**  container.
    
8.  In the  **data**  container, navigate through the folder hierarchy, which includes a folder for the current year, with subfolders for the month, day, and hour.
    
9.  In the folder for the hour, select the file that has been created, which should have a name similar to  **0_xxxxxxxxxxxxxxxx.json**.

10.  On the page for the file, select  **Edit**, and review the contents of the file; which should consist of a JSON record for each 10 second period, showing the number of messages received from IoT devices, like this:
     
     ```
      {"starttime":"2021-10-23T01:02:13.2221657Z","endtime":"2021-10-23T01:02:23.2221657Z","device":"iotdevice","messages":2}
      {"starttime":"2021-10-23T01:02:14.5366678Z","endtime":"2021-10-23T01:02:24.5366678Z","device":"iotdevice","messages":3}
      {"starttime":"2021-10-23T01:02:15.7413754Z","endtime":"2021-10-23T01:02:25.7413754Z","device":"iotdevice","messages":4}
    
     ```
      
    
11.  Use the  **↻ Refresh**  button to refresh the file, nothing that additional results are written to the file as Stream Analytics job processes the device data in real time as it is streamed from the device to the IoT Hub.
    
12.  Return to the Azure Cloud Shell and wait for the device simulation to finish (it should run for around 3 minutes).
    
13.  Back in the Azure portal, refresh the file one more time to see the full set of results that were produced during the simulation.
    
14.  Return to the  **learnxxxxxxxxxxxxxxxxx...**   resource group, and re-open the  **streamxxxxxxxxxxxxx...**  Stream Analytics job.
    
15.  At the top of the Stream Analytics job page, use the  **⬜ Stop**  button to stop the job, confirming when prompted.

     > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
     > - Click the Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation Page.
     > - Hit the Validate button for the corresponding task.If you receive a success message, you can proceed to the next task. 
     > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
     > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Review
In this lab, you have completed:
- Create Azure resources
- Explore the Azure resources
- Use the resources to analyze streaming data
  
## You have successfully completed this lab.

