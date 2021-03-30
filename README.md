# Azure Services 
How to use Azure services to create enriched dataset that can be consumed by data analysts/scientists

1. Create a Resource Group using PowerShell
   
   $location = "centralindia"
   $resourceGroup = "rapidcircleresource"
   New-AzResourceGroup -Name $resourceGroup -Location $location
   
2. Create Azure Storage Account using PowerShell

   $location = "centralindia"
   $resourceGroup = "rapidcircleresource"
   New-AzStorageAccount -ResourceGroupName $resourceGroup -Name rapidstorageacc999 -Location $location -SkuName Standard_RAGRS -Kind StorageV2 -EnableHierarchicalNamespace $True
   $ctx = $storageAccount.Context
   
3. Create a Container

   $containerName = "container1"
   New-AzStorageContainer -Name $containerName -Context $ctx -Permission blob
   
4. Create a Data Factory

   $location = "centralindia"
   $resourceGroup = "rapidcircleresource"
   $dataFactoryName = "ADFRapidCircle"
   $DataFactory = Set-AzDataFactoryV2 -ResourceGroupName $resourceGroup -Location $location -Name $dataFactoryName
   
5. Create a SQL Server

   New-AzSqlServer -ResourceGroupName 'rapidcircleresource' -ServerName 'rapsqlsrv-int-01' -Location 'Central India' -SqlAdministratorCredentials $(New-Object -TypeName      System.Management.Automation.PSCredential -ArgumentList "username", $(ConvertTo-SecureString -String "password" -AsPlainText -Force))
   Get-AzSqlServer | select FullyQualifiedDomainName
   #rapsqlsrv-int-01.database.windows.net
   
6. Create a Server Firewall Rule

   $myIp = (Invoke-WebRequest ifconfig.me/ip).Content
   New-AzSqlServerFirewallRule -ResourceGroupName 'rapidcircleresource' -ServerName 'rapsqlsrv-int-01' -FirewallRuleName "AllowedIPs" -StartIpAddress $myIp -EndIpAddress $myIp

7. Create a database

   New-AzSqlDatabase  -ResourceGroupName 'rapidcircleresource' -ServerName 'rapsqlsrv-int-01' -DatabaseName 'databasename' -RequestedServiceObjectiveName "S0" -SampleName "AdventureWorksLT"
   
8. To download a sample dataset use the below link
    https://www.kaggle.com/datasets
  
9. Follow the below document for other steps.
   [Blob to Azure SQL.docx](https://github.com/aslam0316/azureservices/files/6228728/Blob.to.Azure.SQL.docx)

    
