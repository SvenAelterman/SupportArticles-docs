---
title: Error 0x8004106C while you run WMI queries
description: Provides a solution to fix the error 0x8004106C that occurs when you run WMI queries.
ms.date: 09/08/2020
author: delhan
ms.author: Delead-Han
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: WMI
ms.technology: SysManagementComponents
---
# WMI Error: 0x8004106C Description: Quota violation, while you run WMI queries

This article helps fix the error 0x8004106C that occurs when you run WMI queries.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2404366

## Symptoms

You're unable to run WMI queries. You may receive an error similar to the following if you run a query. In this example, the following query was run from the root\cimv2 namespace:

Select * From Win32_LogicalDisk Where FreeSpace > 200000

The error returned was:
0x8004106C
Description: Quota violation.

## Cause

This error can occur if the WMI Provider service has reached its quota limit.

## Resolution

Raise the memory quota of the WMI Provider service by carrying out the following steps:
 
- Go to Start--> Run and type **wbemtest.exe**.
- Click **Connect**. 
- In the namespace text box type "root" (without quotes).
- Click **Connect.**  
- Click **Enum Instances...**  
- In the Class Info dialog box, enter Superclass Name as "__ProviderHostQuotaConfiguration" (without quotes) and press **OK**. **Note**: the Superclass name includes a double underscore at the front.
- In the **Query Result** window, double-click "__ProviderHostQuotaConfiguration=@"
- In the **Object Editor** window, double-click whichever Property name you wish to modify the quota for.
- In the **Value** dialog, type in 536870912 (512 MB) for XP and Windows 2003, for Vista a newer start with new value of 805306368 (768), then move to 1073741824 (1024) if still needing room. If this does not resolve quotat violation issue, then need to troubleshoot cause of high memory usage
- Click **Save Property.**  
- Click **Save Object.**  
- Close **Wbemtest.**  
- Restart the computer.
 **Note:**  Windows XP and Windows Server 2003 have a memory quota per host of 128 MB with a limit of 512 MB.  Windows Vista and Windows Server 2008 has a memory quota per host of 512 MB that is not the imposed limit as with XP and 2003 and can increase this number higher.