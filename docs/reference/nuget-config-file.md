---
title: nuget.config 檔案參考
description: NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 28fae46a65bd4c2b7050e12568c21123fc8658c1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623158"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="552f9-103">nuget.config 參考</span><span class="sxs-lookup"><span data-stu-id="552f9-103">nuget.config reference</span></span>

<span data-ttu-id="552f9-104">NuGet 行為是由不同或檔案中的設定所控制， `NuGet.Config` `nuget.config` 如 [一般 NuGet](../consume-packages/configuring-nuget-behavior.md)設定中所述。</span><span class="sxs-lookup"><span data-stu-id="552f9-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="552f9-105">`nuget.config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。</span><span class="sxs-lookup"><span data-stu-id="552f9-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="552f9-106">每個區段包含零或多個專案。</span><span class="sxs-lookup"><span data-stu-id="552f9-106">Each section contains zero or more items.</span></span> <span data-ttu-id="552f9-107">請參閱[設定檔範例](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="552f9-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="552f9-108">設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="552f9-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="552f9-109">config 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-109">config section</span></span>

<span data-ttu-id="552f9-110">包含可使用[ `nuget config` 命令](../reference/cli-reference/cli-ref-config.md)設定的其他設定。</span><span class="sxs-lookup"><span data-stu-id="552f9-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="552f9-111">`dependencyVersion` 並 `repositoryPath` 僅適用于使用的 `packages.config` 專案。</span><span class="sxs-lookup"><span data-stu-id="552f9-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="552f9-112">`globalPackagesFolder` 只適用于使用 PackageReference 格式的專案。</span><span class="sxs-lookup"><span data-stu-id="552f9-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="552f9-113">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-113">Key</span></span> | <span data-ttu-id="552f9-114">值</span><span class="sxs-lookup"><span data-stu-id="552f9-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-115">dependencyVersion (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="552f9-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="552f9-116">當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。</span><span class="sxs-lookup"><span data-stu-id="552f9-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="552f9-117">NuGet 套件管理員 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="552f9-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="552f9-118">值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="552f9-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="552f9-119">使用僅限 PackageReference 的 globalPackagesFolder (專案) </span><span class="sxs-lookup"><span data-stu-id="552f9-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="552f9-120">預設全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="552f9-120">The location of the default global packages folder.</span></span> <span data-ttu-id="552f9-121">預設值為 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="552f9-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="552f9-122">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="552f9-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="552f9-123">這項設定是由 NUGET_PACKAGES 環境變數所覆寫，這會優先使用。</span><span class="sxs-lookup"><span data-stu-id="552f9-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="552f9-124">repositoryPath (僅 `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="552f9-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="552f9-125">要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="552f9-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="552f9-126">相對路徑可用於專案特有的 `nuget.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="552f9-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="552f9-127">這項設定是由 NUGET_PACKAGES 環境變數所覆寫，這會優先使用。</span><span class="sxs-lookup"><span data-stu-id="552f9-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="552f9-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="552f9-128">defaultPushSource</span></span> | <span data-ttu-id="552f9-129">識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。</span><span class="sxs-lookup"><span data-stu-id="552f9-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="552f9-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="552f9-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="552f9-131">連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="552f9-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="552f9-132">密碼會加密，且無法手動新增。</span><span class="sxs-lookup"><span data-stu-id="552f9-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="552f9-133">對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="552f9-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="552f9-134">您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。</span><span class="sxs-lookup"><span data-stu-id="552f9-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="552f9-135">如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="552f9-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="552f9-136">因為 signaturevalidationmode</span><span class="sxs-lookup"><span data-stu-id="552f9-136">signatureValidationMode</span></span> | <span data-ttu-id="552f9-137">指定驗證模式，用來驗證封裝安裝和還原的封裝簽章。</span><span class="sxs-lookup"><span data-stu-id="552f9-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="552f9-138">值為 `accept` 、 `require` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="552f9-139">預設為 `accept`。</span><span class="sxs-lookup"><span data-stu-id="552f9-139">Defaults to `accept`.</span></span>

<span data-ttu-id="552f9-140">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="552f9-141">bindingRedirects 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-141">bindingRedirects section</span></span>

<span data-ttu-id="552f9-142">設定 NuGet 在安裝套件時，是否自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="552f9-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="552f9-143">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-143">Key</span></span> | <span data-ttu-id="552f9-144">值</span><span class="sxs-lookup"><span data-stu-id="552f9-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-145">skip</span><span class="sxs-lookup"><span data-stu-id="552f9-145">skip</span></span> | <span data-ttu-id="552f9-146">布林值，指出是否略過自動繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="552f9-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="552f9-147">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="552f9-147">The default is false.</span></span> |

<span data-ttu-id="552f9-148">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="552f9-149">packageRestore 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-149">packageRestore section</span></span>

<span data-ttu-id="552f9-150">控制建置期間的套件還原。</span><span class="sxs-lookup"><span data-stu-id="552f9-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="552f9-151">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-151">Key</span></span> | <span data-ttu-id="552f9-152">值</span><span class="sxs-lookup"><span data-stu-id="552f9-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-153">已啟用</span><span class="sxs-lookup"><span data-stu-id="552f9-153">enabled</span></span> | <span data-ttu-id="552f9-154">布林值，指出 NuGet 是否可以執行自動還原。</span><span class="sxs-lookup"><span data-stu-id="552f9-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="552f9-155">您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。</span><span class="sxs-lookup"><span data-stu-id="552f9-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="552f9-156">automatic</span><span class="sxs-lookup"><span data-stu-id="552f9-156">automatic</span></span> | <span data-ttu-id="552f9-157">布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="552f9-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="552f9-158">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="552f9-159">solution 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-159">solution section</span></span>

<span data-ttu-id="552f9-160">控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="552f9-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="552f9-161">本區段只適用於解決方案資料夾中的 `nuget.config` 檔。</span><span class="sxs-lookup"><span data-stu-id="552f9-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="552f9-162">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-162">Key</span></span> | <span data-ttu-id="552f9-163">值</span><span class="sxs-lookup"><span data-stu-id="552f9-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="552f9-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="552f9-165">布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="552f9-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="552f9-166">預設值為 false。</span><span class="sxs-lookup"><span data-stu-id="552f9-166">The default value is false.</span></span> |

<span data-ttu-id="552f9-167">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="552f9-168">套件來源區段</span><span class="sxs-lookup"><span data-stu-id="552f9-168">Package source sections</span></span>

<span data-ttu-id="552f9-169">`packageSources`、、 `packageSourceCredentials` `apikeys` 、 `activePackageSource` `disabledPackageSources` 和全都會 `trustedSigners` 一起運作，以設定在安裝、還原和更新作業期間，NuGet 與套件存放庫的搭配運作方式。</span><span class="sxs-lookup"><span data-stu-id="552f9-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="552f9-170">[ `nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)通常用來管理這些設定，但 `apikeys` 使用[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)來管理，以及 `trustedSigners` 使用[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)管理的例外。</span><span class="sxs-lookup"><span data-stu-id="552f9-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="552f9-171">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="552f9-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="552f9-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="552f9-172">packageSources</span></span>

<span data-ttu-id="552f9-173">列出所有已知的套件來源。</span><span class="sxs-lookup"><span data-stu-id="552f9-173">Lists all known package sources.</span></span> <span data-ttu-id="552f9-174">在還原作業期間，以及使用 PackageReference 格式的任何專案時，會忽略順序。</span><span class="sxs-lookup"><span data-stu-id="552f9-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="552f9-175">NuGet 會遵循使用專案進行安裝和更新作業的來源順序 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="552f9-176">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-176">Key</span></span> | <span data-ttu-id="552f9-177">值</span><span class="sxs-lookup"><span data-stu-id="552f9-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-178">(要指派給套件來源的名稱)</span><span class="sxs-lookup"><span data-stu-id="552f9-178">(name to assign to the package source)</span></span> | <span data-ttu-id="552f9-179">套件來源的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="552f9-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="552f9-180">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="552f9-181">指定節點具有 `<clear />` 時，NuGet 會忽略先前針對該節點所定義的組態值。</span><span class="sxs-lookup"><span data-stu-id="552f9-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="552f9-182">[深入瞭解設定的套用方式](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="552f9-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="552f9-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="552f9-183">packageSourceCredentials</span></span>

<span data-ttu-id="552f9-184">儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。</span><span class="sxs-lookup"><span data-stu-id="552f9-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="552f9-185">依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。</span><span class="sxs-lookup"><span data-stu-id="552f9-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="552f9-186">（選擇性）使用參數可以指定有效的驗證類型 `-validauthenticationtypes` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="552f9-187">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-187">Key</span></span> | <span data-ttu-id="552f9-188">值</span><span class="sxs-lookup"><span data-stu-id="552f9-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-189">username</span><span class="sxs-lookup"><span data-stu-id="552f9-189">username</span></span> | <span data-ttu-id="552f9-190">純文字的來源使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="552f9-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="552f9-191">密碼</span><span class="sxs-lookup"><span data-stu-id="552f9-191">password</span></span> | <span data-ttu-id="552f9-192">加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="552f9-192">The encrypted password for the source.</span></span> <span data-ttu-id="552f9-193">只有在 Windows 上才支援加密的密碼，而且只有在同一部電腦上使用時，以及透過與原始加密相同的使用者才能解密。</span><span class="sxs-lookup"><span data-stu-id="552f9-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="552f9-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="552f9-194">cleartextpassword</span></span> | <span data-ttu-id="552f9-195">未加密的來源密碼。</span><span class="sxs-lookup"><span data-stu-id="552f9-195">The unencrypted password for the source.</span></span> <span data-ttu-id="552f9-196">注意：環境變數可以用來改善安全性。</span><span class="sxs-lookup"><span data-stu-id="552f9-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="552f9-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="552f9-197">validauthenticationtypes</span></span> | <span data-ttu-id="552f9-198">此來源的有效驗證類型清單（以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="552f9-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="552f9-199">將此設定為， `basic` 如果伺服器通告 NTLM 或 Negotiate，而且您的認證必須使用基本機制傳送，例如，搭配內部部署 Azure DevOps Server 使用 PAT。</span><span class="sxs-lookup"><span data-stu-id="552f9-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="552f9-200">其他有效的值包括 `negotiate` 、 `kerberos` 、 `ntlm` 和 `digest` ，但這些值不太可能很有用。</span><span class="sxs-lookup"><span data-stu-id="552f9-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="552f9-201">**範例︰**</span><span class="sxs-lookup"><span data-stu-id="552f9-201">**Example:**</span></span>

<span data-ttu-id="552f9-202">設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020_`)。</span><span class="sxs-lookup"><span data-stu-id="552f9-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="552f9-203">也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="552f9-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="552f9-204">使用儲存在環境變數中的未加密密碼時：</span><span class="sxs-lookup"><span data-stu-id="552f9-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="552f9-205">使用未加密的密碼時：</span><span class="sxs-lookup"><span data-stu-id="552f9-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="552f9-206">此外，也可以提供有效的驗證方法：</span><span class="sxs-lookup"><span data-stu-id="552f9-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="552f9-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="552f9-207">apikeys</span></span>

<span data-ttu-id="552f9-208">儲存使用 API 金鑰驗證之來源的金鑰，如[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)所設定。</span><span class="sxs-lookup"><span data-stu-id="552f9-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="552f9-209">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-209">Key</span></span> | <span data-ttu-id="552f9-210">值</span><span class="sxs-lookup"><span data-stu-id="552f9-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-211">(來源 URL)</span><span class="sxs-lookup"><span data-stu-id="552f9-211">(source URL)</span></span> | <span data-ttu-id="552f9-212">加密的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="552f9-212">The encrypted API key.</span></span> |

<span data-ttu-id="552f9-213">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="552f9-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="552f9-214">disabledPackageSources</span></span>

<span data-ttu-id="552f9-215">識別目前已停用的來源。</span><span class="sxs-lookup"><span data-stu-id="552f9-215">Identified currently disabled sources.</span></span> <span data-ttu-id="552f9-216">可以是空的。</span><span class="sxs-lookup"><span data-stu-id="552f9-216">May be empty.</span></span>

| <span data-ttu-id="552f9-217">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-217">Key</span></span> | <span data-ttu-id="552f9-218">值</span><span class="sxs-lookup"><span data-stu-id="552f9-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-219">(來源名稱)</span><span class="sxs-lookup"><span data-stu-id="552f9-219">(name of source)</span></span> | <span data-ttu-id="552f9-220">布林值，指出是否停用來源。</span><span class="sxs-lookup"><span data-stu-id="552f9-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="552f9-221">**範例︰**</span><span class="sxs-lookup"><span data-stu-id="552f9-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="552f9-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="552f9-222">activePackageSource</span></span>

<span data-ttu-id="552f9-223">*(僅 2.x，在 3.x+ 中已被取代)*</span><span class="sxs-lookup"><span data-stu-id="552f9-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="552f9-224">識別目前作用中的來源，或表示所有來源的彙總。</span><span class="sxs-lookup"><span data-stu-id="552f9-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="552f9-225">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-225">Key</span></span> | <span data-ttu-id="552f9-226">值</span><span class="sxs-lookup"><span data-stu-id="552f9-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-227">(來源名稱) 或 `All`</span><span class="sxs-lookup"><span data-stu-id="552f9-227">(name of source) or `All`</span></span> | <span data-ttu-id="552f9-228">如果金鑰是來源的名稱，則值是來源路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="552f9-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="552f9-229">若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。</span><span class="sxs-lookup"><span data-stu-id="552f9-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="552f9-230">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="552f9-231">trustedSigners 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-231">trustedSigners section</span></span>

<span data-ttu-id="552f9-232">在安裝或還原時，儲存用來允許套件的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="552f9-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="552f9-233">當使用者將設定為時，此清單不可以是空的 `signatureValidationMode` `require` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="552f9-234">您可以使用[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)來更新此區段。</span><span class="sxs-lookup"><span data-stu-id="552f9-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="552f9-235">**架構**：</span><span class="sxs-lookup"><span data-stu-id="552f9-235">**Schema**:</span></span>

<span data-ttu-id="552f9-236">受信任的簽署者有一個 `certificate` 專案集合，這些專案會登錄識別指定之簽署者的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="552f9-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="552f9-237">受信任的簽署者可以是 `Author` 或 `Repository` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="552f9-238">受信任的存放 *庫* 也會指定存放 `serviceIndex` 庫 (的，其必須是有效的 `https` uri) 而且可以選擇性地指定以分號分隔的清單， `owners` 以限制更多受該特定存放庫信任的物件。</span><span class="sxs-lookup"><span data-stu-id="552f9-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="552f9-239">用於憑證指紋的支援雜湊演算法為 `SHA256` 、 `SHA384` 和 `SHA512` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="552f9-240">如果 `certificate` 指定為指定的 `allowUntrustedRoot` 憑證，則在 `true` 建立憑證鏈作為簽章驗證的一部分時，允許鏈至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="552f9-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="552f9-241">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-241">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="552f9-242">fallbackPackageFolders 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="552f9-243">\* (3.5 +) \* 提供預先安裝封裝的方法，因此，如果在回溯資料夾中找到封裝，就不需要執行任何工作。</span><span class="sxs-lookup"><span data-stu-id="552f9-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="552f9-244">Fallback 封裝資料夾與全域封裝資料夾的資料夾和檔案結構完全相同： *nupkg* 存在，而且所有檔案都已解壓縮。</span><span class="sxs-lookup"><span data-stu-id="552f9-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="552f9-245">這項設定的查閱邏輯是：</span><span class="sxs-lookup"><span data-stu-id="552f9-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="552f9-246">查看全域封裝資料夾，查看是否已下載套件/版本。</span><span class="sxs-lookup"><span data-stu-id="552f9-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="552f9-247">查看 [回復] 資料夾中是否有套件/版本相符。</span><span class="sxs-lookup"><span data-stu-id="552f9-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="552f9-248">如果其中一項查閱成功，則不需要下載。</span><span class="sxs-lookup"><span data-stu-id="552f9-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="552f9-249">如果找不到相符項，則 NuGet 會檢查檔案來源，然後再檢查 HTTP 來源，然後下載套件。</span><span class="sxs-lookup"><span data-stu-id="552f9-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="552f9-250">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-250">Key</span></span> | <span data-ttu-id="552f9-251">值</span><span class="sxs-lookup"><span data-stu-id="552f9-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-252"> (的 [fallback] 資料夾名稱) </span><span class="sxs-lookup"><span data-stu-id="552f9-252">(name of fallback folder)</span></span> | <span data-ttu-id="552f9-253">Fallback 資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="552f9-253">Path to fallback folder.</span></span> |

<span data-ttu-id="552f9-254">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="552f9-255">packageManagement 區段</span><span class="sxs-lookup"><span data-stu-id="552f9-255">packageManagement section</span></span>

<span data-ttu-id="552f9-256">設定預設封裝管理格式（ *packages.config* 或 PackageReference）。</span><span class="sxs-lookup"><span data-stu-id="552f9-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="552f9-257">SDK 樣式的專案一律使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="552f9-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="552f9-258">Key</span><span class="sxs-lookup"><span data-stu-id="552f9-258">Key</span></span> | <span data-ttu-id="552f9-259">值</span><span class="sxs-lookup"><span data-stu-id="552f9-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="552f9-260">format</span><span class="sxs-lookup"><span data-stu-id="552f9-260">format</span></span> | <span data-ttu-id="552f9-261">指出預設封裝管理格式的布林值。</span><span class="sxs-lookup"><span data-stu-id="552f9-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="552f9-262">如果 `1` 為，則格式為 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="552f9-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="552f9-263">如果 `0` 為，則 *packages.config*格式。</span><span class="sxs-lookup"><span data-stu-id="552f9-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="552f9-264">disabled</span><span class="sxs-lookup"><span data-stu-id="552f9-264">disabled</span></span> | <span data-ttu-id="552f9-265">布林值，指出是否要在第一次安裝套件時顯示提示以選取預設封裝格式。</span><span class="sxs-lookup"><span data-stu-id="552f9-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="552f9-266">`False` 隱藏提示。</span><span class="sxs-lookup"><span data-stu-id="552f9-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="552f9-267">**範例**：</span><span class="sxs-lookup"><span data-stu-id="552f9-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="552f9-268">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="552f9-268">Using environment variables</span></span>

<span data-ttu-id="552f9-269">您可以在 `nuget.config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。</span><span class="sxs-lookup"><span data-stu-id="552f9-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="552f9-270">例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="552f9-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="552f9-271">請注意，您必須使用 Windows 樣式的環境變數 (以% ) 作為開頭和結尾，即使是在 Mac/Linux 上也是如此。</span><span class="sxs-lookup"><span data-stu-id="552f9-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="552f9-272">`$HOME/NuGetRepository`無法解析設定檔中的 Having。</span><span class="sxs-lookup"><span data-stu-id="552f9-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="552f9-273">在 Mac/Linux 上，的值 `%HOME%/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository` 。</span><span class="sxs-lookup"><span data-stu-id="552f9-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="552f9-274">如果找不到環境變數，NuGet 會使用來自設定檔的常值。</span><span class="sxs-lookup"><span data-stu-id="552f9-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="552f9-275">例如， `%MY_UNDEFINED_VAR%/NuGetRepository` 將解析為 `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="552f9-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="552f9-276">下表顯示 NuGet.Config 檔案的環境變數語法和路徑分隔符號的支援。</span><span class="sxs-lookup"><span data-stu-id="552f9-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="552f9-277">NuGet.Config 環境變數支援</span><span class="sxs-lookup"><span data-stu-id="552f9-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="552f9-278">語法</span><span class="sxs-lookup"><span data-stu-id="552f9-278">Syntax</span></span> | <span data-ttu-id="552f9-279">Dir 分隔符號</span><span class="sxs-lookup"><span data-stu-id="552f9-279">Dir separator</span></span> | <span data-ttu-id="552f9-280">Windows nuget.exe</span><span class="sxs-lookup"><span data-stu-id="552f9-280">Windows nuget.exe</span></span> | <span data-ttu-id="552f9-281">Windows dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="552f9-281">Windows dotnet.exe</span></span> | <span data-ttu-id="552f9-282">Mono 中的 Mac nuget.exe () </span><span class="sxs-lookup"><span data-stu-id="552f9-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="552f9-283">Mac dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="552f9-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="552f9-284">是</span><span class="sxs-lookup"><span data-stu-id="552f9-284">Yes</span></span> | <span data-ttu-id="552f9-285">是</span><span class="sxs-lookup"><span data-stu-id="552f9-285">Yes</span></span> | <span data-ttu-id="552f9-286">是</span><span class="sxs-lookup"><span data-stu-id="552f9-286">Yes</span></span> | <span data-ttu-id="552f9-287">是</span><span class="sxs-lookup"><span data-stu-id="552f9-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="552f9-288">是</span><span class="sxs-lookup"><span data-stu-id="552f9-288">Yes</span></span> | <span data-ttu-id="552f9-289">是</span><span class="sxs-lookup"><span data-stu-id="552f9-289">Yes</span></span> | <span data-ttu-id="552f9-290">否</span><span class="sxs-lookup"><span data-stu-id="552f9-290">No</span></span> | <span data-ttu-id="552f9-291">否</span><span class="sxs-lookup"><span data-stu-id="552f9-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="552f9-292">否</span><span class="sxs-lookup"><span data-stu-id="552f9-292">No</span></span> | <span data-ttu-id="552f9-293">否</span><span class="sxs-lookup"><span data-stu-id="552f9-293">No</span></span> | <span data-ttu-id="552f9-294">否</span><span class="sxs-lookup"><span data-stu-id="552f9-294">No</span></span> | <span data-ttu-id="552f9-295">否</span><span class="sxs-lookup"><span data-stu-id="552f9-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="552f9-296">否</span><span class="sxs-lookup"><span data-stu-id="552f9-296">No</span></span> | <span data-ttu-id="552f9-297">否</span><span class="sxs-lookup"><span data-stu-id="552f9-297">No</span></span> | <span data-ttu-id="552f9-298">否</span><span class="sxs-lookup"><span data-stu-id="552f9-298">No</span></span> | <span data-ttu-id="552f9-299">否</span><span class="sxs-lookup"><span data-stu-id="552f9-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="552f9-300">範例設定檔</span><span class="sxs-lookup"><span data-stu-id="552f9-300">Example config file</span></span>

<span data-ttu-id="552f9-301">以下是範例檔案 `nuget.config` ，其中說明許多設定，包括選擇性的設定：</span><span class="sxs-lookup"><span data-stu-id="552f9-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
