---
title: NuGet 的.nuspec 檔案參考
description: .nuspec 檔案包含建置套件時使用的套件中繼資料，並向套件取用者提供資訊。
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e8d4ed1f3fe4394d084a5847200901b23a1b7b39
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944076"
---
# <a name="nuspec-reference"></a><span data-ttu-id="1bf54-103">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-103">.nuspec reference</span></span>

<span data-ttu-id="1bf54-104">`.nuspec` 檔案是包含套件中繼資料的 XML 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="1bf54-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="1bf54-105">此資訊清單用來建置套件和向取用者提供資訊。</span><span class="sxs-lookup"><span data-stu-id="1bf54-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="1bf54-106">資訊清單一律包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="1bf54-107">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="1bf54-107">In this topic:</span></span>

- [<span data-ttu-id="1bf54-108">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="1bf54-109">[取代權杖](#replacement-tokens) (搭配 Visual Studio 專案使用時)</span><span class="sxs-lookup"><span data-stu-id="1bf54-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="1bf54-110">相依性</span><span class="sxs-lookup"><span data-stu-id="1bf54-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="1bf54-111">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="1bf54-112">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="1bf54-113">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="1bf54-114">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="1bf54-115">範例 nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="1bf54-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="1bf54-116">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-116">General form and schema</span></span>

<span data-ttu-id="1bf54-117">目前的 `nuspec.xsd` 結構描述檔案位於 [NuGet GitHub 存放庫](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="1bf54-118">在此結構描述內，`.nuspec` 檔案有下列一般格式：</span><span class="sxs-lookup"><span data-stu-id="1bf54-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="1bf54-119">為能清晰呈現結構描述，請在 Visual Studio 中以設計模式開啟結構描述檔案，按一下 [XML 結構描述總管] 連結。</span><span class="sxs-lookup"><span data-stu-id="1bf54-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="1bf54-120">或者，將檔案開啟為程式碼，在編輯器中按一下滑鼠右鍵，選取 [Show XML Schema Explorer] (顯示 XML 結構描述總管)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="1bf54-121">任一方式都可取得類似以下的檢視 (大部分展開時)：</span><span class="sxs-lookup"><span data-stu-id="1bf54-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![開啟了 nuspec.xsd 的 Visual Studio 結構描述總管](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="1bf54-123">必要的中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-123">Required metadata elements</span></span>

<span data-ttu-id="1bf54-124">雖然下列項目是套件的最低需求，但您應該考慮新增[選擇性中繼資料項目](#optional-metadata-elements)以改善開發人員使用套件的整體體驗。</span><span class="sxs-lookup"><span data-stu-id="1bf54-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="1bf54-125">這些項目必須出現在 `<metadata>` 項目中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="1bf54-126">id</span><span class="sxs-lookup"><span data-stu-id="1bf54-126">id</span></span> 
<span data-ttu-id="1bf54-127">不區分大小寫的套件識別碼，在整個 nuget.org 或套件所在的任何組件庫中都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1bf54-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="1bf54-128">識別碼可能不包含對 URL 而言無效的空格或字元，而且通常會遵循 .NET 命名空間規則。</span><span class="sxs-lookup"><span data-stu-id="1bf54-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="1bf54-129">如需指導方針，請參閱[選擇唯一的套件識別碼](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="1bf54-130">版本</span><span class="sxs-lookup"><span data-stu-id="1bf54-130">version</span></span>
<span data-ttu-id="1bf54-131">套件版本，遵循 *major.minor.patch* 模式。</span><span class="sxs-lookup"><span data-stu-id="1bf54-131">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="1bf54-132">版本號碼可以包含預先發行版本的後置詞，如[套件版本控制](../reference/package-versioning.md#pre-release-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="1bf54-132">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="1bf54-133">描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-133">description</span></span>
<span data-ttu-id="1bf54-134">UI 顯示中的套件詳細描述。</span><span class="sxs-lookup"><span data-stu-id="1bf54-134">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="1bf54-135">authors</span><span class="sxs-lookup"><span data-stu-id="1bf54-135">authors</span></span>
<span data-ttu-id="1bf54-136">以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些名稱會顯示在 nuget.org 的 NuGet 組件庫中，並用來交互參照相同作者的其他套件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-136">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="1bf54-137">選擇性中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-137">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="1bf54-138">標題</span><span class="sxs-lookup"><span data-stu-id="1bf54-138">title</span></span>
<span data-ttu-id="1bf54-139">套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="1bf54-140">如未指定，則使用套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="1bf54-140">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="1bf54-141">owners</span><span class="sxs-lookup"><span data-stu-id="1bf54-141">owners</span></span>
<span data-ttu-id="1bf54-142">以逗號分隔的套件作者清單，使用 nuget.org 上的設定檔名稱。這通常和 `authors` 是同一份清單，將套件上傳至 nuget.org 時會忽略。請參閱[在 nuget.org 上管理套件擁有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-142">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="1bf54-143">projectUrl</span><span class="sxs-lookup"><span data-stu-id="1bf54-143">projectUrl</span></span>
<span data-ttu-id="1bf54-144">套件首頁的 URL，通常會顯示在 UI 顯示及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-144">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="1bf54-145">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="1bf54-145">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="1bf54-146">licenseUrl 已被取代。</span><span class="sxs-lookup"><span data-stu-id="1bf54-146">licenseUrl is being deprecated.</span></span> <span data-ttu-id="1bf54-147">改為使用授權。</span><span class="sxs-lookup"><span data-stu-id="1bf54-147">Use license instead.</span></span>

<span data-ttu-id="1bf54-148">套件授權的 URL，通常會顯示在 UI 顯示及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-148">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="1bf54-149">授權</span><span class="sxs-lookup"><span data-stu-id="1bf54-149">license</span></span>
<span data-ttu-id="1bf54-150">SPDX 授權運算式或套件，通常會顯示在 UI 顯示及 nuget.org 中的授權檔案的路徑。如果您要授權常見例如 BSD 2 子句或 MIT 授權底下的封裝，使用相關聯的 SPDX 授權識別碼。</span><span class="sxs-lookup"><span data-stu-id="1bf54-150">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="1bf54-151">例如： `<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="1bf54-151">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="1bf54-152">以下是完整的清單[SPDX 授權識別碼](https://spdx.org/licenses/)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-152">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="1bf54-153">NuGet.org 接受僅 OSI 或 FSF 核准授權時使用的授權類型的運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf54-153">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="1bf54-154">如果您的套件係依據多個常見的授權，您可以指定複合的授權，使用[SPDX 運算式語法版本 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-154">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="1bf54-155">例如： `<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="1bf54-155">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="1bf54-156">如果您使用授權未被指派 SPDX 識別項，或是自訂的授權，您就可以封裝授權文字的檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-156">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file with the license text.</span></span> <span data-ttu-id="1bf54-157">例如: </span><span class="sxs-lookup"><span data-stu-id="1bf54-157">For example:</span></span>
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```
<span data-ttu-id="1bf54-158">NuGet 的授權運算式的正確語法是如下中所述[ABNF](https://tools.ietf.org/html/rfc5234)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-158">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="1bf54-159">iconUrl</span><span class="sxs-lookup"><span data-stu-id="1bf54-159">iconUrl</span></span>
<span data-ttu-id="1bf54-160">具有透明背景之 64x64 映像的 URL，該映像會用作套件在 UI 顯示中的圖示。</span><span class="sxs-lookup"><span data-stu-id="1bf54-160">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="1bf54-161">確定這個項目包含「直接映像 URL」，不是包含影像的網頁 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf54-161">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="1bf54-162">例如，若要使用 GitHub 的映像，使用 原始檔 URL，如<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>。</span><span class="sxs-lookup"><span data-stu-id="1bf54-162">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="1bf54-163">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1bf54-163">requireLicenseAcceptance</span></span>
<span data-ttu-id="1bf54-164">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="1bf54-164">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="1bf54-165">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="1bf54-165">developmentDependency</span></span>
<span data-ttu-id="1bf54-166">*(2.8+)* 布林值，指定套件是否標示為僅限開發相依性，這可防止套件包含為其他套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-166">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="1bf54-167">使用 PackageReference (NuGet 4.8 +)，這個旗標也表示，它會將排除編譯時期資產編譯。</span><span class="sxs-lookup"><span data-stu-id="1bf54-167">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="1bf54-168">請參閱[DevelopmentDependency 支援 PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="1bf54-168">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="1bf54-169">摘要</span><span class="sxs-lookup"><span data-stu-id="1bf54-169">summary</span></span>
<span data-ttu-id="1bf54-170">UI 顯示中的套件簡短描述。</span><span class="sxs-lookup"><span data-stu-id="1bf54-170">A short description of the package for UI display.</span></span> <span data-ttu-id="1bf54-171">如果省略，即使用截斷版本的 `description`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-171">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="1bf54-172">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="1bf54-172">releaseNotes</span></span>
<span data-ttu-id="1bf54-173">*(1.5+)* 此版本套件中的變更描述，通常用於 Visual Studio Package Manager 的 [更新] 索引標籤等 UI 中，以取代套件描述。</span><span class="sxs-lookup"><span data-stu-id="1bf54-173">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="1bf54-174">Copyright</span><span class="sxs-lookup"><span data-stu-id="1bf54-174">copyright</span></span>
<span data-ttu-id="1bf54-175">*(1.5+)* 套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1bf54-175">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="1bf54-176">語言</span><span class="sxs-lookup"><span data-stu-id="1bf54-176">language</span></span>
<span data-ttu-id="1bf54-177">套件的地區設定識別碼。</span><span class="sxs-lookup"><span data-stu-id="1bf54-177">The locale ID for the package.</span></span> <span data-ttu-id="1bf54-178">請參閱[建立當地語系化的套件](../create-packages/creating-localized-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-178">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="1bf54-179">標記</span><span class="sxs-lookup"><span data-stu-id="1bf54-179">tags</span></span>
<span data-ttu-id="1bf54-180">以逗號分隔的標記與關鍵字清單，描述套件並透過搜尋和篩選協助探索套件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-180">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="1bf54-181">可自行維修</span><span class="sxs-lookup"><span data-stu-id="1bf54-181">serviceable</span></span> 
<span data-ttu-id="1bf54-182">*(3.3+)* 僅供內部 NuGet 使用。</span><span class="sxs-lookup"><span data-stu-id="1bf54-182">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="1bf54-183">儲存機制</span><span class="sxs-lookup"><span data-stu-id="1bf54-183">repository</span></span>
<span data-ttu-id="1bf54-184">存放庫的中繼資料，其中包含四個選擇性屬性：*型別*並*url* *（4.0 +）*，以及*分支*和*認可* *（4.6 +）*。</span><span class="sxs-lookup"><span data-stu-id="1bf54-184">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="1bf54-185">這些屬性可讓您將對應至儲存機制，建置它，以取得可能的.nupkg 為個別的分支或認可建置套件所述。</span><span class="sxs-lookup"><span data-stu-id="1bf54-185">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="1bf54-186">這應該是公開可用的 url，可以是直接由叫用版本控制軟體。</span><span class="sxs-lookup"><span data-stu-id="1bf54-186">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="1bf54-187">因為這適用於電腦，它不應該是 html 網頁。</span><span class="sxs-lookup"><span data-stu-id="1bf54-187">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="1bf54-188">對於連結至專案的頁面，使用`projectUrl`欄位中，改為。</span><span class="sxs-lookup"><span data-stu-id="1bf54-188">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="1bf54-189">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="1bf54-189">minClientVersion</span></span>
<span data-ttu-id="1bf54-190">指定可安裝此套件的最低 NuGet 用戶端版本，此作業是由 nuget.exe 和 Visual Studio 套件管理員強制執行。</span><span class="sxs-lookup"><span data-stu-id="1bf54-190">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="1bf54-191">每當套件依存於 NuGet 用戶端新增的 `.nuspec` 檔案特定功能時，就會使用。</span><span class="sxs-lookup"><span data-stu-id="1bf54-191">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="1bf54-192">例如，套件使用的 `developmentDependency` 屬性應該為 `minClientVersion` 指定 "2.8"。</span><span class="sxs-lookup"><span data-stu-id="1bf54-192">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="1bf54-193">同樣地，使用 `contentFiles` 項目的套件 (請參閱下一節) 應將 `minClientVersion` 設定成 "3.3"。</span><span class="sxs-lookup"><span data-stu-id="1bf54-193">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="1bf54-194">另請注意，因為 2.5 之前的 NuGet 用戶端無法辨識此旗標，所以它們「一律」拒絕安裝套件，無論 `minClientVersion` 包含什麼。</span><span class="sxs-lookup"><span data-stu-id="1bf54-194">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="1bf54-195">集合項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-195">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="1bf54-196">Packagetypes></span><span class="sxs-lookup"><span data-stu-id="1bf54-196">packageTypes</span></span>
<span data-ttu-id="1bf54-197">*(3.5+)* 零或多個 `<packageType>` 元素的集合，如果不是傳統相依性套件，則會指定套件類型。</span><span class="sxs-lookup"><span data-stu-id="1bf54-197">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="1bf54-198">每個 packageType 都有「名稱」和「版本」屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-198">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="1bf54-199">請參閱[設定套件類型](../create-packages/creating-a-package.md#setting-a-package-type)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-199">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="1bf54-200">相依性</span><span class="sxs-lookup"><span data-stu-id="1bf54-200">dependencies</span></span>
<span data-ttu-id="1bf54-201">零或多個 `<dependency>` 項目的集合，指定套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-201">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="1bf54-202">每個相依性都有「識別碼」、「版本」、「包含」(3.x+) 和「排除」(3.x+) 屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-202">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="1bf54-203">請參閱下文的[相依性](#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-203">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="1bf54-204">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="1bf54-204">frameworkAssemblies</span></span>
<span data-ttu-id="1bf54-205">*(1.2+)* 零或多個 `<frameworkAssembly>` 項目的集合，識別此套件需要的 .NET Framework 組件參考，它們可確保參考會新增至取用套件的專案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-205">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="1bf54-206">每個 frameworkAssembly 都有 *assemblyName* 和 *targetFramework* 屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-206">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="1bf54-207">請參閱下文的[指定 Framework 組件參考 GAC](#specifying-framework-assembly-references-gac)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-207">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="1bf54-208">參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-208">references</span></span>
<span data-ttu-id="1bf54-209">*(1.5+)* 在套件的 `lib` 資料夾中命名組件的零或多個 `<reference>` 項目集合，這些項目可新增為專案參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-209">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="1bf54-210">每個參考都有 *file* 屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-210">Each reference has a *file* attribute.</span></span> <span data-ttu-id="1bf54-211">`<references>` 也可以包含具有 *targetFramework* 屬性的 `<group>` 項目，然後即可包含 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-211">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="1bf54-212">如果省略，就會包含 `lib` 中的所有參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-212">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="1bf54-213">請參閱下文中的[指定明確的組件參考](#specifying-explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-213">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="1bf54-214">contentFiles</span><span class="sxs-lookup"><span data-stu-id="1bf54-214">contentFiles</span></span>
<span data-ttu-id="1bf54-215">*(3.3+)* `<files>` 項目的集合，可識別要包含在取用專案中的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-215">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="1bf54-216">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定。</span><span class="sxs-lookup"><span data-stu-id="1bf54-216">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="1bf54-217">請參閱下文中的[指定要包含在套件中的檔案](#specifying-files-to-include-in-the-package)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-217">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="1bf54-218">個檔案</span><span class="sxs-lookup"><span data-stu-id="1bf54-218">files</span></span> 
<span data-ttu-id="1bf54-219">`<package>`節點可包含`<files>`同層級節點`<metadata>`，以及`<contentFiles>`下的子系`<metadata>`，指定要包含在封裝中的哪些組件和內容檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-219">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="1bf54-220">如需詳細資料，請參閱本主題下文中的[包含組件檔](#including-assembly-files)和[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-220">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="1bf54-221">取代權杖</span><span class="sxs-lookup"><span data-stu-id="1bf54-221">Replacement tokens</span></span>

<span data-ttu-id="1bf54-222">建立套件時，[`nuget pack` 命令](../tools/cli-ref-pack.md) 會使用來自專案檔的值或來自 `pack` 命令的 `-properties` 參數值，取代 `.nuspec` 檔案之 `<metadata>` 節點的 $ 分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="1bf54-222">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="1bf54-223">在命令列中，您可以使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定權杖值。</span><span class="sxs-lookup"><span data-stu-id="1bf54-223">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="1bf54-224">例如，您可以在 `.nuspec` 中使用權杖，例如 `$owners$` 和 `$desc$`，並在封裝階段提供值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1bf54-224">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="1bf54-225">若要使用專案中的值，請指定下表中描述的權杖 (AssemblyInfo 是指 `Properties` 中的檔案，例如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-225">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="1bf54-226">若要使用這些權杖，請執行 `nuget pack` 與專案檔，非僅 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-226">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="1bf54-227">例如，使用下列命令時，專案的 `AssemblyName` 和 `AssemblyVersion` 值會取代為 `.nuspec` 檔案中的 `$id$` 和 `$version$` 權杖：</span><span class="sxs-lookup"><span data-stu-id="1bf54-227">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="1bf54-228">通常，當您擁有專案時，一開始會使用自動包含這些標準權杖一部分的 `nuget spec MyProject.csproj` 來建立 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-228">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="1bf54-229">不過，如果專案沒有所需之 `.nuspec` 項目的值，則 `nuget pack` 會失敗。</span><span class="sxs-lookup"><span data-stu-id="1bf54-229">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="1bf54-230">此外，如果變更專案值，請務必在建立套件前重建；使用 pack 命令的 `build` 參數很容易完成此作業。</span><span class="sxs-lookup"><span data-stu-id="1bf54-230">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="1bf54-231">除 `$configuration$` 以外，專案中值的使用順序優先於任何指派給命令列上相同權杖的值。</span><span class="sxs-lookup"><span data-stu-id="1bf54-231">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="1bf54-232">語彙基元</span><span class="sxs-lookup"><span data-stu-id="1bf54-232">Token</span></span> | <span data-ttu-id="1bf54-233">值來源</span><span class="sxs-lookup"><span data-stu-id="1bf54-233">Value source</span></span> | <span data-ttu-id="1bf54-234">值</span><span class="sxs-lookup"><span data-stu-id="1bf54-234">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="1bf54-235">**$id$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-235">**$id$**</span></span> | <span data-ttu-id="1bf54-236">專案檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-236">Project file</span></span> | <span data-ttu-id="1bf54-237">從專案檔的 AssemblyName （標題）</span><span class="sxs-lookup"><span data-stu-id="1bf54-237">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="1bf54-238">**$version$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-238">**$version$**</span></span> | <span data-ttu-id="1bf54-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1bf54-239">AssemblyInfo</span></span> | <span data-ttu-id="1bf54-240">如有則為 AssemblyInformationalVersion，否則為 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="1bf54-240">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="1bf54-241">**$authors $**</span><span class="sxs-lookup"><span data-stu-id="1bf54-241">**$authors$**</span></span> | <span data-ttu-id="1bf54-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1bf54-242">AssemblyInfo</span></span> | <span data-ttu-id="1bf54-243">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="1bf54-243">AssemblyCompany</span></span> |
| <span data-ttu-id="1bf54-244">**$title$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-244">**$title$**</span></span> | <span data-ttu-id="1bf54-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1bf54-245">AssemblyInfo</span></span> | <span data-ttu-id="1bf54-246">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="1bf54-246">AssemblyTitle</span></span> |
| <span data-ttu-id="1bf54-247">**$description$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-247">**$description$**</span></span> | <span data-ttu-id="1bf54-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1bf54-248">AssemblyInfo</span></span> | <span data-ttu-id="1bf54-249">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="1bf54-249">AssemblyDescription</span></span> |
| <span data-ttu-id="1bf54-250">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-250">**$copyright$**</span></span> | <span data-ttu-id="1bf54-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1bf54-251">AssemblyInfo</span></span> | <span data-ttu-id="1bf54-252">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="1bf54-252">AssemblyCopyright</span></span> |
| <span data-ttu-id="1bf54-253">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="1bf54-253">**$configuration$**</span></span> | <span data-ttu-id="1bf54-254">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="1bf54-254">Assembly DLL</span></span> | <span data-ttu-id="1bf54-255">用以建置組件的組態，預設為偵錯。</span><span class="sxs-lookup"><span data-stu-id="1bf54-255">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="1bf54-256">請注意，若要建立使用版本組態的套件，命令列上一律要使用 `-properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-256">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="1bf54-257">當您包含[組件檔](#including-assembly-files)和[內容檔](#including-content-files)時，也可使用權杖來解析路徑。</span><span class="sxs-lookup"><span data-stu-id="1bf54-257">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="1bf54-258">權杖和 MSBuild 屬性有相同的名稱，所以您才能夠根據目前的組建組態選取要包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-258">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="1bf54-259">例如，如果在 `.nuspec` 檔案中使用下列權杖：</span><span class="sxs-lookup"><span data-stu-id="1bf54-259">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="1bf54-260">而您建置的組件，其 `AssemblyName` 是在 MSBuild 中有 `Release` 組態的 `LoggingLibrary`，在套件的 `.nuspec` 檔案中產生的程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="1bf54-260">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="1bf54-261">相依性項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-261">Dependencies element</span></span>

<span data-ttu-id="1bf54-262">`<metadata>` 內的 `<dependencies>` 項目包含任意數目的 `<dependency>` 項目，可識別最上層套件依存的其他套件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-262">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="1bf54-263">每個 `<dependency>` 的屬性如下：</span><span class="sxs-lookup"><span data-stu-id="1bf54-263">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="1bf54-264">屬性</span><span class="sxs-lookup"><span data-stu-id="1bf54-264">Attribute</span></span> | <span data-ttu-id="1bf54-265">描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-265">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="1bf54-266">(必要) 相依性的套件識別碼，例如 "EntityFramework" 與 "NUnit"，是在套件頁面上顯示的套件 nuget.org 名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf54-266">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="1bf54-267">(必要) 可接受為相依性的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="1bf54-267">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="1bf54-268">如需確切的語法，請參閱[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-268">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="1bf54-269">include</span><span class="sxs-lookup"><span data-stu-id="1bf54-269">include</span></span> | <span data-ttu-id="1bf54-270">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要包含的相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-270">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="1bf54-271">預設值是 `all`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-271">The default value is `all`.</span></span> |
| <span data-ttu-id="1bf54-272">exclude</span><span class="sxs-lookup"><span data-stu-id="1bf54-272">exclude</span></span> | <span data-ttu-id="1bf54-273">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要排除的相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-273">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="1bf54-274">預設值是`build,analyzers`可能會覆寫。</span><span class="sxs-lookup"><span data-stu-id="1bf54-274">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="1bf54-275">但`content/ ContentFiles`也會隱含地被排除在最終的套件無法覆寫。</span><span class="sxs-lookup"><span data-stu-id="1bf54-275">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="1bf54-276">以 `exclude` 指定的標記優先於以 `include` 指定的標記。</span><span class="sxs-lookup"><span data-stu-id="1bf54-276">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="1bf54-277">例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="1bf54-277">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="1bf54-278">包含/排除標記</span><span class="sxs-lookup"><span data-stu-id="1bf54-278">Include/Exclude tag</span></span> | <span data-ttu-id="1bf54-279">目標的受影響資料夾</span><span class="sxs-lookup"><span data-stu-id="1bf54-279">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="1bf54-280">contentFiles</span><span class="sxs-lookup"><span data-stu-id="1bf54-280">contentFiles</span></span> | <span data-ttu-id="1bf54-281">內容</span><span class="sxs-lookup"><span data-stu-id="1bf54-281">Content</span></span> |
| <span data-ttu-id="1bf54-282">執行階段</span><span class="sxs-lookup"><span data-stu-id="1bf54-282">runtime</span></span> | <span data-ttu-id="1bf54-283">執行階段、資源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="1bf54-283">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="1bf54-284">compile</span><span class="sxs-lookup"><span data-stu-id="1bf54-284">compile</span></span> | <span data-ttu-id="1bf54-285">lib</span><span class="sxs-lookup"><span data-stu-id="1bf54-285">lib</span></span> |
| <span data-ttu-id="1bf54-286">build</span><span class="sxs-lookup"><span data-stu-id="1bf54-286">build</span></span> | <span data-ttu-id="1bf54-287">組建 (MSBuild props 和目標)</span><span class="sxs-lookup"><span data-stu-id="1bf54-287">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="1bf54-288">native</span><span class="sxs-lookup"><span data-stu-id="1bf54-288">native</span></span> | <span data-ttu-id="1bf54-289">native</span><span class="sxs-lookup"><span data-stu-id="1bf54-289">native</span></span> |
| <span data-ttu-id="1bf54-290">無</span><span class="sxs-lookup"><span data-stu-id="1bf54-290">none</span></span> | <span data-ttu-id="1bf54-291">無資料夾</span><span class="sxs-lookup"><span data-stu-id="1bf54-291">No folders</span></span> |
| <span data-ttu-id="1bf54-292">全部</span><span class="sxs-lookup"><span data-stu-id="1bf54-292">all</span></span> | <span data-ttu-id="1bf54-293">全部資料夾</span><span class="sxs-lookup"><span data-stu-id="1bf54-293">All folders</span></span> |

<span data-ttu-id="1bf54-294">例如，下列幾行程式碼指出 `PackageA`1.1.0 版或更高版本與 `PackageB` 1.x 版的相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-294">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="1bf54-295">下列幾行程式碼指出相同套件的相依性，但指定要包含 `PackageA` 的 `contentFiles` 和 `build` 資料夾，以及 `PackageB` 的 `native` 和 `compile` 資料夾以外的所有一切</span><span class="sxs-lookup"><span data-stu-id="1bf54-295">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="1bf54-296">注意：從專案使用 `nuget spec` 建立 `.nuspec` 時，存在於該專案中的相依性會自動包含在產生的 `.nuspec` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-296">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="1bf54-297">相依性群組</span><span class="sxs-lookup"><span data-stu-id="1bf54-297">Dependency groups</span></span>

<span data-ttu-id="1bf54-298">*2.0+ 版*</span><span class="sxs-lookup"><span data-stu-id="1bf54-298">*Version 2.0+*</span></span>

<span data-ttu-id="1bf54-299">當作單一一般清單的替代方案，您可以使用 `<dependencies>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-299">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="1bf54-300">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<dependency>` 項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-300">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="1bf54-301">當目標 Framework 與專案的 Framework 設定檔相容時，會同時安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="1bf54-301">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1bf54-302">沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援相依性清單。</span><span class="sxs-lookup"><span data-stu-id="1bf54-302">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="1bf54-303">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-303">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1bf54-304">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="1bf54-304">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="1bf54-305">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="1bf54-305">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="1bf54-306">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-306">Explicit assembly references</span></span>

<span data-ttu-id="1bf54-307">`<references>` 項目明確指定使用套件時，目標專案應該參考的組件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-307">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="1bf54-308">有此項目時，NuGet 只會將參考新增至列出的組件。它不會在套件的 `lib` 資料夾中新增任何其他組件的參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-308">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="1bf54-309">例如，以下 `<references>` 項目會指示 NuGet 只將參考新增至 `xunit.dll` 和 `xunit.extensions.dll`，即使套件中有其他組件：</span><span class="sxs-lookup"><span data-stu-id="1bf54-309">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="1bf54-310">明確參考通常只用於設計階段的組件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-310">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="1bf54-311">例如使用 [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts) (程式碼合約) 時，合約組件必須在它們擴大的執行階段組件旁邊，讓 Visual Studio 可以找到它們，但是合約組件不需要被專案參考，或複製到專案的 `bin` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1bf54-311">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="1bf54-312">同樣地，明確參考可以用於單元測試 Framework ，例如 XUnit，這需要它的工具組件位在執行階段組件旁邊，但它們不需要包含為專案參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-312">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="1bf54-313">參考群組</span><span class="sxs-lookup"><span data-stu-id="1bf54-313">Reference groups</span></span>

<span data-ttu-id="1bf54-314">當作單一一般清單的替代方案，您可以使用 `<references>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-314">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="1bf54-315">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-315">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="1bf54-316">當目標 Framework 與專案的 Framework 設定檔相容時，這些參考會新增至專案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-316">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1bf54-317">沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援參考清單。</span><span class="sxs-lookup"><span data-stu-id="1bf54-317">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="1bf54-318">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-318">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1bf54-319">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="1bf54-319">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="1bf54-320">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="1bf54-320">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="1bf54-321">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="1bf54-321">Framework assembly references</span></span>

<span data-ttu-id="1bf54-322">Framework 組件屬於 .NET Framework，應該已經在任何指定電腦的全域組件快取 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-322">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="1bf54-323">找出 `<frameworkAssemblies>` 項目內的這些組件，套件可以確保所需的參考已新增至事件的專案，該專案尚未有這類參考。</span><span class="sxs-lookup"><span data-stu-id="1bf54-323">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="1bf54-324">當然，這類組件不直接包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-324">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="1bf54-325">`<frameworkAssemblies>` 項目包含零或多個 `<frameworkAssembly>` 項目，它們每一個都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="1bf54-325">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="1bf54-326">屬性</span><span class="sxs-lookup"><span data-stu-id="1bf54-326">Attribute</span></span> | <span data-ttu-id="1bf54-327">描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-327">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1bf54-328">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="1bf54-328">**assemblyName**</span></span> | <span data-ttu-id="1bf54-329">(必要) 完整組件名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf54-329">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="1bf54-330">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="1bf54-330">**targetFramework**</span></span> | <span data-ttu-id="1bf54-331">(選擇性) 指定要套用這個參考的目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="1bf54-331">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="1bf54-332">如果省略，則表示參考適用於所有 Framework。</span><span class="sxs-lookup"><span data-stu-id="1bf54-332">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="1bf54-333">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-333">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="1bf54-334">下列範例會顯示所有目標 Framework 的 `System.Net` 參考，以及僅供 .NET Framework 4.0 使用的 `System.ServiceModel` 參考：</span><span class="sxs-lookup"><span data-stu-id="1bf54-334">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="1bf54-335">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-335">Including assembly files</span></span>

<span data-ttu-id="1bf54-336">如果遵循[建立套件](../create-packages/creating-a-package.md)中所述的慣例，即不必在 `.nuspec` 檔案中明確指定檔案清單。</span><span class="sxs-lookup"><span data-stu-id="1bf54-336">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="1bf54-337">`nuget pack` 命令會自動挑選必要的檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-337">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="1bf54-338">當套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，「排除」那些名為 `.resources.dll` 的參考，因為它們假設是當地語系化的附屬組件。</span><span class="sxs-lookup"><span data-stu-id="1bf54-338">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="1bf54-339">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-339">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="1bf54-340">為略過這項自動行為並明確控制套件要包含哪些檔案，請放置 `<files>` 項目當作 `<package>` 的子系 (和 `<metadata>` 的同層級)，找出每個有不同 `<file>` 項目的檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-340">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="1bf54-341">例如: </span><span class="sxs-lookup"><span data-stu-id="1bf54-341">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="1bf54-342">使用 NuGet 2.x 及更舊版本，並規劃使用 `packages.config`；在安裝套件時，也會使用 `<files>` 項目包含不可變的內容檔。</span><span class="sxs-lookup"><span data-stu-id="1bf54-342">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="1bf54-343">使用 NuGet 3.3+ 和專案 PackageReference，則改用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="1bf54-343">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="1bf54-344">如需詳細資料，請參閱下文中的[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-344">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="1bf54-345">檔案項目屬性</span><span class="sxs-lookup"><span data-stu-id="1bf54-345">File element attributes</span></span>

<span data-ttu-id="1bf54-346">每個 `<file>` 項目都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="1bf54-346">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="1bf54-347">屬性</span><span class="sxs-lookup"><span data-stu-id="1bf54-347">Attribute</span></span> | <span data-ttu-id="1bf54-348">描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-348">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1bf54-349">**src**</span><span class="sxs-lookup"><span data-stu-id="1bf54-349">**src**</span></span> | <span data-ttu-id="1bf54-350">要包含的檔案位置，會受到 `exclude` 屬性指定的排除項目約束。</span><span class="sxs-lookup"><span data-stu-id="1bf54-350">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1bf54-351">路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="1bf54-351">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="1bf54-352">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf54-352">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1bf54-353">**目標**</span><span class="sxs-lookup"><span data-stu-id="1bf54-353">**target**</span></span> | <span data-ttu-id="1bf54-354">套件內資料夾的相對路徑是放置原始程式檔的位置，其開頭必須是 `lib`、`content`、`build` 或 `tools`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-354">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="1bf54-355">請參閱[從慣例的工作目錄建立 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-355">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="1bf54-356">**排除**</span><span class="sxs-lookup"><span data-stu-id="1bf54-356">**exclude**</span></span> | <span data-ttu-id="1bf54-357">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="1bf54-357">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1bf54-358">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf54-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="1bf54-359">範例</span><span class="sxs-lookup"><span data-stu-id="1bf54-359">Examples</span></span>

<span data-ttu-id="1bf54-360">**單一組件**</span><span class="sxs-lookup"><span data-stu-id="1bf54-360">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="1bf54-361">**目標 Framework 的特定單一組件**</span><span class="sxs-lookup"><span data-stu-id="1bf54-361">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="1bf54-362">**使用萬用字元的 DLL 集合**</span><span class="sxs-lookup"><span data-stu-id="1bf54-362">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="1bf54-363">**不同 Framework 的 DLL**</span><span class="sxs-lookup"><span data-stu-id="1bf54-363">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="1bf54-364">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="1bf54-364">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="1bf54-365">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-365">Including content files</span></span>

<span data-ttu-id="1bf54-366">內容檔是不可變的檔案，套件必須將它們包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="1bf54-366">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="1bf54-367">因為不可變，所以取用專案不宜修改它們。</span><span class="sxs-lookup"><span data-stu-id="1bf54-367">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="1bf54-368">內容檔範例包括：</span><span class="sxs-lookup"><span data-stu-id="1bf54-368">Example content files include:</span></span>

- <span data-ttu-id="1bf54-369">內嵌為資源的映像</span><span class="sxs-lookup"><span data-stu-id="1bf54-369">Images that are embedded as resources</span></span>
- <span data-ttu-id="1bf54-370">已編譯原始程式檔</span><span class="sxs-lookup"><span data-stu-id="1bf54-370">Source files that are already compiled</span></span>
- <span data-ttu-id="1bf54-371">需要以專案的組建輸出包含的指令碼</span><span class="sxs-lookup"><span data-stu-id="1bf54-371">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="1bf54-372">套件的組態檔必須包含在專案中，但不需要專門針對任何專案變更</span><span class="sxs-lookup"><span data-stu-id="1bf54-372">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="1bf54-373">內容檔包含在使用 `<files>` 項目的套件中，指定 `target` 屬性中的 `content` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1bf54-373">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="1bf54-374">不過，使用 PackageReference 在專案中安裝套件時，會忽略這類檔案，改用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="1bf54-374">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="1bf54-375">為取得取用專案的最大相容性，套件應該在兩個項目中都指定內容檔。</span><span class="sxs-lookup"><span data-stu-id="1bf54-375">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="1bf54-376">內容檔使用 files 項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-376">Using the files element for content files</span></span>

<span data-ttu-id="1bf54-377">內容檔只要使用和組件檔相同的格式即可，但要在 `target` 屬性中指定 `content` 作為基底資料夾，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1bf54-377">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="1bf54-378">**基本內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-378">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="1bf54-379">**具有目錄結構的內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-379">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="1bf54-380">**目標 Framework 的特定內容檔案**</span><span class="sxs-lookup"><span data-stu-id="1bf54-380">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="1bf54-381">**複製到資料夾，名稱中有點的內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-381">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="1bf54-382">在此情況下，NuGet 會看到 `target` 的副檔名與 `src` 的副檔名不相符，因此會將 `target` 名稱的該部分視為資料夾：</span><span class="sxs-lookup"><span data-stu-id="1bf54-382">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="1bf54-383">**無副檔名的內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-383">**Content files without extensions**</span></span>

<span data-ttu-id="1bf54-384">若要包含不含副檔名的檔案，請使用 `*` 或 `**` 萬用字元：</span><span class="sxs-lookup"><span data-stu-id="1bf54-384">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="1bf54-385">**有深路徑和深層目標的內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-385">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="1bf54-386">在此情況下，因為原始程式檔的副檔名和目標相符，所以 NuGet 會假設目標是檔案名稱，不是資料夾：</span><span class="sxs-lookup"><span data-stu-id="1bf54-386">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="1bf54-387">**重新命名套件中的內容檔**</span><span class="sxs-lookup"><span data-stu-id="1bf54-387">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="1bf54-388">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="1bf54-388">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="1bf54-389">內容檔使用 contentFiles 項目</span><span class="sxs-lookup"><span data-stu-id="1bf54-389">Using the contentFiles element for content files</span></span>

<span data-ttu-id="1bf54-390">*NuGet 4.0+ 與 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="1bf54-390">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="1bf54-391">根據預設，套件會將內容放在 `contentFiles` 資料夾 (請參閱下文)，而 `nuget pack` 包含使用預設屬性資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-391">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="1bf54-392">在此情況下，`.nuspec` 完全不需要包含 `contentFiles` 節點。</span><span class="sxs-lookup"><span data-stu-id="1bf54-392">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="1bf54-393">為控制包含哪些檔案，`<contentFiles>` 項目要指定 `<files>` 項目的集合，找出正確的檔案。</span><span class="sxs-lookup"><span data-stu-id="1bf54-393">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="1bf54-394">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定：</span><span class="sxs-lookup"><span data-stu-id="1bf54-394">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="1bf54-395">屬性</span><span class="sxs-lookup"><span data-stu-id="1bf54-395">Attribute</span></span> | <span data-ttu-id="1bf54-396">描述</span><span class="sxs-lookup"><span data-stu-id="1bf54-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1bf54-397">**include**</span><span class="sxs-lookup"><span data-stu-id="1bf54-397">**include**</span></span> | <span data-ttu-id="1bf54-398">(必要) 要包含的檔案位置，受限於 `exclude` 屬性所指定的排除項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-398">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1bf54-399">路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="1bf54-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="1bf54-400">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf54-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1bf54-401">**排除**</span><span class="sxs-lookup"><span data-stu-id="1bf54-401">**exclude**</span></span> | <span data-ttu-id="1bf54-402">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="1bf54-402">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1bf54-403">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf54-403">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1bf54-404">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="1bf54-404">**buildAction**</span></span> | <span data-ttu-id="1bf54-405">要指派給 MSBuild 內容項目的建置動作，例如 `Content`、`None`、`Embedded Resource`、`Compile` 等等。預設為 `Compile`。</span><span class="sxs-lookup"><span data-stu-id="1bf54-405">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="1bf54-406">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="1bf54-406">**copyToOutput**</span></span> | <span data-ttu-id="1bf54-407">布林值，指出是否要將內容項目複製到組建 （或發行） 的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="1bf54-407">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="1bf54-408">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="1bf54-408">The default is false.</span></span> |
| <span data-ttu-id="1bf54-409">**flatten**</span><span class="sxs-lookup"><span data-stu-id="1bf54-409">**flatten**</span></span> | <span data-ttu-id="1bf54-410">布林值，指出要將內容項目複製到組建輸出的單一資料夾 (true)，或保留套件中的資料夾結構 (false)。</span><span class="sxs-lookup"><span data-stu-id="1bf54-410">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="1bf54-411">這個旗標僅適用於將 copyToOutput 旗標設為 true 時。</span><span class="sxs-lookup"><span data-stu-id="1bf54-411">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="1bf54-412">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="1bf54-412">The default is false.</span></span> |

<span data-ttu-id="1bf54-413">安裝套件時，NuGet 會由上而下套用 `<contentFiles>` 的子項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-413">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="1bf54-414">如有多個項目符合同一檔案，則套用所有項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-414">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="1bf54-415">如果相同的屬性發生衝突，則最上層項目會覆寫較低的項目。</span><span class="sxs-lookup"><span data-stu-id="1bf54-415">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="1bf54-416">套件資料夾結構</span><span class="sxs-lookup"><span data-stu-id="1bf54-416">Package folder structure</span></span>

<span data-ttu-id="1bf54-417">套件專案應該結構化使用下列模式的內容：</span><span class="sxs-lookup"><span data-stu-id="1bf54-417">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="1bf54-418">`codeLanguages` 可能是 `cs`、`vb`、`fs`、`any`，或指定的 `$(ProjectLanguage)` 小寫對等項</span><span class="sxs-lookup"><span data-stu-id="1bf54-418">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="1bf54-419">`TxM` 是 NuGet 支援的任何合法目標 Framework Moniker (請參閱[目標 Framework](../reference/target-frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="1bf54-419">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="1bf54-420">這個語法的結尾可以附加任何資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="1bf54-420">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="1bf54-421">例如: </span><span class="sxs-lookup"><span data-stu-id="1bf54-421">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="1bf54-422">空資料夾可以使用 `.` 選擇不提供特定語言和 TxM 組合的內容，例如：</span><span class="sxs-lookup"><span data-stu-id="1bf54-422">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="1bf54-423">contentFiles 區段範例</span><span class="sxs-lookup"><span data-stu-id="1bf54-423">Example contentFiles section</span></span>

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="1bf54-424">範例 nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="1bf54-424">Example nuspec files</span></span>

<span data-ttu-id="1bf54-425">**簡單的 `.nuspec` 不指定相依性或檔案**</span><span class="sxs-lookup"><span data-stu-id="1bf54-425">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="1bf54-426">**具有相依性的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="1bf54-426">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="1bf54-427">**具有檔案的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="1bf54-427">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="1bf54-428">**具有 Framework 組件的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="1bf54-428">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="1bf54-429">在此範例中，特定專案目標會安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="1bf54-429">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="1bf54-430">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="1bf54-430">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="1bf54-431">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="1bf54-431">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="1bf54-432">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="1bf54-432">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="1bf54-433">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="1bf54-433">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="1bf54-434">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="1bf54-434">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
