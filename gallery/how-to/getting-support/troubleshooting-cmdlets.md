---
ms.date: 06/12/2017
contributor: manikb
keywords: galleriet, powershell, cmdlet, psget
title: 'Felsökning av cmdlet: ar'
ms.openlocfilehash: f5cd9c0cc23fef5891bf02c10b6541ab0f9d418a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084189"
---
# <a name="troubleshooting-cmdlets"></a>Felsökning av cmdlet: ar

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Så här löser du ”varning: Det gick inte att hämta paketet ditt paketnamn ”problem

Rapporteras den som `Install-Module` eller `Update-Module` Ibland misslyckas på vissa datorer.
Baserat på vår undersökning, är det att göra med nätverksanslutningen.
Nyligen har uppdaterat vi NuGet-providern så att den kan hämta paket på ett tillförlitligt sätt.
Du kan följa anvisningarna nedan för att installera den senaste versionen av NuGet-providern och sedan installera eller uppdatera din modul.
Nu ska vi använda ”Azure”-modulen som exemplet nedan.

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```
