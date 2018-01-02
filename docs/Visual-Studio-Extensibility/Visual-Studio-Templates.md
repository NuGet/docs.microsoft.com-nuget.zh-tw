---
title: "Visual Studio 範本中的 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "將 NuGet 套件包含為 Visual Studio 專案和項目範本一部分的指示。"
keywords: "Visual Studio 中的 NuGet, Visual Studio 專案範本, Visual Studio 項目範本, 專案範本中的套件, 項目範本中的套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="76baf-104">Visual Studio 範本中的套件</span><span class="sxs-lookup"><span data-stu-id="76baf-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="76baf-105">在建立專案或項目時，Visual Studio 專案和項目範本經常需要確保已安裝特定的套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-105">Visual Studio project and item templates often need to ensure that certain packages are installed into when the project or item is created.</span></span> <span data-ttu-id="76baf-106">例如，ASP.NET MVC 3 範本會安裝 jQuery、Modernizr 和其他套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="76baf-107">若要支援此作業，範本作者可以指示 NuGet 安裝必要的套件，而不是個別的程式庫。</span><span class="sxs-lookup"><span data-stu-id="76baf-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="76baf-108">開發人員稍後便可以隨時輕鬆地更新那些套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="76baf-109">若要深入了解自行撰寫範本，請參閱[在 Visual Studio 中建立專案和項目範本](https://msdn.microsoft.com/library/s365byhx.aspx)或[使用 Visual Studio SDK 建立自訂專案與項目範本](https://msdn.microsoft.com/library/ff527340.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76baf-109">To learn more about authoring templates themselves, refer to [Creating Project and Item Templates in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) or [Creating Custom Project and Item Templates with the Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span></span>

<span data-ttu-id="76baf-110">本節的其餘部分描述在撰寫範本以正確包含 NuGet 套件時要採取的特定步驟。</span><span class="sxs-lookup"><span data-stu-id="76baf-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="76baf-111">將套件新增至範本</span><span class="sxs-lookup"><span data-stu-id="76baf-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="76baf-112">最佳做法</span><span class="sxs-lookup"><span data-stu-id="76baf-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="76baf-113">如需範例，請參閱 [NuGetInVsTemplates 範例](https://bitbucket.org/marcind/nugetinvstemplates)。</span><span class="sxs-lookup"><span data-stu-id="76baf-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>


## <a name="adding-packages-to-a-template"></a><span data-ttu-id="76baf-114">將套件新增至範本</span><span class="sxs-lookup"><span data-stu-id="76baf-114">Adding packages to a template</span></span>

<span data-ttu-id="76baf-115">具現化範本時，會叫用[範本精靈](https://msdn.microsoft.com/library/ms185301.aspx)來載入要安裝的套件清單，以及何處可以找到這些套件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="76baf-115">When a template is instantiated, a [template wizard](https://msdn.microsoft.com/library/ms185301.aspx) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="76baf-116">套件可以內嵌在 VSIX 中、內嵌在範本中，或位於本機硬碟上，在此情況下您會使用登錄機碼來參考檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="76baf-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="76baf-117">這些位置的詳細資料稍後會在本節中提供。</span><span class="sxs-lookup"><span data-stu-id="76baf-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="76baf-118">預先安裝的套件使用[範本精靈](http://msdn.microsoft.com/library/ms185301.aspx)來運作。</span><span class="sxs-lookup"><span data-stu-id="76baf-118">Preinstalled packages work using [template wizards](http://msdn.microsoft.com/library/ms185301.aspx).</span></span> <span data-ttu-id="76baf-119">範本具現化時，會叫用特殊的精靈。</span><span class="sxs-lookup"><span data-stu-id="76baf-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="76baf-120">精靈會載入需要安裝的套件清單，並將該資訊傳遞至適當的 NuGet API。</span><span class="sxs-lookup"><span data-stu-id="76baf-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="76baf-121">要在範本中包含套件的步驟：</span><span class="sxs-lookup"><span data-stu-id="76baf-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="76baf-122">在您的 `vstemplate` 檔案中，藉由新增 [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) 項目新增對 NuGet 範本精靈的參考：</span><span class="sxs-lookup"><span data-stu-id="76baf-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="76baf-123">`NuGet.VisualStudio.Interop.dll` 是一個組件，它只包含 `TemplateWizard` 類別，這是簡單的包裝函式，它會呼叫 `NuGet.VisualStudio.dll` 中的實際實作。</span><span class="sxs-lookup"><span data-stu-id="76baf-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="76baf-124">組件版本永遠不會變更，以便專案/項目範本繼續使用新版的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="76baf-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="76baf-125">在專案中新增要安裝的套件清單：</span><span class="sxs-lookup"><span data-stu-id="76baf-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="76baf-126">*(NuGet 2.2.1+)* 精靈支援多個 `<package>` 項目以支援多個套件來源。</span><span class="sxs-lookup"><span data-stu-id="76baf-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="76baf-127">同時需要 `id` 和 `version` 屬性，這表示即使有較新版本，也將會安裝該特定版本的套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="76baf-128">這可防止套件更新中斷範本，讓使用範本的開發人員能選擇是否更新套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>


1. <span data-ttu-id="76baf-129">指定 NuGet 可以找到套件的儲存機制，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="76baf-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="76baf-130">VSIX 套件儲存機制</span><span class="sxs-lookup"><span data-stu-id="76baf-130">VSIX package repository</span></span>

<span data-ttu-id="76baf-131">Visual Studio 專案/項目範本的建議部署方法是 [VSIX 延伸模組](http://msdn.microsoft.com/library/ff363239.aspx)，因為它可讓您將多個專案/項目範本封裝在一起，並可讓開發人員輕鬆地使用 VS 延伸模組管理員或 Visual Studio 組件庫探索您的範本。</span><span class="sxs-lookup"><span data-stu-id="76baf-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](http://msdn.microsoft.com/library/ff363239.aspx) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="76baf-132">延伸模組的更新也很容易使用 [Visual Studio 延伸模組管理員自動更新機制](http://msdn.microsoft.com/library/dd997169.aspx)部署。</span><span class="sxs-lookup"><span data-stu-id="76baf-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](http://msdn.microsoft.com/library/dd997169.aspx).</span></span>

<span data-ttu-id="76baf-133">VSIX 本身可以作為範本所需的套件來源：</span><span class="sxs-lookup"><span data-stu-id="76baf-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="76baf-134">修改 `.vstemplate` 檔案中的 `<packages>` 項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="76baf-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="76baf-135">`repository` 屬性指定儲存機制的類型為 `extension`，而 `repositoryId` 是 VSIX 本身的唯一識別碼 (這是延伸模組之 `vsixmanifest` 檔中的 [`ID` 屬性](http://msdn.microsoft.com/library/dd393688.aspx)值)。</span><span class="sxs-lookup"><span data-stu-id="76baf-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the [`ID` attribute](http://msdn.microsoft.com/library/dd393688.aspx) in the extension’s `vsixmanifest` file).</span></span>

1. <span data-ttu-id="76baf-136">將您 `nupkg` 檔案放在 VSIX 內稱為 `Packages` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="76baf-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>
1. <span data-ttu-id="76baf-137">將所需的套件檔案新增為 `source.extension.vsixmanifest` 檔案中的[自訂延伸模組內容](http://msdn.microsoft.com/library/dd393737.aspx)。</span><span class="sxs-lookup"><span data-stu-id="76baf-137">Add the necessary package files as [custom extension content](http://msdn.microsoft.com/library/dd393737.aspx) in your `source.extension.vsixmanifest` file.</span></span> <span data-ttu-id="76baf-138">如果您使用 2.0 結構描述，看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="76baf-138">If you're using the 2.0 schema it should look like this:</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    <span data-ttu-id="76baf-139">如果您使用 1.0 結構描述，看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="76baf-139">If you're using the 1.0 schema it should look like this:</span></span>

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. <span data-ttu-id="76baf-140">請注意，您可以在與您專案範本相同的 VSIX 中提供套件，或者可以在對您的案例更有意義時將它們放在個別的 VSIX 中。</span><span class="sxs-lookup"><span data-stu-id="76baf-140">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="76baf-141">不過，請勿參考您無法控制的任何 VSIX，因為該延伸模組的變更可能會破壞您的範本。</span><span class="sxs-lookup"><span data-stu-id="76baf-141">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>


### <a name="template-package-repository"></a><span data-ttu-id="76baf-142">範本套件儲存機制</span><span class="sxs-lookup"><span data-stu-id="76baf-142">Template package repository</span></span>

<span data-ttu-id="76baf-143">如果您只散發單一專案/項目範本，且不需要將多個範本封裝在一起，您可以使用較簡單但較多限制的方法，將套件直接包含在專案/項目範本 ZIP 檔案：</span><span class="sxs-lookup"><span data-stu-id="76baf-143">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="76baf-144">修改 `.vstemplate` 檔案中的 `<packages>` 項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="76baf-144">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="76baf-145">`repository` 屬性有 `template` 值，且 `repositoryId` 屬性不是必要。</span><span class="sxs-lookup"><span data-stu-id="76baf-145">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="76baf-146">將套件放在專案/項目範本 ZIP 檔案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="76baf-146">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="76baf-147">請注意，在包含多個範本的 VSIX 中使用這種方法，會在一或多個套件是範本皆通用時導致不必要的膨脹。</span><span class="sxs-lookup"><span data-stu-id="76baf-147">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="76baf-148">在這種情況下，請使用 [VSIX 作為儲存機制](#vsix-package-repository)，如上一節中所述。</span><span class="sxs-lookup"><span data-stu-id="76baf-148">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>


### <a name="registry-specified-folder-path"></a><span data-ttu-id="76baf-149">登錄指定的資料夾路徑</span><span class="sxs-lookup"><span data-stu-id="76baf-149">Registry-specified folder path</span></span>

<span data-ttu-id="76baf-150">使用 MSI 安裝的 SDK 可以直接在開發人員的電腦上安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="76baf-150">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="76baf-151">這樣當使用專案或項目範本時它們便立即可用，而不需要在這段時間擷取它們。</span><span class="sxs-lookup"><span data-stu-id="76baf-151">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="76baf-152">ASP.NET 範本使用此方法。</span><span class="sxs-lookup"><span data-stu-id="76baf-152">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="76baf-153">讓 MSI 將套件安裝至電腦。</span><span class="sxs-lookup"><span data-stu-id="76baf-153">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="76baf-154">您可以只安裝 `.nupkg` 檔案，或是與展開的內容一起安裝，以在使用範本時節省額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="76baf-154">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="76baf-155">在此情況下，請遵循 NuGet 的標準資料夾結構，其中 `.nupkg` 檔案位於根資料夾，然後每個套件會有子資料夾，並以識別碼/版本組作為子資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="76baf-155">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="76baf-156">寫入登錄機碼來識別套件位置：</span><span class="sxs-lookup"><span data-stu-id="76baf-156">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="76baf-157">機碼位置：可能是整部機器的 `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`，或者如果是每個使用者安裝的範本和套件，可以選擇使用 `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="76baf-157">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="76baf-158">機碼名稱：使用您獨有的名稱。</span><span class="sxs-lookup"><span data-stu-id="76baf-158">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="76baf-159">例如，VS 2012 的 ASP.NET MVC 4 範本使用 `AspNetMvc4VS11`。</span><span class="sxs-lookup"><span data-stu-id="76baf-159">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="76baf-160">值：packages 資料夾的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="76baf-160">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="76baf-161">在 `.vstemplate` 檔案的 `<packages>` 項目中，新增屬性 `repository="registry"` 並在 `keyName` 屬性指定您的登錄機碼名稱。</span><span class="sxs-lookup"><span data-stu-id="76baf-161">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="76baf-162">如果您已預先解壓縮套件，請使用 `isPreunzipped="true"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="76baf-162">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="76baf-163">*(NuGet 3.2+)* 如果您想要在套件安裝結束時強制設計階段組建，請新增 `forceDesignTimeBuild="true"` 屬性。</span><span class="sxs-lookup"><span data-stu-id="76baf-163">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="76baf-164">新增 `skipAssemblyReferences="true"` 以便進行最佳化，因為範本本身已經包含必要的參考。</span><span class="sxs-lookup"><span data-stu-id="76baf-164">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="76baf-165">最佳作法</span><span class="sxs-lookup"><span data-stu-id="76baf-165">Best Practices</span></span>

1. <span data-ttu-id="76baf-166">宣告對 NuGet VSIX 的相依性，方法是在您的 VSIX 資訊清單中新增對它的參考：</span><span class="sxs-lookup"><span data-stu-id="76baf-166">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="76baf-167">藉由在 `.vstemplate` 檔案中設定 [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx)，要求在建立時儲存專案/項目範本。</span><span class="sxs-lookup"><span data-stu-id="76baf-167">Require project/item templates to be saved on creation by setting [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="76baf-168">範本不包含 `packages.config` 或 `project.json` 檔案，而且不包含安裝 NuGet 套件時將會新增的任何參考或內容。</span><span class="sxs-lookup"><span data-stu-id="76baf-168">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
