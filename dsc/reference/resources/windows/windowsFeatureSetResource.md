---
ms.date: 06/12/2017
keywords: DSC, powershell, konfiguration, installation
title: DSC WindowsFeatureSet-resurs
ms.openlocfilehash: 8a64168d9ad0d6a6c40eb0398cc734fa93a247dc
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726785"
---
# <a name="dsc-windowsfeatureset-resource"></a>DSC WindowsFeatureSet-resurs

> Gäller för: Windows PowerShell 5.0

Den **WindowsFeatureSet** resursen i Windows PowerShell Desired State Configuration (DSC) är en mekanism för att säkerställa att roller och funktioner läggs till eller tas bort på målnoden.
Den här resursen är en [sammansatta resource](../../../resources/authoringResourceComposite.md) som anropar den [WindowsFeature-resurs](windowsfeatureResource.md) för varje funktion som anges i den `Name` egenskapen.

Använd den här resursen när du vill konfigurera ett antal Windows-funktioner till samma tillstånd.

## <a name="syntax"></a>Syntax

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Egenskaper

|  Egenskap  |  Description   |
|---|---|
| Namn| Namnen på de roller och funktioner som du vill kontrollera läggs till eller tas bort. Det här är samma som den **namn** egenskapen för den [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature?view=winserver2012r2-ps) cmdlet, och inte visningsnamnet för roller eller funktioner.|
| Autentiseringsuppgifter| Autentiseringsuppgifterna som används för att lägga till eller ta bort roller och funktioner.|
| Se till att| Anger om roller och funktioner har lagts till. För att säkerställa att de roller och funktioner är har lagts till, ange den här egenskapen ”aktuella” för att säkerställa att bort roller och funktioner, egenskapen till ””.|
| IncludeAllSubFeature| Den här egenskapen **$true** att inkludera alla nödvändiga underfunktioner med funktioner som du anger med den **namn** egenskapen.|
| LogPath| Sökvägen till en loggfil där du vill att resursprovidern att logga in igen.|
| DependsOn| Anger att konfigurationen av en annan resurs måste köras innan den här resursen har konfigurerats. Till exempel om ID för resurskonfigurationen skriptblock som du vill köra först är __ResourceName__ och är av typen __ResourceType__, syntaxen för den här egenskapen är `DependsOn = "[ResourceType]ResourceName"`.|
| Källa| Anger platsen för källfilen för installationen, om det behövs.|

## <a name="example"></a>Exempel

Följande konfiguration garanterar att den **-webbserver** (IIS) och **SMTP-servern** funktioner och dess underfunktioner vardera, är installerade.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```
