---
title: "How to format a CSV or JSON file for bulk upload in Migration Manager"
ms.reviewer: 
ms.author: jhendr
author: JoanneHendrickson
manager: serdars
recommendations: true
audience: ITPro
f1.keywords:
- CSH
ms.topic: article
ms.service: sharepoint-online
localization_priority: Priority
ms.collection: 
- SPMigration
- M365-collaboration
search.appverid: MET150
description: "How to format a CSV or JSON file for bulk upload in Migration Manager"
---

# Bulk upload tasks into Migration Manager using a CSV or JSON file 

There are two different methods available to bulk upload tasks into Migration Manager.  One is using a comma-separated (CSV) file, and the other is to use a JSON file.  

The entries are manually entered by you into whichever format you choose.  The first row is validated to make sure the destination links are valid. If you receive an invalid destination error, make sure to also check the remainder of your tasks to ensure they have valid destinations. 

>[!Note]
>If you are migrating to OneDrive accounts, make sure the accounts are pre-provisioned before you migrate. You can do this using a script, as shown here: [Pre-provision OneDrive for users in your organization](/onedrive/pre-provision-accounts).

  
## Using a comma-separated value (CSV) file for bulk upload


Migration Manager lets you use a comma-separated (CSV) file to bulk migrate your data. Use any text editor, or an application like Excel, to create the CSV file.
  
 **CSV file format**
  
There are six columns needed in your CSV file -- the first three are your source values, each providing detail about where your data is currently located. The remaining three columns indicate the site, document library and optional sub-folder to where you are migrating your data. All six columns must be accounted for in the file, even if you are not needing a value for a given field.
  
Here's an example of the format for the CSV file. The rows show files that are being migrated from local file shares.

>[!Tip]
>Download the template for bulk uploading using a CSV file:  [Migration Manager bulk upload template](https://download.microsoft.com/download/b/1/9/b1925e76-010c-4db5-aa44-64055f8f3efe/mm-example_csv_bulk_upload.csv)
  
![Sample format when using a CSV file](media/mm-sample-csv.png)
  
This example shows how it would appear in a .txt file.
  
```console
\\MigrationTests\testfiles,,,https://contoso.sharepoint.com/sites/sitecollection,Documents,SubFolderName
\\MigrationTests\testfiles,,,https://contoso-my.sharepoint.com/personal/user_contoso_onmicrosoft_com,Documents,
```




> [!IMPORTANT]
>  *Do not*  include a header row in your CSV file. Remember to account for all six columns in the file, even if you are not needing a value for a given field. 
>  The encoding of the CSV file must be UTF-8.

  
 **To create a CSV file for data migration**
  
The following example uses Excel to create the CSV file.
  
1. Start Excel.
    
2. Enter the values for your migration jobs. Enter one migration source and destination per row. See the reference table below for further explanation of columns.
    
   - **Column A:** Enter a file share path.  *Required.* 
    
   - **Column B:** Leave this column **blank**. This column does not apply to file share migration. 
    
   - **Column C:** Leave this column **blank**. This column does not apply to file share migration. 
    
   - **Column D:** Enter the SharePoint site URL where the files are to be migrated.  *Required.* 
    
   - **Column E:** Enter the name of the document library in the SharePoint site where the files are to be migrated.  *Required.* 
    
   - **Column F:** Enter the name of the subfolder in the document library. If this column is left empty then the files will be moved to the root level.  *Optional.* 
    
3. Close and save as a Comma delimited (\*.csv) file.
    

## Using a JSON file for bulk upload



The following example shows the JSON format used in migrating your data.

The minimum required values are SourcePath, TargetPath and TargetList.  

```json

{

  "Tasks": [

    {
      "SourcePath": "\\\\contoso\\fileshare\\dept1",
      "TargetPath": "https://a830edad9050849387E18042320.sharepoint.com",
      "TargetList": "Documents",
      "TargetListRelativePath": "dept1",

      "Settings": {

        "MigrateHiddenItems": true,
        "MigrateItemsCreatedAfter": "2016-05-22",
        "MigrateItemsModifiedAfter": "2016-05-22",
        "SkipFilesWithExtensions": "txt:mp3",
        "FilterOutPathSpecialCharacters": false,
        "MigrateOneNoteNotebook": true
      }
    },

    {

      "SourcePath": "\\\\contoso\\fileshare\\dept2",
      "TargetPath": "https://a830edad9050849387E18042320.sharepoint.com",
      "TargetList": "Documents",
      "TargetListRelativePath": "dept2",

      "Settings": {

        "MigrateHiddenItems": true,
        "MigrateItemsCreatedAfter": "2016-05-22",
        "MigrateItemsModifiedAfter": "2016-05-22",
        "SkipFilesWithExtensions": "txt:mp3",
        "MigrateOneNoteNotebook": false,
        "FilterOutPathSpecialCharacters": false,

      }

    }
  ]
}
 
```