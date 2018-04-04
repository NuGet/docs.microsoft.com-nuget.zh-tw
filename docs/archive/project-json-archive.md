---
title: NuGet project.json 封存內容 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 從 NuGet 文件的其他區域所移除的各種 project.json 內容。
keywords: NuGet project.json 檔案
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="8b05b-104">project.json 封存</span><span class="sxs-lookup"><span data-stu-id="8b05b-104">project.json archive</span></span>

<span data-ttu-id="8b05b-105">`project.json` 管理格式於 NuGet 3.x 引進並用於某些專案類型。</span><span class="sxs-lookup"><span data-stu-id="8b05b-105">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="8b05b-106">此格式已隨著 PackageReference 格式的引進而被取代，後者將相依性直接列在專案檔中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="8b05b-107">另請參閱：</span><span class="sxs-lookup"><span data-stu-id="8b05b-107">Also see:</span></span>

- [<span data-ttu-id="8b05b-108">project.json 結構描述</span><span class="sxs-lookup"><span data-stu-id="8b05b-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="8b05b-109">project.json 對套件作者的影響</span><span class="sxs-lookup"><span data-stu-id="8b05b-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="8b05b-110">project.json 和 UWP</span><span class="sxs-lookup"><span data-stu-id="8b05b-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="8b05b-111">project.json 管理格式</span><span class="sxs-lookup"><span data-stu-id="8b05b-111">project.json management format</span></span>

<span data-ttu-id="8b05b-112">原本在[套件還原](../what-is-nuget.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="8b05b-113">在管理格式的清單中：</span><span class="sxs-lookup"><span data-stu-id="8b05b-113">In the list of management formats:</span></span>

- <span data-ttu-id="8b05b-114">[`project.json`](project-json.md)：(已過時) 這是一個 JSON 檔案，負責維護相關檔案 (`project.lock.json`) 中專案與整體套件關係圖的相依性清單。</span><span class="sxs-lookup"><span data-stu-id="8b05b-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="8b05b-115">此格式已由 PackageReference 所取代。</span><span class="sxs-lookup"><span data-stu-id="8b05b-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="8b05b-116">在 Mono 上的 nuget restore</span><span class="sxs-lookup"><span data-stu-id="8b05b-116">nuget restore on Mono</span></span>

<span data-ttu-id="8b05b-117">原本在[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)中</span><span class="sxs-lookup"><span data-stu-id="8b05b-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="8b05b-118">適用於 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="8b05b-119">使用還原限制套件版本</span><span class="sxs-lookup"><span data-stu-id="8b05b-119">Constraining package versions with restore</span></span>

<span data-ttu-id="8b05b-120">原本在[套件還原](../consume-packages/package-restore.md#constraining-package-versions-with-restore)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="8b05b-121">`project.json`：直接使用相依性的版本號碼來指定版本範圍。</span><span class="sxs-lookup"><span data-stu-id="8b05b-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="8b05b-122">例如: </span><span class="sxs-lookup"><span data-stu-id="8b05b-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="8b05b-123">NuGet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="8b05b-123">NuGet CLI commands</span></span>

- <span data-ttu-id="8b05b-124">`nuget install` 不適用於 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="8b05b-125">`nuget restore`：針對使用 `project.json` 的專案，會視需要產生 `project.lock.json` 檔案和 `<project>.nuget.props` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8b05b-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="8b05b-126">(兩個檔案都可以從原始檔控制省略)。`<projectPath>` 引數可以指向 `project.json` 檔案，且其行為就和指向 `packages.config` 或專案檔一樣。</span><span class="sxs-lookup"><span data-stu-id="8b05b-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="8b05b-127">根據套件資料夾的優先順序，使用 `project.json` 時會先搜尋 `%userprofile%\.nuget\packages`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="8b05b-128">`nuget update`：在 Mono 上，此命令無法與使用 `project.json` 的專案搭配使用。</span><span class="sxs-lookup"><span data-stu-id="8b05b-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="8b05b-129">使用 PackageReference 的相依性解析</span><span class="sxs-lookup"><span data-stu-id="8b05b-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="8b05b-130">原本在[相依性解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="8b05b-131">PackageReference 的行為也適用於 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="8b05b-132">NuGet restore 將相依性關係圖寫入名為 `project.lock.json` 和 `project.json` 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="8b05b-133">管理相依性資產</span><span class="sxs-lookup"><span data-stu-id="8b05b-133">Managing dependency assets</span></span>

<span data-ttu-id="8b05b-134">原本在[相依性解析](../consume-packages/dependency-resolution.md#managing-dependency-assets)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="8b05b-135">使用 `project.json` 格式時，您可以控制從相依性流入最上層專案的資產。</span><span class="sxs-lookup"><span data-stu-id="8b05b-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="8b05b-136">如需詳細資訊，請參閱 [project.json](project-json.md)。</span><span class="sxs-lookup"><span data-stu-id="8b05b-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="8b05b-137">排除參考</span><span class="sxs-lookup"><span data-stu-id="8b05b-137">Excluding references</span></span>

<span data-ttu-id="8b05b-138">原本在[相依性解析](../consume-packages/dependency-resolution.md#excluding-references)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="8b05b-139">`project.json`：在套件 C 的相依性中新增 `"exclude" : "all"`：</span><span class="sxs-lookup"><span data-stu-id="8b05b-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="8b05b-140">解決不相容的套件錯誤</span><span class="sxs-lookup"><span data-stu-id="8b05b-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="8b05b-141">原本在[相依性解析](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="8b05b-142">新增解決錯誤的方法：</span><span class="sxs-lookup"><span data-stu-id="8b05b-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="8b05b-143">**不建議**：作為與套件作者合作時的暫時方案，目標設為 `netcore`、`netstandard` 和 `netcoreapp` 的專案可以將其他架構表示為相容，進而允許使用將目標設為這些其他架構的套件。</span><span class="sxs-lookup"><span data-stu-id="8b05b-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="8b05b-144">請參閱 [project.json 匯入](project-json.md#imports)和 [MSBuild 還原目標 PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback)。</span><span class="sxs-lookup"><span data-stu-id="8b05b-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="8b05b-145">這可能會造成非預期的行為，因此，同樣地，最好與套件作者合作處理更新，以解決套件不相容。</span><span class="sxs-lookup"><span data-stu-id="8b05b-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="8b05b-146">目標 Framework</span><span class="sxs-lookup"><span data-stu-id="8b05b-146">Target frameworks</span></span>

<span data-ttu-id="8b05b-147">原本在[目標 Framework](../reference/target-frameworks.md) 中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="8b05b-148">[project.json](project-json.md)：`frameworks` 節點會指定專案可以編譯的 Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="8b05b-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="8b05b-149">建立套件</span><span class="sxs-lookup"><span data-stu-id="8b05b-149">Creating a package</span></span>

<span data-ttu-id="8b05b-150">原本在[建立套件](../create-packages/creating-a-package.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="8b05b-151">設定套件類型</span><span class="sxs-lookup"><span data-stu-id="8b05b-151">Setting a package type</span></span>

<span data-ttu-id="8b05b-152">使用 .NET Core 1.x 時，若安裝了 DotnetCliTool 套件，Visual Studio 會將套件放入 `project.json` `tools` 節點中，而不是 `dependencies` 節點。</span><span class="sxs-lookup"><span data-stu-id="8b05b-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="8b05b-153">套件類型是在 `project.json` 中設定的。</span><span class="sxs-lookup"><span data-stu-id="8b05b-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="8b05b-154">`project.json`：指出 `packOptions.packageType` 屬性 json 內的套件類型：</span><span class="sxs-lookup"><span data-stu-id="8b05b-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="8b05b-155">新增 MSBuild 的目標與 props</span><span class="sxs-lookup"><span data-stu-id="8b05b-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="8b05b-156">原本在[使用 Visual Studio 2015 建立 .NET Standard NuGet 套件](../guides/create-net-standard-packages-vs2015.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="8b05b-157">當使用 `project.json` 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。</span><span class="sxs-lookup"><span data-stu-id="8b05b-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="8b05b-158">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="8b05b-158">Package versioning</span></span>

<span data-ttu-id="8b05b-159">原本在[套件版本控制](../reference/package-versioning.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="8b05b-160">當使用 `project.json` 格式時，針對編號的主要、次要、修補和發行前版本後置詞部分，NuGet 也支援使用萬用字元標記法 (\*)。</span><span class="sxs-lookup"><span data-stu-id="8b05b-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="8b05b-161">NuGet.Config 參考</span><span class="sxs-lookup"><span data-stu-id="8b05b-161">NuGet.Config reference</span></span>

<span data-ttu-id="8b05b-162">原本在 [NuGet.Config 參考](../reference/nuget-config-file.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="8b05b-163">`globalPackagesFolder` 僅適用於 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-163">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="8b05b-164">(新增附註：也適用於 PackageReference。)</span><span class="sxs-lookup"><span data-stu-id="8b05b-164">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="8b05b-165">nuspec 檔案參考</span><span class="sxs-lookup"><span data-stu-id="8b05b-165">nuspec file reference</span></span>

<span data-ttu-id="8b05b-166">原本在 [nuspec 參考](../reference/nuspec.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-166">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="8b05b-167">使用 `<contentFiles>` 元素，而不是包含 `project.json` 的 `<files>`。</span><span class="sxs-lookup"><span data-stu-id="8b05b-167">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="8b05b-168">套件管理員選項控制</span><span class="sxs-lookup"><span data-stu-id="8b05b-168">Package manager options control</span></span>

<span data-ttu-id="8b05b-169">原本在[套件管理員 UI 參考](../tools/package-manager-ui.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-169">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="8b05b-170">使用 `project.json` 管理格式的專案只顯示 [顯示預覽視窗] 選項。</span><span class="sxs-lookup"><span data-stu-id="8b05b-170">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="8b05b-171">Visual Studio 範本</span><span class="sxs-lookup"><span data-stu-id="8b05b-171">Visual Studio Templates</span></span>

<span data-ttu-id="8b05b-172">原本在 [Visual Studio 範本中的 NuGet 套件](../visual-studio-extensibility/visual-studio-templates.md)中。</span><span class="sxs-lookup"><span data-stu-id="8b05b-172">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="8b05b-173">最佳做法：範本不包含 `project.json` 檔案，而且不包含安裝 NuGet 套件時所新增的任何參考或內容。</span><span class="sxs-lookup"><span data-stu-id="8b05b-173">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>