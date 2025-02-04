---
ms.date: 06/05/2017
keywords: PowerShell cmdlet
title: ISEAddOnToolCollection-objektet
ms.openlocfilehash: 28ab9747e573b7a76ee655289b341870b1728bc2
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030617"
---
# <a name="the-iseaddontoolcollection-object"></a>ISEAddOnToolCollection-objektet

Den **ISEAddOnToolCollection** objekt är en samling **ISEAddOnTool** objekt. Ett exempel är den **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objekt.

## <a name="methods"></a>Metoder

### <a name="add-name-controltype-isvisible-"></a>Lägg till\( namn, kontrolltyp, \[IsVisible\] \)

Stöds i Windows PowerShell ISE 3.0 och senare och finns inte i tidigare versioner.

Lägger till ett nytt tilläggsverktyg till samlingen. Returnerar den nyligen tillagda tilläggsverktyg. Innan du kör det här kommandot måste du installera verktyget tillägg på den lokala datorn och läsa in sammansättningen.

**Namn på** -sträng Anger visningsnamnet för verktyget tillägg har lagts till i Windows PowerShell ISE.

**Kontrolltyp** -typen anger den kontroll som har lagts till.

**\[IsVisible\]**  -valfritt booleskt om **$true**, verktyget tillägg visas omedelbart i verktygsfönstret associerade.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Ta bort\( objekt \)

Stöds i Windows PowerShell ISE 3.0 och senare och finns inte i tidigare versioner.

Tar bort den angivna tilläggsverktyg från samlingen.

**Objektet** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool anger objektet som ska tas bort från Windows PowerShell ISE.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)

Stöds i Windows PowerShell ISE 3.0 och senare och finns inte i tidigare versioner.

Väljer PowerShell fliken som den **psTab** parametern anger.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab PowerShell-fliken väljer.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a>Ta bort\( psTab \)

Stöds i Windows PowerShell ISE 3.0 och senare och finns inte i tidigare versioner.

Tar bort PowerShell fliken som den **psTab** parametern anger.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab PowerShell-flik för att ta bort.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>Se även

- [The PowerShellTab Object](The-PowerShellTab-Object.md)
- [Syftet med den Windows PowerShell ISE-Skriptobjektmodellen](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarki för ISE-objektmodellen](The-ISE-Object-Model-Hierarchy.md)
