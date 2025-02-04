---
title: Definiera standardmedlemmen anger för objekt | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 77f94326-8ffe-4d40-bd2a-b79fb0b4a4e5
caps.latest.revision: 8
ms.openlocfilehash: 2d634e7638ec0e0117d65ca0b2d08e68f0068a03
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068257"
---
# <a name="defining-default-member-sets-for-objects"></a>Definiera standardmedlemsuppsättningar för objekt

PSStandardMembers uppsättningen används av Windows PowerShell för att definiera de standard-egenskaperna för ett objekt. Standardegenskapsuppsättningar kan användas av kommandon, till exempel formatering cmdletar för att visa endast de egenskaper som definieras av egenskapsuppsättningen. De standard-egenskaperna är DefaultDisplayProperty, DefaultDisplayPropertySet och DefaultKeyPropertySet. Windows PowerShell ignorerar alla andra medlemsuppsättningar och andra egenskapsuppsättningar läggas till i PSStandardMembers medlem.

## <a name="member-set-for-systemdiagnosticsprocess"></a>Uppsättningen för System.Diagnostics.Process

I följande exempel definierar PSStandardMembers uppsättningen egenskapsuppsättningen DefaultDisplayPropertySet för [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objekt. Den här egenskapen angiven används av den [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet.

```xml
<Type>
  <Name>System.Diagnostics.Process</Name>
  <Members>
    <MemberSet>
     <Name>PSStandardMembers</Name>
     <Members>
       <PropertySet>
         <Name>DefaultDisplayPropertySet</Name>
         <ReferencedProperties>
           <Name>Id</Name>
           <Name>Handles</Name>
           <Name>CPU</Name>
           <Name>Name</Name>
         </ReferencedProperties>
      </PropertySet>
    </Members>
  </MemberSet>
```

Följande utdata visar standardegenskaperna som returneras av den [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet. Endast den `Id`, `Handles`, `CPU`, och `Name` egenskaper returneras för varje processobjekt.

```powershell
Get-Process | format-list
```

```output
Id      : 2036
Handles : 27
CPU     :
Name    : AEADISRV

Id      : 272
Handles : 38
CPU     :
Name    : agrsmsvc
...
```

## <a name="see-also"></a>Se även

[Skriva en Windows PowerShell-Cmdlet](./writing-a-windows-powershell-cmdlet.md)
