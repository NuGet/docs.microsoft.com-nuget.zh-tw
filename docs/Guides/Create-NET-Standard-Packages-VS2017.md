---
title: "使用 Visual Studio 2017 建立 .NET Standard 2.0 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "使用 NuGet 4.x 和 Visual Studio 2017 建立 .NET Standard 2.0 NuGet 套件的端對端逐步解說。"
keywords: "建立套件, .NET Standard 套件, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="d441d-104">使用 Visual Studio 2017 建立 .NET Standard 2.0 套件</span><span class="sxs-lookup"><span data-stu-id="d441d-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="d441d-105">*適用於 NuGet 4.x+ 和 Visual Studio 2017 Update 3 提供的 MSBuild 15.3+。對於舊版的 Visual Studio 2017，這些指示適用於 .NET Standard 1.4 到 1.6，方法是變更 \<TargetFramework\> 屬性。另請參閱[使用 Visual Studio 2015 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2015.md)，以便使用 NuGet 3.x+。*</span><span class="sxs-lookup"><span data-stu-id="d441d-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="d441d-106">[.NET Standard 程式庫](https://docs.microsoft.com/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。</span><span class="sxs-lookup"><span data-stu-id="d441d-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="d441d-107">.NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。</span><span class="sxs-lookup"><span data-stu-id="d441d-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="d441d-108">它可讓開發人員產生可跨所有 .NET 執行階段使用的 PCL，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。</span><span class="sxs-lookup"><span data-stu-id="d441d-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="d441d-109">本指南將引導您使用 Visual Studio 2017 Update 3 和 NuGet 4.0，建立以 .NET Standard 程式庫 2.0 為目標的 nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="d441d-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="d441d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d441d-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="d441d-111">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="d441d-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="d441d-112">編輯 .csproj 檔案中的中繼資料</span><span class="sxs-lookup"><span data-stu-id="d441d-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="d441d-113">封裝元件</span><span class="sxs-lookup"><span data-stu-id="d441d-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="d441d-114">相關主題</span><span class="sxs-lookup"><span data-stu-id="d441d-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="d441d-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="d441d-115">Pre-requisites</span></span>

<span data-ttu-id="d441d-116">本逐步解說需要 Visual Studio 2017 Update 3 與 **.NET Core 跨平台開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="d441d-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="d441d-117">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，或使用 Professional Edition 和 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="d441d-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="d441d-118">需要的工作負載會如下所示出現在 Visual Studio 安裝程式：</span><span class="sxs-lookup"><span data-stu-id="d441d-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Visual Studio 安裝程式中的 .NET Core 跨平台開發工作負載](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="d441d-120">建立 .NET Standard 類別庫專案</span><span class="sxs-lookup"><span data-stu-id="d441d-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="d441d-121">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [.NET Standard] 節點、選取 [類別庫 (Net Standard)]、將名稱變更為 AppLogger，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d441d-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![建立新的類別庫專案](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="d441d-123">將組建組態變更為 [發行]。</span><span class="sxs-lookup"><span data-stu-id="d441d-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="d441d-124">以滑鼠右鍵按一下方案總管中的 `AppLogger` 專案、依序選取 [屬性]、[建置] 索引標籤，核取 [XML 文件檔] 的方塊，並將檔案名稱設為 `AppLogger.xml`。</span><span class="sxs-lookup"><span data-stu-id="d441d-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="d441d-125">然後儲存專案。</span><span class="sxs-lookup"><span data-stu-id="d441d-125">Then save the project.</span></span>

1. <span data-ttu-id="d441d-126">將您的程式碼新增至元件，如下所示 (它很清楚只輸出訊息至主控台)：</span><span class="sxs-lookup"><span data-stu-id="d441d-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="d441d-127">(使用發行組態) 建置專案，並確認 DLL 和 XML 檔案已產生在 `bin\Release\netstandard2.0` 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="d441d-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="d441d-128">編輯 .csproj 檔案中的中繼資料</span><span class="sxs-lookup"><span data-stu-id="d441d-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="d441d-129">使用 NuGet 4.0 和 .NET Core 專案，套件中繼資料會直接包含在 `.csproj` 檔，而不是外部檔案，例如 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="d441d-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="d441d-130">該中繼資料的完整描述位於 [NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="d441d-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="d441d-131">以滑鼠右鍵按一下方案總管中的專案、選取 [編輯 AppLogger.csproj]，然後編輯第一個屬性群組以包含套件資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d441d-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="d441d-132">儲存專案，然後以滑鼠右鍵按一下方案，並選取 [建置方案]，再次產生套件的所有檔案 (這次是使用正確的中繼資料)。</span><span class="sxs-lookup"><span data-stu-id="d441d-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="d441d-133">封裝元件</span><span class="sxs-lookup"><span data-stu-id="d441d-133">Package the component</span></span>

<span data-ttu-id="d441d-134">NuGet 4.0 支援在當專案包含所需的套件中繼資料時使用 MSBuild 15.1+ 版 (包括 Visual Studio 2017 Update 3 提供的 MSBuild 15.3) 的組件目標，如上一節所新增。</span><span class="sxs-lookup"><span data-stu-id="d441d-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="d441d-135">若要以這種方式叫用 MSBuild，只要在命令列上，在與 `.csproj` 檔案的相同資料夾中指定組件目標：</span><span class="sxs-lookup"><span data-stu-id="d441d-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="d441d-136">如需 `msbuild /t:pack` 的其他選項，例如包含內容檔案、符號和原始程式碼，請參閱 [NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="d441d-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="d441d-137">在任何情況下，上述命令依預設會在它建立該組態時，在 `bin\Release` 資料夾中產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="d441d-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="d441d-138">如果您省略 `/p` 參數，預設組態將為 `Debug`。</span><span class="sxs-lookup"><span data-stu-id="d441d-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="d441d-139">在例如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="d441d-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![顯示 AppLogger 套件的 NuGet 套件總管](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d441d-141">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="d441d-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d441d-142">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="d441d-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d441d-143">若要讓其他開發人員使用您的套件，請遵循[發行套件](../create-packages/publish-a-package.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="d441d-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d441d-144">相關主題</span><span class="sxs-lookup"><span data-stu-id="d441d-144">Related topics</span></span>

- <span data-ttu-id="d441d-145">[專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)描述直接在專案檔中描述您套件的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d441d-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="d441d-146">[NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md)描述使用 `msbuild /t:pack` 建立套件的所有選項。</span><span class="sxs-lookup"><span data-stu-id="d441d-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="d441d-147">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="d441d-147">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="d441d-148">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="d441d-148">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
