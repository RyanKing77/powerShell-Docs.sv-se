---
title: RunSpace07 kodexempel | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ad306d9-45c2-4d55-8e64-fdcba43402c5
caps.latest.revision: 6
ms.openlocfilehash: 232b282e366c9fad167686337696ef2ccd8b30d8
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734956"
---
# <a name="runspace07-code-sample"></a>RunSpace07 – kodexempel

Här är källkoden för Runspace07-exemplet som beskrivs i [skapar ett program som lägger till konsolkommandon för en Pipeline](https://msdn.microsoft.com/en-us/01eb7808-e97b-4905-80be-9e2fa38c262e). Det här exempelprogrammet skapar ett körningsutrymme, skapas en pipeline, lägger till två kommandon i pipelinen och sedan körs pipelinen. Kommandona läggs till i pipeline är den `Get-Process` och `Measure-Object` cmdletar.

> [!NOTE]
> Du kan ladda ned den C# källfilen (runspace07.cs) med hjälp av Microsoft Windows Software Development Kit för Windows Vista och Microsoft .NET Framework 3.0-körtidskomponenter. Hämta anvisningar finns i [hur du installerar Windows PowerShell och ladda ned Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).
>
> Hämtade källfilerna är tillgängliga i den  **\<PowerShell-exempel >** directory.

## <a name="code-sample"></a>Kodexempel

[!code-csharp[Runspace07.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace07/Runspace07.cs#L11-L108 "Runspace07.cs")]

## <a name="see-also"></a>Se även

[Programmeringsguide för Windows PowerShell](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)