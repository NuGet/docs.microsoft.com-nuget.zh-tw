---
title: 使用 Visual Studio 2015 建立 .NET Standard 和 .NET Framework NuGet 套件 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: 使用 NuGet 3.x 和 Visual Studio 2015 建立 .NET Standard 和 NuGet 套件的逐步解說。
keywords: 建立套件, .NET Standard 套件, .NET Framework 套件
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="b6042-104">使用 Visual Studio 2015 建立 NET Standard 和 NET Framework 套件</span><span class="sxs-lookup"><span data-stu-id="b6042-104">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="b6042-105">**注意：**建議使用 Visual Studio 2017 來開發 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b6042-105">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="b6042-106">可以使用 Visual Studio 2015，但 .NET Core 工具僅提供為「預覽」階段。</span><span class="sxs-lookup"><span data-stu-id="b6042-106">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="b6042-107">如需使用 NuGet 4.x+ 和 Visual Studio 2017 的資訊，請參閱[使用 Visual Studio 2017 建立和發佈套件](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="b6042-107">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="b6042-108">[.NET Standard 程式庫](/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。</span><span class="sxs-lookup"><span data-stu-id="b6042-108">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="b6042-109">.NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。</span><span class="sxs-lookup"><span data-stu-id="b6042-109">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="b6042-110">其可讓開發人員產生可跨所有 .NET 執行階段使用的程式碼，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。</span><span class="sxs-lookup"><span data-stu-id="b6042-110">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="b6042-111">本指南引導您建立以 .NET Standard Library 1.4 為目標的 NuGet 套件，或是以 .NET Framework 4.6 為目標的套件。</span><span class="sxs-lookup"><span data-stu-id="b6042-111">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="b6042-112">.NET Standard 1.4 程式庫可用於 .NET Framework 4.6.1、Universal Windows Platform 10、.NET Core 和 Mono/Xamarin。</span><span class="sxs-lookup"><span data-stu-id="b6042-112">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="b6042-113">如需詳細資訊，請參閱 [.NET Standard 對應表](/dotnet/standard/net-standard#net-implementation-support) (.NET 文件)。</span><span class="sxs-lookup"><span data-stu-id="b6042-113">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="b6042-114">您可以依需求選擇其他版本的 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="b6042-114">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6042-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6042-115">Prerequisites</span></span>

1. <span data-ttu-id="b6042-116">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="b6042-116">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="b6042-117">(僅限 .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="b6042-117">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="b6042-118">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="b6042-118">NuGet CLI.</span></span> <span data-ttu-id="b6042-119">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="b6042-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="b6042-120">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="b6042-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="b6042-121">nuget.exe 本身是 CLI 工具，不是安裝程式，所以請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="b6042-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="b6042-122">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="b6042-122">Create the class library project</span></span>

1. <span data-ttu-id="b6042-123">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點，選取 [類別庫 (可攜式)]將名稱變更為 AppLogger，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b6042-123">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![建立新的類別庫專案](media/NetStandard-NewProject.png)

1. <span data-ttu-id="b6042-125">在顯示的 [加入可攜式類別庫] 對話方塊中，選取 `.NET Framework 4.6` 和 `ASP.NET Core 1.0` 的選項。</span><span class="sxs-lookup"><span data-stu-id="b6042-125">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="b6042-126">(如果目標是 .NET Framework，您可以選取任何適當的選項。)</span><span class="sxs-lookup"><span data-stu-id="b6042-126">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="b6042-127">如果目標是 .NET Standard，在 [方案總管] 中，以滑鼠右鍵按一下 [`AppLogger (Portable)`]，選取 [屬性]，選取 [程式庫] 索引標籤，然後在 [目標] 區段中選取 [目標 .NET 平台標準]。</span><span class="sxs-lookup"><span data-stu-id="b6042-127">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="b6042-128">此動作會提示您確認，之後您就可以從下拉式清單中選取 `.NET Standard 1.4` (或其他可用版本)：</span><span class="sxs-lookup"><span data-stu-id="b6042-128">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![將目標設定為 .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="b6042-130">按一下 [組建] 索引標籤，將 [組態] 變更為 `Release`，並核取 [XML 文件檔] 方塊。</span><span class="sxs-lookup"><span data-stu-id="b6042-130">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="b6042-131">將程式碼新增至元件，例如：</span><span class="sxs-lookup"><span data-stu-id="b6042-131">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="b6042-132">將組態設定為發行、建置專案，並確認 DLL 和 XML 檔案已產生在 `bin\Release` 資料夾內。</span><span class="sxs-lookup"><span data-stu-id="b6042-132">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="b6042-133">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="b6042-133">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="b6042-134">開啟命令提示字元，巡覽至包含 `AppLogger.csproj` 資料夾的資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `AppLogger.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="b6042-134">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="b6042-135">在編輯器中開啟 `AppLogger.nuspec`，更新它使符合下列內容，以適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="b6042-135">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="b6042-136">尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="b6042-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="b6042-137">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b6042-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="b6042-138">將參考組件新增至 `.nuspec` 檔案，也就是程式庫的 DLL 和 IntelliSense XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="b6042-138">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="b6042-139">如果目標是 .NET Standard，項目會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="b6042-139">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="b6042-140">如果目標是 .NET Framework，項目會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="b6042-140">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="b6042-141">以滑鼠右鍵按一下解決方案，然後選取 [組建方案] 產生套件的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="b6042-141">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="b6042-142">宣告相依性</span><span class="sxs-lookup"><span data-stu-id="b6042-142">Declaring dependencies</span></span>

<span data-ttu-id="b6042-143">如有其他 NuGet 套件的任何相依性，請使用 `<group>` 項目在資訊清單的 `<dependencies>` 項目中加以列出。</span><span class="sxs-lookup"><span data-stu-id="b6042-143">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="b6042-144">例如，若要宣告對 NewtonSoft.Json 8.0.3 或更新版本的相依性，請新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="b6042-144">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="b6042-145">*version* 屬性的語法在此表示接受該版本 8.0.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b6042-145">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="b6042-146">若要指定不同的版本範圍，請參閱[套件版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="b6042-146">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="b6042-147">新增讀我檔案</span><span class="sxs-lookup"><span data-stu-id="b6042-147">Adding a readme</span></span>

<span data-ttu-id="b6042-148">請建立您的 `readme.txt` 檔案，將其置於專案根資料夾中，並在 `.nuspec` 檔案中加以參考：</span><span class="sxs-lookup"><span data-stu-id="b6042-148">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="b6042-149">當套件安裝至專案中時，Visual Studio 會顯示 `readme.txt`。</span><span class="sxs-lookup"><span data-stu-id="b6042-149">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="b6042-150">安裝至 .NET Core 專案時，或對於已安裝為相依性的套件，檔案則不會顯示。</span><span class="sxs-lookup"><span data-stu-id="b6042-150">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="b6042-151">封裝元件</span><span class="sxs-lookup"><span data-stu-id="b6042-151">Package the component</span></span>

<span data-ttu-id="b6042-152">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="b6042-152">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="b6042-153">這會產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="b6042-153">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="b6042-154">在 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) \(英文\) 之類的工具中開啟此檔案，並展開所有節點，您會看到以下內容 (顯示的是 .NET Standard)：</span><span class="sxs-lookup"><span data-stu-id="b6042-154">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![顯示 AppLogger 套件的 NuGet 套件總管](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="b6042-156">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="b6042-156">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="b6042-157">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="b6042-157">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="b6042-158">若要讓其他開發人員使用您的套件，請遵循[發佈套件](../create-packages/publish-a-package.md)上的指示。</span><span class="sxs-lookup"><span data-stu-id="b6042-158">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="b6042-159">請注意，`pack` 在 Mac OS X 上需要 Mono 4.4.2，而且無法在 Linux 系統上運作。</span><span class="sxs-lookup"><span data-stu-id="b6042-159">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="b6042-160">在 Mac 上，您也必須將 `.nuspec` 檔案中的 Windows 路徑名稱轉換成 Unix 模式路徑。</span><span class="sxs-lookup"><span data-stu-id="b6042-160">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="b6042-161">相關主題</span><span class="sxs-lookup"><span data-stu-id="b6042-161">Related topics</span></span>

- [<span data-ttu-id="b6042-162">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="b6042-162">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="b6042-163">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="b6042-163">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b6042-164">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="b6042-164">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="b6042-165">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="b6042-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b6042-166">符號套件</span><span class="sxs-lookup"><span data-stu-id="b6042-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="b6042-167">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="b6042-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b6042-168">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="b6042-168">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b6042-169">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="b6042-169">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
