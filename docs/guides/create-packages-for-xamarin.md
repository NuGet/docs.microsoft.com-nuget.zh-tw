---
title: 建立適用于 Xamarin （適用于 iOS、Android 和 Windows）的 NuGet 套件（含 Visual Studio 2017 或2019）
description: 有關如何為 Xamarin 建立 NuGet 套件的端對端逐步解說，而這些套件在 iOS、Android 和 Windows 上使用原生 API。
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230898"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="85f8f-103">建立具有 Visual Studio 2017 或2019之 Xamarin 的套件</span><span class="sxs-lookup"><span data-stu-id="85f8f-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="85f8f-104">適用於 Xamarin 的套件包含使用 iOS、Android 和 Windows (視執行階段作業系統而定) 上原生 API 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="85f8f-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="85f8f-105">雖然這十分簡單，但最好是讓開發人員使用 PCL 中的套件，或透過通用 API 介面區的 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="85f8f-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="85f8f-106">在本逐步解說中，您會使用 Visual Studio 2017 或2019來建立可在 iOS、Android 和 Windows 上的行動專案中使用的跨平臺 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="85f8f-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="85f8f-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="85f8f-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="85f8f-108">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="85f8f-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="85f8f-109">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="85f8f-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="85f8f-110">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="85f8f-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="85f8f-111">封裝元件</span><span class="sxs-lookup"><span data-stu-id="85f8f-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="85f8f-112">相關主題</span><span class="sxs-lookup"><span data-stu-id="85f8f-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="85f8f-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="85f8f-113">Prerequisites</span></span>

1. <span data-ttu-id="85f8f-114">使用通用 Windows 平臺（UWP）和 Xamarin Visual Studio 2017 或2019。</span><span class="sxs-lookup"><span data-stu-id="85f8f-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="85f8f-115">從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="85f8f-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="85f8f-116">若要包含 UWP 和 Xamarin 工具，請選取 [自訂安裝] 並檢查適當的選項。</span><span class="sxs-lookup"><span data-stu-id="85f8f-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="85f8f-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="85f8f-117">NuGet CLI.</span></span> <span data-ttu-id="85f8f-118">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="85f8f-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="85f8f-119">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="85f8f-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="85f8f-120">nuget.exe 本身是 CLI 工具，不是安裝程式，因此請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="85f8f-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="85f8f-121">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="85f8f-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="85f8f-122">下載並執行適用于 Visual Studio 的[跨平臺 .NET Standard 外掛程式範本延伸模組](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。</span><span class="sxs-lookup"><span data-stu-id="85f8f-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="85f8f-123">這些範本可讓您輕鬆建立此逐步解說的必要專案結構。</span><span class="sxs-lookup"><span data-stu-id="85f8f-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="85f8f-124">在 Visual Studio 2017，檔案 **> 新增 > 專案**中，搜尋 `Plugin`，選取 [**跨平臺 .NET Standard 程式庫外掛程式**] 範本，將名稱變更為 LoggingLibrary，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="85f8f-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![VS 2017 中的新空白應用程式（Xamarin. 表單可攜）專案](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="85f8f-126">在 Visual Studio 2019，檔案 **> 新增 > 專案**中，搜尋 `Plugin`，選取 [**跨平臺 .NET Standard 程式庫外掛程式**] 範本，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="85f8f-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![VS 2019 中的新空白應用程式（Xamarin. 表單可攜）專案](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="85f8f-128">將名稱變更為 LoggingLibrary，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="85f8f-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![VS 2019 中的新空白應用程式（Xamarin 形式可攜）設定](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="85f8f-130">產生的方案包含兩個共用的專案，以及各種不同的平臺特定專案：</span><span class="sxs-lookup"><span data-stu-id="85f8f-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="85f8f-131">`ILoggingLibrary` 專案（包含在 `ILoggingLibrary.shared.cs` 檔案中）會定義元件的公用介面（API 表面區域）。</span><span class="sxs-lookup"><span data-stu-id="85f8f-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="85f8f-132">這是您在其中定義程式庫介面的位置。</span><span class="sxs-lookup"><span data-stu-id="85f8f-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="85f8f-133">另一個共用專案包含 `CrossLoggingLibrary.shared.cs` 中的程式碼，可在執行時間找出抽象介面的平臺特定執行。</span><span class="sxs-lookup"><span data-stu-id="85f8f-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="85f8f-134">您通常不需要修改這個檔案。</span><span class="sxs-lookup"><span data-stu-id="85f8f-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="85f8f-135">平臺特定專案（例如 `LoggingLibrary.android.cs`）各自包含介面的原生執行，其各自的 `LoggingLibraryImplementation.cs` （VS 2017）或 `LoggingLibrary.<PLATFORM>.cs` （VS 2019）檔案。</span><span class="sxs-lookup"><span data-stu-id="85f8f-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="85f8f-136">這是您建置程式庫程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="85f8f-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="85f8f-137">根據預設，`ILoggingLibrary` 專案的 ILoggingLibrary.shared.cs 檔包含介面定義，但沒有方法。</span><span class="sxs-lookup"><span data-stu-id="85f8f-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="85f8f-138">基於本逐步解說的目的，新增 `Log` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85f8f-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="85f8f-139">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="85f8f-139">Write your platform-specific code</span></span>

<span data-ttu-id="85f8f-140">若要實作 `ILoggingLibrary` 介面的平台特定實作和其方法，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="85f8f-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="85f8f-141">開啟每個平臺專案的 `LoggingLibraryImplementation.cs` （VS 2017）或 `LoggingLibrary.<PLATFORM>.cs` （VS 2019）檔案，並新增必要的程式碼。</span><span class="sxs-lookup"><span data-stu-id="85f8f-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="85f8f-142">例如（使用 `Android` 平臺專案）：</span><span class="sxs-lookup"><span data-stu-id="85f8f-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="85f8f-143">針對每個您想要支援的平台，重複專案中的這個實作。</span><span class="sxs-lookup"><span data-stu-id="85f8f-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="85f8f-144">以滑鼠右鍵按一下方案，然後選取 [建置方案] 檢查您的工作，並產生之後將封裝的成品。</span><span class="sxs-lookup"><span data-stu-id="85f8f-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="85f8f-145">如果您收到有關遺漏參考的錯誤，請以滑鼠右鍵按一下方案，然後選取 [還原 NuGet 套件] 以安裝相依性並重建。</span><span class="sxs-lookup"><span data-stu-id="85f8f-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="85f8f-146">如果您使用 Visual Studio 2019，在選取 [**還原 NuGet 套件**] 並嘗試重建之前，您必須將 `MSBuild.Sdk.Extras` 的版本變更為 `LoggingLibrary.csproj`中的 `2.0.54`。</span><span class="sxs-lookup"><span data-stu-id="85f8f-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="85f8f-147">只有先以滑鼠右鍵按一下專案（在方案底下），然後選取 [`Unload Project`]，然後在已卸載的專案上按一下滑鼠右鍵，然後選取 [`Edit LoggingLibrary.csproj`]，才能存取這個檔案。</span><span class="sxs-lookup"><span data-stu-id="85f8f-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="85f8f-148">若要針對 iOS 建置，您需要連線至 Visual Studio 的網路 Mac，如　[Xamarin.iOS for Visual Studio 簡介](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)上所述。</span><span class="sxs-lookup"><span data-stu-id="85f8f-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="85f8f-149">如果您沒有可用的 Mac，請在組態管理員中清除 iOS 專案 (上述步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="85f8f-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="85f8f-150">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="85f8f-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="85f8f-151">開啟命令提示字元，並巡覽至 `LoggingLibrary` 資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `Package.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="85f8f-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="85f8f-152">將這個檔案重新命名為 `LoggingLibrary.nuspec`，並在編輯器中予以開啟。</span><span class="sxs-lookup"><span data-stu-id="85f8f-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="85f8f-153">更新檔案使其符合下列內容，並使用適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="85f8f-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="85f8f-154">尤其是在整個 nuget.org 中，`<id>` 值必須為唯一 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="85f8f-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="85f8f-155">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="85f8f-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="85f8f-156">您的套件版本可以加上 `-alpha`、`-beta` 或 `-rc` 後置詞，以將套件標示為發行前版本，如需發行前版本的詳細資訊，請檢查[發行前版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="85f8f-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="85f8f-157">新增參考組件</span><span class="sxs-lookup"><span data-stu-id="85f8f-157">Add reference assemblies</span></span>

<span data-ttu-id="85f8f-158">若要包含平台特定參考組件，請針對您的支援平台適當地將下列新增至 `<files>` 的 `LoggingLibrary.nuspec` 項目：</span><span class="sxs-lookup"><span data-stu-id="85f8f-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="85f8f-159">若要縮短 DLL 和 XML 檔案的名稱，請以滑鼠右鍵按一下任何指定的專案，並選取 [程式庫] 索引標籤，然後變更組件名稱。</span><span class="sxs-lookup"><span data-stu-id="85f8f-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="85f8f-160">新增相依性</span><span class="sxs-lookup"><span data-stu-id="85f8f-160">Add dependencies</span></span>

<span data-ttu-id="85f8f-161">如果您有原生實作的特定相依性，請搭配使用 `<dependencies>` 項目與 `<group>` 項目來指定它們，例如：</span><span class="sxs-lookup"><span data-stu-id="85f8f-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="85f8f-162">例如，下列會將 iTextSharp 設定為 UAP 目標的相依性：</span><span class="sxs-lookup"><span data-stu-id="85f8f-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="85f8f-163">最終 .nuspec</span><span class="sxs-lookup"><span data-stu-id="85f8f-163">Final .nuspec</span></span>

<span data-ttu-id="85f8f-164">最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：</span><span class="sxs-lookup"><span data-stu-id="85f8f-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="85f8f-165">封裝元件</span><span class="sxs-lookup"><span data-stu-id="85f8f-165">Package the component</span></span>

<span data-ttu-id="85f8f-166">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="85f8f-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="85f8f-167">這將產生 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="85f8f-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="85f8f-168">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="85f8f-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 LoggingLibrary 套件的 NuGet 套件總管](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="85f8f-170">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="85f8f-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="85f8f-171">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="85f8f-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="85f8f-172">若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="85f8f-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="85f8f-173">相關主題</span><span class="sxs-lookup"><span data-stu-id="85f8f-173">Related topics</span></span>

- [<span data-ttu-id="85f8f-174">Nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="85f8f-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="85f8f-175">符號套件</span><span class="sxs-lookup"><span data-stu-id="85f8f-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="85f8f-176">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="85f8f-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="85f8f-177">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="85f8f-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="85f8f-178">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="85f8f-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="85f8f-179">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="85f8f-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
