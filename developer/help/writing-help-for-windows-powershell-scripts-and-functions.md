---
title: Skriva hjälp för PowerShell-skript och-funktioner | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 859a6e22-75b1-43d4-ba62-62c107803b37
caps.latest.revision: 7
ms.openlocfilehash: af989fb2eeba6b68f2e3e6506f3f60d5be6f7d8a
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848096"
---
# <a name="writing-help-for-powershell-scripts-and-functions"></a>Skriva hjälp för PowerShell-skript och-funktioner

PowerShell-skript och-funktioner bör vara fullständigt dokumenterade när de delas med andra.
Cmdleten visar hjälp avsnitten för skript och funktioner i samma format som det visar hjälp för cmdlets och alla `Get-Help` parametrar fungerar i hjälp avsnitten för skript och funktioner. `Get-Help`

PowerShell-skript kan innehålla ett hjälp avsnitt om skript och hjälp avsnitt om varje funktion i skriptet.
Funktioner som delas oberoende av skript kan innehålla egna hjälp avsnitt.

I det här dokumentet beskrivs formatet och rätt placering av hjälp avsnitten, och det föreslår rikt linjer för innehållet.

## <a name="types-of-script-and-function-help"></a>Typer av skript-och funktions hjälp

### <a name="comment-based-help"></a>Kommenterings-baserad hjälp
Hjälp avsnittet som beskriver ett skript eller en funktion kan implementeras som en uppsättning kommentarer i skriptet eller funktionen.
När du skriver en kommenterings-baserad hjälp för ett skript och funktioner i ett skript, bör du tänka noga noga med reglerna för att placera den kommenterade hjälpen.
Placeringen avgör om `Get-Help` cmdleten associerar hjälp avsnittet med skriptet eller en funktion.
Mer information om hur du skriver kommentarer baserade hjälp avsnitt finns i [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).

### <a name="xml-based-command-help"></a>Hjälp för XML-baserat kommando
Hjälp avsnittet som beskriver ett skript eller en funktion kan implementeras i en XML-fil som använder kommandot hjälp schema för kommandot.
Om du vill associera skriptet eller funktionen med XML-filen använder du `ExternalHelp` kommentarens nyckelord följt av XML-filens sökväg och namn.

När nyckelordet `Get-Help`kommentarfinns företräde framför den kommenterade hjälpen, även om det inte går att hitta en hjälpfil som `ExternalHelp` matchar värdet för nyckelordet. `ExternalHelp`

### <a name="online-help"></a>Onlinehjälp
Du kan publicera dina hjälp avsnitt på Internet och sedan direkt `Get-Help` för att öppna ämnena.
Mer information om hur du skriver kommenterade hjälp avsnitt finns i [support online](../module/supporting-online-help.md).

Det finns ingen upprättad metod för att skriva konceptuella ämnen för skript och funktioner.
Du kan dock lägga till konceptuella ämnen i Internet listan över avsnitten och deras URL: er i avsnittet relaterade länkar i ett kommando i hjälp avsnittet.

## <a name="content-considerations-for-script-and-function-help"></a>Innehålls överväganden för skript-och funktions hjälp

- Om du skriver ett mycket kort hjälp avsnitt med bara några av de tillgängliga kommando hjälp avsnitten måste du se till att ta med tydliga beskrivningar av skript-eller funktions parametrarna. Inkludera även ett eller två exempel kommandon i avsnittet exempel, även om du bestämmer dig för att utelämna exempel beskrivningar.

- I alla beskrivningar, referera till kommandot som ett skript eller en funktion. Den här informationen hjälper användaren att förstå och hantera kommandot.

  Följande detaljerade Beskrivning anger till exempel att kommandot New-topic är ett skript. Detta påminner användarna om att de måste ange sökvägen och det fullständiga namnet när de kör den.

  > "Det nya ämnes skriptet skapar ett tomt konceptuellt avsnitt för varje ämnes namn i indatafilen..."

  Följande detaljerade beskrivnings steg `Disable-PSRemoting` är en funktion. Den här informationen är särskilt användbar för användare när sessionen innehåller flera kommandon med samma namn, varav vissa kan vara dolda med ett kommando med högre prioritet.

  > `Disable-PSRemoting` Funktionen inaktiverar alla sessionsinställningar på den lokala datorn...

- I ett hjälp avsnitt om skript förklarar du hur du använder skriptet som helhet. Om du också skriver hjälp avsnitt för funktioner i skriptet, nämner du funktionerna i skript hjälp avsnittet och inkluderar referenser till funktions hjälp ämnena i avsnittet relaterade länkar i hjälp avsnittet för skript. När en funktion är en del av ett skript förklarar du i funktions hjälp avsnittet den roll som funktionen spelar i skriptet och hur den kan användas separat. Ange sedan ett hjälp avsnitt för skriptet i avsnittet relaterade länkar i hjälp avsnittet för funktionen.

- När du skriver exempel för ett skripts hjälp avsnitt, måste du ta med sökvägen till skript filen i kommandot example. Detta påminner användarna om att de måste ange sökvägen explicit, även om skriptet finns i den aktuella katalogen.

- I ett funktions hjälp avsnitt kan du påminna användare om att funktionen bara finns i den aktuella sessionen och, om du vill använda den i andra sessioner, måste du lägga till den eller lägga till den i en PowerShell-profil.

- `Get-Help`Visar hjälp avsnittet för ett skript eller en funktion endast när skript filen och hjälp ämnets filer sparas på rätt platser. Därför är det inte praktiskt att inkludera instruktioner för att installera PowerShell eller Spara eller installera skriptet eller funktionen i ett skript eller funktions hjälp avsnitt. Ta i stället in installations anvisningarna i det dokument som du använder för att distribuera skriptet eller funktionen.

## <a name="see-also"></a>Se även

[Skriva kommentarer baserade hjälp avsnitt](./writing-comment-based-help-topics.md)
