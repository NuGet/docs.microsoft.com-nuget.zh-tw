---
title: "NuGet.Config 檔案參考 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。"
keywords: "NuGet.Config 檔案, NuGet 組態參考, NuGet 組態選項"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a5be1ebcca0accafcdaf32f0b1b7ca66ec53425
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="9e762-104">NuGet.Config 參考</span><span class="sxs-lookup"><span data-stu-id="9e762-104">NuGet.Config reference</span></span>

<span data-ttu-id="9e762-105">NuGet 行為受到不同 `NuGet.Config` 檔案中的設定所控制，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="9e762-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="9e762-106">`NuGet.Config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。</span><span class="sxs-lookup"><span data-stu-id="9e762-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="9e762-107">每一個區段包含零個或更多 `<add>` 項目與 `key` 和 `value` 屬性。</span><span class="sxs-lookup"><span data-stu-id="9e762-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="9e762-108">請參閱[設定檔範例](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="9e762-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="9e762-109">設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="9e762-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="9e762-110">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="9e762-110">In this topic:</span></span>

- [<span data-ttu-id="9e762-111">config 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-111">config section</span></span>](#config-section)
- [<span data-ttu-id="9e762-112">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="9e762-113">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="9e762-114">solution 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="9e762-115">[套件來源區段](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="9e762-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="9e762-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="9e762-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="9e762-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="9e762-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="9e762-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="9e762-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="9e762-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="9e762-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="9e762-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="9e762-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="9e762-121">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="9e762-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="9e762-122">設定檔範例</span><span class="sxs-lookup"><span data-stu-id="9e762-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="9e762-123">config 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-123">config section</span></span>

<span data-ttu-id="9e762-124">包含其他組態設定，可以使用 [`nuget config` 命令](../tools/cli-ref-config.md)設定。</span><span class="sxs-lookup"><span data-stu-id="9e762-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="9e762-125">注意：`dependencyVersion` 和 `repositoryPath` 僅適用於使用 `packages.config` 的專案。</span><span class="sxs-lookup"><span data-stu-id="9e762-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="9e762-126">`globalPackagesFolder` 僅適用於使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="9e762-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="9e762-127">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-127">Key</span></span> | <span data-ttu-id="9e762-128">值</span><span class="sxs-lookup"><span data-stu-id="9e762-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-129">dependencyVersion (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="9e762-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="9e762-130">當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="9e762-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="9e762-131">NuGet 套件管理員 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="9e762-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="9e762-132">值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="9e762-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="9e762-133">globalPackagesFolder (不使用 `packages.config` 的專案)</span><span class="sxs-lookup"><span data-stu-id="9e762-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="9e762-134">預設全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="9e762-134">The location of the default global packages folder.</span></span> <span data-ttu-id="9e762-135">預設值為 `%USERPROFILE%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="9e762-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="9e762-136">相對路徑可用於專案特有的 `Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e762-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="9e762-137">repositoryPath (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="9e762-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="9e762-138">要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e762-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="9e762-139">相對路徑可用於專案特有的 `Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e762-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="9e762-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="9e762-140">defaultPushSource</span></span> | <span data-ttu-id="9e762-141">識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。</span><span class="sxs-lookup"><span data-stu-id="9e762-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="9e762-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="9e762-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="9e762-143">連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="9e762-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="9e762-144">密碼會加密，且無法手動新增。</span><span class="sxs-lookup"><span data-stu-id="9e762-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="9e762-145">對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="9e762-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="9e762-146">您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9e762-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="9e762-147">如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="9e762-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="9e762-148">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="9e762-149">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-149">bindingRedirects section</span></span>

<span data-ttu-id="9e762-150">設定 NuGet 在安裝套件時，是否自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="9e762-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="9e762-151">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-151">Key</span></span> | <span data-ttu-id="9e762-152">值</span><span class="sxs-lookup"><span data-stu-id="9e762-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-153">skip</span><span class="sxs-lookup"><span data-stu-id="9e762-153">skip</span></span> | <span data-ttu-id="9e762-154">布林值，指出是否略過自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="9e762-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="9e762-155">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="9e762-155">The default is false.</span></span> |

<span data-ttu-id="9e762-156">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="9e762-157">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-157">packageRestore section</span></span>

<span data-ttu-id="9e762-158">控制建置期間的套件還原。</span><span class="sxs-lookup"><span data-stu-id="9e762-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="9e762-159">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-159">Key</span></span> | <span data-ttu-id="9e762-160">值</span><span class="sxs-lookup"><span data-stu-id="9e762-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-161">enabled</span><span class="sxs-lookup"><span data-stu-id="9e762-161">enabled</span></span> | <span data-ttu-id="9e762-162">布林值，指出 NuGet 是否可以執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="9e762-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="9e762-163">您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e762-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="9e762-164">自動</span><span class="sxs-lookup"><span data-stu-id="9e762-164">automatic</span></span> | <span data-ttu-id="9e762-165">布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="9e762-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="9e762-166">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="9e762-167">solution 區段</span><span class="sxs-lookup"><span data-stu-id="9e762-167">solution section</span></span>

<span data-ttu-id="9e762-168">控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="9e762-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="9e762-169">本區段只適用於解決方案資料夾中的 `Nuget.Config` 檔。</span><span class="sxs-lookup"><span data-stu-id="9e762-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="9e762-170">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-170">Key</span></span> | <span data-ttu-id="9e762-171">值</span><span class="sxs-lookup"><span data-stu-id="9e762-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="9e762-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="9e762-173">布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e762-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="9e762-174">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="9e762-174">The default value is false.</span></span> |

<span data-ttu-id="9e762-175">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="9e762-176">套件來源區段</span><span class="sxs-lookup"><span data-stu-id="9e762-176">Package source sections</span></span>

<span data-ttu-id="9e762-177">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起運作，以設定 NuGet 在安裝、還原及更新作業期間，如何處理套件儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9e762-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="9e762-178">[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用來管理這些設定，但 `apikeys` 例外，它是使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)來管理。</span><span class="sxs-lookup"><span data-stu-id="9e762-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="9e762-179">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="9e762-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="9e762-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="9e762-180">packageSources</span></span>

<span data-ttu-id="9e762-181">列出所有已知的套件來源。</span><span class="sxs-lookup"><span data-stu-id="9e762-181">Lists all known package sources.</span></span> <span data-ttu-id="9e762-182">在還原作業期間，以及與任何使用 PackageReference 格式的專案，會忽略順序。</span><span class="sxs-lookup"><span data-stu-id="9e762-182">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="9e762-183">NuGet 尊重安裝的來源順序，並使用專案以更新 operations `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="9e762-183">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="9e762-184">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-184">Key</span></span> | <span data-ttu-id="9e762-185">值</span><span class="sxs-lookup"><span data-stu-id="9e762-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-186">(要指派給套件來源的名稱)</span><span class="sxs-lookup"><span data-stu-id="9e762-186">(name to assign to the package source)</span></span> | <span data-ttu-id="9e762-187">套件來源的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="9e762-187">The path or URL of the package source.</span></span> |

<span data-ttu-id="9e762-188">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-188">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="9e762-189">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="9e762-189">packageSourceCredentials</span></span>

<span data-ttu-id="9e762-190">儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。</span><span class="sxs-lookup"><span data-stu-id="9e762-190">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="9e762-191">依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。</span><span class="sxs-lookup"><span data-stu-id="9e762-191">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="9e762-192">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-192">Key</span></span> | <span data-ttu-id="9e762-193">值</span><span class="sxs-lookup"><span data-stu-id="9e762-193">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-194">username</span><span class="sxs-lookup"><span data-stu-id="9e762-194">username</span></span> | <span data-ttu-id="9e762-195">純文字的來源使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9e762-195">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="9e762-196">密碼</span><span class="sxs-lookup"><span data-stu-id="9e762-196">password</span></span> | <span data-ttu-id="9e762-197">加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="9e762-197">The encrypted password for the source.</span></span> |
| <span data-ttu-id="9e762-198">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="9e762-198">cleartextpassword</span></span> | <span data-ttu-id="9e762-199">未加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="9e762-199">The unencrypted password for the source.</span></span> |

<span data-ttu-id="9e762-200">**範例：**</span><span class="sxs-lookup"><span data-stu-id="9e762-200">**Example:**</span></span>

<span data-ttu-id="9e762-201">設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020_`)。</span><span class="sxs-lookup"><span data-stu-id="9e762-201">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="9e762-202">也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="9e762-202">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="9e762-203">使用未加密的密碼時：</span><span class="sxs-lookup"><span data-stu-id="9e762-203">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="9e762-204">apikeys</span><span class="sxs-lookup"><span data-stu-id="9e762-204">apikeys</span></span>

<span data-ttu-id="9e762-205">為使用 API 金鑰驗證的來源儲存金鑰，如同以 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)所設。</span><span class="sxs-lookup"><span data-stu-id="9e762-205">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="9e762-206">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-206">Key</span></span> | <span data-ttu-id="9e762-207">值</span><span class="sxs-lookup"><span data-stu-id="9e762-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-208">(來源 URL)</span><span class="sxs-lookup"><span data-stu-id="9e762-208">(source URL)</span></span> | <span data-ttu-id="9e762-209">加密的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e762-209">The encrypted API key.</span></span> |

<span data-ttu-id="9e762-210">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-210">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="9e762-211">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="9e762-211">disabledPackageSources</span></span>

<span data-ttu-id="9e762-212">識別目前已停用的來源。</span><span class="sxs-lookup"><span data-stu-id="9e762-212">Identified currently disabled sources.</span></span> <span data-ttu-id="9e762-213">可以是空的。</span><span class="sxs-lookup"><span data-stu-id="9e762-213">May be empty.</span></span>

| <span data-ttu-id="9e762-214">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-214">Key</span></span> | <span data-ttu-id="9e762-215">值</span><span class="sxs-lookup"><span data-stu-id="9e762-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-216">(來源名稱)</span><span class="sxs-lookup"><span data-stu-id="9e762-216">(name of source)</span></span> | <span data-ttu-id="9e762-217">布林值，指出是否停用來源。</span><span class="sxs-lookup"><span data-stu-id="9e762-217">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="9e762-218">**範例：**</span><span class="sxs-lookup"><span data-stu-id="9e762-218">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="9e762-219">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="9e762-219">activePackageSource</span></span>

<span data-ttu-id="9e762-220">*(僅 2.x，在 3.x+ 中已被取代)*</span><span class="sxs-lookup"><span data-stu-id="9e762-220">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="9e762-221">識別目前作用中的來源，或表示所有來源的彙總。</span><span class="sxs-lookup"><span data-stu-id="9e762-221">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="9e762-222">Key</span><span class="sxs-lookup"><span data-stu-id="9e762-222">Key</span></span> | <span data-ttu-id="9e762-223">值</span><span class="sxs-lookup"><span data-stu-id="9e762-223">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9e762-224">(來源名稱) 或 `All`</span><span class="sxs-lookup"><span data-stu-id="9e762-224">(name of source) or `All`</span></span> | <span data-ttu-id="9e762-225">如果金鑰是來源的名稱，則值是來源路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="9e762-225">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="9e762-226">若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="9e762-226">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="9e762-227">**範例**：</span><span class="sxs-lookup"><span data-stu-id="9e762-227">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="9e762-228">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="9e762-228">Using environment variables</span></span>

<span data-ttu-id="9e762-229">您可以在 `NuGet.Config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。</span><span class="sxs-lookup"><span data-stu-id="9e762-229">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="9e762-230">例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="9e762-230">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="9e762-231">同樣地，如果 Mac/Linux 上的 `HOME` 設為 `/home/myStuff`，則設定檔中的 `$HOME/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="9e762-231">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="9e762-232">如果找不到環境變數，NuGet 會使用來自設定檔的常值。</span><span class="sxs-lookup"><span data-stu-id="9e762-232">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="9e762-233">範例設定檔</span><span class="sxs-lookup"><span data-stu-id="9e762-233">Example config file</span></span>

<span data-ttu-id="9e762-234">以下是 `NuGet.Config` 檔範例，說明多項設定：</span><span class="sxs-lookup"><span data-stu-id="9e762-234">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
