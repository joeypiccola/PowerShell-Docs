﻿---
author: jpjofre
description: 
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
keywords: powershell, cmdlet
manager: carolz
ms.date: 2016-09-30
ms.prod: powershell
ms.technology: powershell
ms.topic: reference
online version: http://go.microsoft.com/fwlink/?LinkId=821580
schema: 2.0.0
title: Get-ChildItem
---

# Get-ChildItem

## SYNOPSIS
Gets the items and child items in one or more specified locations.

## SYNTAX

### Items (Default)
```
Get-ChildItem [[-Path] <String[]>] [[-Filter] <String>] [-Include <String[]>] [-Exclude <String[]>] [-Recurse]
 [-Depth <UInt32>] [-Force] [-Name] [-UseTransaction]
 [-Attributes <System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]>] [-Directory] [-File]
 [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]
```

### LiteralItems
```
Get-ChildItem -LiteralPath <String[]> [[-Filter] <String>] [-Include <String[]>] [-Exclude <String[]>]
 [-Recurse] [-Depth <UInt32>] [-Force] [-Name] [-UseTransaction]
 [-Attributes <System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]>] [-Directory] [-File]
 [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]
```

## DESCRIPTION
The **Get-ChildItem** cmdlet gets the items in one or more specified locations.
If the item is a container, it gets the items inside the container, known as child items.
You can use the *Recurse* parameter to get items in all child containers.

A location can be a file system location, such as a directory, or a location exposed by a different Windows PowerShell provider, such as a registry hive or a certificate store.

## EXAMPLES

### Example 1: Get child items in the current directory
```
PS C:\>Get-ChildItem
```

This command gets the child items in the current location.
If the location is a file system directory, it gets the files and sub-directories in the current directory.
If the item does not have child items, this command returns to the command prompt without displaying anything.

The default display lists the mode (attributes), last write time, file size (length), and the name of the file.
The valid values for mode are d (directory), a (archive), r (read-only), h (hidden), and s (system).

### Example 2: Get all files with the specified file extension in the current directory and subdirectories
```
PS C:\>Get-ChildItem -Path "*.txt" -Recurse -Force
```

This command gets all of the .txt files in the current directory and its subdirectories.
The *Recurse* parameter directs Windows PowerShell to get objects recursively, and it indicates that the subject of the command is the specified directory and its contents.
The Force parameter adds hidden files to the display.

To use the *Recurse* parameter on Windows PowerShell 2.0 and earlier versions of Windows PowerShell, the *Path* parameter must be a container.
Use the *Include* parameter to specify the .txt file type.
For instance, `Get-ChildItem -Path .\* -Include *.txt -Recurse`

### Example 3: Get all child items using an inclusion and exclusion
```
PS C:\>Get-ChildItem -Path "C:\Windows\Logs\*" -Include "*.txt" -Exclude "A*"
```

This command lists the .txt files in the Logs subdirectory, except for those whose names start with the letter A.
It uses the wildcard character (*) to indicate the contents of the Logs subdirectory, not the directory container.
Because the command does not include the *Recurse* parameter, the command does not include the content of directory automatically; you need to specify it.

### Example 4: Get all registry keys in a specific key
```
PS C:\>Get-ChildItem -Path "HKLM:\Software"
```

This command gets all of the registry keys in the HKEY_LOCAL_MACHINE\SOFTWARE key in the registry of the local computer.

### Example 5: Get the name of items in the current directory
```
PS C:\>Get-ChildItem -Name
```

This command gets only the names of items in the current directory.

### Example 6: Get all certificates in a certification drive that have code-signing authority
```
PS C:\>Import-Module Microsoft.PowerShell.Security
PS C:\>Get-ChildItem -Path "Cert:\*" -Recurse -CodeSigningCert
```

This command gets all of the certificates in the Windows PowerShell Cert: drive that have code-signing authority.

The first command imports the **Microsoft.PowerShell.Security** module into the session.
This module includes the Certificate provider that creates the Cert: drive.

The second command uses the **Get-ChildItem** cmdlet.
The value of the *Path* parameter is the Cert: drive.
The *Recurse* parameter requests a recursive search.
The *CodeSigningCertificate* parameter is a dynamic parameter that the Certificate provider adds to the **Get-ChildItem** cmdlet.
This parameter gets only certificates that have code-signing authority.

For more information about the Certificate provider and the Cert: drive, go to http://go.microsoft.com/fwlink/?LinkID=113433http://go.microsoft.com/fwlink/?LinkID=113433 or use the Update-Help cmdlet to download the help files for the **Microsoft.PowerShell.Security** module and then type `Get-Help Certificate`.

### Example 7: Get all items in the specified directory and its subdirectories that have an inclusion and exclusion
```
PS C:\>Get-ChildItem -Path C:\Windows -Include "*mouse*" -Exclude "*.png"
```

This command gets all of the items in the C:\Windows directory and its subdirectories that have mouse in the file name, except for those with a .png file name extension.

## PARAMETERS

### -Attributes
{{Fill Attributes Description}}

```yaml
Type: System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]
Parameter Sets: (All)
Aliases: 
Accepted values: ReadOnly, Hidden, System, Directory, Archive, Device, Normal, Temporary, SparseFile, ReparsePoint, Compressed, Offline, NotContentIndexed, Encrypted, IntegrityStream, NoScrubData

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Depth
{{Fill Depth Description}}

```yaml
Type: UInt32
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Directory
{{Fill Directory Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ad, d

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Exclude
Specifies, as a string array, an item or items that this cmdlet excludes in the operation.
The value of this parameter qualifies the *Path* parameter.
Enter a path element or pattern, such as *.txt.
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -File
{{Fill File Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: af

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Filter
Specifies a filter in the provider's format or language.
The value of this parameter qualifies the *Path* parameter.
The syntax of the filter, including the use of wildcards, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when retrieving the objects, rather than having Windows PowerShell filter the objects after they are retrieved.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force
Forces the command to run without asking for user confirmation.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Hidden
{{Fill Hidden Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ah, h

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Include
Specifies, as a string array, an item or items that this cmdlet includes in the operation.
The value of this parameter qualifies the *Path* parameter.
Enter a path element or pattern, such as *.txt.
Wildcards are permitted.

The *Include* parameter is effective only when the command includes the *Recurse* parameter or the path leads to the contents of a directory, such as C:\Windows\*, where the wildcard character specifies the contents of the C:\Windows directory.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath
Specifies, as a string arrya, a path to one or more locations.
Unlike the *Path* parameter, the value of the *LiteralPath* parameter is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: LiteralItems
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name
Indicates that this cmdlet gets only the names of the items in the locations.
If you pipe the output of this command to another command, only the item names are sent.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Specifies a path to one or more locations.
Wildcards are permitted.
The default location is the current directory (.).

```yaml
Type: String[]
Parameter Sets: Items
Aliases: 

Required: False
Position: 0
Default value: Current directory
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -ReadOnly
{{Fill ReadOnly Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ar

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Recurse
Indicates that this cmdlet gets the items in the specified locations and in all child items of the locations.

In Windows PowerShell 2.0 and earlier versions of Windows PowerShell, the *Recurse* parameter works only when the value of the *Path* parameter is a container that has child items, such as C:\Windows or C:\Windows\*, and not when it is an item does not have child items, such as C:\Windows\*.exe.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: s

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -System
{{Fill System Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: as

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTransaction
Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String
You can pipe a string that contains a path to this cmdlet.

## OUTPUTS

### System.Object
The type of object that this cmdlet returns is determined by the objects in the provider drive path.

### System.String
If you use the *Name* parameter, **Get-ChildItem** returns the object names as strings.

## NOTES
* You can also refer to **Get-ChildItem** by its built-in aliases, ls, dir, and gci. For more information, see about_Aliases.

  This cmdlet does not get hidden items by default.
To get hidden items, use the *Force* parameter.

  The **Get-ChildItem** cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type `Get-PSProvider`.
For more information, see about_Providers (http://go.microsoft.com/fwlink/?LinkID=113250).

*

## RELATED LINKS

[Get-Item](Get-Item.md)

[Get-Location](Get-Location.md)

[Get-Process](Get-Process.md)

[Get-PSProvider](Get-PSProvider.md)

