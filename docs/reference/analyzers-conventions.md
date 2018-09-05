---
title: .NET 編譯器平台 nuget 的分析器格式
description: .NET 分析器的慣例，這些分析器會使用實作 API 或程式庫的 NuGet 套件來封裝與散發。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a5ccbba5fbc189eb59acfdeb86a4a03dcf907a9a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547627"
---
# <a name="analyzer-nuget-formats"></a>分析器 NuGet 格式

.NET 編譯器平台 (也稱為"Roslyn") 可讓開發人員建立[分析器](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)，檢查語法樹狀結構和語意的程式碼正在寫入時。 這提供開發人員一種方法，來建立網域特定分析工具，例如可協助引導使用特定 API 或程式庫的工具。 您可以在 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub Wiki 找到更多資訊。 另請參閱 MSDN Magazine 中的文件：[使用 Roslyn 為您的 API 撰寫即時程式碼分析器](https://msdn.microsoft.com/magazine/dn879356.aspx)。

分析器本身通常會封裝並散發作為實作討論中 API 或程式庫之 NuGet 套件的一部分。

如果良好的範例，請參閱 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 套件，它具有下列內容：

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

如您所見，您將分析器 DLL 放入套件中的 `analyzers` 資料夾。

Props 檔案 (為了分析器實作而包含以停用舊式 FxCop 規則) 放在 `build` 資料夾。

使用 `packages.config` 支援專案的安裝和解除安裝指令碼放在 `tools`。

另請注意，因為此套件沒有平台特有的需求，所以省略 `platform` 資料夾。


## <a name="analyzers-path-format"></a>分析器路徑格式

`analyzers` 資料夾的使用類似於[目標架構](../create-packages/supporting-multiple-target-frameworks.md)所用的資料夾，只除了路徑中的規範描述開發主應用程式相依性，而不是建置時間。 一般格式如下：

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**：「選擇性」的 .NET Framework API 介面區，此為包含的 DLL 執行所需。 `dotnet` 是目前唯一有效的值，因為 Roslyn 是唯一可以執行分析器的主機。 如果未指定目標，DLL 會假設套用至「所有」目標。
- **supported_language**：DLL 適用的語言，`cs`(C#) 和 `vb`(Visual Basic) 其中之一，以及 `fs`F#)。 語言表示應該僅針對使用該語言的專案載入分析器。 如果未指定語言，則 DLL 會假設要套用至「所有」支援分析器的語言。
- **analyzer_name**：指定分析器的 DLL。 如果您需要 DLL 以外的其他檔案，它們必須透過目標檔或屬性檔包含進來。


## <a name="install-and-uninstall-scripts"></a>安裝和解除安裝指令碼

如果使用者的專案使用 `packages.config`，則挑選分析器的 MSBuild 指令碼沒有作用，所以您應該以下述內容 `tools` 資料夾中的 `install.ps1` 和 `uninstall.ps1`。

**install.ps1 檔案內容**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


**uninstall.ps1 檔案內容**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
