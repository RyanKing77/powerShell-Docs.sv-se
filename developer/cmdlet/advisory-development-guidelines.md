---
title: Riktlinjer för rådgivande utveckling | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 79c9bcbc-a2eb-4253-a4b8-65ba54ce8d01
caps.latest.revision: 9
ms.openlocfilehash: 980b488800587e31286e2ca2ece924e07f8af3f3
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/17/2019
ms.locfileid: "65854868"
---
# <a name="advisory-development-guidelines"></a>Rekommenderade riktlinjer för utveckling

Det här avsnittet beskriver riktlinjer som du bör överväga för att säkerställa bra upplevelser för utveckling och användare. Ibland kan de gäller, och ibland kan de inte.

## <a name="design-guidelines"></a>Designriktlinjer

Följande riktlinjer bör övervägas när du utformar cmdletar. När du har hittat en Design riktlinje som gäller för din situation bör du titta på koden riktlinjer för liknande riktlinjer.

### <a name="support-an-inputobject-parameter-ad01"></a>Stöd för en InputObject-Parameter (AD01)

Eftersom Windows PowerShell fungerar direkt med Microsoft .NET Framework-objekt, finns ett .NET Framework-objekt ofta att exakt matchar typ du behöver utföra en viss åtgärd. `InputObject` är standardnamnet för en parameter som tar ett objekt som som indata. Till exempel exemplet **stoppa Proc** cmdlet i den [StopProc självstudien](./stopproc-tutorial.md) definierar en `InputObject` parameter av typen Process som har stöd för indata från pipeline. Användaren kan få en uppsättning processen objekt, ändra dem för att välja exakt vilka objekt att stoppa och sedan skicka dem till den **stoppa Proc** cmdlet direkt.

### <a name="support-the-force-parameter-ad02"></a>Stöd för parametern Force (AD02)

Ibland kan måste en cmdlet skydda användaren från att utföra en begärd åtgärd. Ska ha stöd för sådana en cmdlet en `Force` parametern så att användaren att åsidosätta det skyddet om användaren har behörighet att utföra åtgärden.

Till exempel den [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item) cmdlet tar normalt inte bort en skrivskyddad fil. Denna cmdlet stöder dock en `Force` parametern så att en användare kan Framtvinga borttagning av en skrivskyddad fil. Om användaren har redan behörighet att ändra attributet skrivskyddad och användaren tar bort filen, användning av den `Force` parametern förenklar igen. Men om användaren inte har behörighet att ta bort filen, den `Force` parametern har ingen effekt.

### <a name="handle-credentials-through-windows-powershell-ad03"></a>Hantera autentiseringsuppgifter via Windows PowerShell (AD03)

En cmdlet bör definiera en `Credential` parameter för att representera autentiseringsuppgifter. Den här parametern måste vara av typen [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) och måste definieras med hjälp av en deklaration av autentiseringsuppgift attribut. Det här stödet meddelanderuta automatiskt för användarnamnet, lösenordet eller båda när en fullständig autentiseringsuppgift anges direkt. Mer information om attributet autentiseringsuppgifter finns i [Credential attributet deklarationen](./credential-attribute-declaration.md).

### <a name="support-encoding-parameters-ad04"></a>Stöd för kodning parametrar (AD04)

Om cmdlet: läser eller skriver ut text till eller från en binär form, till exempel skriva till eller läsa från en fil i ett filsystem har cmdlet: ha Encoding-parameter som anger hur texten är kodat i binär form.

### <a name="test-cmdlets-should-return-a-boolean-ad05"></a>Test-cmdlet: ar ska returnera ett booleskt värde (AD05)

Cmdlet: ar som utför testerna mot sina resurser ska returnera en [System.Boolean](/dotnet/api/System.Boolean) skriver till pipelinen så att de kan användas i villkorsuttryck.

## <a name="code-guidelines"></a>Riktlinjer för kod

Följande riktlinjer bör övervägas när du skriver kod för cmdlet. När du har hittat en riktlinje som gäller för din situation bör du titta på designriktlinjer för liknande riktlinjer.

### <a name="follow-cmdlet-class-naming-conventions-ac01"></a>Följ namnkonventioner för cmdlet: en klass (AC01)

Du gör dina cmdlets enklare genom att följande namngivningsregler, och du hjälpa användaren förstå exakt vad cmdletarna som gör. Den här metoden är särskilt viktigt för andra utvecklare som använder Windows PowerShell eftersom cmdlet: ar är offentliga typer.

#### <a name="define-a-cmdlet-in-the-correct-namespace"></a>Definiera en Cmdlet i rätt Namespace

Du vanligtvis definierar klassen för en cmdlet i en .NET Framework-namnområde som lägger till ”. -Kommandon ”till namnområdet som representerar produkten där cmdleten körs. Till exempel cmdletar som ingår i Windows PowerShell har definierats i den `Microsoft.PowerShell.Commands` namnområde.

#### <a name="name-the-cmdlet-class-to-match-the-cmdlet-name"></a>Namnge Cmdlet-klassen för att matcha Cmdlet-namn

När du namnger .NET Framework-klass som implementerar en cmdlet, ge klassen namnet ”*\<Verb >**\<substantiv >**\<kommando >*”, där du ersätter  *\<Verb >* och  *\<substantiv >* platshållare med verb och substantiv som används för cmdlet-namn. Till exempel den [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet implementeras av en klass med namnet `GetProcessCommand`.

### <a name="if-no-pipeline-input-override-the-beginprocessing-method-ac02"></a>Om inga indata från Pipeline åsidosätter metoden BeginProcessing (AC02)

Om din cmdlet inte tar emot indata från pipeline, bearbetning bör implementeras inom den [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metod. Användning av den här metoden gör att Windows PowerShell för att underhålla sortering mellan cmdlets. Den första cmdlet: i pipelinen returnerar alltid dess objekt innan de återstående cmdletarna i pipelinen prova att starta bearbetningen.

### <a name="to-handle-stop-requests-override-the-stopprocessing-method-ac03"></a>För att hantera åsidosätta stoppbegäran metoden StopProcessing (AC03)

Åsidosätta den [System.Management.Automation.Cmdlet.StopProcessing](/dotnet/api/System.Management.Automation.Cmdlet.StopProcessing) metod så att din cmdlet kan hantera stoppsignal. Vissa cmdlets ta lång tid att slutföra deras funktion och de gör det lång tid skickar mellan anrop till Windows PowerShell-körning, till exempel när cmdleten blockerar tråd i tidskrävande RPC-anrop. Detta inkluderar cmdletar som göra anrop till den [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metod till den [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metoden och annan feedback mekanismer som kan ta lång tid att slutföra. För dessa fall kan användaren behöva skicka en stoppsignal till dessa cmdletar.

### <a name="implement-the-idisposable-interface-ac04"></a>Implementera gränssnittet IDisposable (AC04)

Om din cmdlet har objekt som inte kasseras (skrivna till pipelinen) av den [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metoden cmdlet: kan kräva ytterligare objekt borttagning. Exempel: om cmdlet: öppnar en filreferens i dess [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metod och ser referensen öppna för användning av den [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metoden, den här referensen har stängs i slutet av bearbetning.

Windows PowerShell-runtime anropar alltid inte den [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metod. Till exempel den [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metoden kan inte anropas om cmdlet: en har avbrutits mitt via dess drift eller om avslutande fel uppstår i någon del av cmdlet: en. Därför .NET Framework-klass för en cmdlet som kräver att objektet rensningen ska implementera hela [System.IDisposable](/dotnet/api/System.IDisposable) gränssnittet mönstret, inklusive finaliserare, så att Windows PowerShell-runtime kan anropa både den [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) och [System.IDisposable.Dispose*](/dotnet/api/System.IDisposable.Dispose) metoder i slutet av bearbetning.

### <a name="use-serialization-friendly-parameter-types-ac05"></a>Använda serialisering-vänlig parametertyper (AC05)

Om du vill kan du köra cmdlet: på fjärrdatorer, använda typer som kan enkelt serialiseras på klientdatorn och sedan extraheras på serverdatorn. Följ typerna är serialisering-vänlig.

Primitiva typer:

- Byte, SByte, Decimal, Single, Double, Int16, Int32, Int64, Uint16, UInt32 och UInt64.

- Booleskt värde, Guid, Byte [], tidsintervall, DateTime, Uri och Version.

- Char, String, XmlDocument.

Inbyggda rehydratable typer:

- PSPrimitiveDictionary

- SwitchParameter

- PSListModifier

- PSCredential

- IPAddress, MailAddress

- CultureInfo

- X509Certificate2, X500DistinguishedName

- DirectorySecurity, FileSecurity, RegistrySecurity

Andra typer:

- SecureString

- Behållare (listor och ordlistor av ovanstående typ.)

### <a name="use-securestring-for-sensitive-data-ac06"></a>Använd SecureString för känsliga Data (AC06)

Vid hantering av känsliga data alltid använda den [System.Security.Securestring](/dotnet/api/System.Security.SecureString) datatyp. Detta kan omfatta pipeline-indata till parametrar, samt returnera känsliga data till pipelinen.

## <a name="see-also"></a>Se även

[Riktlinjer för nödvändiga utveckling](./required-development-guidelines.md)

[Vi rekommenderar utveckling riktlinjer](./strongly-encouraged-development-guidelines.md)

[Skriva en Windows PowerShell-Cmdlet](./writing-a-windows-powershell-cmdlet.md)
