---
title: 使用 Visual Studio 2015 建立適用於 Xamarin (適用於 iOS、Android 和 Windows) 的 NuGet 套件
description: 有關如何為 Xamarin 建立 NuGet 套件的端對端逐步解說，而這些套件在 iOS、Android 和 Windows 上使用原生 API。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 81f78de02d9b6510f195e04c78436e38f9b7353d
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842426"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="a5f27-103">使用 Visual Studio 2015 建立適用於 Xamarin 的套件</span><span class="sxs-lookup"><span data-stu-id="a5f27-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="a5f27-104">適用於 Xamarin 的套件包含使用 iOS、Android 和 Windows (視執行階段作業系統而定) 上原生 API 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a5f27-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="a5f27-105">雖然這十分簡單，但最好是讓開發人員使用 PCL 中的套件，或透過通用 API 介面區的 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a5f27-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="a5f27-106">在此逐步解說中，您要使用 Visual Studio 2015 建立可用於 iOS、Android 和 Windows 行動專案中的跨平台 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a5f27-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="a5f27-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5f27-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="a5f27-108">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="a5f27-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="a5f27-109">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="a5f27-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="a5f27-110">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="a5f27-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="a5f27-111">封裝元件</span><span class="sxs-lookup"><span data-stu-id="a5f27-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="a5f27-112">相關主題</span><span class="sxs-lookup"><span data-stu-id="a5f27-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="a5f27-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5f27-113">Prerequisites</span></span>

1. <span data-ttu-id="a5f27-114">含通用 Windows 平台 (UWP) 和 Xamarin 的 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="a5f27-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="a5f27-115">從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，當然也可以使用 Professional Edition 和 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="a5f27-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="a5f27-116">若要包含 UWP 和 Xamarin 工具，請選取 [自訂安裝] 並檢查適當的選項。</span><span class="sxs-lookup"><span data-stu-id="a5f27-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="a5f27-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="a5f27-117">NuGet CLI.</span></span> <span data-ttu-id="a5f27-118">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版的 nuget.exe，並將它儲存至您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="a5f27-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="a5f27-119">如果尚未新增，則請將該位置新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5f27-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="a5f27-120">nuget.exe 本身是 CLI 工具，不是安裝程式，因此請務必從瀏覽器儲存下載的檔案，而不是執行它。</span><span class="sxs-lookup"><span data-stu-id="a5f27-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="a5f27-121">建立專案結構和抽象程式碼</span><span class="sxs-lookup"><span data-stu-id="a5f27-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="a5f27-122">針對 Visual Studio，下載並執行 [ Xamarin 範本延伸模組外掛程式](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)。</span><span class="sxs-lookup"><span data-stu-id="a5f27-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="a5f27-123">這些範本可讓您輕鬆建立此逐步解說的必要專案結構。</span><span class="sxs-lookup"><span data-stu-id="a5f27-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="a5f27-124">在 Visual Studio 中，選取 [檔案] > [新增] > [專案]  、搜尋 `Plugin`、選取 [Plugin for Xamarin ] (Xamarin 的外掛程式)  範本、將名稱變更為 LoggingLibrary，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a5f27-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio 中的新空白應用程式 (Xamarin.Forms 可攜式) 專案](media/CrossPlatform-NewProject.png)

<span data-ttu-id="a5f27-126">所產生的方案包含兩個 PCL 專案，以及各種平台特定專案：</span><span class="sxs-lookup"><span data-stu-id="a5f27-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="a5f27-127">名為 `Plugin.LoggingLibrary.Abstractions (Portable)` 的 PCL 會定義元件的公用介面 (API 介面區)；在此情況下，ILoggingLibrary.cs 檔案中包含 `ILoggingLibrary` 介面。</span><span class="sxs-lookup"><span data-stu-id="a5f27-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="a5f27-128">這是您在其中定義程式庫介面的位置。</span><span class="sxs-lookup"><span data-stu-id="a5f27-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="a5f27-129">其他 PCL `Plugin.LoggingLibrary (Portable)` 會在 CrossLoggingLibrary.cs 中包含程式碼，以找出執行階段之抽象介面的平台特定實作。</span><span class="sxs-lookup"><span data-stu-id="a5f27-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="a5f27-130">您通常不需要修改這個檔案。</span><span class="sxs-lookup"><span data-stu-id="a5f27-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="a5f27-131">平台特定專案 (例如 `Plugin.LoggingLibrary.Android`)，每個專案都會在其個別 LoggingLibraryImplementation.cs 檔案中包含原生介面實作。</span><span class="sxs-lookup"><span data-stu-id="a5f27-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="a5f27-132">這是您建置程式庫程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="a5f27-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="a5f27-133">Abstractions 專案的 ILoggingLibrary.cs 檔案預設會包含介面定義，但沒有任何方法。</span><span class="sxs-lookup"><span data-stu-id="a5f27-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="a5f27-134">基於本逐步解說的目的，新增 `Log` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5f27-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="a5f27-135">撰寫平台特定程式碼</span><span class="sxs-lookup"><span data-stu-id="a5f27-135">Write your platform-specific code</span></span>

<span data-ttu-id="a5f27-136">若要實作 `ILoggingLibrary` 介面的平台特定實作和其方法，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="a5f27-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="a5f27-137">開啟每個平台專案的 `LoggingLibraryImplementation.cs` 檔案，並新增必要程式碼。</span><span class="sxs-lookup"><span data-stu-id="a5f27-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="a5f27-138">例如 (使用 `Plugin.LoggingLibrary.Android` 專案)：</span><span class="sxs-lookup"><span data-stu-id="a5f27-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. <span data-ttu-id="a5f27-139">針對每個您想要支援的平台，重複專案中的這個實作。</span><span class="sxs-lookup"><span data-stu-id="a5f27-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="a5f27-140">以滑鼠右鍵按一下 iOS 專案、選取 [屬性]  、按一下 [建置]  索引標籤，然後從 [輸出路徑]  和 [XML 文件檔案]  設定中移除 "\iPhone"。</span><span class="sxs-lookup"><span data-stu-id="a5f27-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="a5f27-141">在本逐步解說中，這只是方便之後使用。</span><span class="sxs-lookup"><span data-stu-id="a5f27-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="a5f27-142">在完成時儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="a5f27-142">Save the file when done.</span></span>
1. <span data-ttu-id="a5f27-143">以滑鼠右鍵按一下方案，並選取 [組態管理員]  ，然後為 PCL 和每個所支援的平台核取 [建置]  方塊。</span><span class="sxs-lookup"><span data-stu-id="a5f27-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="a5f27-144">以滑鼠右鍵按一下方案，然後選取 [建置方案]  檢查您的工作，並產生之後將封裝的成品。</span><span class="sxs-lookup"><span data-stu-id="a5f27-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="a5f27-145">如果您收到有關遺漏參考的錯誤，請以滑鼠右鍵按一下方案，然後選取 [還原 NuGet 套件]  以安裝相依性並重建。</span><span class="sxs-lookup"><span data-stu-id="a5f27-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="a5f27-146">若要針對 iOS 建置，您需要連線至 Visual Studio 的網路 Mac，如　[Xamarin.iOS for Visual Studio 簡介](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)上所述。</span><span class="sxs-lookup"><span data-stu-id="a5f27-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="a5f27-147">如果您沒有可用的 Mac，請在組態管理員中清除 iOS 專案 (上述步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="a5f27-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="a5f27-148">建立和更新 .nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="a5f27-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="a5f27-149">開啟命令提示字元，並巡覽至 `LoggingLibrary` 資料夾 (低於 `.sln` 檔案一階)，然後執行 NuGet `spec` 命令以建立初始的 `Package.nuspec` 檔案：</span><span class="sxs-lookup"><span data-stu-id="a5f27-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="a5f27-150">將這個檔案重新命名為 `LoggingLibrary.nuspec`，並在編輯器中予以開啟。</span><span class="sxs-lookup"><span data-stu-id="a5f27-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="a5f27-151">更新檔案使其符合下列內容，並使用適當的值取代 YOUR_NAME。</span><span class="sxs-lookup"><span data-stu-id="a5f27-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="a5f27-152">尤其是在整個 nuget.org 中，`<id>` 值必須為唯一 (請參閱[建立套件](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)中所述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="a5f27-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="a5f27-153">另請注意，您也必須更新作者和描述標記，否則會在封裝步驟期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a5f27-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="a5f27-154">您的套件版本可以加上 `-alpha`、`-beta` 或 `-rc` 後置詞，以將套件標示為發行前版本，如需發行前版本的詳細資訊，請檢查[發行前版本](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="a5f27-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="a5f27-155">新增參考組件</span><span class="sxs-lookup"><span data-stu-id="a5f27-155">Add reference assemblies</span></span>

<span data-ttu-id="a5f27-156">若要包含平台特定參考組件，請針對您的支援平台適當地將下列新增至 `LoggingLibrary.nuspec` 的 `<files>` 項目：</span><span class="sxs-lookup"><span data-stu-id="a5f27-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="a5f27-157">若要縮短 DLL 和 XML 檔案的名稱，請以滑鼠右鍵按一下任何指定的專案，並選取 [程式庫]  索引標籤，然後變更組件名稱。</span><span class="sxs-lookup"><span data-stu-id="a5f27-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="a5f27-158">新增相依性</span><span class="sxs-lookup"><span data-stu-id="a5f27-158">Add dependencies</span></span>

<span data-ttu-id="a5f27-159">如果您有原生實作的特定相依性，請搭配使用 `<dependencies>` 項目與 `<group>` 項目來指定它們，例如：</span><span class="sxs-lookup"><span data-stu-id="a5f27-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="a5f27-160">例如，下列會將 iTextSharp 設定為 UAP 目標的相依性：</span><span class="sxs-lookup"><span data-stu-id="a5f27-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="a5f27-161">最終 .nuspec</span><span class="sxs-lookup"><span data-stu-id="a5f27-161">Final .nuspec</span></span>

<span data-ttu-id="a5f27-162">最終 `.nuspec` 檔案現在看起來應該如下所示，並且應該將 YOUR_NAME 取代為適當值：</span><span class="sxs-lookup"><span data-stu-id="a5f27-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="a5f27-163">封裝元件</span><span class="sxs-lookup"><span data-stu-id="a5f27-163">Package the component</span></span>

<span data-ttu-id="a5f27-164">只要已完成的 `.nuspec` 參考您需要包含在套件中的所有檔案，就可隨時執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="a5f27-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="a5f27-165">這會產生 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="a5f27-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="a5f27-166">在如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="a5f27-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![顯示 LoggingLibrary 套件的 NuGet 套件總管](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="a5f27-168">`.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。</span><span class="sxs-lookup"><span data-stu-id="a5f27-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="a5f27-169">然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="a5f27-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="a5f27-170">若要讓其他開發人員使用您的套件，請遵循[發行套件](../nuget-org/publish-a-package.md)上的指示。</span><span class="sxs-lookup"><span data-stu-id="a5f27-170">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="a5f27-171">相關主題</span><span class="sxs-lookup"><span data-stu-id="a5f27-171">Related topics</span></span>

- [<span data-ttu-id="a5f27-172">Nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="a5f27-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="a5f27-173">符號套件</span><span class="sxs-lookup"><span data-stu-id="a5f27-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="a5f27-174">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="a5f27-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="a5f27-175">支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="a5f27-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a5f27-176">在套件中包含 MSBuild 屬性和目標</span><span class="sxs-lookup"><span data-stu-id="a5f27-176">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="a5f27-177">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="a5f27-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)