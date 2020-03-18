---
title: nuget.exe 檔案參考
description: NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429126"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="8d020-103">nuget.exe 參考</span><span class="sxs-lookup"><span data-stu-id="8d020-103">nuget.config reference</span></span>

<span data-ttu-id="8d020-104">NuGet 行為是由不同 `NuGet.Config` 或 `nuget.config` 檔案中的設定所控制，如[一般 NuGet](../consume-packages/configuring-nuget-behavior.md)設定中所述。</span><span class="sxs-lookup"><span data-stu-id="8d020-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8d020-105">`nuget.config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。</span><span class="sxs-lookup"><span data-stu-id="8d020-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="8d020-106">每個區段都包含零個或多個專案。</span><span class="sxs-lookup"><span data-stu-id="8d020-106">Each section contains zero or more items.</span></span> <span data-ttu-id="8d020-107">請參閱[設定檔範例](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="8d020-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="8d020-108">設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="8d020-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="8d020-109">config 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-109">config section</span></span>

<span data-ttu-id="8d020-110">包含其他組態設定，可以使用 [`nuget config` 命令](../reference/cli-reference/cli-ref-config.md)設定。</span><span class="sxs-lookup"><span data-stu-id="8d020-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="8d020-111">`dependencyVersion` 和 `repositoryPath` 僅適用于使用 `packages.config`的專案。</span><span class="sxs-lookup"><span data-stu-id="8d020-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="8d020-112">`globalPackagesFolder` 只適用于使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="8d020-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="8d020-113">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-113">Key</span></span> | <span data-ttu-id="8d020-114">值</span><span class="sxs-lookup"><span data-stu-id="8d020-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-115">dependencyVersion (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8d020-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="8d020-116">當未直接指定 `DependencyVersion` 參數時，套件安裝、還原及更新的預設 `-DependencyVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="8d020-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="8d020-117">NuGet 套件管理員 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="8d020-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="8d020-118">值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="8d020-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="8d020-119">globalPackagesFolder （僅使用 PackageReference 的專案）</span><span class="sxs-lookup"><span data-stu-id="8d020-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="8d020-120">預設全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="8d020-120">The location of the default global packages folder.</span></span> <span data-ttu-id="8d020-121">預設值為 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="8d020-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="8d020-122">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d020-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="8d020-123">NUGET_PACKAGES 環境變數會覆寫此設定，其優先順序較高。</span><span class="sxs-lookup"><span data-stu-id="8d020-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8d020-124">repositoryPath (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8d020-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="8d020-125">要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d020-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="8d020-126">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d020-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="8d020-127">NUGET_PACKAGES 環境變數會覆寫此設定，其優先順序較高。</span><span class="sxs-lookup"><span data-stu-id="8d020-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8d020-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="8d020-128">defaultPushSource</span></span> | <span data-ttu-id="8d020-129">識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。</span><span class="sxs-lookup"><span data-stu-id="8d020-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="8d020-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="8d020-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="8d020-131">連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="8d020-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="8d020-132">密碼會加密，且無法手動新增。</span><span class="sxs-lookup"><span data-stu-id="8d020-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="8d020-133">對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="8d020-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="8d020-134">您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。</span><span class="sxs-lookup"><span data-stu-id="8d020-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="8d020-135">如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="8d020-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="8d020-136">因為 signaturevalidationmode</span><span class="sxs-lookup"><span data-stu-id="8d020-136">signatureValidationMode</span></span> | <span data-ttu-id="8d020-137">指定驗證模式，用來驗證封裝安裝和還原的封裝簽章。</span><span class="sxs-lookup"><span data-stu-id="8d020-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="8d020-138">值為 `accept`，`require`。</span><span class="sxs-lookup"><span data-stu-id="8d020-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="8d020-139">預設為 `accept`。</span><span class="sxs-lookup"><span data-stu-id="8d020-139">Defaults to `accept`.</span></span>

<span data-ttu-id="8d020-140">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="8d020-141">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-141">bindingRedirects section</span></span>

<span data-ttu-id="8d020-142">設定 NuGet 在安裝套件時，是否自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="8d020-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="8d020-143">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-143">Key</span></span> | <span data-ttu-id="8d020-144">值</span><span class="sxs-lookup"><span data-stu-id="8d020-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-145">skip</span><span class="sxs-lookup"><span data-stu-id="8d020-145">skip</span></span> | <span data-ttu-id="8d020-146">布林值，指出是否略過自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="8d020-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="8d020-147">預設為 false。</span><span class="sxs-lookup"><span data-stu-id="8d020-147">The default is false.</span></span> |

<span data-ttu-id="8d020-148">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="8d020-149">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-149">packageRestore section</span></span>

<span data-ttu-id="8d020-150">控制建置期間的套件還原。</span><span class="sxs-lookup"><span data-stu-id="8d020-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="8d020-151">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-151">Key</span></span> | <span data-ttu-id="8d020-152">值</span><span class="sxs-lookup"><span data-stu-id="8d020-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-153">已啟用</span><span class="sxs-lookup"><span data-stu-id="8d020-153">enabled</span></span> | <span data-ttu-id="8d020-154">布林值，指出 NuGet 是否可以執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="8d020-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="8d020-155">您也可以使用 `EnableNuGetPackageRestore` 值來設定 `True` 環境變數，而不是在設定檔中設定此金鑰。</span><span class="sxs-lookup"><span data-stu-id="8d020-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="8d020-156">automatic</span><span class="sxs-lookup"><span data-stu-id="8d020-156">automatic</span></span> | <span data-ttu-id="8d020-157">布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="8d020-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="8d020-158">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="8d020-159">solution 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-159">solution section</span></span>

<span data-ttu-id="8d020-160">控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="8d020-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="8d020-161">本區段只適用於解決方案資料夾中的 `nuget.config` 檔。</span><span class="sxs-lookup"><span data-stu-id="8d020-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="8d020-162">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-162">Key</span></span> | <span data-ttu-id="8d020-163">值</span><span class="sxs-lookup"><span data-stu-id="8d020-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="8d020-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="8d020-165">布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8d020-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="8d020-166">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="8d020-166">The default value is false.</span></span> |

<span data-ttu-id="8d020-167">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="8d020-168">套件來源區段</span><span class="sxs-lookup"><span data-stu-id="8d020-168">Package source sections</span></span>

<span data-ttu-id="8d020-169">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、`disabledPackageSources` 和 `trustedSigners` 會共同運作，以設定 NuGet 如何在安裝、還原和更新作業期間與套件存放庫搭配運作。</span><span class="sxs-lookup"><span data-stu-id="8d020-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="8d020-170">[`nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)通常用來管理這些設定，除了使用[`nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)管理的 `apikeys`，以及使用[`nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)管理的 `trustedSigners` 以外。</span><span class="sxs-lookup"><span data-stu-id="8d020-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="8d020-171">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="8d020-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="8d020-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="8d020-172">packageSources</span></span>

<span data-ttu-id="8d020-173">列出所有已知的套件來源。</span><span class="sxs-lookup"><span data-stu-id="8d020-173">Lists all known package sources.</span></span> <span data-ttu-id="8d020-174">在還原作業期間，以及使用 PackageReference 格式的任何專案，都會忽略順序。</span><span class="sxs-lookup"><span data-stu-id="8d020-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="8d020-175">NuGet 會遵循使用 `packages.config`的專案進行安裝和更新作業的來源順序。</span><span class="sxs-lookup"><span data-stu-id="8d020-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="8d020-176">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-176">Key</span></span> | <span data-ttu-id="8d020-177">值</span><span class="sxs-lookup"><span data-stu-id="8d020-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-178">(要指派給套件來源的名稱)</span><span class="sxs-lookup"><span data-stu-id="8d020-178">(name to assign to the package source)</span></span> | <span data-ttu-id="8d020-179">套件來源的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="8d020-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="8d020-180">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="8d020-181">指定節點具有 `<clear />` 時，NuGet 會忽略先前針對該節點所定義的組態值。</span><span class="sxs-lookup"><span data-stu-id="8d020-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="8d020-182">[深入瞭解設定的套用方式](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="8d020-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="8d020-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8d020-183">packageSourceCredentials</span></span>

<span data-ttu-id="8d020-184">儲存來源的使用者名稱和密碼，通常使用 `-username` 的 `-password` 和 `nuget sources` 參數來指定。</span><span class="sxs-lookup"><span data-stu-id="8d020-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="8d020-185">依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。</span><span class="sxs-lookup"><span data-stu-id="8d020-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="8d020-186">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-186">Key</span></span> | <span data-ttu-id="8d020-187">值</span><span class="sxs-lookup"><span data-stu-id="8d020-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-188">username</span><span class="sxs-lookup"><span data-stu-id="8d020-188">username</span></span> | <span data-ttu-id="8d020-189">純文字的來源使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8d020-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="8d020-190">密碼</span><span class="sxs-lookup"><span data-stu-id="8d020-190">password</span></span> | <span data-ttu-id="8d020-191">加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="8d020-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="8d020-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="8d020-192">cleartextpassword</span></span> | <span data-ttu-id="8d020-193">未加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="8d020-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="8d020-194">**範例︰**</span><span class="sxs-lookup"><span data-stu-id="8d020-194">**Example:**</span></span>

<span data-ttu-id="8d020-195">設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020_`)。</span><span class="sxs-lookup"><span data-stu-id="8d020-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="8d020-196">也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="8d020-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="8d020-197">使用未加密的密碼時：</span><span class="sxs-lookup"><span data-stu-id="8d020-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="8d020-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="8d020-198">apikeys</span></span>

<span data-ttu-id="8d020-199">為使用 API 金鑰驗證的來源儲存金鑰，如同以 [`nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)所設。</span><span class="sxs-lookup"><span data-stu-id="8d020-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="8d020-200">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-200">Key</span></span> | <span data-ttu-id="8d020-201">值</span><span class="sxs-lookup"><span data-stu-id="8d020-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-202">(來源 URL)</span><span class="sxs-lookup"><span data-stu-id="8d020-202">(source URL)</span></span> | <span data-ttu-id="8d020-203">加密的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="8d020-203">The encrypted API key.</span></span> |

<span data-ttu-id="8d020-204">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="8d020-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8d020-205">disabledPackageSources</span></span>

<span data-ttu-id="8d020-206">識別目前已停用的來源。</span><span class="sxs-lookup"><span data-stu-id="8d020-206">Identified currently disabled sources.</span></span> <span data-ttu-id="8d020-207">可以是空的。</span><span class="sxs-lookup"><span data-stu-id="8d020-207">May be empty.</span></span>

| <span data-ttu-id="8d020-208">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-208">Key</span></span> | <span data-ttu-id="8d020-209">值</span><span class="sxs-lookup"><span data-stu-id="8d020-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-210">(來源名稱)</span><span class="sxs-lookup"><span data-stu-id="8d020-210">(name of source)</span></span> | <span data-ttu-id="8d020-211">布林值，指出是否停用來源。</span><span class="sxs-lookup"><span data-stu-id="8d020-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="8d020-212">**範例︰**</span><span class="sxs-lookup"><span data-stu-id="8d020-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="8d020-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8d020-213">activePackageSource</span></span>

<span data-ttu-id="8d020-214">*(僅 2.x，在 3.x+ 中已被取代)*</span><span class="sxs-lookup"><span data-stu-id="8d020-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="8d020-215">識別目前作用中的來源，或表示所有來源的彙總。</span><span class="sxs-lookup"><span data-stu-id="8d020-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="8d020-216">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-216">Key</span></span> | <span data-ttu-id="8d020-217">值</span><span class="sxs-lookup"><span data-stu-id="8d020-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-218">(來源名稱) 或 `All`</span><span class="sxs-lookup"><span data-stu-id="8d020-218">(name of source) or `All`</span></span> | <span data-ttu-id="8d020-219">如果金鑰是來源的名稱，則值是來源路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="8d020-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="8d020-220">若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="8d020-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="8d020-221">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="8d020-222">trustedSigners 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-222">trustedSigners section</span></span>

<span data-ttu-id="8d020-223">在安裝或還原時，儲存用來允許套件的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="8d020-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="8d020-224">當使用者將 `signatureValidationMode` 設定為 `require`時，此清單不可以是空的。</span><span class="sxs-lookup"><span data-stu-id="8d020-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="8d020-225">您可以使用[`nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)來更新此區段。</span><span class="sxs-lookup"><span data-stu-id="8d020-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="8d020-226">**結構描述**：</span><span class="sxs-lookup"><span data-stu-id="8d020-226">**Schema**:</span></span>

<span data-ttu-id="8d020-227">受信任的簽署者具有 `certificate` 專案的集合，這些專案會登錄識別指定簽署者的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="8d020-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="8d020-228">受信任的簽署者可以是 `Author` 或 `Repository`。</span><span class="sxs-lookup"><span data-stu-id="8d020-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="8d020-229">受信任的存放*庫*也會指定存放庫的 `serviceIndex` （必須是有效的 `https` uri），而且可以選擇性地指定以分號分隔的 `owners` 清單，以限制更多受該特定存放庫信任的使用者。</span><span class="sxs-lookup"><span data-stu-id="8d020-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="8d020-230">憑證指紋所支援的雜湊演算法是 `SHA256`、`SHA384` 和 `SHA512`。</span><span class="sxs-lookup"><span data-stu-id="8d020-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="8d020-231">如果 `certificate` 將 `allowUntrustedRoot` 指定 `true` 為，則在將憑證鏈建立為簽章驗證的一部分時，允許將指定的憑證連結到不受信任的根目錄。</span><span class="sxs-lookup"><span data-stu-id="8d020-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="8d020-232">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="8d020-233">fallbackPackageFolders 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="8d020-234">*（3.5 +）* 提供方法來預先安裝封裝，因此如果在回溯資料夾中找到封裝，則不需要執行任何工作。</span><span class="sxs-lookup"><span data-stu-id="8d020-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="8d020-235">Fallback 封裝資料夾與全域封裝資料夾的資料夾和檔案結構完全相同： *。 nupkg*存在，而且所有檔案都會解壓縮。</span><span class="sxs-lookup"><span data-stu-id="8d020-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="8d020-236">此設定的查閱邏輯如下：</span><span class="sxs-lookup"><span data-stu-id="8d020-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="8d020-237">查看全域封裝資料夾，查看套件/版本是否已下載。</span><span class="sxs-lookup"><span data-stu-id="8d020-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="8d020-238">查看 [fallback] 資料夾中是否有套件/版本相符。</span><span class="sxs-lookup"><span data-stu-id="8d020-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="8d020-239">如果其中一項查閱成功，則不需要下載。</span><span class="sxs-lookup"><span data-stu-id="8d020-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="8d020-240">如果找不到相符項，則 NuGet 會檢查檔案來源，然後再進行 HTTP 來源，然後下載封裝。</span><span class="sxs-lookup"><span data-stu-id="8d020-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="8d020-241">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-241">Key</span></span> | <span data-ttu-id="8d020-242">值</span><span class="sxs-lookup"><span data-stu-id="8d020-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-243">（fallback 資料夾的名稱）</span><span class="sxs-lookup"><span data-stu-id="8d020-243">(name of fallback folder)</span></span> | <span data-ttu-id="8d020-244">Fallback 資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="8d020-244">Path to fallback folder.</span></span> |

<span data-ttu-id="8d020-245">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="8d020-246">packageManagement 區段</span><span class="sxs-lookup"><span data-stu-id="8d020-246">packageManagement section</span></span>

<span data-ttu-id="8d020-247">設定預設的封裝管理格式，也*就是 PackageReference。*</span><span class="sxs-lookup"><span data-stu-id="8d020-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="8d020-248">SDK 樣式專案一律使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="8d020-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="8d020-249">Key</span><span class="sxs-lookup"><span data-stu-id="8d020-249">Key</span></span> | <span data-ttu-id="8d020-250">值</span><span class="sxs-lookup"><span data-stu-id="8d020-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8d020-251">格式</span><span class="sxs-lookup"><span data-stu-id="8d020-251">format</span></span> | <span data-ttu-id="8d020-252">布林值，指出預設的封裝管理格式。</span><span class="sxs-lookup"><span data-stu-id="8d020-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="8d020-253">如果 `1`，格式為 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="8d020-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="8d020-254">如果 `0`，則格式為*封裝 .config*。</span><span class="sxs-lookup"><span data-stu-id="8d020-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="8d020-255">停用</span><span class="sxs-lookup"><span data-stu-id="8d020-255">disabled</span></span> | <span data-ttu-id="8d020-256">布林值，指出是否要在第一次封裝安裝時顯示選取預設封裝格式的提示。</span><span class="sxs-lookup"><span data-stu-id="8d020-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="8d020-257">`False` 隱藏提示。</span><span class="sxs-lookup"><span data-stu-id="8d020-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="8d020-258">**範例**：</span><span class="sxs-lookup"><span data-stu-id="8d020-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="8d020-259">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="8d020-259">Using environment variables</span></span>

<span data-ttu-id="8d020-260">您可以在 `nuget.config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。</span><span class="sxs-lookup"><span data-stu-id="8d020-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="8d020-261">例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="8d020-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="8d020-262">請注意，您必須使用 Windows 樣式的環境變數（開頭和結尾都是%）即使在 Mac/Linux 上也一樣。</span><span class="sxs-lookup"><span data-stu-id="8d020-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="8d020-263">在設定檔中擁有 `$HOME/NuGetRepository` 將無法解析。</span><span class="sxs-lookup"><span data-stu-id="8d020-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="8d020-264">在 Mac/Linux 上，`%HOME%\NuGetRepository` 的值會解析為 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="8d020-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="8d020-265">如果找不到環境變數，NuGet 會使用來自設定檔的常值。</span><span class="sxs-lookup"><span data-stu-id="8d020-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="8d020-266">範例設定檔</span><span class="sxs-lookup"><span data-stu-id="8d020-266">Example config file</span></span>

<span data-ttu-id="8d020-267">以下是範例 `nuget.config` 檔案，其中說明一些設定，包括選擇性的設定：</span><span class="sxs-lookup"><span data-stu-id="8d020-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
