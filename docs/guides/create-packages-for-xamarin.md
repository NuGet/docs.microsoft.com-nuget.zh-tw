---
title: 使用 Visual Studio 2017 或 2019 為 Xamarin(適用於 iOS、Android 和 Windows)建立 NuGet 套件
description: 有關如何為 Xamarin 建立 NuGet 套件的端對端逐步解說，而這些套件在 iOS、Android 和 Windows 上使用原生 API。
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230898"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="9d1dc-103">以 Visual Studio 2017 或 2019 為 Xamarin 建立套件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="9d1dc-104">適用於 Xamarin 的套件包含使用 iOS、Android 和 Windows (視執行階段作業系統而定) 上原生 API 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="9d1dc-105">雖然這十分簡單，但最好是讓開發人員使用 PCL 中的套件，或透過通用 API 介面區的 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="9d1dc-106">在本演練中,您可以使用 Visual Studio 2017 或 2019 創建可在 iOS、Android 和 Windows 上的行動專案中使用的跨平臺 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="9d1dc-107">先決條件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="9d1dc-108">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="9d1dc-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="9d1dc-109">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="9d1dc-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="9d1dc-110">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="9d1dc-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="9d1dc-111">封裝元件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="9d1dc-112">相關主題</span><span class="sxs-lookup"><span data-stu-id="9d1dc-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="9d1dc-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d1dc-113">Prerequisites</span></span>

1. <span data-ttu-id="9d1dc-114">Visual Studio 2017 或 2019 與通用 Windows 平臺 (UWP) 和 Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9d1dc-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="9d1dc-115">從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="9d1dc-116">若要包含 UWP 和 Xamarin 工具，請選取 [自訂安裝] 並檢查適當的選項。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="9d1dc-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-117">NuGet CLI.</span></span> <span data-ttu-id="9d1dc-118">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9d1dc-119">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="9d1dc-120">nuget.exe 本身是 CLI 工具，不是安裝程式，因此請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="9d1dc-121">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="9d1dc-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="9d1dc-122">下載並執行 Visual Studio[的跨平臺 .NET 標準外掛程式樣本延伸](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="9d1dc-123">這些範本可讓您輕鬆建立此逐步解說的必要專案結構。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="9d1dc-124">在 Visual Studio 2017 中,**檔>"新>專案**"中,搜索`Plugin`,選擇**跨平臺 .NET 標準庫外掛程式**樣本,將名稱更改為日誌記錄庫,然後單擊" 確定"</span><span class="sxs-lookup"><span data-stu-id="9d1dc-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![VS 2017 中的新空白應用程式 (Xamarin.Forms 可攜式) 專案](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="9d1dc-126">在 Visual Studio 2019**中,檔>新的>專案**,搜索`Plugin`,選擇**跨平臺 .NET 標準庫外掛程式**樣本,然後單擊"下一步」。。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![VS 2019 年的新空白應用程式 (Xamarin.Forms 可攜式) 專案](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="9d1dc-128">將名稱更改為日誌記錄庫,然後單擊"創建"。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![VS 2019 中的新空白應用程式 (Xamarin.Forms 可移植)設定](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="9d1dc-130">產生的解決方案包含兩個共享專案以及各種特定於平臺的專案:</span><span class="sxs-lookup"><span data-stu-id="9d1dc-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="9d1dc-131">包含在`ILoggingLibrary``ILoggingLibrary.shared.cs`檔案中的項目定義元件的公共介面(API 表面積)。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="9d1dc-132">這是您在其中定義程式庫介面的位置。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="9d1dc-133">另一個共用專案包含代碼`CrossLoggingLibrary.shared.cs`,這些代碼將在運行時找到抽象介面特定於平台的實現。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="9d1dc-134">您通常不需要修改這個檔案。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="9d1dc-135">特定於平臺的專案(如`LoggingLibrary.android.cs`),每個專案都在其各自`LoggingLibraryImplementation.cs`的 (VS 2017) 或`LoggingLibrary.<PLATFORM>.cs`(VS 2019) 檔中包含介面的本機實現。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="9d1dc-136">這是您建置程式庫程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="9d1dc-137">默認情況下,`ILoggingLibrary`專案的ILoggingLibrary.shared.cs檔包含介面定義,但沒有方法。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="9d1dc-138">基於本逐步解說的目的，新增 `Log` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="9d1dc-139">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="9d1dc-139">Write your platform-specific code</span></span>

<span data-ttu-id="9d1dc-140">若要實作 `ILoggingLibrary` 介面的平台特定實作和其方法，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="9d1dc-141">打開每個`LoggingLibraryImplementation.cs`平台專案的 (VS 2017) 或`LoggingLibrary.<PLATFORM>.cs`(VS 2019) 檔並添加必要的代碼。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="9d1dc-142">例如(使用`Android`平台專案):</span><span class="sxs-lookup"><span data-stu-id="9d1dc-142">For example (using the `Android` platform project):</span></span>

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

1. <span data-ttu-id="9d1dc-143">針對每個您想要支援的平台，重複專案中的這個實作。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="9d1dc-144">以滑鼠右鍵按一下方案，然後選取 [建置方案]\*\*\*\* 檢查您的工作，並產生之後將封裝的成品。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="9d1dc-145">如果您收到有關遺漏參考的錯誤，請以滑鼠右鍵按一下方案，然後選取 [還原 NuGet 套件]\*\*\*\* 以安裝相依性並重建。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="9d1dc-146">如果您使用的是 Visual Studio 2019,在選擇 **「還原 NuGet 套件**並嘗試`MSBuild.Sdk.Extras``2.0.54`重建」`LoggingLibrary.csproj`之前,您需要將的版本更改為 。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="9d1dc-147">此檔案只能透過下右鍵單擊專案(在解決方案下方)並選擇`Unload Project`存取 ,然後右鍵按一下卸載`Edit LoggingLibrary.csproj`的項目並選擇 。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="9d1dc-148">若要針對 iOS 建置，您需要連線至 Visual Studio 的網路 Mac，如　[Xamarin.iOS for Visual Studio 簡介](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)上所述。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="9d1dc-149">如果您沒有可用的 Mac，請在組態管理員中清除 iOS 專案 (上述步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9d1dc-150">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="9d1dc-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9d1dc-151">開啟命令提示字元，並巡覽至 `LoggingLibrary` 資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `Package.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9d1dc-152">將這個檔案重新命名為 `LoggingLibrary.nuspec`，並在編輯器中予以開啟。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="9d1dc-153">更新檔案使其符合下列內容，並使用適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9d1dc-154">尤其是在整個 nuget.org 中，`<id>` 值必須是唯一的 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="9d1dc-155">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="9d1dc-156">您的套件版本可以加上 `-alpha`、`-beta` 或 `-rc` 後置詞，以將套件標示為發行前版本，如需發行前版本的詳細資訊，請檢查[發行前版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="9d1dc-157">新增參考組件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-157">Add reference assemblies</span></span>

<span data-ttu-id="9d1dc-158">若要包含平台特定參考組件，請針對您的支援平台適當地將下列新增至 `LoggingLibrary.nuspec` 的 `<files>` 項目：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="9d1dc-159">若要縮短 DLL 和 XML 檔案的名稱，請以滑鼠右鍵按一下任何指定的專案，並選取 [程式庫]\*\*\*\* 索引標籤，然後變更組件名稱。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="9d1dc-160">新增相依性</span><span class="sxs-lookup"><span data-stu-id="9d1dc-160">Add dependencies</span></span>

<span data-ttu-id="9d1dc-161">如果您有原生實作的特定相依性，請搭配使用 `<dependencies>` 項目與 `<group>` 項目來指定它們，例如：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="9d1dc-162">例如，下列會將 iTextSharp 設定為 UAP 目標的相依性：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="9d1dc-163">最終 .nuspec</span><span class="sxs-lookup"><span data-stu-id="9d1dc-163">Final .nuspec</span></span>

<span data-ttu-id="9d1dc-164">最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="9d1dc-165">封裝元件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-165">Package the component</span></span>

<span data-ttu-id="9d1dc-166">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="9d1dc-167">這將產生 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9d1dc-168">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="9d1dc-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 LoggingLibrary 套件的 NuGet 套件總管](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9d1dc-170">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9d1dc-171">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9d1dc-172">若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="9d1dc-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="9d1dc-173">相關主題</span><span class="sxs-lookup"><span data-stu-id="9d1dc-173">Related topics</span></span>

- [<span data-ttu-id="9d1dc-174">努斯佩克參考</span><span class="sxs-lookup"><span data-stu-id="9d1dc-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9d1dc-175">符號包</span><span class="sxs-lookup"><span data-stu-id="9d1dc-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9d1dc-176">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="9d1dc-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="9d1dc-177">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="9d1dc-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9d1dc-178">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="9d1dc-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9d1dc-179">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="9d1dc-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
