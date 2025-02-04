---
ms.date: 06/05/2017
keywords: PowerShell cmdlet
title: ISEFile-objektet
ms.openlocfilehash: ebb5a35f6ea9d93eab633b9f4e6c84e4fddd6ae8
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/12/2019
ms.locfileid: "67028956"
---
# <a name="the-isefile-object"></a>ISEFile-objektet

En **ISEFile** -objektet representerar en fil i Windows PowerShell® Integrated Scripting Environment (ISE). Det är en instans av klassen Microsoft.PowerShell.Host.ISE.ISEFile. Det här avsnittet visas dess medlem metoder och egenskaper. Den **$psISE.CurrentFile** filerna i samlingen filer i en PowerShell-flik är alla instanser av klassen Microsoft.PowerShell.Host.ISE.ISEFile.

## <a name="methods"></a>Metoder

### <a name="save-saveencoding-"></a>Spara\( \[saveEncoding\] \)

Stöds i Windows PowerShell ISE 2.0 och senare.

Sparar filen till disk.

**\[saveEncoding\]**  – valfritt [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) ett valfritt tecken kodning parametern som ska användas för den sparade filen. Standardvärdet är **UTF8**.

### <a name="exceptions"></a>Undantag

- **System.IO.IOException**: Det gick inte att spara filen.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>Spara\(filnamnet \[saveEncoding\]\)

Stöds i Windows PowerShell ISE 2.0 och senare.

Sparar filen med det angivna filnamnet och kodning.

**filename** -String-namn som används för att spara filen.

**\[saveEncoding\]**  – valfritt [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) ett valfritt tecken kodning parametern som ska användas för den sparade filen. Standardvärdet är **UTF8**.

### <a name="exceptions"></a>Undantag

- **System.ArgumentNullException**: Den **filename** parametern är null.
- **System.ArgumentException**: Den **filename** parametern är tom.
- **System.IO.IOException**: Det gick inte att spara filen.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Egenskaper

### <a name="displayname"></a>Visningsnamn

Stöds i Windows PowerShell ISE 2.0 och senare.

Den skrivskyddade egenskapen som hämtar den sträng som innehåller visningsnamnet för den här filen. Namnet visas på den **filen** fliken högst upp i redigeraren. Förekomsten av en asterisk \( \* \) anger att filen har ändringar som inte har sparats i slutet av namnet.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Redigeringsprogram

Stöds i Windows PowerShell ISE 2.0 och senare.

Skrivskyddad egenskap som hämtar den [editor-objekt](The-ISEEditor-Object.md) som används för den angivna filen.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Encoding

Stöds i Windows PowerShell ISE 2.0 och senare.

Den skrivskyddade egenskapen som hämtar den ursprungliga Filkodning. Det här är en **System.Text.Encoding** objekt.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

Stöds i Windows PowerShell ISE 2.0 och senare.

Den skrivskyddade egenskapen som hämtar den sträng som anger den fullständiga sökvägen till den öppna filen.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

Stöds i Windows PowerShell ISE 2.0 och senare.

Den skrivskyddade boolesk egenskap som returnerar **$true** om filen har sparats sedan den senast ändrades.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

Stöds i Windows PowerShell ISE 2.0 och senare.

Skrivskyddad egenskap som returnerar **$true** om filen har aldrig fått en rubrik.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Se även

- [The ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [Syftet med den Windows PowerShell ISE-Skriptobjektmodellen](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarki för ISE-objektmodellen](The-ISE-Object-Model-Hierarchy.md)
