---
title: "NuGet.Config 檔案參考 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: "NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。"
keywords: "NuGet.Config 檔案, NuGet 組態參考, NuGet 組態選項"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 830c622f622b894a228b18dfdb3a790bccfde8a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="b40b4-104">NuGet.Config 參考</span><span class="sxs-lookup"><span data-stu-id="b40b4-104">NuGet.Config reference</span></span>

<span data-ttu-id="b40b4-105">NuGet 行為受到不同 `NuGet.Config` 檔案中的設定所控制，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="b40b4-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="b40b4-106">`NuGet.Config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。</span><span class="sxs-lookup"><span data-stu-id="b40b4-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="b40b4-107">每一個區段包含零個或更多 `<add>` 項目與 `key` 和 `value` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b40b4-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="b40b4-108">請參閱[設定檔範例](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="b40b4-109">設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="b40b4-110">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="b40b4-110">In this topic:</span></span>

- [<span data-ttu-id="b40b4-111">config 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-111">config section</span></span>](#config-section)
- [<span data-ttu-id="b40b4-112">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="b40b4-113">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="b40b4-114">solution 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="b40b4-115">[套件來源區段](#package-source-sections)：-[packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="b40b4-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="b40b4-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="b40b4-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="b40b4-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="b40b4-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="b40b4-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="b40b4-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="b40b4-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="b40b4-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="b40b4-120">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="b40b4-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="b40b4-121">設定檔範例</span><span class="sxs-lookup"><span data-stu-id="b40b4-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="b40b4-122">config 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-122">config section</span></span>

<span data-ttu-id="b40b4-123">包含其他組態設定，可以使用 [`nuget config` 命令](../tools/cli-ref-config.md)設定。</span><span class="sxs-lookup"><span data-stu-id="b40b4-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="b40b4-124">注意：`dependencyVersion` 和 `repositoryPath` 僅適用於使用 `packages.config` 的專案。</span><span class="sxs-lookup"><span data-stu-id="b40b4-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="b40b4-125">`globalPackagesFolder` 僅適用於使用 `project.json` 和 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="b40b4-125">`globalPackagesFolder` applies only to projects using `project.json` and PackageReference formats.</span></span>

| <span data-ttu-id="b40b4-126">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-126">Key</span></span> | <span data-ttu-id="b40b4-127">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-128">dependencyVersion (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="b40b4-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="b40b4-129">當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="b40b4-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="b40b4-130">NuGet 套件管理員 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="b40b4-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="b40b4-131">值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="b40b4-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="b40b4-132">globalPackagesFolder (不使用 `packages.config` 的專案)</span><span class="sxs-lookup"><span data-stu-id="b40b4-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="b40b4-133">預設全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="b40b4-133">The location of the default global packages folder.</span></span> <span data-ttu-id="b40b4-134">預設值為 `%USERPROFILE%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="b40b4-135">相對路徑可用於專案特有的 `Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b40b4-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="b40b4-136">repositoryPath (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="b40b4-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="b40b4-137">要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b40b4-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="b40b4-138">相對路徑可用於專案特有的 `Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b40b4-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="b40b4-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="b40b4-139">defaultPushSource</span></span> | <span data-ttu-id="b40b4-140">識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。</span><span class="sxs-lookup"><span data-stu-id="b40b4-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="b40b4-141">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="b40b4-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="b40b4-142">連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="b40b4-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="b40b4-143">密碼會加密，且無法手動新增。</span><span class="sxs-lookup"><span data-stu-id="b40b4-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="b40b4-144">對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="b40b4-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="b40b4-145">您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。</span><span class="sxs-lookup"><span data-stu-id="b40b4-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="b40b4-146">如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="b40b4-147">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="b40b4-148">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-148">bindingRedirects section</span></span>

<span data-ttu-id="b40b4-149">設定 NuGet 在安裝套件時，是否自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="b40b4-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="b40b4-150">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-150">Key</span></span> | <span data-ttu-id="b40b4-151">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-152">skip</span><span class="sxs-lookup"><span data-stu-id="b40b4-152">skip</span></span> | <span data-ttu-id="b40b4-153">布林值，指出是否略過自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="b40b4-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="b40b4-154">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="b40b4-154">The default is false.</span></span> |

<span data-ttu-id="b40b4-155">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="b40b4-156">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-156">packageRestore section</span></span>

<span data-ttu-id="b40b4-157">*在 2.7+ 中忽略*</span><span class="sxs-lookup"><span data-stu-id="b40b4-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="b40b4-158">控制建置期間的套件還原。</span><span class="sxs-lookup"><span data-stu-id="b40b4-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="b40b4-159">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-159">Key</span></span> | <span data-ttu-id="b40b4-160">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-161">enabled</span><span class="sxs-lookup"><span data-stu-id="b40b4-161">enabled</span></span> | <span data-ttu-id="b40b4-162">布林值，指出 NuGet 是否可以執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="b40b4-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="b40b4-163">您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。</span><span class="sxs-lookup"><span data-stu-id="b40b4-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="b40b4-164">自動</span><span class="sxs-lookup"><span data-stu-id="b40b4-164">automatic</span></span> | <span data-ttu-id="b40b4-165">布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="b40b4-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="b40b4-166">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="b40b4-167">solution 區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-167">solution section</span></span>

<span data-ttu-id="b40b4-168">控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="b40b4-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="b40b4-169">本區段只適用於解決方案資料夾中的 `Nuget.Config` 檔。</span><span class="sxs-lookup"><span data-stu-id="b40b4-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="b40b4-170">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-170">Key</span></span> | <span data-ttu-id="b40b4-171">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="b40b4-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="b40b4-173">布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b40b4-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="b40b4-174">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="b40b4-174">The default value is false.</span></span> |

<span data-ttu-id="b40b4-175">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="b40b4-176">套件來源區段</span><span class="sxs-lookup"><span data-stu-id="b40b4-176">Package source sections</span></span>

<span data-ttu-id="b40b4-177">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起運作，以設定 NuGet 在安裝、還原及更新作業期間，如何處理套件儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b40b4-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="b40b4-178">[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用來管理這些設定，但 `apikeys` 例外，它是使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)來管理。</span><span class="sxs-lookup"><span data-stu-id="b40b4-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="b40b4-179">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="b40b4-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="b40b4-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="b40b4-180">packageSources</span></span>

<span data-ttu-id="b40b4-181">列出所有已知的套件來源。</span><span class="sxs-lookup"><span data-stu-id="b40b4-181">Lists all known package sources.</span></span>

| <span data-ttu-id="b40b4-182">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-182">Key</span></span> | <span data-ttu-id="b40b4-183">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-184">(要指派給套件來源的名稱)</span><span class="sxs-lookup"><span data-stu-id="b40b4-184">(name to assign to the package source)</span></span> | <span data-ttu-id="b40b4-185">套件來源的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="b40b4-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="b40b4-186">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="b40b4-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="b40b4-187">packageSourceCredentials</span></span>

<span data-ttu-id="b40b4-188">儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。</span><span class="sxs-lookup"><span data-stu-id="b40b4-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="b40b4-189">依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。</span><span class="sxs-lookup"><span data-stu-id="b40b4-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="b40b4-190">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-190">Key</span></span> | <span data-ttu-id="b40b4-191">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-192">username</span><span class="sxs-lookup"><span data-stu-id="b40b4-192">username</span></span> | <span data-ttu-id="b40b4-193">純文字的來源使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b40b4-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="b40b4-194">密碼</span><span class="sxs-lookup"><span data-stu-id="b40b4-194">password</span></span> | <span data-ttu-id="b40b4-195">加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="b40b4-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="b40b4-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="b40b4-196">cleartextpassword</span></span> | <span data-ttu-id="b40b4-197">未加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="b40b4-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="b40b4-198">**範例：**</span><span class="sxs-lookup"><span data-stu-id="b40b4-198">**Example:**</span></span>

<span data-ttu-id="b40b4-199">設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020+`)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="b40b4-200">也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="b40b4-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="b40b4-201">使用未加密的密碼時：</span><span class="sxs-lookup"><span data-stu-id="b40b4-201">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="b40b4-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="b40b4-202">apikeys</span></span>

<span data-ttu-id="b40b4-203">為使用 API 金鑰驗證的來源儲存金鑰，如同以 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)所設。</span><span class="sxs-lookup"><span data-stu-id="b40b4-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="b40b4-204">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-204">Key</span></span> | <span data-ttu-id="b40b4-205">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-206">(來源 URL)</span><span class="sxs-lookup"><span data-stu-id="b40b4-206">(source URL)</span></span> | <span data-ttu-id="b40b4-207">加密的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b40b4-207">The encrypted API key.</span></span> |

<span data-ttu-id="b40b4-208">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="b40b4-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="b40b4-209">disabledPackageSources</span></span>

<span data-ttu-id="b40b4-210">識別目前已停用的來源。</span><span class="sxs-lookup"><span data-stu-id="b40b4-210">Identified currently disabled sources.</span></span> <span data-ttu-id="b40b4-211">可以是空的。</span><span class="sxs-lookup"><span data-stu-id="b40b4-211">May be empty.</span></span>

| <span data-ttu-id="b40b4-212">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-212">Key</span></span> | <span data-ttu-id="b40b4-213">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-214">(來源名稱)</span><span class="sxs-lookup"><span data-stu-id="b40b4-214">(name of source)</span></span> | <span data-ttu-id="b40b4-215">布林值，指出是否停用來源。</span><span class="sxs-lookup"><span data-stu-id="b40b4-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="b40b4-216">**範例：**</span><span class="sxs-lookup"><span data-stu-id="b40b4-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="b40b4-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="b40b4-217">activePackageSource</span></span>

<span data-ttu-id="b40b4-218">*(僅 2.x，在 3.x+ 中已被取代)*</span><span class="sxs-lookup"><span data-stu-id="b40b4-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="b40b4-219">識別目前作用中的來源，或表示所有來源的彙總。</span><span class="sxs-lookup"><span data-stu-id="b40b4-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="b40b4-220">Key</span><span class="sxs-lookup"><span data-stu-id="b40b4-220">Key</span></span> | <span data-ttu-id="b40b4-221">值</span><span class="sxs-lookup"><span data-stu-id="b40b4-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b40b4-222">(來源名稱) 或 `All`</span><span class="sxs-lookup"><span data-stu-id="b40b4-222">(name of source) or `All`</span></span> | <span data-ttu-id="b40b4-223">如果金鑰是來源的名稱，則值是來源路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="b40b4-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="b40b4-224">若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="b40b4-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="b40b4-225">**範例**：</span><span class="sxs-lookup"><span data-stu-id="b40b4-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="b40b4-226">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="b40b4-226">Using environment variables</span></span>

<span data-ttu-id="b40b4-227">您可以在 `NuGet.Config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。</span><span class="sxs-lookup"><span data-stu-id="b40b4-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="b40b4-228">例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="b40b4-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="b40b4-229">同樣地，如果 Mac/Linux 上的 `HOME` 設為 `/home/myStuff`，則設定檔中的 `$HOME/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="b40b4-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="b40b4-230">如果找不到環境變數，NuGet 會使用來自設定檔的常值。</span><span class="sxs-lookup"><span data-stu-id="b40b4-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="b40b4-231">範例設定檔</span><span class="sxs-lookup"><span data-stu-id="b40b4-231">Example config file</span></span>

<span data-ttu-id="b40b4-232">以下是 `NuGet.Config` 檔範例，說明多項設定：</span><span class="sxs-lookup"><span data-stu-id="b40b4-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
