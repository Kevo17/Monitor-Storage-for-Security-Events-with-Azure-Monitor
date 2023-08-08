<h1>Monitor Storage for Security Events with Azure Monitor</h1>


<h2>Description</h2>
The Azure Monitor Logs feature of Azure Monitor collects, stores, and organizes log and performance data from monitored resources. In this lab, you will enable diagnostic settings on a storage account to send Blob storage logs to a Log Analytics workspace. You will also use Azure Monitor Logs to query for anonymous access to blobs and create an Azure Monitor alert to notify you when anonymous access to a storage account is logged.
<br />

<h2>Environments Used </h2>

- <b>Azure</b>
- <b>Windows 11</b>
  
<h2>Program walk-through:</h2>

<h3>Configure Diagnostic Settings</h3>


1. From the Azure portal, click the provisioned storage account to open it.
2. On the left menu, scroll down to Monitoring and select Diagnostic settings.
3. Select blob to open the Blob service for the storage account.
4. Click Add diagnostic setting.
5. In Diagnostic setting name, type "Send Blob Service to Log Analytics".
6. Under Category details, select all of the log types.
7. Under Destination details, select Send to Log Analytics workspace.
8. At the top, click Save.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/2oQjlcQ.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Perform Anonymous Access</h3>

1. On the left menu, scroll up to Data storage and select Containers.
2. Click data to open the data container.
3. Click Upload.
4. Under Upload blob to the right, click the folder icon.
5. Select a sample file on your local machine and click Open.
6. Click Upload.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/0SvkGmY.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Click Change access level.
- View the public access level and click OK.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/2CUJsAk.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Copy the URL to the clipboard for later use.
2. Open a new browser tab and paste in the URL to access the file anonymously.
3. Refresh the page several times to generate multiple log entries (Shift+Reload on Mac, Control+Reload on Windows).


<br/>
 
<p align="center">
<img src="https://i.imgur.com/vOe0w1a.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Use Azure Monitor Logs to Query Logs</h3>

1. From the Azure portal search bar, type and select Monitor to navigate to Azure monitored.
2. On the left menu, select Logs.
3. Close the Welcome to Log Analytics window.
4. In the Select a scope pane beneath Scope, select the resource group and click Apply.



<br/>
 
<p align="center">
<img src="https://i.imgur.com/NDYFbf8.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- In Tables beneath Storage Accounts, click StorageBlobLogs and select Use in editor.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/picJaKE.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- In the query window, paste in the Kusto Query Language (KQL) code to query for anonymous access:
```
StorageBlobLogs |
where AuthenticationType == 'Anonymous'
```
- Click Run

<br/>
 
<p align="center">
<img src="https://i.imgur.com/1zMu0iC.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Modify the query to include the StatusCode of 200:
```
where AuthenticationType == 'Anonymous' and StatusCode == 200
Click Run.
```


<br/>
 
<p align="center">
<img src="https://i.imgur.com/UQUBEkE.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Create an Azure Monitor Alert</h3>

1. Click New alert rule.
2. Scroll down to Alert logic and set the Threshold value to 0.
3. Click Next: Actions > Next: Details.
4. Set the following values: Severity: 2 - Warning Alert rule name: Anonymous Blob Access
5. Beneath Advanced options deselect Automatically resolve alerts.
6. Click Review + create.
7. Click Create.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/269951E.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br/>

<p align="center">
<img src="https://i.imgur.com/Uee4Bl9.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

