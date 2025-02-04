---
ms.date: 06/05/2017
keywords: PowerShell cmdlet
title: Upprepa en uppgift för flera objekt ForEach-Object
ms.openlocfilehash: 1442507c4213476f65df3401c1021f8d0fc31956
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030813"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Upprepa en uppgift för flera objekt (ForEach-Object)

Den **ForEach-Object** cmdlet använder skriptblocken och `$_` beskrivning av det aktuella pipeline-objektet så att du kan köra ett kommando för varje objekt i pipelinen. Detta kan användas för att utföra vissa komplicerade uppgifter.

En situation där det kan vara användbart manipulera data för att göra det mer användbart. Win32_LogicalDisk klassen från WMI kan till exempel användas för att returnera information om ledigt utrymme för varje lokal disk. Data returneras när det gäller byte, men, vilket gör det svårt att läsa:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Vi kan konvertera FreeSpace värdet till megabyte genom att dividera varje värde med 1024 två gånger. data är i kilobyte efter första divisionen och efter den andra delen av är det megabyte. Du kan göra det i en ForEach-Object-skriptblocket genom att skriva:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Utdata är tyvärr nu data med inga associerade etiketten. Du kan inte direkt konvertera FreeSpace eftersom WMI-egenskaper som detta är skrivskyddade. Om du anger detta:

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Du får ett felmeddelande visas:

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Du kan ordna om data med hjälp av några avancerade tekniker, men en enklare metod är att skapa ett nytt objekt genom att använda **Select-Object**.
