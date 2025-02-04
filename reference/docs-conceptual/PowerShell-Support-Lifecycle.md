---
title: Supportlängd för PowerShell Core
description: Principer som styr support för PowerShell Core
ms.date: 08/06/2018
ms.openlocfilehash: 60999ed54ca3be15232ffee3ab0c49cb94873a8f
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986738"
---
# <a name="powershell-core-support-lifecycle"></a>Supportlängd för PowerShell Core

PowerShell Core är en distinkt uppsättning verktyg och komponenter som levereras, installeras och konfigureras separat från Windows PowerShell. Därför ingår inte PowerShell-kärnan i licens avtalen för Windows 7/8.1/10 eller Windows Server.

PowerShell Core stöds dock i traditionella Microsofts support avtal, inklusive [Högsta][], [Microsoft Enterprise Agreement][enterprise-agreement]och [Microsoft Software Assurance][assurance].
Du kan också betala för [assisterad support][] för PowerShell Core genom att skicka en support förfrågan om ditt problem.

## <a name="community-support"></a>Community-support

Vi erbjuder också [Community-support][] på GitHub där du kan skicka ett problem, en bugg eller en funktions förfrågan.
Du kan också få hjälp från andra medlemmar i communityn i [Microsoft-Community][] eller Microsoft [PowerShell-Tech-community][]. Vi erbjuder ingen garanti där communityn kommer att åtgärda problemet inom rimlig tid. Om du har ett problem som kräver omedelbar uppmärksamhet bör du använda de traditionella, avgiftsbelagda support alternativen.

## <a name="lifecycle-of-powershell-core"></a>Livs cykel för PowerShell Core

PowerShell Core antar [Microsofts moderna livs cykel policy][modern]. Den här support livs cykeln är avsedd att hålla kunderna uppdaterade med de senaste versionerna.

Grenen för version 6. x av PowerShell Core kommer att uppdateras ungefär en gång var sjätte månad (exempel: 6,0, 6,1, 6,2 osv.)

> [!IMPORTANT]
> Du måste uppdatera inom sex månader efter att varje ny del versions version fortsätter att få support.

Om exempelvis PowerShell Core 6,1 lanseras den 1 juli 2018 förväntas du uppdatera till PowerShell Core 6,1 före den 1 januari 2019 för att underhålla supporten.

> [!IMPORTANT]
> Du måste uppdatera inom 30 dagar efter att varje ny korrigerings version släpps för att fortsätta få support.

Om du till exempel kör PowerShell Core 6,1 och 6.1.3 släpptes den 19 februari 2019 förväntas du uppdatera till PowerShell Core 6.1.3 senast 21 mars 2019, vilket är 30 dagar efter att stödet har släppts. Om det finns några korrigeringar som krävs kommer korrigeringarna att lanseras i nästa kumulativa uppdatering.

Den moderna livs cykel policyn kräver också att Microsoft ger kunderna tolv månaders varsel innan de kan avbryta supporten för en produkt (dvs. PowerShell Core).

Slutligen förväntar vi sig att PowerShell Core kommer att anta den långsiktiga etablerings metoden. I den här underhålls metoden behöver vi bara underhålla och uppdatera säkerhets uppdateringar för att hålla stöd för en speciell gren/version av 6. x.

## <a name="supported-platforms"></a>Plattformar som stöds

För att bekräfta om din plattform och version av PowerShell Core stöds officiellt, se följande tabell.

Vår community har också bidragit med paket för vissa plattformar, men de stöds inte officiellt. Dessa paket är markerade som `Community` i tabellen.

Plattformar som anges `Experimental` som inte stöds officiellt, men som är tillgängliga för experimentering och feedback.

| Plattform                                          | 6.1         | 6.2         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7, 8,1 och 10                            | Stöds   | Stöds   |
| Windows Server 2008 R2, 2012 R2, 2016             | Stöds   | Stöds   |
| [Windows Server, halvårs kanal][semi-annual] | Stöds   | Stöds   |
| Ubuntu 16,04 och 18,04                            | Stöds   | Stöds   |
| Ubuntu 18,10 (via Snap-paket)                   | Community   | Community   |
| Ubuntu 19,04 (via Snap-paket)                   | Community   | Community   |
| Debian 9                                          | Stöds   | Stöds   |
| CentOS 7                                          | Stöds   | Stöds   |
| Red Hat Enterprise Linux 7                        | Stöds   | Stöds   |
| openSUSE 42,3                                     | Stöds   | Stöds   |
| Fedora 28                                         | Stöds   | Stöds   |
| macOS 10.12 +                                      | Stöds   | Stöds   |
| Båge                                              | Community   | Community   |
| Raspbian                                          | Community   | Community   |
| Kali                                              | Community   | Community   |
| AppImage (fungerar på flera Linux-plattformar)      | Community   | Community   |
| [Snapin-paket](https://snapcraft.io/powershell)   | Se Obs!    | Se Obs!    |

> [!NOTE]
> Snapin-paket stöds på samma sätt som den distribution som du kör paketet på.

## <a name="powershell-releases-end-of-life"></a>Slut på livs längd för PowerShell-versioner

Baserat på [livs cykeln för PowerShell Core](#lifecycle-of-powershell-core)visar följande tabell de datum då olika versioner inte längre kommer att stödjas.

| Version | Livs längd                   |
|---------|-------------------------------|
| 6.0     | 13 februari 2019             |
| 6.1     | 28 september 2019            |
| 6.2     | 6 månader efter 7 utgåvor     |

## <a name="unsupported-platforms"></a>Plattformar som inte stöds

När en plattforms version når livs längd som definieras av plattforms ägaren, kommer PowerShell-kärnan också upphöra att stödja den plattforms versionen. Tidigare utgivna paket är fortfarande tillgängliga för kunder som behöver åtkomst men formell support och uppdateringar av någon typ kommer inte längre att tillhandahållas.

Distributions ägarna avslutade därför stödet för följande versioner och stöds inte.

| Plattform | Version | Uttjänta                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 24      | [2017 augusti](https://fedoramagazine.org/fedora-24-eol/)                                    |
| Fedora   | 25      | [December 2017](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 26      | [Maj 2018](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| openSUSE | 42.1    | [Maj 2017](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| openSUSE | 42,2    | [Januari 2018](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| Ubuntu   | 16,10   | [Juli 2017](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| Ubuntu   | 17,04   | [Januari 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 17,10   | [Juli 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |
| Debian   | 8       | [2018 juni](https://lists.debian.org/debian-security-announce/2018/msg00132.html)           |
| Fedora   | 27      | [November 2018](https://fedoramagazine.org/fedora-27-end-of-life/)                          |
| Ubuntu   | 14.04   | [April 2019](https://wiki.ubuntu.com/Releases)                                              |

## <a name="notes-on-licensing"></a>Anteckningar om licensiering

PowerShell-kärnan släpps under [MIT-licens][]. Under den här licensen och utan ett betalt support avtal är användare begränsade till [Community-support][]. Med community-support ger Microsoft inga garantier för svars tider eller korrigeringar.

## <a name="windows-powershell-module"></a>Windows PowerShell-modul

Stöd för PowerShell Core inkluderar inte produktmallar, om inte dessa moduler uttryckligen stöder PowerShell-kärnan. Till exempel är det ett `ActiveDirectory` scenario som inte stöds om du använder modulen som levereras som en del av Windows Server.

Moduler som inte uttryckligen stöder PowerShell-kärnan kan dock vara kompatibla i vissa fall. Genom att installera [`WindowsPSModulePath`][] modulen kan du lägga till Windows PowerShell `PSModulePath` i PowerShell-kärnan `PSModulePath`.

Installera `WindowsPSModulePath` först modulen från PowerShell-galleriet:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

När du har installerat den här modulen `Add-WindowsPSModulePath` kör du cmdleten för att `PSModulePath` lägga till Windows PowerShell till PowerShell-kärnan:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="experimental-features"></a>Experimentella funktioner

[Experimentella funktioner][] är begränsade till [Community-support](#community-support).

[Högsta]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[Community-support]: https://github.com/powershell/powershell/issues
[Microsoft-Community]: https://answers.microsoft.com/
[PowerShell-Tech-community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[assisterad support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT-licens]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
['WindowsPSModulePath']: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[Experimentella funktioner]: /powershell/module/microsoft.powershell.core/about/about_powershell_config?view=powershell-6#experimentalfeatures
