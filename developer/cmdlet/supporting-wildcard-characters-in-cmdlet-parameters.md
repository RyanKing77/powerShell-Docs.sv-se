---
title: Ge stöd för jokertecken i cmdlet-parametrar
ms.custom: ''
ms.date: 08/26/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.openlocfilehash: 19644c5bc186a5554d6b134a67fc7c4d7aa7b64c
ms.sourcegitcommit: a02ccbeaa17c0e513d6c4a21b877c88ac7725458
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2019
ms.locfileid: "70104452"
---
# <a name="supporting-wildcard-characters-in-cmdlet-parameters"></a>Ge stöd för jokertecken i cmdlet-parametrar

Du måste ofta utforma en cmdlet för att kunna köras mot en grupp resurser i stället för till en enda resurs. En cmdlet kan till exempel behöva hitta alla filer i ett data lager som har samma namn eller tillägg. Du måste ge stöd för jokertecken när du skapar en cmdlet som ska köras mot en grupp med resurser.

> [!NOTE]
> Användning av jokertecken kallas ibland *globbing*.

## <a name="windows-powershell-cmdlets-that-use-wildcards"></a>Windows PowerShell-cmdletar som använder jokertecken

 Många Windows PowerShell-cmdlets stöder jokertecken för sina parameter värden. Till exempel nästan alla cmdletar som har en `Name` - `Path` eller-parameter stöder jokertecken för dessa parametrar. (Även om de flesta cmdletar som `Path` har en parameter också `LiteralPath` har en parameter som inte stöder jokertecken.) Följande kommando visar hur ett jokertecken används för att returnera alla cmdletar i den aktuella sessionen vars namn innehåller verbet get.

 `Get-Command get-*`

## <a name="supported-wildcard-characters"></a>Jokertecken som stöds

Windows PowerShell stöder följande jokertecken.

| Användning |                             Beskrivning                             |  Exempel   |     Matchningar      | Matchar inte |
| -------- | ------------------------------------------------------------------- | ---------- | ---------------- | -------------- |
| *        | Matchar noll eller flera tecken, med början vid den angivna positionen | `a*`       | A, AG, Apple     |                |
| ?        | Matchar alla bokstäver vid angiven position                     | `?n`       | En, i, på       | kördes            |
| [ ]      | Matchar ett tecken intervall                                       | `[a-l]ook` | bok, Cook, utseende | Nook, vidtog     |
| [ ]      | Matchar de angivna tecknen                                    | `[bn]ook`  | bok, Nook       | laga, titta     |

När du utformar cmdletar som stöder jokertecken kan du använda kombinationer av jokertecken. Följande kommando använder `Get-ChildItem` till exempel cmdleten för att hämta alla. txt-filer som finns i mappen c:\Techdocs och som börjar med bokstäverna "a" till "l".

`Get-ChildItem c:\techdocs\[a-l]\*.txt`

Föregående kommando använder området jokertecken `[a-l]` för att ange att fil namnet ska börja med tecknen "a" till och med "l" och `*` använder jokertecknet som plats hållare för alla tecken mellan den första bokstaven i fil namnet och tillägget **. txt** .

I följande exempel används ett mönster med jokertecken som utesluter bokstaven "d", men innehåller alla andra bokstäver från "a" till "f".

`Get-ChildItem c:\techdocs\[a-cef]\*.txt`

## <a name="handling-literal-characters-in-wildcard-patterns"></a>Hantera tecken i mönster med jokertecken

Om det jokertecken du anger innehåller litterala tecken som inte ska tolkas som jokertecken använder du bakstrecks tecknet`` ` ``() som ett escape-tecken. Om du anger litterala tecken int PowerShell-API: et använder du ett enda baktick. Använd två baktick när du anger litterala tecken i PowerShell-Kommandotolken.

Följande mönster innehåller till exempel två hakparenteser som måste beaktas bokstavligen.

När det används i PowerShell-API: et använder du:

- "John Svensson \`[*"] "

När det används från PowerShell-Kommandotolken:

- "John Svensson \` \`[*\`"] "

Det här mönstret matchar "John Svensson [Marketing]" eller "John Svensson [Development]". Till exempel:

```
PS> "John Smith [Marketing]" -like "John Smith ``[*``]"
True

PS> "John Smith [Development]" -like "John Smith ``[*``]"
True
```

## <a name="cmdlet-output-and-wildcard-characters"></a>Cmdlet-utdata och jokertecken

När cmdlet-parametrarna har stöd för jokertecken genererar åtgärden vanligt vis en mat ris utmatning.
Ibland är det ingen mening att stödja mat ris utdata eftersom användaren bara kan använda ett enda objekt. Till exempel `Set-Location` stöder cmdleten inte mat ris utdata eftersom användaren bara anger en enda plats. I den här instansen stöder cmdlet: en fortfarande jokertecken, men den framtvingar matchning till en enda plats.

## <a name="see-also"></a>Se även

[Skriva en Windows PowerShell-cmdlet](./writing-a-windows-powershell-cmdlet.md)

[WildcardPattern-klass](/dotnet/api/system.management.automation.wildcardpattern)
