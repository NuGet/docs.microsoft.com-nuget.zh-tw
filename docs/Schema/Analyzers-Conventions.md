---
title: "NuGet 的 .NET Compiler Platform 分析器格式 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a86e2080-93dd-4081-ac9b-d3bd66ba3799
description: ".NET 分析器的慣例，這些分析器會使用實作 API 或程式庫的 NuGet 套件來封裝與散發。"
keywords: "NuGet 分析器慣例, .NET 分析器, NuGet 和 .NET Compiler Platform, NuGet 和 Roslyn"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d26e879cc37047ce88aa7292c8c0b1e08e5fd89f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="fa6aa-104">分析器 NuGet 格式</span><span class="sxs-lookup"><span data-stu-id="fa6aa-104">Analyzer NuGet formats</span></span>

<span data-ttu-id="fa6aa-105">.NET Compiler Platform (也稱為"Roslyn") 可讓開發人員建立[分析器] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)，在撰寫的同時檢查程式碼的語法樹狀結構與語意。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-105">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="fa6aa-106">這提供開發人員一種方法，來建立網域特定分析工具，例如可協助引導使用特定 API 或程式庫的工具。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-106">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="fa6aa-107">您可以在 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub Wiki 找到更多資訊。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-107">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="fa6aa-108">另請參閱 MSDN Magazine 中的文件：[使用 Roslyn 為您的 API 撰寫即時程式碼分析器](https://msdn.microsoft.com/magazine/dn879356.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-108">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="fa6aa-109">分析器本身通常會封裝並散發作為實作討論中 API 或程式庫之 NuGet 套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-109">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="fa6aa-110">如果良好的範例，請參閱 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 套件，它具有下列內容：</span><span class="sxs-lookup"><span data-stu-id="fa6aa-110">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="fa6aa-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fa6aa-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="fa6aa-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fa6aa-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="fa6aa-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fa6aa-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="fa6aa-114">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="fa6aa-114">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="fa6aa-115">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fa6aa-115">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="fa6aa-116">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fa6aa-116">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="fa6aa-117">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fa6aa-117">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="fa6aa-118">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="fa6aa-118">tools\install.ps1</span></span>
- <span data-ttu-id="fa6aa-119">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="fa6aa-119">tools\uninstall.ps1</span></span>

<span data-ttu-id="fa6aa-120">如您所見，您將分析器 DLL 放入套件中的 `analyzers` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-120">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="fa6aa-121">Props 檔案 (為了分析器實作而包含以停用舊式 FxCop 規則) 放在 `build` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-121">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="fa6aa-122">使用 `packages.config` 支援專案的安裝和解除安裝指令碼放在 `tools`。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-122">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="fa6aa-123">另請注意，因為此套件沒有平台特有的需求，所以省略 `platform` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-123">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="fa6aa-124">分析器路徑格式</span><span class="sxs-lookup"><span data-stu-id="fa6aa-124">Analyzers path format</span></span>

<span data-ttu-id="fa6aa-125">`analyzers` 資料夾的使用類似於[目標架構](../create-packages/supporting-multiple-target-frameworks.md)所用的資料夾，只除了路徑中的規範描述開發主應用程式相依性，而不是建置時間。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-125">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="fa6aa-126">一般格式如下：</span><span class="sxs-lookup"><span data-stu-id="fa6aa-126">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="fa6aa-127">**framework_name**：「選擇性」的 .NET Framework API 介面區，此為包含的 DLL 執行所需。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-127">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="fa6aa-128">`dotnet` 是目前唯一有效的值，因為 Roslyn 是唯一可以執行分析器的主機。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-128">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="fa6aa-129">如果未指定目標，DLL 會假設套用至「所有」目標。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-129">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="fa6aa-130">**supported_language**：DLL 適用的語言，`cs`(C#) 和 `vb`(Visual Basic) 其中之一，以及 `fs`F#)。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-130">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="fa6aa-131">語言表示應該僅針對使用該語言的專案載入分析器。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-131">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="fa6aa-132">如果未指定語言，則 DLL 會假設要套用至「所有」支援分析器的語言。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-132">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="fa6aa-133">**analyzer_name**：指定分析器的 DLL。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-133">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="fa6aa-134">如果您需要 DLL 以外的其他檔案，它們必須透過目標檔或屬性檔包含進來。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-134">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="fa6aa-135">安裝和解除安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="fa6aa-135">Install and uninstall scripts</span></span>

<span data-ttu-id="fa6aa-136">如果使用者的專案使用 `packages.config`，則挑選分析器的 MSBuild 指令碼沒有作用，所以您應該以下述內容 `tools` 資料夾中的 `install.ps1` 和 `uninstall.ps1`。</span><span class="sxs-lookup"><span data-stu-id="fa6aa-136">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="fa6aa-137">**install.ps1 檔案內容**</span><span class="sxs-lookup"><span data-stu-id="fa6aa-137">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="fa6aa-138">**uninstall.ps1 檔案內容**</span><span class="sxs-lookup"><span data-stu-id="fa6aa-138">**uninstall.ps1 file contents**</span></span>

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
