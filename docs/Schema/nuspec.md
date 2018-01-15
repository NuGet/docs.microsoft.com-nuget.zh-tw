---
title: "NuGet 的 .nuspec 檔案參考 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d4a4db9b-5c2d-46aa-9107-d2b01733df7c
description: ".nuspec 檔案包含建置套件時使用的套件中繼資料，並向套件取用者提供資訊。"
keywords: "nuspec 參考, NuGet 套件中繼資料, NuGet 套件資訊清單, nuspec 結構描述"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: cd5b7c79ad0af07b167e062d4a2f5142ef2d718a
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="2a824-104">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="2a824-104">.nuspec reference</span></span>

<span data-ttu-id="2a824-105">`.nuspec` 檔案是包含套件中繼資料的 XML 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="2a824-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="2a824-106">此資訊清單用來建置套件和向取用者提供資訊。</span><span class="sxs-lookup"><span data-stu-id="2a824-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="2a824-107">資訊清單一律包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="2a824-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="2a824-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="2a824-108">In this topic:</span></span>

- [<span data-ttu-id="2a824-109">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="2a824-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="2a824-110">[取代權杖](#replacement-tokens) (搭配 Visual Studio 專案使用時)</span><span class="sxs-lookup"><span data-stu-id="2a824-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="2a824-111">相依性</span><span class="sxs-lookup"><span data-stu-id="2a824-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="2a824-112">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="2a824-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="2a824-113">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="2a824-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="2a824-114">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="2a824-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="2a824-115">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="2a824-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="2a824-116">範例</span><span class="sxs-lookup"><span data-stu-id="2a824-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="2a824-117">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="2a824-117">General form and schema</span></span>

<span data-ttu-id="2a824-118">目前的 `nuspec.xsd` 結構描述檔案位於 [NuGet GitHub 存放庫](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)。</span><span class="sxs-lookup"><span data-stu-id="2a824-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="2a824-119">在此結構描述內，`.nuspec` 檔案有下列一般格式：</span><span class="sxs-lookup"><span data-stu-id="2a824-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="2a824-120">為能清晰呈現結構描述，請在 Visual Studio 中以設計模式開啟結構描述檔案，按一下 [XML 結構描述總管] 連結。</span><span class="sxs-lookup"><span data-stu-id="2a824-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="2a824-121">或者，將檔案開啟為程式碼，在編輯器中按一下滑鼠右鍵，選取 [Show XML Schema Explorer] (顯示 XML 結構描述總管)。</span><span class="sxs-lookup"><span data-stu-id="2a824-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="2a824-122">任一方式都可取得類似以下的檢視 (大部分展開時)：</span><span class="sxs-lookup"><span data-stu-id="2a824-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![開啟了 nuspec.xsd 的 Visual Studio 結構描述總管](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="2a824-124">中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-124">Metadata attributes</span></span>

<span data-ttu-id="2a824-125">`<metadata>` 項目支援下表所描述的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a824-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="2a824-126">屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-126">Attribute</span></span> | <span data-ttu-id="2a824-127">必要</span><span class="sxs-lookup"><span data-stu-id="2a824-127">Required</span></span> | <span data-ttu-id="2a824-128">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="2a824-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="2a824-129">**minClientVersion**</span></span> | <span data-ttu-id="2a824-130">否</span><span class="sxs-lookup"><span data-stu-id="2a824-130">No</span></span> | <span data-ttu-id="2a824-131">*(2.5+)* 指定可安裝此套件的最低 NuGet 用戶端版本，此作業是由 nuget.exe 和 Visual Studio 套件管理員強制執行。</span><span class="sxs-lookup"><span data-stu-id="2a824-131">*(2.5+)* Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="2a824-132">每當套件依存於 NuGet 用戶端新增的 `.nuspec` 檔案特定功能時，就會使用。</span><span class="sxs-lookup"><span data-stu-id="2a824-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="2a824-133">例如，套件使用的 `developmentDependency` 屬性應該為 `minClientVersion` 指定 "2.8"。</span><span class="sxs-lookup"><span data-stu-id="2a824-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="2a824-134">同樣地，使用 `contentFiles` 項目的套件 (請參閱下一節) 應將 `minClientVersion` 設定成 "3.3"。</span><span class="sxs-lookup"><span data-stu-id="2a824-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="2a824-135">另請注意，因為 2.5 之前的 NuGet 用戶端無法辨識此旗標，所以它們「一律」拒絕安裝套件，無論 `minClientVersion` 包含什麼。</span><span class="sxs-lookup"><span data-stu-id="2a824-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="2a824-136">必要的中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="2a824-136">Required metadata elements</span></span>

<span data-ttu-id="2a824-137">雖然下列項目是套件的最低需求，但您應該考慮新增[選擇性中繼資料項目](#optional-metadata-elements)以改善開發人員使用套件的整體體驗。</span><span class="sxs-lookup"><span data-stu-id="2a824-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="2a824-138">這些項目必須出現在 `<metadata>` 項目中。</span><span class="sxs-lookup"><span data-stu-id="2a824-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="2a824-139">元素</span><span class="sxs-lookup"><span data-stu-id="2a824-139">Element</span></span> | <span data-ttu-id="2a824-140">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-141">**id**</span><span class="sxs-lookup"><span data-stu-id="2a824-141">**id**</span></span> | <span data-ttu-id="2a824-142">不區分大小寫的套件識別碼，在整個 nuget.org 或套件所在的任何組件庫中都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2a824-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="2a824-143">識別碼可能不包含對 URL 而言無效的空格或字元，而且通常會遵循 .NET 命名空間規則。</span><span class="sxs-lookup"><span data-stu-id="2a824-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="2a824-144">如需指導方針，請參閱[選擇唯一的套件識別碼](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="2a824-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="2a824-145">**version**</span><span class="sxs-lookup"><span data-stu-id="2a824-145">**version**</span></span> | <span data-ttu-id="2a824-146">套件版本，遵循 *major.minor.patch* 模式。</span><span class="sxs-lookup"><span data-stu-id="2a824-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="2a824-147">版本號碼可以包含預先發行版本的後置詞，如[套件版本控制](../reference/package-versioning.md#pre-release-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="2a824-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="2a824-148">**description**</span><span class="sxs-lookup"><span data-stu-id="2a824-148">**description**</span></span> | <span data-ttu-id="2a824-149">UI 顯示中的套件詳細描述。</span><span class="sxs-lookup"><span data-stu-id="2a824-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="2a824-150">**作者**</span><span class="sxs-lookup"><span data-stu-id="2a824-150">**authors**</span></span> | <span data-ttu-id="2a824-151">以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些名稱會顯示在 nuget.org 的 NuGet 組件庫中，並用來交互參照相同作者的其他套件。</span><span class="sxs-lookup"><span data-stu-id="2a824-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="2a824-152">選擇性中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="2a824-152">Optional metadata elements</span></span>

<span data-ttu-id="2a824-153">這些元素可能會出現在 `<metadata>` 元素內。</span><span class="sxs-lookup"><span data-stu-id="2a824-153">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="2a824-154">單一項目</span><span class="sxs-lookup"><span data-stu-id="2a824-154">Single elements</span></span>

| <span data-ttu-id="2a824-155">元素</span><span class="sxs-lookup"><span data-stu-id="2a824-155">Element</span></span> | <span data-ttu-id="2a824-156">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-157">**標題**</span><span class="sxs-lookup"><span data-stu-id="2a824-157">**title**</span></span> | <span data-ttu-id="2a824-158">套件的易記標題，通常會用於 UI 顯示，以及 nuget.org 和 Visual Studio 套件管理員中。</span><span class="sxs-lookup"><span data-stu-id="2a824-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="2a824-159">如未指定，則使用套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a824-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="2a824-160">**擁有者**</span><span class="sxs-lookup"><span data-stu-id="2a824-160">**owners**</span></span> | <span data-ttu-id="2a824-161">以逗號分隔的套件作者清單，使用 nuget.org 上的設定檔名稱。這通常和 `authors` 是同一份清單，將套件上傳至 nuget.org 時會忽略。請參閱[在 nuget.org 上管理套件擁有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="2a824-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="2a824-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="2a824-162">**projectUrl**</span></span> | <span data-ttu-id="2a824-163">套件首頁的 URL，通常會顯示在 UI 顯示及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="2a824-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="2a824-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="2a824-164">**licenseUrl**</span></span> | <span data-ttu-id="2a824-165">套件授權的 URL，通常會顯示在 UI 顯示及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="2a824-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="2a824-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="2a824-166">**iconUrl**</span></span> | <span data-ttu-id="2a824-167">具有透明背景之 64x64 映像的 URL，該映像會用作套件在 UI 顯示中的圖示。</span><span class="sxs-lookup"><span data-stu-id="2a824-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="2a824-168">確定這個項目包含「直接映像 URL」，不是包含影像的網頁 URL。</span><span class="sxs-lookup"><span data-stu-id="2a824-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="2a824-169">例如，若要使用 GitHub 的映像，請使用原始檔 URL，如 `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`。</span><span class="sxs-lookup"><span data-stu-id="2a824-169">For example, to use an image from GitHub, use the raw file URL like `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span></span> |
| <span data-ttu-id="2a824-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="2a824-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="2a824-171">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="2a824-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="2a824-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="2a824-172">**developmentDependency**</span></span> | <span data-ttu-id="2a824-173">*(2.8+)* 布林值，指定套件是否標示為僅限開發相依性，這可防止套件包含為其他套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="2a824-174">**summary**</span><span class="sxs-lookup"><span data-stu-id="2a824-174">**summary**</span></span> | <span data-ttu-id="2a824-175">UI 顯示中的套件簡短描述。</span><span class="sxs-lookup"><span data-stu-id="2a824-175">A short description of the package for UI display.</span></span> <span data-ttu-id="2a824-176">如果省略，即使用截斷版本的 `description`。</span><span class="sxs-lookup"><span data-stu-id="2a824-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="2a824-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="2a824-177">**releaseNotes**</span></span> | <span data-ttu-id="2a824-178">*(1.5+)* 此版本套件中的變更描述，通常用於 Visual Studio Package Manager 的 [更新] 索引標籤等 UI 中，以取代套件描述。</span><span class="sxs-lookup"><span data-stu-id="2a824-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="2a824-179">**著作權**</span><span class="sxs-lookup"><span data-stu-id="2a824-179">**copyright**</span></span> | <span data-ttu-id="2a824-180">*(1.5+)* 套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a824-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="2a824-181">**language**</span><span class="sxs-lookup"><span data-stu-id="2a824-181">**language**</span></span> | <span data-ttu-id="2a824-182">套件的地區設定識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a824-182">The locale ID for the package.</span></span> <span data-ttu-id="2a824-183">請參閱[建立當地語系化的套件](../create-packages/creating-localized-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="2a824-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="2a824-184">**標記**</span><span class="sxs-lookup"><span data-stu-id="2a824-184">**tags**</span></span> | <span data-ttu-id="2a824-185">以逗號分隔的標記與關鍵字清單，描述套件並透過搜尋和篩選協助探索套件。</span><span class="sxs-lookup"><span data-stu-id="2a824-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="2a824-186">**能否提供服務**</span><span class="sxs-lookup"><span data-stu-id="2a824-186">**serviceable**</span></span> | <span data-ttu-id="2a824-187">*(3.3+)* 僅供內部 NuGet 使用。</span><span class="sxs-lookup"><span data-stu-id="2a824-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="2a824-188">集合項目</span><span class="sxs-lookup"><span data-stu-id="2a824-188">Collection elements</span></span>

| <span data-ttu-id="2a824-189">元素</span><span class="sxs-lookup"><span data-stu-id="2a824-189">Element</span></span> | <span data-ttu-id="2a824-190">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="2a824-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="2a824-191">**packageTypes**</span></span> | <span data-ttu-id="2a824-192">*(3.3+)* 零或多個 `<packageType>` 項目的集合，指定非傳統相依性套件以外的套件類型。</span><span class="sxs-lookup"><span data-stu-id="2a824-192">*(3.3+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="2a824-193">每個 packageType 都有「名稱」和「版本」屬性。</span><span class="sxs-lookup"><span data-stu-id="2a824-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="2a824-194">請參閱[設定套件類型](../create-packages/creating-a-package.md#setting-a-package-type)。</span><span class="sxs-lookup"><span data-stu-id="2a824-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="2a824-195">**相依性**</span><span class="sxs-lookup"><span data-stu-id="2a824-195">**dependencies**</span></span> | <span data-ttu-id="2a824-196">零或多個 `<dependency>` 項目的集合，指定套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="2a824-197">每個相依性都有「識別碼」、「版本」、「包含」(3.x+) 和「排除」(3.x+) 屬性。</span><span class="sxs-lookup"><span data-stu-id="2a824-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="2a824-198">請參閱下文的[相依性](#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="2a824-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="2a824-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="2a824-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="2a824-200">*(1.2+)* 零或多個 `<frameworkAssembly>` 項目的集合，識別此套件需要的 .NET Framework 組件參考，它們可確保參考會新增至取用套件的專案。</span><span class="sxs-lookup"><span data-stu-id="2a824-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="2a824-201">每個 frameworkAssembly 都有 *assemblyName* 和 *targetFramework* 屬性。</span><span class="sxs-lookup"><span data-stu-id="2a824-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="2a824-202">請參閱下文的[指定 Framework 組件參考 GAC](#specifying-framework-assembly-references-gac)。</span><span class="sxs-lookup"><span data-stu-id="2a824-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="2a824-203">**參考**</span><span class="sxs-lookup"><span data-stu-id="2a824-203">**references**</span></span> | <span data-ttu-id="2a824-204">*(1.5+)* 在套件的 `lib` 資料夾中命名組件的零或多個 `<reference>` 項目集合，這些項目可新增為專案參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="2a824-205">每個參考都有 *file* 屬性。</span><span class="sxs-lookup"><span data-stu-id="2a824-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="2a824-206">`<references>` 也可以包含具有 *targetFramework* 屬性的 `<group>` 項目，然後即可包含 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="2a824-207">如果省略，就會包含 `lib` 中的所有參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="2a824-208">請參閱下文中的[指定明確的組件參考](#specifying-explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="2a824-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="2a824-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="2a824-209">**contentFiles**</span></span> | <span data-ttu-id="2a824-210">*(3.3+)* `<files>` 項目的集合，可識別要包含在取用專案中的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="2a824-211">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定。</span><span class="sxs-lookup"><span data-stu-id="2a824-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="2a824-212">請參閱下文中的[指定要包含在套件中的檔案](#specifying-files-to-include-in-the-package)。</span><span class="sxs-lookup"><span data-stu-id="2a824-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="2a824-213">Files 項目</span><span class="sxs-lookup"><span data-stu-id="2a824-213">Files element</span></span>

<span data-ttu-id="2a824-214">`<package>` 節點可包含一個與 `<metadata>` 同層級的 `<files>` 節點，及/或一個 `<metadata>` 下的 `<contentFiles>` 子系，指定要在套件中包含哪些組件和內容檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="2a824-215">如需詳細資料，請參閱本主題下文中的[包含組件檔](#including-assembly-files)和[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="2a824-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="2a824-216">取代權杖</span><span class="sxs-lookup"><span data-stu-id="2a824-216">Replacement tokens</span></span>

<span data-ttu-id="2a824-217">建立套件時，[`nuget pack` 命令](../tools/cli-ref-pack.md) 會使用來自專案檔的值或來自 `pack` 命令的 `-properties` 參數值，取代 `.nuspec` 檔案之 `<metadata>` 節點的 $ 分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="2a824-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="2a824-218">在命令列中，您可以使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定權杖值。</span><span class="sxs-lookup"><span data-stu-id="2a824-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="2a824-219">例如，您可以在 `.nuspec` 中使用權杖，例如 `$owners$` 和 `$desc$`，並在封裝階段提供值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2a824-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="2a824-220">若要使用專案中的值，請指定下表中描述的權杖 (AssemblyInfo 是指 `Properties` 中的檔案，例如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`)。</span><span class="sxs-lookup"><span data-stu-id="2a824-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="2a824-221">若要使用這些權杖，請執行 `nuget pack` 與專案檔，非僅 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="2a824-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="2a824-222">例如，使用下列命令時，專案的 `AssemblyName` 和 `AssemblyVersion` 值會取代為 `.nuspec` 檔案中的 `$id$` 和 `$version$` 權杖：</span><span class="sxs-lookup"><span data-stu-id="2a824-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="2a824-223">通常，當您擁有專案時，一開始會使用自動包含這些標準權杖一部分的 `nuget spec MyProject.csproj` 來建立 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="2a824-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="2a824-224">不過，如果專案沒有所需之 `.nuspec` 項目的值，則 `nuget pack` 會失敗。</span><span class="sxs-lookup"><span data-stu-id="2a824-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="2a824-225">此外，如果變更專案值，請務必在建立套件前重建；使用 pack 命令的 `build` 參數很容易完成此作業。</span><span class="sxs-lookup"><span data-stu-id="2a824-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="2a824-226">除 `$configuration$` 以外，專案中值的使用順序優先於任何指派給命令列上相同權杖的值。</span><span class="sxs-lookup"><span data-stu-id="2a824-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="2a824-227">語彙基元</span><span class="sxs-lookup"><span data-stu-id="2a824-227">Token</span></span> | <span data-ttu-id="2a824-228">值來源</span><span class="sxs-lookup"><span data-stu-id="2a824-228">Value source</span></span> | <span data-ttu-id="2a824-229">值</span><span class="sxs-lookup"><span data-stu-id="2a824-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="2a824-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="2a824-230">**$id$**</span></span> | <span data-ttu-id="2a824-231">專案檔</span><span class="sxs-lookup"><span data-stu-id="2a824-231">Project file</span></span> | <span data-ttu-id="2a824-232">來自專案檔的 AssemblyName</span><span class="sxs-lookup"><span data-stu-id="2a824-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="2a824-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="2a824-233">**$version$**</span></span> | <span data-ttu-id="2a824-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2a824-234">AssemblyInfo</span></span> | <span data-ttu-id="2a824-235">如有則為 AssemblyInformationalVersion，否則為 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="2a824-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="2a824-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="2a824-236">**$author$**</span></span> | <span data-ttu-id="2a824-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2a824-237">AssemblyInfo</span></span> | <span data-ttu-id="2a824-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="2a824-238">AssemblyCompany</span></span> |
| <span data-ttu-id="2a824-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="2a824-239">**$description$**</span></span> | <span data-ttu-id="2a824-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2a824-240">AssemblyInfo</span></span> | <span data-ttu-id="2a824-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="2a824-241">AssemblyDescription</span></span> |
| <span data-ttu-id="2a824-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="2a824-242">**$copyright$**</span></span> | <span data-ttu-id="2a824-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="2a824-243">AssemblyInfo</span></span> | <span data-ttu-id="2a824-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="2a824-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="2a824-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="2a824-245">**$configuration$**</span></span> | <span data-ttu-id="2a824-246">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="2a824-246">Assembly DLL</span></span> | <span data-ttu-id="2a824-247">用以建置組件的組態，預設為偵錯。</span><span class="sxs-lookup"><span data-stu-id="2a824-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="2a824-248">請注意，若要建立使用版本組態的套件，命令列上一律要使用 `-properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="2a824-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="2a824-249">當您包含[組件檔](#including-assembly-files)和[內容檔](#including-content-files)時，也可使用權杖來解析路徑。</span><span class="sxs-lookup"><span data-stu-id="2a824-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="2a824-250">權杖和 MSBuild 屬性有相同的名稱，所以您才能夠根據目前的組建組態選取要包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="2a824-251">例如，如果在 `.nuspec` 檔案中使用下列權杖：</span><span class="sxs-lookup"><span data-stu-id="2a824-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="2a824-252">而您建置的組件，其 `AssemblyName` 是在 MSBuild 中有 `Release` 組態的 `LoggingLibrary`，在套件的 `.nuspec` 檔案中產生的程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="2a824-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="2a824-253">相依性</span><span class="sxs-lookup"><span data-stu-id="2a824-253">Dependencies</span></span>

<span data-ttu-id="2a824-254">`<metadata>` 內的 `<dependencies>` 項目包含任意數目的 `<dependency>` 項目，可識別最上層套件依存的其他套件。</span><span class="sxs-lookup"><span data-stu-id="2a824-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="2a824-255">每個 `<dependency>` 的屬性如下：</span><span class="sxs-lookup"><span data-stu-id="2a824-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="2a824-256">屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-256">Attribute</span></span> | <span data-ttu-id="2a824-257">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-257">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="2a824-258">(必要) 相依性的套件識別碼，例如 "EntityFramework" 與 "NUnit"，是在套件頁面上顯示的套件 nuget.org 名稱。</span><span class="sxs-lookup"><span data-stu-id="2a824-258">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="2a824-259">(必要) 可接受為相依性的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="2a824-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="2a824-260">如需確切的語法，請參閱[套件版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="2a824-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="2a824-261">include</span><span class="sxs-lookup"><span data-stu-id="2a824-261">include</span></span> | <span data-ttu-id="2a824-262">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要包含的相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="2a824-263">預設值是 `none`。</span><span class="sxs-lookup"><span data-stu-id="2a824-263">The default value is `none`.</span></span> |
| <span data-ttu-id="2a824-264">exclude</span><span class="sxs-lookup"><span data-stu-id="2a824-264">exclude</span></span> | <span data-ttu-id="2a824-265">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要排除的相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="2a824-266">預設值為 `all`。</span><span class="sxs-lookup"><span data-stu-id="2a824-266">The  default value is `all`.</span></span> <span data-ttu-id="2a824-267">以 `exclude` 指定的標記優先於以 `include` 指定的標記。</span><span class="sxs-lookup"><span data-stu-id="2a824-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="2a824-268">例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="2a824-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="2a824-269">包含/排除標記</span><span class="sxs-lookup"><span data-stu-id="2a824-269">Include/Exclude tag</span></span> | <span data-ttu-id="2a824-270">目標的受影響資料夾</span><span class="sxs-lookup"><span data-stu-id="2a824-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-271">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2a824-271">contentFiles</span></span> | <span data-ttu-id="2a824-272">內容</span><span class="sxs-lookup"><span data-stu-id="2a824-272">Content</span></span>  |
| <span data-ttu-id="2a824-273">執行階段</span><span class="sxs-lookup"><span data-stu-id="2a824-273">runtime</span></span> | <span data-ttu-id="2a824-274">執行階段、資源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="2a824-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="2a824-275">compile</span><span class="sxs-lookup"><span data-stu-id="2a824-275">compile</span></span> | <span data-ttu-id="2a824-276">lib</span><span class="sxs-lookup"><span data-stu-id="2a824-276">lib</span></span> |
| <span data-ttu-id="2a824-277">組建</span><span class="sxs-lookup"><span data-stu-id="2a824-277">build</span></span> | <span data-ttu-id="2a824-278">組建 (MSBuild props 和目標)</span><span class="sxs-lookup"><span data-stu-id="2a824-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="2a824-279">native</span><span class="sxs-lookup"><span data-stu-id="2a824-279">native</span></span> | <span data-ttu-id="2a824-280">native</span><span class="sxs-lookup"><span data-stu-id="2a824-280">native</span></span> |
| <span data-ttu-id="2a824-281">無</span><span class="sxs-lookup"><span data-stu-id="2a824-281">none</span></span> | <span data-ttu-id="2a824-282">無資料夾</span><span class="sxs-lookup"><span data-stu-id="2a824-282">No folders</span></span> |
| <span data-ttu-id="2a824-283">全部</span><span class="sxs-lookup"><span data-stu-id="2a824-283">all</span></span> | <span data-ttu-id="2a824-284">全部資料夾</span><span class="sxs-lookup"><span data-stu-id="2a824-284">All folders</span></span> |

<span data-ttu-id="2a824-285">例如，下列幾行程式碼指出 `PackageA`1.1.0 版或更高版本與 `PackageB` 1.x 版的相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="2a824-286">下列幾行程式碼指出相同套件的相依性，但指定要包含 `PackageA` 的 `contentFiles` 和 `build` 資料夾，以及 `PackageB` 的 `native` 和 `compile` 資料夾以外的所有一切</span><span class="sxs-lookup"><span data-stu-id="2a824-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="2a824-287">注意：從專案使用 `nuget spec` 建立 `.nuspec` 時，存在於該專案中的相依性會自動包含在產生的 `.nuspec` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="2a824-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="2a824-288">相依性群組</span><span class="sxs-lookup"><span data-stu-id="2a824-288">Dependency groups</span></span>

<span data-ttu-id="2a824-289">*2.0+ 版*</span><span class="sxs-lookup"><span data-stu-id="2a824-289">*Version 2.0+*</span></span>

<span data-ttu-id="2a824-290">當作單一一般清單的替代方案，您可以使用 `<dependencies>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="2a824-291">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<dependency>` 項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="2a824-292">當目標 Framework 與專案的 Framework 設定檔相容時，會同時安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="2a824-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="2a824-293">沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援相依性清單。</span><span class="sxs-lookup"><span data-stu-id="2a824-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="2a824-294">如需確切的 Framework 識別碼，請參閱[目標 Framework](../schema/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="2a824-294">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="2a824-295">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="2a824-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="2a824-296">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="2a824-296">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="2a824-297">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="2a824-297">Explicit assembly references</span></span>

<span data-ttu-id="2a824-298">`<references>` 項目明確指定使用套件時，目標專案應該參考的組件。</span><span class="sxs-lookup"><span data-stu-id="2a824-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="2a824-299">有此項目時，NuGet 只會將參考新增至列出的組件。它不會在套件的 `lib` 資料夾中新增任何其他組件的參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="2a824-300">例如，以下 `<references>` 項目會指示 NuGet 只將參考新增至 `xunit.dll` 和 `xunit.extensions.dll`，即使套件中有其他組件：</span><span class="sxs-lookup"><span data-stu-id="2a824-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="2a824-301">明確參考通常只用於設計階段的組件。</span><span class="sxs-lookup"><span data-stu-id="2a824-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="2a824-302">例如使用 [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts) (程式碼合約) 時，合約組件必須在它們擴大的執行階段組件旁邊，讓 Visual Studio 可以找到它們，但是合約組件不需要被專案參考，或複製到專案的 `bin` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a824-302">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="2a824-303">同樣地，明確參考可以用於單元測試 Framework ，例如 XUnit，這需要它的工具組件位在執行階段組件旁邊，但它們不需要包含為專案參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="2a824-304">參考群組</span><span class="sxs-lookup"><span data-stu-id="2a824-304">Reference groups</span></span>

<span data-ttu-id="2a824-305">*2.5+ 版本*</span><span class="sxs-lookup"><span data-stu-id="2a824-305">*Version 2.5+*</span></span>

<span data-ttu-id="2a824-306">當作單一一般清單的替代方案，您可以使用 `<references>` 內的 `<group>` 項目，根據目標專案的 Framework 設定檔指定參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-306">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="2a824-307">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-307">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="2a824-308">當目標 Framework 與專案的 Framework 設定檔相容時，這些參考會新增至專案。</span><span class="sxs-lookup"><span data-stu-id="2a824-308">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="2a824-309">沒有 `targetFramework` 屬性的 `<group>` 項目用為預設值或後援參考清單。</span><span class="sxs-lookup"><span data-stu-id="2a824-309">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="2a824-310">如需確切的 Framework 識別碼，請參閱[目標 Framework](../schema/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="2a824-310">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="2a824-311">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="2a824-311">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="2a824-312">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="2a824-312">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="2a824-313">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="2a824-313">Framework assembly references</span></span>

<span data-ttu-id="2a824-314">Framework 組件屬於 .NET Framework，應該已經在任何指定電腦的全域組件快取 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="2a824-314">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="2a824-315">找出 `<frameworkAssemblies>` 項目內的這些組件，套件可以確保所需的參考已新增至事件的專案，該專案尚未有這類參考。</span><span class="sxs-lookup"><span data-stu-id="2a824-315">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="2a824-316">當然，這類組件不直接包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="2a824-316">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="2a824-317">`<frameworkAssemblies>` 項目包含零或多個 `<frameworkAssembly>` 項目，它們每一個都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="2a824-317">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="2a824-318">屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-318">Attribute</span></span> | <span data-ttu-id="2a824-319">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-319">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-320">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="2a824-320">**assemblyName**</span></span> | <span data-ttu-id="2a824-321">(必要) 完整組件名稱。</span><span class="sxs-lookup"><span data-stu-id="2a824-321">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="2a824-322">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="2a824-322">**targetFramework**</span></span> | <span data-ttu-id="2a824-323">(選擇性) 指定要套用這個參考的目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="2a824-323">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="2a824-324">如果省略，則表示參考適用於所有 Framework。</span><span class="sxs-lookup"><span data-stu-id="2a824-324">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="2a824-325">如需確切的 Framework 識別碼，請參閱[目標 Framework](../schema/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="2a824-325">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="2a824-326">下列範例會顯示所有目標 Framework 的 `System.Net` 參考，以及僅供 .NET Framework 4.0 使用的 `System.ServiceModel` 參考：</span><span class="sxs-lookup"><span data-stu-id="2a824-326">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="2a824-327">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="2a824-327">Including assembly files</span></span>

<span data-ttu-id="2a824-328">如果遵循[建立套件](../create-packages/creating-a-package.md)中所述的慣例，即不必在 `.nuspec` 檔案中明確指定檔案清單。</span><span class="sxs-lookup"><span data-stu-id="2a824-328">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="2a824-329">`nuget pack` 命令會自動挑選必要的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-329">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="2a824-330">當套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，「排除」那些名為 `.resources.dll` 的參考，因為它們假設是當地語系化的附屬組件。</span><span class="sxs-lookup"><span data-stu-id="2a824-330">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="2a824-331">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="2a824-331">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="2a824-332">為略過這項自動行為並明確控制套件要包含哪些檔案，請放置 `<files>` 項目當作 `<package>` 的子系 (和 `<metadata>` 的同層級)，找出每個有不同 `<file>` 項目的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-332">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="2a824-333">例如: </span><span class="sxs-lookup"><span data-stu-id="2a824-333">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="2a824-334">使用 NuGet 2.x 及更舊版本，並規劃使用 `packages.config`；在安裝套件時，也會使用 `<files>` 項目包含不可變的內容檔。</span><span class="sxs-lookup"><span data-stu-id="2a824-334">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="2a824-335">使用 NuGet 3.3+ 和使用 `project.json` pr PackageReference 的專案，則改用 `<contentFiles>` 項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-335">With NuGet 3.3+ and projects using `project.json` pr PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="2a824-336">如需詳細資料，請參閱下文中的[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="2a824-336">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="2a824-337">檔案項目屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-337">File element attributes</span></span>

<span data-ttu-id="2a824-338">每個 `<file>` 項目都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="2a824-338">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="2a824-339">屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-339">Attribute</span></span> | <span data-ttu-id="2a824-340">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-340">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-341">**src**</span><span class="sxs-lookup"><span data-stu-id="2a824-341">**src**</span></span> | <span data-ttu-id="2a824-342">要包含的檔案位置，會受到 `exclude` 屬性指定的排除項目約束。</span><span class="sxs-lookup"><span data-stu-id="2a824-342">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="2a824-343">路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="2a824-343">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="2a824-344">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="2a824-344">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2a824-345">**目標**</span><span class="sxs-lookup"><span data-stu-id="2a824-345">**target**</span></span> | <span data-ttu-id="2a824-346">套件內資料夾的相對路徑是放置原始程式檔的位置，其開頭必須是 `lib`、`content`、`build` 或 `tools`。</span><span class="sxs-lookup"><span data-stu-id="2a824-346">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="2a824-347">請參閱[從慣例的工作目錄建立 .nuspec](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory)。</span><span class="sxs-lookup"><span data-stu-id="2a824-347">See [Creating a .nuspec from a convention-based working directory](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="2a824-348">**排除**</span><span class="sxs-lookup"><span data-stu-id="2a824-348">**exclude**</span></span> | <span data-ttu-id="2a824-349">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="2a824-349">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="2a824-350">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="2a824-350">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="2a824-351">範例</span><span class="sxs-lookup"><span data-stu-id="2a824-351">Examples</span></span>

<span data-ttu-id="2a824-352">**單一組件**</span><span class="sxs-lookup"><span data-stu-id="2a824-352">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="2a824-353">**目標 Framework 的特定單一組件**</span><span class="sxs-lookup"><span data-stu-id="2a824-353">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="2a824-354">**使用萬用字元的 DLL 集合**</span><span class="sxs-lookup"><span data-stu-id="2a824-354">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="2a824-355">**不同 Framework 的 DLL**</span><span class="sxs-lookup"><span data-stu-id="2a824-355">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="2a824-356">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="2a824-356">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="2a824-357">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="2a824-357">Including content files</span></span>

<span data-ttu-id="2a824-358">內容檔是不可變的檔案，套件必須將它們包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="2a824-358">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="2a824-359">因為不可變，所以取用專案不宜修改它們。</span><span class="sxs-lookup"><span data-stu-id="2a824-359">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="2a824-360">內容檔範例包括：</span><span class="sxs-lookup"><span data-stu-id="2a824-360">Example content files include:</span></span>

- <span data-ttu-id="2a824-361">內嵌為資源的映像</span><span class="sxs-lookup"><span data-stu-id="2a824-361">Images that are embedded as resources</span></span>
- <span data-ttu-id="2a824-362">已編譯原始程式檔</span><span class="sxs-lookup"><span data-stu-id="2a824-362">Source files that are already compiled</span></span>
- <span data-ttu-id="2a824-363">需要以專案的組建輸出包含的指令碼</span><span class="sxs-lookup"><span data-stu-id="2a824-363">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="2a824-364">套件的組態檔必須包含在專案中，但不需要專門針對任何專案變更</span><span class="sxs-lookup"><span data-stu-id="2a824-364">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="2a824-365">內容檔包含在使用 `<files>` 項目的套件中，指定 `target` 屬性中的 `content` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a824-365">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="2a824-366">不過，在使用 `project.json` 系統 (NuGet 3.3+) 或 PackageReference (NuGet 4+) 的專案中安裝套件時，會忽略這類檔案，改用 `<contentFiles>` 項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-366">However, such files are ignored when the package is installed in a project using the `project.json` system in NuGet 3.3+ or PackageReference in NuGet 4+, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="2a824-367">為取得取用專案的最大相容性，套件應該在兩個項目中都指定內容檔。</span><span class="sxs-lookup"><span data-stu-id="2a824-367">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="2a824-368">內容檔使用 files 項目</span><span class="sxs-lookup"><span data-stu-id="2a824-368">Using the files element for content files</span></span>

<span data-ttu-id="2a824-369">內容檔只要使用和組件檔相同的格式即可，但要在 `target` 屬性中指定 `content` 作為基底資料夾，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="2a824-369">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="2a824-370">**基本內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-370">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="2a824-371">**具有目錄結構的內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-371">**Content files with directory structure**</span></span>

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

<span data-ttu-id="2a824-372">**目標 Framework 的特定內容檔案**</span><span class="sxs-lookup"><span data-stu-id="2a824-372">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="2a824-373">**複製到資料夾，名稱中有點的內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-373">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="2a824-374">在此情況下，NuGet 會看到 `target` 的副檔名與 `src` 的副檔名不相符，因此會將 `target` 名稱的該部分視為資料夾：</span><span class="sxs-lookup"><span data-stu-id="2a824-374">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="2a824-375">**無副檔名的內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-375">**Content files without extensions**</span></span>

<span data-ttu-id="2a824-376">若要包含不含副檔名的檔案，請使用 `*` 或 `**` 萬用字元：</span><span class="sxs-lookup"><span data-stu-id="2a824-376">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="2a824-377">**有深路徑和深層目標的內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-377">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="2a824-378">在此情況下，因為原始程式檔的副檔名和目標相符，所以 NuGet 會假設目標是檔案名稱，不是資料夾：</span><span class="sxs-lookup"><span data-stu-id="2a824-378">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="2a824-379">**重新命名套件中的內容檔**</span><span class="sxs-lookup"><span data-stu-id="2a824-379">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="2a824-380">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="2a824-380">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="2a824-381">內容檔使用 contentFiles 項目</span><span class="sxs-lookup"><span data-stu-id="2a824-381">Using the contentFiles element for content files</span></span>

<span data-ttu-id="2a824-382">*3.3+ 版與 project.json 和 4.0+ 版與 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="2a824-382">*Version 3.3+ with project.json and 4.0+ with PackageReference*</span></span>

<span data-ttu-id="2a824-383">根據預設，套件會將內容放在 `contentFiles` 資料夾 (請參閱下文)，而 `nuget pack` 包含使用預設屬性資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-383">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="2a824-384">在此情況下，`.nuspec` 完全不需要包含 `contentFiles` 節點。</span><span class="sxs-lookup"><span data-stu-id="2a824-384">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="2a824-385">為控制包含哪些檔案，`<contentFiles>` 項目要指定 `<files>` 項目的集合，找出正確的檔案。</span><span class="sxs-lookup"><span data-stu-id="2a824-385">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="2a824-386">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定：</span><span class="sxs-lookup"><span data-stu-id="2a824-386">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="2a824-387">屬性</span><span class="sxs-lookup"><span data-stu-id="2a824-387">Attribute</span></span> | <span data-ttu-id="2a824-388">描述</span><span class="sxs-lookup"><span data-stu-id="2a824-388">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a824-389">**include**</span><span class="sxs-lookup"><span data-stu-id="2a824-389">**include**</span></span> | <span data-ttu-id="2a824-390">(必要) 要包含的檔案位置，受限於 `exclude` 屬性所指定的排除項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-390">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="2a824-391">路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="2a824-391">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="2a824-392">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="2a824-392">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2a824-393">**排除**</span><span class="sxs-lookup"><span data-stu-id="2a824-393">**exclude**</span></span> | <span data-ttu-id="2a824-394">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="2a824-394">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="2a824-395">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="2a824-395">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="2a824-396">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="2a824-396">**buildAction**</span></span> | <span data-ttu-id="2a824-397">要指派給 MSBuild 內容項目的建置動作，例如 `Content`、`None`、`Embedded Resource`、`Compile` 等等。預設為 `Compile`。</span><span class="sxs-lookup"><span data-stu-id="2a824-397">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="2a824-398">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="2a824-398">**copyToOutput**</span></span> | <span data-ttu-id="2a824-399">布林值，指出是否要將內容項目複製到組建輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a824-399">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="2a824-400">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="2a824-400">The default is false.</span></span> |
| <span data-ttu-id="2a824-401">**flatten**</span><span class="sxs-lookup"><span data-stu-id="2a824-401">**flatten**</span></span> | <span data-ttu-id="2a824-402">布林值，指出要將內容項目複製到組建輸出的單一資料夾 (true)，或保留套件中的資料夾結構 (false)。</span><span class="sxs-lookup"><span data-stu-id="2a824-402">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="2a824-403">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="2a824-403">The default is false.</span></span> |

<span data-ttu-id="2a824-404">安裝套件時，NuGet 會由上而下套用 `<contentFiles>` 的子項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="2a824-405">如有多個項目符合同一檔案，則套用所有項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="2a824-406">如果相同的屬性發生衝突，則最上層項目會覆寫較低的項目。</span><span class="sxs-lookup"><span data-stu-id="2a824-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="2a824-407">套件資料夾結構</span><span class="sxs-lookup"><span data-stu-id="2a824-407">Package folder structure</span></span>

<span data-ttu-id="2a824-408">套件專案應該結構化使用下列模式的內容：</span><span class="sxs-lookup"><span data-stu-id="2a824-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="2a824-409">`codeLanguages` 可能是 `cs`、`vb`、`fs`、`any`，或指定的 `$(ProjectLanguage)` 小寫對等項</span><span class="sxs-lookup"><span data-stu-id="2a824-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="2a824-410">`TxM` 是 NuGet 支援的任何合法目標 Framework Moniker (請參閱[目標 Framework](../schema/target-frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="2a824-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../schema/target-frameworks.md)).</span></span>
- <span data-ttu-id="2a824-411">這個語法的結尾可以附加任何資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="2a824-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="2a824-412">例如: </span><span class="sxs-lookup"><span data-stu-id="2a824-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="2a824-413">空資料夾可以使用 `.` 選擇不提供特定語言和 TxM 組合的內容，例如：</span><span class="sxs-lookup"><span data-stu-id="2a824-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="2a824-414">contentFiles 區段範例</span><span class="sxs-lookup"><span data-stu-id="2a824-414">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="2a824-415">.nuspec 檔案範例</span><span class="sxs-lookup"><span data-stu-id="2a824-415">Example .nuspec files</span></span>

<span data-ttu-id="2a824-416">**簡單的 `.nuspec` 不指定相依性或檔案**</span><span class="sxs-lookup"><span data-stu-id="2a824-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="2a824-417">**具有相依性的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="2a824-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="2a824-418">**具有檔案的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="2a824-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="2a824-419">**具有 Framework 組件的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="2a824-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="2a824-420">在此範例中，特定專案目標會安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="2a824-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="2a824-421">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="2a824-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="2a824-422">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="2a824-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="2a824-423">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="2a824-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="2a824-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="2a824-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="2a824-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="2a824-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
