---
title: Med Visual Studio Code för PowerShell-utveckling
description: Med Visual Studio Code för PowerShell-utveckling
ms.date: 08/06/2018
ms.openlocfilehash: 6a0da6e060693dc7cfc08d40fd658414dc23d660
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733886"
---
# <a name="using-visual-studio-code-for-powershell-development"></a>Med Visual Studio Code för PowerShell-utveckling

Förutom den [PowerShell ISE][ise], PowerShell är också väl stöds i Visual Studio Code.
Dessutom stöds ISE inte med PowerShell Core Visual Studio Code har stöd för PowerShell Core på alla plattformar (Windows, macOS och Linux)

Du kan använda Visual Studio Code på Windows med PowerShell version 5 med hjälp av Windows 10 eller genom att installera [Windows Management Framework 5.0 RTM](https://devblogs.microsoft.com/powershell/windows-management-framework-wmf-5-0-rtm-is-now-available-via-the-microsoft-update-catalog/) för äldre Windows-operativsystem (t.ex. Windows 8.1, osv.).

Kontrollera att PowerShell finns i systemet innan du startar den.
Moderna arbetsbelastningar i Windows, macOS och Linux finns här:

- [Installera PowerShell Core i Linux][install-pscore-linux]
- [Installera PowerShell Core i macOS][install-pscore-macos]
- [Installera PowerShell Core i Windows][install-pscore-windows]

Traditionella Windows PowerShell-arbetsbelastningar, se [installera Windows PowerShell][install-winps].

## <a name="editing-with-visual-studio-code"></a>Redigera med Visual Studio Code

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. Installera Visual Studio Code](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: Följ installationsanvisningarna på den [som körs på Linux i VS Code](https://code.visualstudio.com/docs/setup/linux) sidan

- **macOS**: Följ installationsanvisningarna på den [köra VS-kod i Mac OS](https://code.visualstudio.com/docs/setup/mac) sidan

  > [!IMPORTANT]
  > I macOS, måste du installera OpenSSL för PowerShell-tillägget ska fungera korrekt.
  > Det enklaste sättet att göra detta är att installera [Homebrew](https://brew.sh/) och kör sedan `brew install openssl`.
  > VS Code kan nu läsa in PowerShell-tillägget har.

- **Windows**: Följ installationsanvisningarna på den [köra VS Code på Windows](https://code.visualstudio.com/docs/setup/windows) sidan

### <a name="2-installing-powershell-extension"></a>2. Installera PowerShell-tillägget

- Starta Visual Studio Code app genom att:
  - **Windows**: att skriva `code` i PowerShell-sessionen
  - **Linux**: att skriva `code` i terminalen
  - **macOS**: att skriva `code` i terminalen

- Starta **snabb öppna** genom att trycka på **Ctrl + P** (**Cmd + P** på Mac).
- Snabb Skriv `ext install powershell` och därefter **RETUR**.
- Den **tillägg** öppnas i Sidopanel. Välj tillägget PowerShell från Microsoft.
  Du bör se ut ungefär som nedan:

  ![VSCode](../../images/vscode.png)

- Klicka på den **installera** knappen på PowerShell-tillägget från Microsoft.
- Efter installationen visas den **installera** knappen övergår i **Reload**.
  Klicka på **Reload**.
- När Visual Studio Code har läs in igen, är det dags för redigering.

Exempelvis för att skapa en ny fil, klickar du på **File -> Nytt**.
Om du vill spara den, klickar du på **Arkiv -> Spara** och ange sedan ett filnamn, låt oss säga att `HelloWorld.ps1`.
Stäng filen genom att klicka på ”x” bredvid namnet på filen.
Avsluta Visual Studio Code **Arkiv -> Avsluta**.

### <a name="installing-the-powershell-extension-on-restricted-systems"></a>Installera PowerShell-tillägget på begränsade system

Vissa system är inställda på ett sätt som kräver alla kod signaturer som ska kontrolleras och därför kräver PowerShell redigeraren tjänster att manuellt godkänna för att köras på systemet.
En uppdatering av grupprinciper som ändrar körningsprincipen är en trolig orsak om du har installerat tillägget PowerShell men ansluter till ett fel som:

```
Language server startup failed.
```

Öppna ett PowerShell och kör för att manuellt godkänna PowerShell redigeraren tjänster och därmed PowerShell-tillägget för VSCode:

```powershell
Import-Module $HOME\.vscode\extensions\ms-vscode.powershell*\modules\PowerShellEditorServices\PowerShellEditorServices.psd1
```

Du uppmanas via ”vill du köra programvaran från denna ej betrodda utgivare”?
Typ `R` att köra filen. Öppna Visual Studio Code och kontrollera att tillägget PowerShell fungerar korrekt. Om du fortfarande har problem med att komma igång, berätta för oss på [GitHub](https://github.com/PowerShell/vscode-powershell/issues).

#### <a name="choosing-a-version-of-powershell-to-use-with-the-extension"></a>Välja en version av PowerShell för att använda i tillägget

Med PowerShell Core installation sida vid sida med Windows PowerShell, är det nu möjligt att använda en viss version av PowerShell i PowerShell-tillägget. Använd följande här för att välja versionen:

1. Öppna kommandot utbud (<kbd>Ctrl</kbd>+<kbd>SKIFT</kbd>+<kbd>P</kbd> på Windows och Linux, <kbd>Cmd</kbd> + <kbd>SKIFT</kbd>+<kbd>P</kbd> på macOS).
1. Sök efter ”Session”.
1. Klicka på ”PowerShell: Visa Session menyn ”.
1. Välj versionen av PowerShell som du vill använda från listan – till exempel PowerShell Core ””.

>[!IMPORTANT]
> Den här funktionen tittar på några välkända sökvägar i olika operativsystem för att identifiera platser för installation av PowerShell. Om du har installerat PowerShell på en icke-vanliga plats kan den inte visas först i menyn Session. Du kan utöka menyn sessionen genom att [att lägga till dina egna anpassade sökvägar](#adding-your-own-powershell-paths-to-the-session-menu) enligt beskrivningen nedan.

>[!NOTE]
> Det finns ett annat sätt att komma till menyn session. När en PowerShell-fil är öppna i redigeringsprogram, visas en grön versionsnumret i det nedre högra hörnet. Klicka på det här versionsnumret kommer du till menyn session.

##### <a name="adding-your-own-powershell-paths-to-the-session-menu"></a>Att lägga till egna PowerShell-sökvägar till menyn session

Du kan lägga till andra körbara sökvägar PowerShell session-menyn genom att VS Code.

Lägg till ett objekt i listan `powershell.powerShellAdditionalExePaths` eller skapa listan om den inte finns i din `settings.json`:

```json
{
    // other settings...

    "powershell.powerShellAdditionalExePaths": [
        {
            "exePath": "C:\\Users\\tyler\\Downloads\\PowerShell\\pwsh.exe",
            "versionName": "Downloaded PowerShell"
        }
    ],
    
    // other settings...
}
```

Varje objekt måste ha:

* `exePath`: Sökvägen till den `pwsh` eller `powershell` körbara.
* `versionName`: Den text som visas i menyn session.

Du kan ange standard PowerShell-version du använder med hjälp av den `powershell.powerShellDefaultVersion` inställningen av inställningen detta i texten visas i menyn session (även kallat den `versionName` i den senaste inställningen):

```json
{
    // other settings...

    "powershell.powerShellAdditionalExePaths": [
        {
            "exePath": "C:\\Users\\tyler\\Downloads\\PowerShell\\pwsh.exe",
            "versionName": "Downloaded PowerShell"
        }
    ],
    
    "powershell.powerShellDefaultVersion": "Downloaded PowerShell",
    
    // other settings...
}
```

När du har ställt in den här inställningen kan starta om Visual Studio Code eller använda den i ”utvecklare: Läs in på nytt fönster ”utbud Kommandoåtgärden att uppdatera aktuella vscode-fönstret.

Om du öppnar menyn sessionen, kommer du nu se ditt ytterligare PowerShell-versioner!

> [!NOTE]
> Om du skapar PowerShell från källan, är det här ett bra sätt att testa din lokal version av PowerShell.

#### <a name="configuration-settings-for-visual-studio-code"></a>Konfigurationsinställningar för Visual Studio Code

Med hjälp av stegen i föregående stycke kan du lägga till konfigurationsinställningar i `settings.json`.

Vi rekommenderar följande konfigurationsinställningar för Visual Studio Code:

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true,
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

Om du inte vill att dessa inställningar påverkar alla filtyper, kan VSCode också konfigurationer per språk. Skapa en specifik språkinställning genom att ange inställningar i en `[<language-name>]` fält. Till exempel:

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

Mer information om filen kodning i VS Code finns i [förstå Filkodning](understanding-file-encoding.md).

## <a name="debugging-with-visual-studio-code"></a>Felsöka med Visual Studio Code

### <a name="no-workspace-debugging"></a>Ingen arbetsyta felsökning

Du kan felsöka PowerShell-skript utan att öppna den mapp som innehåller PowerShell-skriptet från och med Visual Studio Code-versionen 1.9. Öppna PowerShell-skriptfil med **Arkiv -> Öppna fil...** , ange en brytpunkt på rad (tryck på F9) och tryck på F5 för att starta felsökningen. Du bör se Debug åtgärdsfönstret visas där du kan dela i felsökare, steg, återuppta och stoppa felsökning.

### <a name="workspace-debugging"></a>Felsökning av arbetsyta

Felsökning av arbetsytan refererar till felsökning i samband med en mapp som du har öppnat i Visual Studio Code med **Öppna mapp...**  från den **filen** menyn.
Den mapp som du öppnar är vanligtvis projektmappen PowerShell och/eller roten för Git-lagringsplatsen.

Även i det här läget kan starta du felsökning markerade PowerShell-skriptet genom att bara trycka på F5.
Dock kan arbetsytan felsökning du definiera konfigurationer med flera debug än bara felsökning öppna filen.
Du kan exempelvis lägga till en konfigurationer för att:

- Starta Pester tester i felsökningsprogrammet
- Starta en viss fil med argumenten i Felsökning
- Starta en interaktiv session i Felsökning
- Bifoga felsökningsprogrammet till en värdprocess för PowerShell

Följ dessa steg för att skapa konfigurationsfilen debug:

  1. Öppna den **felsöka** vyn genom att trycka på **Ctrl + Skift + D** (**Cmd + SKIFT + D** på Mac).
  2. Tryck på den **konfigurera** kugghjulsikonen i verktygsfältet.
  3. Visual Studio Code uppmanas du att **Välj miljö**. Välj **PowerShell**.

  När du gör detta skapar en katalog och en fil ”.vscode\launch.json” i roten av din arbetsytemapp Visual Studio Code.
  Det här är där din debug-konfiguration lagras. Om filerna finns i en Git-lagringsplats, vill du förmodligen att genomföra launch.json-filen.
  Innehållet i launch.json-filen är:

  ```json
  {
    "version": "0.2.0",
    "configurations": [
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Launch (current file)",
            "script": "${file}",
            "args": [],
            "cwd": "${file}"
        },
        {
            "type": "PowerShell",
            "request": "attach",
            "name": "PowerShell Attach to Host Process",
            "processId": "${command.PickPSHostProcess}",
            "runspaceId": 1
        },
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Interactive Session",
            "cwd": "${workspaceRoot}"
        }
    ]
  }
  ```

  Detta representerar vanliga scenarier för felsökning.
  Men när du öppnar den här filen i redigeraren kan du se en **Lägg till konfiguration...**  knappen.
  Du kan trycka på knappen för att lägga till fler konfigurationer för felsökning av PowerShell. Är en praktisk konfiguration för att lägga till **PowerShell: Starta skriptet**.
  Med den här konfigurationen kan du ange en viss fil med valfria argument som ska startas varje gång du trycker på F5 oavsett vilken fil som är aktiva i redigeraren.

  När debug-konfigurationen har upprättats kan du välja vilken konfiguration som du vill använda under en felsökningssession genom att välja en från debug konfigurationen listrutan i den **felsöka** vyns verktygsfältet.

Det finns några bloggar som hjälper dig att komma igång med hjälp av PowerShell-tillägget för Visual Studio Code:

- [PowerShell-tillägget][ps-extension]
- [Skriv och Felsök PowerShell-skript i Visual Studio Code][debug]
- [Felsökning av Visual Studio Code-vägledning][vscode-guide]
- [Felsökning av PowerShell i Visual Studio Code][ps-vscode]
- [Kom igång med PowerShell-utveckling i Visual Studio Code][getting-started]
- [Visual Studio Code redigeringsfunktioner för PowerShell-utveckling – del 1][editing-part1]
- [Visual Studio Code redigeringsfunktioner för PowerShell-utveckling – del 2][editing-part2]
- [Felsökning av PowerShell-skriptet i Visual Studio Code – del 1][debugging-part1]
- [Felsökning av PowerShell-skriptet i Visual Studio Code – del 2][debugging-part2]

[ise]: ../ise/Introducing-the-Windows-PowerShell-ISE.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-Linux.md
[install-pscore-macos]:  ../../setup/Installing-PowerShell-Core-on-macOS.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]: https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]: https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]: https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]: https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]: https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a>PowerShell-tillägget för Visual Studio Code

Tillägget PowerShell källkoden finns på [GitHub](https://github.com/PowerShell/vscode-powershell).
