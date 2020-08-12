# Safe Management
> **Note:**The content of the sample_safes.csv is for example only and does not represent real safes

Main capabilities
-----------------
- The tool Uses REST API and can support v9.8 of PVWA and up
- The tool supports listing of Safes, Adding new safes and adding new members to safes
- The tool can take a simple CSV file with safe details and for creation (supported by the Add switch)
- The tool can support comma delimited CSV files (default) or tab delimited CSV files

In order to run the tool you need to run some simple commands in Powershell.
The Tool supports four modes: [*List*](#list-command), [*Add*](#add-command), [*Update*](#update-command), [*Members*](#members-command), [*UpdateMembers*](#update-members-command) and [*Delete*](#delete-command)


### List Command:
```powershell
Safe-Management.ps1 -PVWAURL <string> -List [-SafeName <string>] [<CommonParameters>]
```

If you want to List all safes (Based on the running user permissions):
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -List
```

If you want to Filter a specific safe to see its details:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -List -SafeName "MySafe"
```

### Add Command:
Add a single safe or create safes from a file

```powershell
Safe-Management.ps1 -PVWAURL <string> -Add [-SafeName <string>] [-Description <string>] [-ManagingCPM <string>] [-NumVersionRetention <int>] [-FilePath <string>] [<CommonParameters>]
```

If you want to Create a new single safe called 'MySafe' with the default CPM:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Add -SafeName "MySafe"
```

If you want to Create a new single safe and add a description to that safe:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Add -SafeName "MySafe" -Description "This is My Safe that I Created using REST API"
```

If you want to Create a new single safe and set the Managing CPM and the number of versions for retention:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Add -SafeName "MyDMZSafe" -ManagingCPM PassManagerDMZ -NumVersionRetention 5
```

If you want to Create a list of safes from a file:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Add -FilePath "C:\Temp\safes-sample.csv"
```

### Update Command:
Update a single safe or update a list of safes from a file

```powershell
Safe-Management.ps1 -PVWAURL <string> -Update [-SafeName <string>] [-Description <string>] [-ManagingCPM <string>] [-NumVersionRetention <int>] [-FilePath <string>] [<CommonParameters>]
```

If you want to Update the safe called 'MySafe' with a new description:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Update -SafeName "MySafe" -Description "This is My updated Safe description that I Created using REST API"
```

If you want to Update the safe Managing CPM:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Update -SafeName "MyDMZSafe" -ManagingCPM PassManagerDMZ
```

If you want to Update the description and members of a list of safes from a file:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Update -FilePath "C:\Temp\safes-sample.csv"
```
> *Note*: This command will try to Add the members from the file to the safe. Any existing member will be skipped (will not update it's permissions)

### Members Command:
List or add new members to a single safe
```powershell
Safe-Management.ps1 -PVWAURL <string> -Members -SafeName <string> [-UserName <string>] [-MemberRole <"Admin", "Auditor", "EndUser", "Owner">] [-UserLocation <string>] [<CommonParameters>]
```

If you want to list all members of the safe 'MySafe':
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Members -SafeName "MySafe"
```

If you want to add a new End User (default role) member to the safe 'MySafe':
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Members -SafeName "MySafe" -UserName "MyUser" -MemberRole "EndUser"
```

If you want to add a new Auditor member from LDAP to the safe 'MySafe':
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Members -SafeName "MySafe" -UserName "MyAuditUser" -MemberRole "Auditor" -UserLocation "MyLDAPDomain.com"
```

### Update Members Command:
Update members permissions for a single safe or a list of safes

```powershell
Safe-Management.ps1 -PVWAURL <string> -UpdateMembers [-SafeName <string>] [-UserName <string>] [-MemberRole <"Admin", "Auditor", "EndUser", "Owner">] [-FilePath <string>] [<CommonParameters>]
```

If you want to update an existing End User (default role) member to an Owner role on the safe 'MySafe':
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -UpdateMembers -SafeName "MySafe" -UserName "MyUser" -MemberRole "Owner"
```

If you want to Update members of a list of safes from a file:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -UpdateMembers -FilePath "C:\Temp\safes-sample.csv"
```
> *Note*: This command will try to Update the members from the file to the safe. Any member that does not exist on the safe will be skipped (will not add it to the safe)

### Delete Command:
```powershell
Safe-Management.ps1 -PVWAURL <string> -Delete [-SafeName <string>] [-FilePath <string>] [<CommonParameters>]
```

If you want to Delete a specific safe called 'MySafe':
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Delete -SafeName "MySafe"
```

If you want to Delete a list of safes from a file:
```powershell
& .\Safe-Management.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -Delete -FilePath "C:\Temp\safes-sample.csv"
```
