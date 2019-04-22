---
title: nuget.config 檔案參考
description: NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911084"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="22e78-103">nuget.config 參考</span><span class="sxs-lookup"><span data-stu-id="22e78-103">nuget.config reference</span></span>

<span data-ttu-id="22e78-104">NuGet 行為受到不同 `NuGet.Config` 檔案中的設定所控制，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="22e78-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="22e78-105">`nuget.config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。</span><span class="sxs-lookup"><span data-stu-id="22e78-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="22e78-106">每個區段包含零個以上的項目。</span><span class="sxs-lookup"><span data-stu-id="22e78-106">Each section contains zero or more items.</span></span> <span data-ttu-id="22e78-107">請參閱[設定檔範例](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="22e78-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="22e78-108">設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="22e78-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="22e78-109">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="22e78-109">In this topic:</span></span>

- [<span data-ttu-id="22e78-110">config 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-110">config section</span></span>](#config-section)
- [<span data-ttu-id="22e78-111">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="22e78-112">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="22e78-113">solution 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="22e78-114">[套件來源區段](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="22e78-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="22e78-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="22e78-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="22e78-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="22e78-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="22e78-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="22e78-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="22e78-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="22e78-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="22e78-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="22e78-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="22e78-120">trustedSigners 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="22e78-121">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="22e78-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="22e78-122">設定檔範例</span><span class="sxs-lookup"><span data-stu-id="22e78-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="22e78-123">config 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-123">config section</span></span>

<span data-ttu-id="22e78-124">包含其他組態設定，可以使用 [`nuget config` 命令](../tools/cli-ref-config.md)設定。</span><span class="sxs-lookup"><span data-stu-id="22e78-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="22e78-125">`dependencyVersion` 並`repositoryPath`僅適用於使用專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="22e78-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="22e78-126">`globalPackagesFolder` 只適用於使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="22e78-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="22e78-127">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-127">Key</span></span> | <span data-ttu-id="22e78-128">值</span><span class="sxs-lookup"><span data-stu-id="22e78-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-129">dependencyVersion (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="22e78-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="22e78-130">當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="22e78-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="22e78-131">NuGet 套件管理員 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="22e78-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="22e78-132">值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="22e78-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="22e78-133">globalPackagesFolder （僅限使用 PackageReference 的專案）</span><span class="sxs-lookup"><span data-stu-id="22e78-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="22e78-134">預設全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="22e78-134">The location of the default global packages folder.</span></span> <span data-ttu-id="22e78-135">預設值為 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="22e78-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="22e78-136">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="22e78-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="22e78-137">此設定會覆寫 NUGET_PACKAGES 環境變數，會優先使用。</span><span class="sxs-lookup"><span data-stu-id="22e78-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="22e78-138">repositoryPath (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="22e78-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="22e78-139">要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e78-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="22e78-140">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="22e78-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="22e78-141">此設定會覆寫 NUGET_PACKAGES 環境變數，會優先使用。</span><span class="sxs-lookup"><span data-stu-id="22e78-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="22e78-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="22e78-142">defaultPushSource</span></span> | <span data-ttu-id="22e78-143">識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。</span><span class="sxs-lookup"><span data-stu-id="22e78-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="22e78-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="22e78-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="22e78-145">連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="22e78-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="22e78-146">密碼會加密，且無法手動新增。</span><span class="sxs-lookup"><span data-stu-id="22e78-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="22e78-147">對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="22e78-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="22e78-148">您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。</span><span class="sxs-lookup"><span data-stu-id="22e78-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="22e78-149">如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="22e78-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="22e78-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="22e78-150">signatureValidationMode</span></span> | <span data-ttu-id="22e78-151">指定用來驗證套件安裝的套件簽章和還原的驗證模式。</span><span class="sxs-lookup"><span data-stu-id="22e78-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="22e78-152">值為`accept`， `require`。</span><span class="sxs-lookup"><span data-stu-id="22e78-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="22e78-153">預設值為 `accept`。</span><span class="sxs-lookup"><span data-stu-id="22e78-153">Defaults to `accept`.</span></span>

<span data-ttu-id="22e78-154">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="22e78-155">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-155">bindingRedirects section</span></span>

<span data-ttu-id="22e78-156">設定 NuGet 在安裝套件時，是否自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="22e78-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="22e78-157">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-157">Key</span></span> | <span data-ttu-id="22e78-158">值</span><span class="sxs-lookup"><span data-stu-id="22e78-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-159">skip</span><span class="sxs-lookup"><span data-stu-id="22e78-159">skip</span></span> | <span data-ttu-id="22e78-160">布林值，指出是否略過自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="22e78-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="22e78-161">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="22e78-161">The default is false.</span></span> |

<span data-ttu-id="22e78-162">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="22e78-163">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-163">packageRestore section</span></span>

<span data-ttu-id="22e78-164">控制建置期間的套件還原。</span><span class="sxs-lookup"><span data-stu-id="22e78-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="22e78-165">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-165">Key</span></span> | <span data-ttu-id="22e78-166">值</span><span class="sxs-lookup"><span data-stu-id="22e78-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-167">enabled</span><span class="sxs-lookup"><span data-stu-id="22e78-167">enabled</span></span> | <span data-ttu-id="22e78-168">布林值，指出 NuGet 是否可以執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="22e78-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="22e78-169">您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。</span><span class="sxs-lookup"><span data-stu-id="22e78-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="22e78-170">自動</span><span class="sxs-lookup"><span data-stu-id="22e78-170">automatic</span></span> | <span data-ttu-id="22e78-171">布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="22e78-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="22e78-172">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="22e78-173">solution 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-173">solution section</span></span>

<span data-ttu-id="22e78-174">控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="22e78-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="22e78-175">本區段只適用於解決方案資料夾中的 `nuget.config` 檔。</span><span class="sxs-lookup"><span data-stu-id="22e78-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="22e78-176">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-176">Key</span></span> | <span data-ttu-id="22e78-177">值</span><span class="sxs-lookup"><span data-stu-id="22e78-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="22e78-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="22e78-179">布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e78-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="22e78-180">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="22e78-180">The default value is false.</span></span> |

<span data-ttu-id="22e78-181">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="22e78-182">套件來源區段</span><span class="sxs-lookup"><span data-stu-id="22e78-182">Package source sections</span></span>

<span data-ttu-id="22e78-183">`packageSources`， `packageSourceCredentials`， `apikeys`， `activePackageSource`，`disabledPackageSources`和`trustedSigners`一起，以設定 NuGet 在安裝、 還原及更新作業期間如何使用套件存放庫的所有工作。</span><span class="sxs-lookup"><span data-stu-id="22e78-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="22e78-184">[ `nuget sources`命令](../tools/cli-ref-sources.md)通常用來管理這些設定，除了`apikeys`管理使用[`nuget setapikey`命令](../tools/cli-ref-setapikey.md)，以及`trustedSigners`管理使用[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。</span><span class="sxs-lookup"><span data-stu-id="22e78-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="22e78-185">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="22e78-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="22e78-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="22e78-186">packageSources</span></span>

<span data-ttu-id="22e78-187">列出所有已知的套件來源。</span><span class="sxs-lookup"><span data-stu-id="22e78-187">Lists all known package sources.</span></span> <span data-ttu-id="22e78-188">在還原作業期間，以及任何使用 PackageReference 格式的專案，會忽略順序。</span><span class="sxs-lookup"><span data-stu-id="22e78-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="22e78-189">NuGet 會遵守來源的順序進行安裝和更新作業使用的專案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="22e78-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="22e78-190">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-190">Key</span></span> | <span data-ttu-id="22e78-191">值</span><span class="sxs-lookup"><span data-stu-id="22e78-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-192">(要指派給套件來源的名稱)</span><span class="sxs-lookup"><span data-stu-id="22e78-192">(name to assign to the package source)</span></span> | <span data-ttu-id="22e78-193">套件來源的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="22e78-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="22e78-194">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="22e78-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="22e78-195">packageSourceCredentials</span></span>

<span data-ttu-id="22e78-196">儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。</span><span class="sxs-lookup"><span data-stu-id="22e78-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="22e78-197">依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。</span><span class="sxs-lookup"><span data-stu-id="22e78-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="22e78-198">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-198">Key</span></span> | <span data-ttu-id="22e78-199">值</span><span class="sxs-lookup"><span data-stu-id="22e78-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-200">username</span><span class="sxs-lookup"><span data-stu-id="22e78-200">username</span></span> | <span data-ttu-id="22e78-201">純文字的來源使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="22e78-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="22e78-202">password</span><span class="sxs-lookup"><span data-stu-id="22e78-202">password</span></span> | <span data-ttu-id="22e78-203">加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="22e78-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="22e78-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="22e78-204">cleartextpassword</span></span> | <span data-ttu-id="22e78-205">未加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="22e78-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="22e78-206">**範例：**</span><span class="sxs-lookup"><span data-stu-id="22e78-206">**Example:**</span></span>

<span data-ttu-id="22e78-207">設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020_`)。</span><span class="sxs-lookup"><span data-stu-id="22e78-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="22e78-208">也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="22e78-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="22e78-209">使用未加密的密碼時：</span><span class="sxs-lookup"><span data-stu-id="22e78-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="22e78-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="22e78-210">apikeys</span></span>

<span data-ttu-id="22e78-211">為使用 API 金鑰驗證的來源儲存金鑰，如同以 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)所設。</span><span class="sxs-lookup"><span data-stu-id="22e78-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="22e78-212">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-212">Key</span></span> | <span data-ttu-id="22e78-213">值</span><span class="sxs-lookup"><span data-stu-id="22e78-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-214">(來源 URL)</span><span class="sxs-lookup"><span data-stu-id="22e78-214">(source URL)</span></span> | <span data-ttu-id="22e78-215">加密的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="22e78-215">The encrypted API key.</span></span> |

<span data-ttu-id="22e78-216">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="22e78-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="22e78-217">disabledPackageSources</span></span>

<span data-ttu-id="22e78-218">識別目前已停用的來源。</span><span class="sxs-lookup"><span data-stu-id="22e78-218">Identified currently disabled sources.</span></span> <span data-ttu-id="22e78-219">可以是空的。</span><span class="sxs-lookup"><span data-stu-id="22e78-219">May be empty.</span></span>

| <span data-ttu-id="22e78-220">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-220">Key</span></span> | <span data-ttu-id="22e78-221">值</span><span class="sxs-lookup"><span data-stu-id="22e78-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-222">(來源名稱)</span><span class="sxs-lookup"><span data-stu-id="22e78-222">(name of source)</span></span> | <span data-ttu-id="22e78-223">布林值，指出是否停用來源。</span><span class="sxs-lookup"><span data-stu-id="22e78-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="22e78-224">**範例：**</span><span class="sxs-lookup"><span data-stu-id="22e78-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="22e78-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="22e78-225">activePackageSource</span></span>

<span data-ttu-id="22e78-226">*(僅 2.x，在 3.x+ 中已被取代)*</span><span class="sxs-lookup"><span data-stu-id="22e78-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="22e78-227">識別目前作用中的來源，或表示所有來源的彙總。</span><span class="sxs-lookup"><span data-stu-id="22e78-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="22e78-228">Key</span><span class="sxs-lookup"><span data-stu-id="22e78-228">Key</span></span> | <span data-ttu-id="22e78-229">值</span><span class="sxs-lookup"><span data-stu-id="22e78-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22e78-230">(來源名稱) 或 `All`</span><span class="sxs-lookup"><span data-stu-id="22e78-230">(name of source) or `All`</span></span> | <span data-ttu-id="22e78-231">如果金鑰是來源的名稱，則值是來源路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="22e78-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="22e78-232">若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="22e78-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="22e78-233">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="22e78-234">trustedSigners 區段</span><span class="sxs-lookup"><span data-stu-id="22e78-234">trustedSigners section</span></span>

<span data-ttu-id="22e78-235">用來允許的同時，安裝或還原套件的簽署受信任的存放區。</span><span class="sxs-lookup"><span data-stu-id="22e78-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="22e78-236">使用者設定時，此清單不得為空白`signatureValidationMode`至`require`。</span><span class="sxs-lookup"><span data-stu-id="22e78-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="22e78-237">此區段可使用更新[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。</span><span class="sxs-lookup"><span data-stu-id="22e78-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="22e78-238">**結構描述**:</span><span class="sxs-lookup"><span data-stu-id="22e78-238">**Schema**:</span></span>

<span data-ttu-id="22e78-239">受信任簽署者具有集合`certificate`登錄找出指定的簽署者的所有憑證的項目。</span><span class="sxs-lookup"><span data-stu-id="22e78-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="22e78-240">受信任簽署者可以是`Author`或`Repository`。</span><span class="sxs-lookup"><span data-stu-id="22e78-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="22e78-241">受信任*儲存機制*也會指定`serviceIndex`存放庫 (必須是有效`https`uri) 可以選擇性地指定以分號分隔的清單和`owners`來限制更多人員是信任從特定的存放庫中。</span><span class="sxs-lookup"><span data-stu-id="22e78-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="22e78-242">使用憑證指紋的支援的雜湊演算法`SHA256`，`SHA384`和`SHA512`。</span><span class="sxs-lookup"><span data-stu-id="22e78-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="22e78-243">如果`certificate`指定`allowUntrustedRoot`做為`true`建置憑證鏈結，做為簽章驗證的一部分時允許指定的憑證鏈結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="22e78-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="22e78-244">**範例**：</span><span class="sxs-lookup"><span data-stu-id="22e78-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="22e78-245">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="22e78-245">Using environment variables</span></span>

<span data-ttu-id="22e78-246">您可以在 `nuget.config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。</span><span class="sxs-lookup"><span data-stu-id="22e78-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="22e78-247">例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="22e78-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="22e78-248">同樣地，如果 Mac/Linux 上的 `HOME` 設為 `/home/myStuff`，則設定檔中的 `%HOME%/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="22e78-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="22e78-249">如果找不到環境變數，NuGet 會使用來自設定檔的常值。</span><span class="sxs-lookup"><span data-stu-id="22e78-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="22e78-250">範例設定檔</span><span class="sxs-lookup"><span data-stu-id="22e78-250">Example config file</span></span>

<span data-ttu-id="22e78-251">以下是 `nuget.config` 檔範例，說明多項設定：</span><span class="sxs-lookup"><span data-stu-id="22e78-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
