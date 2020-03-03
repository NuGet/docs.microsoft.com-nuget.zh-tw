---
title: 適用于 NuGet 的 nuspec 檔案參考
description: .nuspec 檔案包含建置套件時使用的套件中繼資料，並向套件取用者提供資訊。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 19e7934e2f249056c532369fa5e8ee6e35cc8086
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230599"
---
# <a name="nuspec-reference"></a><span data-ttu-id="11a89-103">.nuspec 參考</span><span class="sxs-lookup"><span data-stu-id="11a89-103">.nuspec reference</span></span>

<span data-ttu-id="11a89-104">`.nuspec` 檔案是包含套件中繼資料的 XML 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="11a89-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="11a89-105">此資訊清單用來建置套件和向取用者提供資訊。</span><span class="sxs-lookup"><span data-stu-id="11a89-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="11a89-106">資訊清單一律包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="11a89-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="11a89-107">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="11a89-107">In this topic:</span></span>

- [<span data-ttu-id="11a89-108">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="11a89-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="11a89-109">[取代權杖](#replacement-tokens) (搭配 Visual Studio 專案使用時)</span><span class="sxs-lookup"><span data-stu-id="11a89-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- <span data-ttu-id="11a89-110">[Dependencies](#dependencies) (相依性)</span><span class="sxs-lookup"><span data-stu-id="11a89-110">[Dependencies](#dependencies)</span></span>
- [<span data-ttu-id="11a89-111">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="11a89-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="11a89-112">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="11a89-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="11a89-113">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="11a89-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="11a89-114">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="11a89-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="11a89-115">範例 nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="11a89-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="11a89-116">專案類型相容性</span><span class="sxs-lookup"><span data-stu-id="11a89-116">Project type compatibility</span></span>

- <span data-ttu-id="11a89-117">針對使用 `packages.config`的非 SDK 樣式專案，使用 `.nuspec` 搭配 `nuget.exe pack`。</span><span class="sxs-lookup"><span data-stu-id="11a89-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="11a89-118">建立[SDK 樣式專案](../resources/check-project-format.md)的套件（通常是 .net Core 和使用[SDK 屬性](/dotnet/core/tools/csproj#additions)的 .NET Standard 專案）時，不需要 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="11a89-119">（請注意，當您建立封裝時，會產生 `.nuspec`）。</span><span class="sxs-lookup"><span data-stu-id="11a89-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="11a89-120">如果您要使用 `dotnet.exe pack` 或 `msbuild pack target`建立封裝，建議您改為在專案檔的 `.nuspec` 檔案中[包含所有屬性](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="11a89-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="11a89-121">不過，您可以改為選擇[使用 `.nuspec` 檔案，以使用 `dotnet.exe` 或 `msbuild pack target`來](../reference/msbuild-targets.md#packing-using-a-nuspec)封裝。</span><span class="sxs-lookup"><span data-stu-id="11a89-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="11a89-122">若為從 `packages.config` 遷移至[PackageReference](../consume-packages/package-references-in-project-files.md)的專案，則不需要 `.nuspec` 檔案來建立封裝。</span><span class="sxs-lookup"><span data-stu-id="11a89-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="11a89-123">請改用[msbuild-t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。</span><span class="sxs-lookup"><span data-stu-id="11a89-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="11a89-124">一般格式和結構描述</span><span class="sxs-lookup"><span data-stu-id="11a89-124">General form and schema</span></span>

<span data-ttu-id="11a89-125">目前的 `nuspec.xsd` 結構描述檔案位於 [NuGet GitHub 存放庫](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)。</span><span class="sxs-lookup"><span data-stu-id="11a89-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="11a89-126">在此結構描述內，`.nuspec` 檔案有下列一般格式：</span><span class="sxs-lookup"><span data-stu-id="11a89-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="11a89-127">為能清晰呈現結構描述，請在 Visual Studio 中以設計模式開啟結構描述檔案，按一下 [XML 結構描述總管] 連結。</span><span class="sxs-lookup"><span data-stu-id="11a89-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="11a89-128">或者，將檔案開啟為程式碼，在編輯器中按一下滑鼠右鍵，選取 [Show XML Schema Explorer] (顯示 XML 結構描述總管)。</span><span class="sxs-lookup"><span data-stu-id="11a89-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="11a89-129">任一方式都可取得類似以下的檢視 (大部分展開時)：</span><span class="sxs-lookup"><span data-stu-id="11a89-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![開啟了 nuspec.xsd 的 Visual Studio 結構描述總管](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="11a89-131">必要的中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="11a89-131">Required metadata elements</span></span>

<span data-ttu-id="11a89-132">雖然下列項目是套件的最低需求，但您應該考慮新增[選擇性中繼資料項目](#optional-metadata-elements)以改善開發人員使用套件的整體體驗。</span><span class="sxs-lookup"><span data-stu-id="11a89-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="11a89-133">這些項目必須出現在 `<metadata>` 項目中。</span><span class="sxs-lookup"><span data-stu-id="11a89-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="11a89-134">id</span><span class="sxs-lookup"><span data-stu-id="11a89-134">id</span></span> 
<span data-ttu-id="11a89-135">不區分大小寫的套件識別碼，在整個 nuget.org 或套件所在的任何組件庫中都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="11a89-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="11a89-136">識別碼可能不包含對 URL 而言無效的空格或字元，而且通常會遵循 .NET 命名空間規則。</span><span class="sxs-lookup"><span data-stu-id="11a89-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="11a89-137">如需指導方針，請參閱[選擇唯一的套件識別碼](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="11a89-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="11a89-138">version</span><span class="sxs-lookup"><span data-stu-id="11a89-138">version</span></span>
<span data-ttu-id="11a89-139">套件版本，遵循 *major.minor.patch* 模式。</span><span class="sxs-lookup"><span data-stu-id="11a89-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="11a89-140">版本號碼可以包含預先發行版本的後置詞，如[套件版本控制](../concepts/package-versioning.md#pre-release-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="11a89-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="11a89-141">description</span><span class="sxs-lookup"><span data-stu-id="11a89-141">description</span></span>
<span data-ttu-id="11a89-142">UI 顯示的封裝描述。</span><span class="sxs-lookup"><span data-stu-id="11a89-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="11a89-143">authors</span><span class="sxs-lookup"><span data-stu-id="11a89-143">authors</span></span>
<span data-ttu-id="11a89-144">以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。這些會顯示在 nuget.org 上的 NuGet 元件庫中，並用於相同作者的交互參照封裝。</span><span class="sxs-lookup"><span data-stu-id="11a89-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="11a89-145">選擇性中繼資料項目</span><span class="sxs-lookup"><span data-stu-id="11a89-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="11a89-146">owners</span><span class="sxs-lookup"><span data-stu-id="11a89-146">owners</span></span>
<span data-ttu-id="11a89-147">在 nuget.org 上使用設定檔名稱的套件建立者清單（以逗號分隔）。這通常與 `authors`中的清單相同，並會在將封裝上傳至 nuget.org 時予以忽略。請參閱[在 nuget.org 上管理套件擁有](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)者。</span><span class="sxs-lookup"><span data-stu-id="11a89-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="11a89-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="11a89-148">projectUrl</span></span>
<span data-ttu-id="11a89-149">套件首頁的 URL，通常會顯示在 UI 顯示及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="11a89-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="11a89-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="11a89-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="11a89-151">licenseUrl 已被取代。</span><span class="sxs-lookup"><span data-stu-id="11a89-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="11a89-152">請改用授權。</span><span class="sxs-lookup"><span data-stu-id="11a89-152">Use license instead.</span></span>

<span data-ttu-id="11a89-153">套件授權的 URL，通常會顯示在像是 nuget.org 的 Ui 中。</span><span class="sxs-lookup"><span data-stu-id="11a89-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="11a89-154">授權</span><span class="sxs-lookup"><span data-stu-id="11a89-154">license</span></span>
<span data-ttu-id="11a89-155">封裝內授權檔案的 SPDX 授權運算式或路徑，通常會顯示在類似 nuget.org 的 Ui 中。如果您要以一般授權（例如 MIT 或 BSD-2-子句）授權封裝，請使用相關聯的[SPDX 授權識別碼](https://spdx.org/licenses/)。</span><span class="sxs-lookup"><span data-stu-id="11a89-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="11a89-156">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="11a89-157">NuGet.org 只接受開放原始碼計畫或免費軟體基礎核准的授權運算式。</span><span class="sxs-lookup"><span data-stu-id="11a89-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="11a89-158">如果您的套件是以多個一般授權授權，您可以使用[SPDX 運算式語法2.0 版](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)來指定複合授權。</span><span class="sxs-lookup"><span data-stu-id="11a89-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="11a89-159">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="11a89-160">如果您使用授權運算式不支援的自訂授權，您可以使用授權文字來封裝 `.txt` 或 `.md` 檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="11a89-161">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-161">For example:</span></span>

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

<span data-ttu-id="11a89-162">如需對等的 MSBuild，請參閱[封裝授權運算式或授權檔案](msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="11a89-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="11a89-163">NuGet 授權運算式的確切語法在下面的[ABNF](https://tools.ietf.org/html/rfc5234)中有說明。</span><span class="sxs-lookup"><span data-stu-id="11a89-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="11a89-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="11a89-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="11a89-165">iconUrl 已被取代。</span><span class="sxs-lookup"><span data-stu-id="11a89-165">iconUrl is deprecated.</span></span> <span data-ttu-id="11a89-166">請改用圖示。</span><span class="sxs-lookup"><span data-stu-id="11a89-166">Use icon instead.</span></span>

<span data-ttu-id="11a89-167">128x128 影像的 URL，具有透明度背景，以做為 UI 顯示中的套件圖示。</span><span class="sxs-lookup"><span data-stu-id="11a89-167">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="11a89-168">確定這個項目包含「直接映像 URL」，不是包含影像的網頁 URL。</span><span class="sxs-lookup"><span data-stu-id="11a89-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="11a89-169">例如，若要使用 GitHub 中的映射，請使用原始檔案 URL，例如<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>。</span><span class="sxs-lookup"><span data-stu-id="11a89-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="11a89-170">icon</span><span class="sxs-lookup"><span data-stu-id="11a89-170">icon</span></span>

<span data-ttu-id="11a89-171">它是封裝內影像檔案的路徑，通常會顯示在像是 nuget.org 的 Ui 中，做為封裝圖示。</span><span class="sxs-lookup"><span data-stu-id="11a89-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="11a89-172">影像檔案大小限制為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="11a89-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="11a89-173">支援的檔案格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="11a89-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="11a89-174">我們建議使用128x128 的映射解析度。</span><span class="sxs-lookup"><span data-stu-id="11a89-174">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="11a89-175">例如，當您使用 nuget.exe 建立套件時，會將下列內容新增至您的 nuspec：</span><span class="sxs-lookup"><span data-stu-id="11a89-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="11a89-176">封裝圖示 nuspec 範例。</span><span class="sxs-lookup"><span data-stu-id="11a89-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="11a89-177">如需對等的 MSBuild，請參閱[封裝圖示影像檔](msbuild-targets.md#packing-an-icon-image-file)。</span><span class="sxs-lookup"><span data-stu-id="11a89-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="11a89-178">您可以指定 `icon` 和 `iconUrl`，以維持與不支援 `icon`的來源的回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="11a89-178">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="11a89-179">Visual Studio 將支援未來版本中來自以資料夾為基礎的來源之套件的 `icon`。</span><span class="sxs-lookup"><span data-stu-id="11a89-179">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="11a89-180">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="11a89-180">requireLicenseAcceptance</span></span>
<span data-ttu-id="11a89-181">布林值，指定在安裝套件時，用戶端是否必須提示取用者接受套件授權。</span><span class="sxs-lookup"><span data-stu-id="11a89-181">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="11a89-182">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="11a89-182">developmentDependency</span></span>
<span data-ttu-id="11a89-183">*(2.8+)* 布林值，指定套件是否標示為僅限開發相依性，這可防止套件包含為其他套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-183">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="11a89-184">使用 PackageReference （NuGet 4.8 +）時，此旗標也表示它會從編譯中排除編譯時間資產。</span><span class="sxs-lookup"><span data-stu-id="11a89-184">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="11a89-185">請參閱[DevelopmentDependency support For PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="11a89-185">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="11a89-186">summary</span><span class="sxs-lookup"><span data-stu-id="11a89-186">summary</span></span>
> [!Important]
> <span data-ttu-id="11a89-187">`summary` 已被取代。</span><span class="sxs-lookup"><span data-stu-id="11a89-187">`summary` is being deprecated.</span></span> <span data-ttu-id="11a89-188">請改用 `description`。</span><span class="sxs-lookup"><span data-stu-id="11a89-188">Use `description` instead.</span></span>

<span data-ttu-id="11a89-189">UI 顯示中的套件簡短描述。</span><span class="sxs-lookup"><span data-stu-id="11a89-189">A short description of the package for UI display.</span></span> <span data-ttu-id="11a89-190">如果省略，即使用截斷版本的 `description`。</span><span class="sxs-lookup"><span data-stu-id="11a89-190">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="11a89-191">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="11a89-191">releaseNotes</span></span>
<span data-ttu-id="11a89-192">*(1.5+)* 此版本套件中的變更描述，通常用於 Visual Studio Package Manager 的 [更新] 索引標籤等 UI 中，以取代套件描述。</span><span class="sxs-lookup"><span data-stu-id="11a89-192">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="11a89-193">著作權</span><span class="sxs-lookup"><span data-stu-id="11a89-193">copyright</span></span>
<span data-ttu-id="11a89-194">*(1.5+)* 套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="11a89-194">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="11a89-195">語言</span><span class="sxs-lookup"><span data-stu-id="11a89-195">language</span></span>
<span data-ttu-id="11a89-196">套件的地區設定識別碼。</span><span class="sxs-lookup"><span data-stu-id="11a89-196">The locale ID for the package.</span></span> <span data-ttu-id="11a89-197">請參閱[建立當地語系化的套件](../create-packages/creating-localized-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-197">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="11a89-198">tags</span><span class="sxs-lookup"><span data-stu-id="11a89-198">tags</span></span>
<span data-ttu-id="11a89-199">以逗號分隔的標記與關鍵字清單，描述套件並透過搜尋和篩選協助探索套件。</span><span class="sxs-lookup"><span data-stu-id="11a89-199">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="11a89-200">一次性</span><span class="sxs-lookup"><span data-stu-id="11a89-200">serviceable</span></span> 
<span data-ttu-id="11a89-201">*(3.3+)* 僅供內部 NuGet 使用。</span><span class="sxs-lookup"><span data-stu-id="11a89-201">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="11a89-202">repository</span><span class="sxs-lookup"><span data-stu-id="11a89-202">repository</span></span>
<span data-ttu-id="11a89-203">存放庫中繼資料，由四個選擇性屬性組成： `type` 和 `url` *（4.0 +）*，以及 `branch` 和 `commit` *（4.6 +）*。</span><span class="sxs-lookup"><span data-stu-id="11a89-203">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="11a89-204">這些屬性可讓您將 `.nupkg` 對應至建立它的存放庫，而且可能會如個別分支名稱和/或認可建立封裝的 SHA-1 雜湊來取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11a89-204">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="11a89-205">這應該是公開可用的 url，可直接由版本控制軟體叫用。</span><span class="sxs-lookup"><span data-stu-id="11a89-205">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="11a89-206">它不應該是 html 網頁，因為這適用于電腦。</span><span class="sxs-lookup"><span data-stu-id="11a89-206">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="11a89-207">在 [連結至專案] 頁面上，改為使用 [`projectUrl`] 欄位。</span><span class="sxs-lookup"><span data-stu-id="11a89-207">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="11a89-208">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-208">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="11a89-209">title</span><span class="sxs-lookup"><span data-stu-id="11a89-209">title</span></span>
<span data-ttu-id="11a89-210">可在某些 UI 中使用之套件的人易記標題。</span><span class="sxs-lookup"><span data-stu-id="11a89-210">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="11a89-211">（nuget.org 和 Visual Studio 中的套件管理員不會顯示標題）</span><span class="sxs-lookup"><span data-stu-id="11a89-211">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="11a89-212">集合項目</span><span class="sxs-lookup"><span data-stu-id="11a89-212">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="11a89-213">Packagetypes></span><span class="sxs-lookup"><span data-stu-id="11a89-213">packageTypes</span></span>
<span data-ttu-id="11a89-214">*(3.5+)* 零或多個 `<packageType>` 元素的集合，如果不是傳統相依性套件，則會指定套件類型。</span><span class="sxs-lookup"><span data-stu-id="11a89-214">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="11a89-215">每個 packageType 都有「名稱」和「版本」屬性。</span><span class="sxs-lookup"><span data-stu-id="11a89-215">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="11a89-216">請參閱[設定套件類型](../create-packages/set-package-type.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-216">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="11a89-217">相依性</span><span class="sxs-lookup"><span data-stu-id="11a89-217">dependencies</span></span>
<span data-ttu-id="11a89-218">零或多個 `<dependency>` 項目的集合，指定套件的相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-218">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="11a89-219">每個相依性都有「識別碼」、「版本」、「包含」(3.x+) 和「排除」(3.x+) 屬性。</span><span class="sxs-lookup"><span data-stu-id="11a89-219">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="11a89-220">請參閱下文的[相依性](#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="11a89-220">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="11a89-221">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="11a89-221">frameworkAssemblies</span></span>
<span data-ttu-id="11a89-222">*(1.2+)* 零或多個 `<frameworkAssembly>` 項目的集合，識別此套件需要的 .NET Framework 組件參考，它們可確保參考會新增至取用套件的專案。</span><span class="sxs-lookup"><span data-stu-id="11a89-222">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="11a89-223">每個 frameworkAssembly 都有 *assemblyName* 和 *targetFramework* 屬性。</span><span class="sxs-lookup"><span data-stu-id="11a89-223">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="11a89-224">請參閱下文的[指定 Framework 組件參考 GAC](#specifying-framework-assembly-references-gac)。</span><span class="sxs-lookup"><span data-stu-id="11a89-224">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="11a89-225">參考</span><span class="sxs-lookup"><span data-stu-id="11a89-225">references</span></span>
<span data-ttu-id="11a89-226">*(1.5+)* 在套件的 `<reference>` 資料夾中命名組件的零或多個 `lib` 項目集合，這些項目可新增為專案參考。</span><span class="sxs-lookup"><span data-stu-id="11a89-226">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="11a89-227">每個參考都有 *file* 屬性。</span><span class="sxs-lookup"><span data-stu-id="11a89-227">Each reference has a *file* attribute.</span></span> <span data-ttu-id="11a89-228">`<references>` 也可以包含具有 `<group>`targetFramework\* 屬性的 \* 項目，然後即可包含 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-228">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="11a89-229">如果省略，就會包含 `lib` 中的所有參考。</span><span class="sxs-lookup"><span data-stu-id="11a89-229">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="11a89-230">請參閱下文中的[指定明確的組件參考](#specifying-explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="11a89-230">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="11a89-231">contentFiles</span><span class="sxs-lookup"><span data-stu-id="11a89-231">contentFiles</span></span>
<span data-ttu-id="11a89-232">*(3.3+)*`<files>` 項目的集合，可識別要包含在取用專案中的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-232">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="11a89-233">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定。</span><span class="sxs-lookup"><span data-stu-id="11a89-233">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="11a89-234">請參閱下文中的[指定要包含在套件中的檔案](#specifying-files-to-include-in-the-package)。</span><span class="sxs-lookup"><span data-stu-id="11a89-234">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="11a89-235">files</span><span class="sxs-lookup"><span data-stu-id="11a89-235">files</span></span> 
<span data-ttu-id="11a89-236">`<package>` 節點可能會包含 `<files>` 節點做為 `<metadata>`的同級，以及 `<metadata>`下的 `<contentFiles>` 子系，以指定要包含在封裝中的元件和內容檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-236">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="11a89-237">如需詳細資料，請參閱本主題下文中的[包含組件檔](#including-assembly-files)和[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="11a89-237">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="11a89-238">中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-238">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="11a89-239">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="11a89-239">minClientVersion</span></span>
<span data-ttu-id="11a89-240">指定可安裝此套件的最低 NuGet 用戶端版本，此作業是由 nuget.exe 和 Visual Studio 套件管理員強制執行。</span><span class="sxs-lookup"><span data-stu-id="11a89-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="11a89-241">每當套件依存於 NuGet 用戶端新增的 `.nuspec` 檔案特定功能時，就會使用。</span><span class="sxs-lookup"><span data-stu-id="11a89-241">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="11a89-242">例如，套件使用的 `developmentDependency` 屬性應該為 `minClientVersion` 指定 "2.8"。</span><span class="sxs-lookup"><span data-stu-id="11a89-242">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="11a89-243">同樣地，使用 `contentFiles` 項目的套件 (請參閱下一節) 應將 `minClientVersion` 設定成 "3.3"。</span><span class="sxs-lookup"><span data-stu-id="11a89-243">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="11a89-244">另請注意，因為 2.5 之前的 NuGet 用戶端無法辨識此旗標，所以它們「一律」拒絕安裝套件，無論 `minClientVersion` 包含什麼。</span><span class="sxs-lookup"><span data-stu-id="11a89-244">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="11a89-245">取代權杖</span><span class="sxs-lookup"><span data-stu-id="11a89-245">Replacement tokens</span></span>

<span data-ttu-id="11a89-246">建立套件時，[`nuget pack` 命令](../reference/cli-reference/cli-ref-pack.md) 會使用來自專案檔的值或來自 `.nuspec` 命令的 `<metadata>` 參數值，取代 `pack` 檔案之 `-properties` 節點的 $ 分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="11a89-246">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="11a89-247">在命令列中，您可以使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定權杖值。</span><span class="sxs-lookup"><span data-stu-id="11a89-247">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="11a89-248">例如，您可以在 `$owners$` 中使用權杖，例如 `$desc$` 和 `.nuspec`，並在封裝階段提供值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="11a89-248">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="11a89-249">若要使用專案中的值，請指定下表中描述的權杖 (AssemblyInfo 是指 `Properties` 中的檔案，例如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`)。</span><span class="sxs-lookup"><span data-stu-id="11a89-249">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="11a89-250">若要使用這些權杖，請執行 `nuget pack` 與專案檔，非僅 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="11a89-250">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="11a89-251">例如，使用下列命令時，專案的 `$id$` 和 `$version$` 值會取代為 `.nuspec` 檔案中的 `AssemblyName` 和 `AssemblyVersion` 權杖：</span><span class="sxs-lookup"><span data-stu-id="11a89-251">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="11a89-252">通常，當您擁有專案時，一開始會使用自動包含這些標準權杖一部分的 `.nuspec` 來建立 `nuget spec MyProject.csproj`。</span><span class="sxs-lookup"><span data-stu-id="11a89-252">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="11a89-253">不過，如果專案沒有所需之 `.nuspec` 項目的值，則 `nuget pack` 會失敗。</span><span class="sxs-lookup"><span data-stu-id="11a89-253">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="11a89-254">此外，如果變更專案值，請務必在建立套件前重建；使用 pack 命令的 `build` 參數很容易完成此作業。</span><span class="sxs-lookup"><span data-stu-id="11a89-254">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="11a89-255">除 `$configuration$` 以外，專案中值的使用順序優先於任何指派給命令列上相同權杖的值。</span><span class="sxs-lookup"><span data-stu-id="11a89-255">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="11a89-256">Token</span><span class="sxs-lookup"><span data-stu-id="11a89-256">Token</span></span> | <span data-ttu-id="11a89-257">值來源</span><span class="sxs-lookup"><span data-stu-id="11a89-257">Value source</span></span> | <span data-ttu-id="11a89-258">值</span><span class="sxs-lookup"><span data-stu-id="11a89-258">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="11a89-259">**$id$**</span><span class="sxs-lookup"><span data-stu-id="11a89-259">**$id$**</span></span> | <span data-ttu-id="11a89-260">專案檔</span><span class="sxs-lookup"><span data-stu-id="11a89-260">Project file</span></span> | <span data-ttu-id="11a89-261">專案檔中的 AssemblyName （title）</span><span class="sxs-lookup"><span data-stu-id="11a89-261">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="11a89-262">**$version$**</span><span class="sxs-lookup"><span data-stu-id="11a89-262">**$version$**</span></span> | <span data-ttu-id="11a89-263">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="11a89-263">AssemblyInfo</span></span> | <span data-ttu-id="11a89-264">如有則為 AssemblyInformationalVersion，否則為 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="11a89-264">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="11a89-265">**$author$**</span><span class="sxs-lookup"><span data-stu-id="11a89-265">**$author$**</span></span> | <span data-ttu-id="11a89-266">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="11a89-266">AssemblyInfo</span></span> | <span data-ttu-id="11a89-267">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="11a89-267">AssemblyCompany</span></span> |
| <span data-ttu-id="11a89-268">**$title $**</span><span class="sxs-lookup"><span data-stu-id="11a89-268">**$title$**</span></span> | <span data-ttu-id="11a89-269">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="11a89-269">AssemblyInfo</span></span> | <span data-ttu-id="11a89-270">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="11a89-270">AssemblyTitle</span></span> |
| <span data-ttu-id="11a89-271">**$description$**</span><span class="sxs-lookup"><span data-stu-id="11a89-271">**$description$**</span></span> | <span data-ttu-id="11a89-272">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="11a89-272">AssemblyInfo</span></span> | <span data-ttu-id="11a89-273">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="11a89-273">AssemblyDescription</span></span> |
| <span data-ttu-id="11a89-274">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="11a89-274">**$copyright$**</span></span> | <span data-ttu-id="11a89-275">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="11a89-275">AssemblyInfo</span></span> | <span data-ttu-id="11a89-276">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="11a89-276">AssemblyCopyright</span></span> |
| <span data-ttu-id="11a89-277">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="11a89-277">**$configuration$**</span></span> | <span data-ttu-id="11a89-278">組件 DLL</span><span class="sxs-lookup"><span data-stu-id="11a89-278">Assembly DLL</span></span> | <span data-ttu-id="11a89-279">用以建置組件的組態，預設為偵錯。</span><span class="sxs-lookup"><span data-stu-id="11a89-279">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="11a89-280">請注意，若要建立使用版本組態的套件，命令列上一律要使用 `-properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="11a89-280">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="11a89-281">當您包含[組件檔](#including-assembly-files)和[內容檔](#including-content-files)時，也可使用權杖來解析路徑。</span><span class="sxs-lookup"><span data-stu-id="11a89-281">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="11a89-282">權杖和 MSBuild 屬性有相同的名稱，所以您才能夠根據目前的組建組態選取要包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-282">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="11a89-283">例如，如果在 `.nuspec` 檔案中使用下列權杖：</span><span class="sxs-lookup"><span data-stu-id="11a89-283">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="11a89-284">而您建置的組件，其 `AssemblyName` 是在 MSBuild 中有 `LoggingLibrary` 組態的 `Release`，在套件的 `.nuspec` 檔案中產生的程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="11a89-284">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="11a89-285">相依性元素</span><span class="sxs-lookup"><span data-stu-id="11a89-285">Dependencies element</span></span>

<span data-ttu-id="11a89-286">`<dependencies>` 內的 `<metadata>` 項目包含任意數目的 `<dependency>` 項目，可識別最上層套件依存的其他套件。</span><span class="sxs-lookup"><span data-stu-id="11a89-286">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="11a89-287">每個 `<dependency>` 的屬性如下：</span><span class="sxs-lookup"><span data-stu-id="11a89-287">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="11a89-288">屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-288">Attribute</span></span> | <span data-ttu-id="11a89-289">描述</span><span class="sxs-lookup"><span data-stu-id="11a89-289">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="11a89-290">(必要) 相依性的套件識別碼，例如 "EntityFramework" 與 "NUnit"，是在套件頁面上顯示的套件 nuget.org 名稱。</span><span class="sxs-lookup"><span data-stu-id="11a89-290">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="11a89-291">(必要) 可接受為相依性的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="11a89-291">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="11a89-292">如需確切的語法，請參閱[套件版本控制](../concepts/package-versioning.md#version-ranges)。</span><span class="sxs-lookup"><span data-stu-id="11a89-292">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="11a89-293">不支援浮動版本。</span><span class="sxs-lookup"><span data-stu-id="11a89-293">Floating versions are not supported.</span></span> |
| <span data-ttu-id="11a89-294">include</span><span class="sxs-lookup"><span data-stu-id="11a89-294">include</span></span> | <span data-ttu-id="11a89-295">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要包含的相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-295">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="11a89-296">預設值是 `all`。</span><span class="sxs-lookup"><span data-stu-id="11a89-296">The default value is `all`.</span></span> |
| <span data-ttu-id="11a89-297">exclude</span><span class="sxs-lookup"><span data-stu-id="11a89-297">exclude</span></span> | <span data-ttu-id="11a89-298">包含/排除標記的逗號分隔清單 (如下所示)，指出最終套件要排除的相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-298">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="11a89-299">預設值是可覆寫的 `build,analyzers`。</span><span class="sxs-lookup"><span data-stu-id="11a89-299">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="11a89-300">但是 `content/ ContentFiles` 也會在最終封裝中以隱含方式排除，而無法覆寫。</span><span class="sxs-lookup"><span data-stu-id="11a89-300">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="11a89-301">以 `exclude` 指定的標記優先於以 `include` 指定的標記。</span><span class="sxs-lookup"><span data-stu-id="11a89-301">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="11a89-302">例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="11a89-302">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="11a89-303">包含/排除標記</span><span class="sxs-lookup"><span data-stu-id="11a89-303">Include/Exclude tag</span></span> | <span data-ttu-id="11a89-304">目標的受影響資料夾</span><span class="sxs-lookup"><span data-stu-id="11a89-304">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="11a89-305">contentFiles</span><span class="sxs-lookup"><span data-stu-id="11a89-305">contentFiles</span></span> | <span data-ttu-id="11a89-306">內容</span><span class="sxs-lookup"><span data-stu-id="11a89-306">Content</span></span> |
| <span data-ttu-id="11a89-307">執行階段</span><span class="sxs-lookup"><span data-stu-id="11a89-307">runtime</span></span> | <span data-ttu-id="11a89-308">執行階段、資源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="11a89-308">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="11a89-309">compile</span><span class="sxs-lookup"><span data-stu-id="11a89-309">compile</span></span> | <span data-ttu-id="11a89-310">lib</span><span class="sxs-lookup"><span data-stu-id="11a89-310">lib</span></span> |
| <span data-ttu-id="11a89-311">build</span><span class="sxs-lookup"><span data-stu-id="11a89-311">build</span></span> | <span data-ttu-id="11a89-312">組建 (MSBuild props 和目標)</span><span class="sxs-lookup"><span data-stu-id="11a89-312">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="11a89-313">native</span><span class="sxs-lookup"><span data-stu-id="11a89-313">native</span></span> | <span data-ttu-id="11a89-314">native</span><span class="sxs-lookup"><span data-stu-id="11a89-314">native</span></span> |
| <span data-ttu-id="11a89-315">無</span><span class="sxs-lookup"><span data-stu-id="11a89-315">none</span></span> | <span data-ttu-id="11a89-316">無資料夾</span><span class="sxs-lookup"><span data-stu-id="11a89-316">No folders</span></span> |
| <span data-ttu-id="11a89-317">all</span><span class="sxs-lookup"><span data-stu-id="11a89-317">all</span></span> | <span data-ttu-id="11a89-318">全部資料夾</span><span class="sxs-lookup"><span data-stu-id="11a89-318">All folders</span></span> |

<span data-ttu-id="11a89-319">例如，下列幾行程式碼指出 `PackageA`1.1.0 版或更高版本與 `PackageB` 1.x 版的相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-319">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="11a89-320">下列幾行程式碼指出相同套件的相依性，但指定要包含 `contentFiles` 的 `build` 和 `PackageA` 資料夾，以及 `native` 的 `compile` 和 `PackageB` 資料夾以外的所有一切</span><span class="sxs-lookup"><span data-stu-id="11a89-320">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="11a89-321">使用 `nuget spec`從專案建立 `.nuspec` 時，存在於該專案中的相依性不會自動包含在產生的 `.nuspec` 檔中。</span><span class="sxs-lookup"><span data-stu-id="11a89-321">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="11a89-322">相反地，請使用 `nuget pack myproject.csproj`，然後從產生的*nupkg*檔案內取得*nuspec*檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-322">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="11a89-323">*Nuspec*包含相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-323">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="11a89-324">相依性群組</span><span class="sxs-lookup"><span data-stu-id="11a89-324">Dependency groups</span></span>

<span data-ttu-id="11a89-325">*2.0+ 版*</span><span class="sxs-lookup"><span data-stu-id="11a89-325">*Version 2.0+*</span></span>

<span data-ttu-id="11a89-326">當作單一一般清單的替代方案，您可以使用 `<group>` 內的 `<dependencies>` 項目，根據目標專案的 Framework 設定檔指定相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-326">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="11a89-327">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<dependency>` 項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-327">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="11a89-328">當目標 Framework 與專案的 Framework 設定檔相容時，會同時安裝這些相依性。</span><span class="sxs-lookup"><span data-stu-id="11a89-328">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="11a89-329">沒有 `<group>` 屬性的 `targetFramework` 項目用為預設值或後援相依性清單。</span><span class="sxs-lookup"><span data-stu-id="11a89-329">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="11a89-330">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-330">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="11a89-331">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="11a89-331">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="11a89-332">相較于 `dependency groups`中所使用的 TFM，`lib/ref` 資料夾中使用的[目標 Framework 標記（TFM）](../reference/target-frameworks.md)格式會不同。</span><span class="sxs-lookup"><span data-stu-id="11a89-332">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="11a89-333">如果 `dependencies group` 中宣告的目標 framework 和 `.nuspec` 檔的 `lib/ref` 資料夾沒有完全相符的專案，則 `pack` 命令會引發[NuGet 警告 NU5128](../reference/errors-and-warnings/nu5128.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-333">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="11a89-334">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="11a89-334">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="11a89-335">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="11a89-335">Explicit assembly references</span></span>

<span data-ttu-id="11a89-336">使用 `packages.config` 的專案會使用 `<references>` 元素，明確指定使用封裝時，目標專案應參考的元件。</span><span class="sxs-lookup"><span data-stu-id="11a89-336">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="11a89-337">明確參考通常只用於設計階段的組件。</span><span class="sxs-lookup"><span data-stu-id="11a89-337">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="11a89-338">如需詳細資訊，請參閱[選取專案所參考的元件](../create-packages/select-assemblies-referenced-by-projects.md)中的頁面以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="11a89-338">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="11a89-339">例如，以下 `<references>` 項目會指示 NuGet 只將參考新增至 `xunit.dll` 和 `xunit.extensions.dll`，即使套件中有其他組件：</span><span class="sxs-lookup"><span data-stu-id="11a89-339">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="11a89-340">參考群組</span><span class="sxs-lookup"><span data-stu-id="11a89-340">Reference groups</span></span>

<span data-ttu-id="11a89-341">當作單一一般清單的替代方案，您可以使用 `<group>` 內的 `<references>` 項目，根據目標專案的 Framework 設定檔指定參考。</span><span class="sxs-lookup"><span data-stu-id="11a89-341">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="11a89-342">每個群組都有名為 `targetFramework` 的屬性，且包含零或多個 `<reference>` 項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-342">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="11a89-343">當目標 Framework 與專案的 Framework 設定檔相容時，這些參考會新增至專案。</span><span class="sxs-lookup"><span data-stu-id="11a89-343">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="11a89-344">沒有 `<group>` 屬性的 `targetFramework` 項目用為預設值或後援參考清單。</span><span class="sxs-lookup"><span data-stu-id="11a89-344">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="11a89-345">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-345">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="11a89-346">群組格式無法和一般清單混合使用。</span><span class="sxs-lookup"><span data-stu-id="11a89-346">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="11a89-347">下列範例示範 `<group>` 項目的不同變化：</span><span class="sxs-lookup"><span data-stu-id="11a89-347">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="11a89-348">Framework 組件參考</span><span class="sxs-lookup"><span data-stu-id="11a89-348">Framework assembly references</span></span>

<span data-ttu-id="11a89-349">Framework 組件屬於 .NET Framework，應該已經在任何指定電腦的全域組件快取 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="11a89-349">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="11a89-350">找出 `<frameworkAssemblies>` 項目內的這些組件，套件可以確保所需的參考已新增至事件的專案，該專案尚未有這類參考。</span><span class="sxs-lookup"><span data-stu-id="11a89-350">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="11a89-351">當然，這類組件不直接包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="11a89-351">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="11a89-352">`<frameworkAssemblies>` 項目包含零或多個 `<frameworkAssembly>` 項目，它們每一個都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="11a89-352">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="11a89-353">屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-353">Attribute</span></span> | <span data-ttu-id="11a89-354">描述</span><span class="sxs-lookup"><span data-stu-id="11a89-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11a89-355">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="11a89-355">**assemblyName**</span></span> | <span data-ttu-id="11a89-356">(必要) 完整組件名稱。</span><span class="sxs-lookup"><span data-stu-id="11a89-356">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="11a89-357">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="11a89-357">**targetFramework**</span></span> | <span data-ttu-id="11a89-358">(選擇性) 指定要套用這個參考的目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="11a89-358">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="11a89-359">如果省略，則表示參考適用於所有 Framework。</span><span class="sxs-lookup"><span data-stu-id="11a89-359">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="11a89-360">如需確切的 Framework 識別碼，請參閱[目標 Framework](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="11a89-360">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="11a89-361">下列範例會顯示所有目標 Framework 的 `System.Net` 參考，以及僅供 .NET Framework 4.0 使用的 `System.ServiceModel` 參考：</span><span class="sxs-lookup"><span data-stu-id="11a89-361">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="11a89-362">包含組件檔</span><span class="sxs-lookup"><span data-stu-id="11a89-362">Including assembly files</span></span>

<span data-ttu-id="11a89-363">如果遵循[建立套件](../create-packages/creating-a-package.md)中所述的慣例，即不必在 `.nuspec` 檔案中明確指定檔案清單。</span><span class="sxs-lookup"><span data-stu-id="11a89-363">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="11a89-364">`nuget pack` 命令會自動挑選必要的檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-364">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="11a89-365">當套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，「排除」那些名為 `.resources.dll` 的參考，因為它們假設是當地語系化的附屬組件。</span><span class="sxs-lookup"><span data-stu-id="11a89-365">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="11a89-366">因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="11a89-366">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="11a89-367">為略過這項自動行為並明確控制套件要包含哪些檔案，請放置 `<files>` 項目當作 `<package>` 的子系 (和 `<metadata>` 的同層級)，找出每個有不同 `<file>` 項目的檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-367">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="11a89-368">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-368">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="11a89-369">使用 NuGet 2.x 及更舊版本，並規劃使用 `packages.config`；在安裝套件時，也會使用 `<files>` 項目包含不可變的內容檔。</span><span class="sxs-lookup"><span data-stu-id="11a89-369">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="11a89-370">使用 NuGet 3.3+ 和專案 PackageReference，則改用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="11a89-370">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="11a89-371">如需詳細資料，請參閱下文中的[包含內容檔](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="11a89-371">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="11a89-372">檔案項目屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-372">File element attributes</span></span>

<span data-ttu-id="11a89-373">每個 `<file>` 項目都會指定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="11a89-373">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="11a89-374">屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-374">Attribute</span></span> | <span data-ttu-id="11a89-375">描述</span><span class="sxs-lookup"><span data-stu-id="11a89-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11a89-376">**src**</span><span class="sxs-lookup"><span data-stu-id="11a89-376">**src**</span></span> | <span data-ttu-id="11a89-377">要包含的檔案位置，會受到 `exclude` 屬性指定的排除項目約束。</span><span class="sxs-lookup"><span data-stu-id="11a89-377">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="11a89-378">路徑相對於 `.nuspec` 檔案，除非指定絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="11a89-378">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="11a89-379">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="11a89-379">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="11a89-380">**目標**</span><span class="sxs-lookup"><span data-stu-id="11a89-380">**target**</span></span> | <span data-ttu-id="11a89-381">套件內資料夾的相對路徑是放置原始程式檔的位置，其開頭必須是 `lib`、`content`、`build` 或 `tools`。</span><span class="sxs-lookup"><span data-stu-id="11a89-381">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="11a89-382">請參閱[從慣例的工作目錄建立 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。</span><span class="sxs-lookup"><span data-stu-id="11a89-382">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="11a89-383">**排除**</span><span class="sxs-lookup"><span data-stu-id="11a89-383">**exclude**</span></span> | <span data-ttu-id="11a89-384">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="11a89-384">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="11a89-385">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="11a89-385">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="11a89-386">範例</span><span class="sxs-lookup"><span data-stu-id="11a89-386">Examples</span></span>

<span data-ttu-id="11a89-387">**單一組件**</span><span class="sxs-lookup"><span data-stu-id="11a89-387">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="11a89-388">**目標 Framework 的特定單一組件**</span><span class="sxs-lookup"><span data-stu-id="11a89-388">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="11a89-389">**使用萬用字元的 DLL 集合**</span><span class="sxs-lookup"><span data-stu-id="11a89-389">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="11a89-390">**不同 Framework 的 DLL**</span><span class="sxs-lookup"><span data-stu-id="11a89-390">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="11a89-391">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="11a89-391">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="11a89-392">包含內容檔</span><span class="sxs-lookup"><span data-stu-id="11a89-392">Including content files</span></span>

<span data-ttu-id="11a89-393">內容檔是不可變的檔案，套件必須將它們包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="11a89-393">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="11a89-394">因為不可變，所以取用專案不宜修改它們。</span><span class="sxs-lookup"><span data-stu-id="11a89-394">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="11a89-395">內容檔範例包括：</span><span class="sxs-lookup"><span data-stu-id="11a89-395">Example content files include:</span></span>

- <span data-ttu-id="11a89-396">內嵌為資源的映像</span><span class="sxs-lookup"><span data-stu-id="11a89-396">Images that are embedded as resources</span></span>
- <span data-ttu-id="11a89-397">已編譯原始程式檔</span><span class="sxs-lookup"><span data-stu-id="11a89-397">Source files that are already compiled</span></span>
- <span data-ttu-id="11a89-398">需要以專案的組建輸出包含的指令碼</span><span class="sxs-lookup"><span data-stu-id="11a89-398">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="11a89-399">套件的組態檔必須包含在專案中，但不需要專門針對任何專案變更</span><span class="sxs-lookup"><span data-stu-id="11a89-399">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="11a89-400">內容檔包含在使用 `<files>` 項目的套件中，指定 `content` 屬性中的 `target` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="11a89-400">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="11a89-401">不過，使用 PackageReference 在專案中安裝套件時，會忽略這類檔案，改用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="11a89-401">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="11a89-402">為取得取用專案的最大相容性，套件應該在兩個項目中都指定內容檔。</span><span class="sxs-lookup"><span data-stu-id="11a89-402">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="11a89-403">內容檔使用 files 項目</span><span class="sxs-lookup"><span data-stu-id="11a89-403">Using the files element for content files</span></span>

<span data-ttu-id="11a89-404">內容檔只要使用和組件檔相同的格式即可，但要在 `content` 屬性中指定 `target` 作為基底資料夾，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="11a89-404">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="11a89-405">**基本內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-405">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="11a89-406">**具有目錄結構的內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-406">**Content files with directory structure**</span></span>

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

<span data-ttu-id="11a89-407">**目標 Framework 的特定內容檔案**</span><span class="sxs-lookup"><span data-stu-id="11a89-407">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="11a89-408">**複製到資料夾，名稱中有點的內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-408">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="11a89-409">在此情況下，NuGet 會看到 `target` 的副檔名與 `src` 的副檔名不相符，因此會將 `target` 名稱的該部分視為資料夾：</span><span class="sxs-lookup"><span data-stu-id="11a89-409">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="11a89-410">**無副檔名的內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-410">**Content files without extensions**</span></span>

<span data-ttu-id="11a89-411">若要包含不含副檔名的檔案，請使用 `*` 或 `**` 萬用字元：</span><span class="sxs-lookup"><span data-stu-id="11a89-411">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="11a89-412">**有深路徑和深層目標的內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-412">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="11a89-413">在此情況下，因為原始程式檔的副檔名和目標相符，所以 NuGet 會假設目標是檔案名稱，不是資料夾：</span><span class="sxs-lookup"><span data-stu-id="11a89-413">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="11a89-414">**重新命名套件中的內容檔**</span><span class="sxs-lookup"><span data-stu-id="11a89-414">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="11a89-415">**排除檔案**</span><span class="sxs-lookup"><span data-stu-id="11a89-415">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="11a89-416">內容檔使用 contentFiles 項目</span><span class="sxs-lookup"><span data-stu-id="11a89-416">Using the contentFiles element for content files</span></span>

<span data-ttu-id="11a89-417">*NuGet 4.0+ 與 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="11a89-417">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="11a89-418">根據預設，套件會將內容放在 `contentFiles` 資料夾 (請參閱下文)，而 `nuget pack` 包含使用預設屬性資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-418">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="11a89-419">在此情況下，`contentFiles` 完全不需要包含 `.nuspec` 節點。</span><span class="sxs-lookup"><span data-stu-id="11a89-419">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="11a89-420">為控制包含哪些檔案，`<contentFiles>` 項目要指定 `<files>` 項目的集合，找出正確的檔案。</span><span class="sxs-lookup"><span data-stu-id="11a89-420">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="11a89-421">這些檔案是由一組描述如何在專案系統內使用它們的屬性所指定：</span><span class="sxs-lookup"><span data-stu-id="11a89-421">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="11a89-422">屬性</span><span class="sxs-lookup"><span data-stu-id="11a89-422">Attribute</span></span> | <span data-ttu-id="11a89-423">描述</span><span class="sxs-lookup"><span data-stu-id="11a89-423">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11a89-424">**include**</span><span class="sxs-lookup"><span data-stu-id="11a89-424">**include**</span></span> | <span data-ttu-id="11a89-425">(必要) 要包含的檔案位置，受限於 `exclude` 屬性所指定的排除項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-425">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="11a89-426">除非指定絕對路徑，否則路徑會相對於 `contentFiles` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="11a89-426">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="11a89-427">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="11a89-427">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="11a89-428">**排除**</span><span class="sxs-lookup"><span data-stu-id="11a89-428">**exclude**</span></span> | <span data-ttu-id="11a89-429">`src` 位置要排除之以分號分隔的檔案清單或檔案模式。</span><span class="sxs-lookup"><span data-stu-id="11a89-429">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="11a89-430">允許萬用字元 `*`，而雙萬用字元 `**` 表示遞迴資料夾搜尋。</span><span class="sxs-lookup"><span data-stu-id="11a89-430">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="11a89-431">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="11a89-431">**buildAction**</span></span> | <span data-ttu-id="11a89-432">要指派給 MSBuild 內容專案的組建動作，例如 `Content`、`None`、`Embedded Resource`、`Compile`等等。預設值為 `Compile`。</span><span class="sxs-lookup"><span data-stu-id="11a89-432">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="11a89-433">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="11a89-433">**copyToOutput**</span></span> | <span data-ttu-id="11a89-434">布林值，指出是否要將內容專案複製到組建（或發行）輸出檔案夾。</span><span class="sxs-lookup"><span data-stu-id="11a89-434">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="11a89-435">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="11a89-435">The default is false.</span></span> |
| <span data-ttu-id="11a89-436">**flatten**</span><span class="sxs-lookup"><span data-stu-id="11a89-436">**flatten**</span></span> | <span data-ttu-id="11a89-437">布林值，指出要將內容項目複製到組建輸出的單一資料夾 (true)，或保留套件中的資料夾結構 (false)。</span><span class="sxs-lookup"><span data-stu-id="11a89-437">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="11a89-438">這個旗標僅適用於將 copyToOutput 旗標設為 true 時。</span><span class="sxs-lookup"><span data-stu-id="11a89-438">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="11a89-439">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="11a89-439">The default is false.</span></span> |

<span data-ttu-id="11a89-440">安裝套件時，NuGet 會由上而下套用 `<contentFiles>` 的子項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-440">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="11a89-441">如有多個項目符合同一檔案，則套用所有項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-441">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="11a89-442">如果相同的屬性發生衝突，則最上層項目會覆寫較低的項目。</span><span class="sxs-lookup"><span data-stu-id="11a89-442">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="11a89-443">套件資料夾結構</span><span class="sxs-lookup"><span data-stu-id="11a89-443">Package folder structure</span></span>

<span data-ttu-id="11a89-444">套件專案應該結構化使用下列模式的內容：</span><span class="sxs-lookup"><span data-stu-id="11a89-444">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="11a89-445">`codeLanguages` 可能是 `cs`、`vb`、`fs`、`any`，或指定的 `$(ProjectLanguage)` 小寫對等項</span><span class="sxs-lookup"><span data-stu-id="11a89-445">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="11a89-446">`TxM` 是 NuGet 支援的任何合法目標 Framework Moniker (請參閱[目標 Framework](../reference/target-frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="11a89-446">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="11a89-447">這個語法的結尾可以附加任何資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="11a89-447">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="11a89-448">例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-448">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="11a89-449">空資料夾可以使用 `.` 選擇不提供特定語言和 TxM 組合的內容，例如：</span><span class="sxs-lookup"><span data-stu-id="11a89-449">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="11a89-450">contentFiles 區段範例</span><span class="sxs-lookup"><span data-stu-id="11a89-450">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
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
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="11a89-451">架構參考群組</span><span class="sxs-lookup"><span data-stu-id="11a89-451">Framework reference groups</span></span>

<span data-ttu-id="11a89-452">*僅限5.1 版 + 使用 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="11a89-452">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="11a89-453">架構參考是代表共用架構（例如 WPF 或 Windows Forms）的 .NET Core 概念。</span><span class="sxs-lookup"><span data-stu-id="11a89-453">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="11a89-454">藉由指定共用架構，封裝可確保其所有架構相依性都包含在參考專案中。</span><span class="sxs-lookup"><span data-stu-id="11a89-454">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="11a89-455">每個 `<group>` 元素都需要 `targetFramework` 屬性和零或多個 `<frameworkReference>` 元素。</span><span class="sxs-lookup"><span data-stu-id="11a89-455">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="11a89-456">下列範例顯示針對 .NET Core WPF 專案產生的 nuspec。</span><span class="sxs-lookup"><span data-stu-id="11a89-456">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="11a89-457">請注意，不建議使用包含架構參考的手動撰寫 nuspecs。</span><span class="sxs-lookup"><span data-stu-id="11a89-457">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="11a89-458">請考慮改為使用[目標](msbuild-targets.md)套件，這會自動從專案推斷它們。</span><span class="sxs-lookup"><span data-stu-id="11a89-458">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="11a89-459">範例 nuspec 檔案</span><span class="sxs-lookup"><span data-stu-id="11a89-459">Example nuspec files</span></span>

<span data-ttu-id="11a89-460">**簡單的 `.nuspec` 不指定相依性或檔案**</span><span class="sxs-lookup"><span data-stu-id="11a89-460">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="11a89-461">**具有相依性的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="11a89-461">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="11a89-462">**具有檔案的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="11a89-462">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="11a89-463">**具有 Framework 組件的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="11a89-463">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="11a89-464">在此範例中，特定專案目標會安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="11a89-464">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="11a89-465">.NET4 -> `System.Web`、`System.Net`</span><span class="sxs-lookup"><span data-stu-id="11a89-465">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="11a89-466">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="11a89-466">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="11a89-467">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="11a89-467">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="11a89-468">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="11a89-468">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
