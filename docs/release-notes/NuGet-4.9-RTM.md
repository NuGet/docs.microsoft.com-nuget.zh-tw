---
title: NuGet 4.9 RTM 版本資訊
description: NuGet 4.9 版本資訊，包含已知問題、錯誤 (Bug) 修正、新功能與 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735132"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="4daa4-103">NuGet 4.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="4daa4-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="4daa4-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="4daa4-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="4daa4-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="4daa4-105">NuGet version</span></span> | <span data-ttu-id="4daa4-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="4daa4-106">Available in Visual Studio version</span></span>| <span data-ttu-id="4daa4-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4daa4-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="4daa4-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="4daa4-108">**4.9.0**</span></span> | <span data-ttu-id="4daa4-109">Visual Studio 2017 15.9.0 版</span><span class="sxs-lookup"><span data-stu-id="4daa4-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="4daa4-110">2.1.500、2.2.100</span><span class="sxs-lookup"><span data-stu-id="4daa4-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="4daa4-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="4daa4-111">**4.9.1**</span></span> | <span data-ttu-id="4daa4-112">N/A</span><span class="sxs-lookup"><span data-stu-id="4daa4-112">n/a</span></span> | <span data-ttu-id="4daa4-113">N/A</span><span class="sxs-lookup"><span data-stu-id="4daa4-113">n/a</span></span> |
| [<span data-ttu-id="4daa4-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="4daa4-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="4daa4-115">Visual Studio 2017 15.9.4 版</span><span class="sxs-lookup"><span data-stu-id="4daa4-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="4daa4-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="4daa4-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="4daa4-117">摘要：4.9.0 中的新功能</span><span class="sxs-lookup"><span data-stu-id="4daa4-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="4daa4-118">簽署：讓 ClientPolicies 要求使用 NuGet.Config 中所列的一組受信任作者與存放庫 - [#6961](https://github.com/NuGet/Home/issues/6961)、[部落格文章](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="4daa4-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="4daa4-119">建立 ".snupkg" 檔案以在套件中包含符號 -- 加強推送以了解 nuget 通訊協定以接受符號伺服器的 snupkg 檔案 - [#6878](https://github.com/NuGet/Home/issues/6878)、[部落格文章](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="4daa4-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="4daa4-120">NuGet 認證外掛程式 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="4daa4-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="4daa4-121">自封式 NuGet 套件 - 授權 - [#4628](https://github.com/NuGet/Home/issues/4628)、[公告](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="4daa4-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="4daa4-122">啟用 PackageReference 上的選擇性加入 "GeneratePathProperty" 中繼資料以產生每個套件的 MSBuild 屬性到 "Foo.Bar\1.0\" 目錄 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="4daa4-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="4daa4-123">使用 NuGet 作業改進客戶成功 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="4daa4-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4daa4-124">此版本修正的問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-124">Issues fixed in this release</span></span>

* <span data-ttu-id="4daa4-125">由 PackageExtraction 引發的警告提升為錯誤 (透過 WarnAsErrors) 不應該留下擷取的套件 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="4daa4-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="4daa4-126">錯誤簽署的套件最後不應該存在於全域套件資料夾中 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="4daa4-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="4daa4-127">繫結重新導向產生不應該跳過 facade 組件 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="4daa4-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="4daa4-128">VersionRange Equals 無法比較浮點數範圍 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="4daa4-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="4daa4-129">還原：使用新的 .NET Core 2.1 HTTP 堆疊的效能迴歸 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="4daa4-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="4daa4-130">套件的更新不應該修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="4daa4-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="4daa4-131">簽署：若套件有太多套件項目 (>65534)，簽署應該失敗 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="4daa4-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="4daa4-132">"dotnet nuget push" 程式碼路徑應該支援新的認證提供者 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="4daa4-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="4daa4-133">支援執行具有不因文化特性而異的外掛程式 (如 Docker 中所發生) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="4daa4-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="4daa4-134">nuget sources add 不應該從 NuGet.config 刪除認證 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="4daa4-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="4daa4-135">安裝 devDependency PackageReference 不應該預設為 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="4daa4-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="4daa4-136">修正移轉程式選項以針對所有專案顯示並在專案不相容時顯示錯誤 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="4daa4-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="4daa4-137">"dotnet add package" 應該認可它對資產檔案所執行的還原 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="4daa4-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="4daa4-138">簽署：改進簽署相關錯誤訊息 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="4daa4-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="4daa4-139">[測試失敗][zh-TW]套件管理器主控台上的 "Package Manager Console" 字串未當地語系化 - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="4daa4-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="4daa4-140">有關「找不到專案資訊」的錯誤訊息在 VS 內應該更確切一點 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="4daa4-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="4daa4-141">不正確地使用 nuget 套件的 nuspec 版本標記時沒有幫助的錯誤訊息 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="4daa4-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="4daa4-142">DCR - 簽署：支援 NuGet 通訊協定：RepositorySignatures/4.9.0 資源- [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="4daa4-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="4daa4-143">DCR - 現在將會在套件擷取期間建立 .nupkg.metadata 檔案 - 包含 "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="4daa4-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="4daa4-144">DCR - 在 Mono 上執行時跳過外掛程式的 Authenticode 驗證 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="4daa4-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="4daa4-145">此 4.9.0 版中修更的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="4daa4-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="4daa4-146">摘要: 4.9.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="4daa4-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="4daa4-147">新增透過新的命令受信任簽署者將寫入項目讀取到 nuget.config 的支援 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="4daa4-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4daa4-148">此版本修正的問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-148">Issues fixed in this release</span></span>

* <span data-ttu-id="4daa4-149">修正授權連結產生 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="4daa4-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="4daa4-150">用於驗證簽章的錯誤碼迴歸 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="4daa4-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="4daa4-151">NuGet.Build.Tasks.Pack 套件沒有授權資訊 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="4daa4-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="4daa4-152">此 4.9.1 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="4daa4-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="4daa4-153">摘要: 4.9.2 中的新功能</span><span class="sxs-lookup"><span data-stu-id="4daa4-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4daa4-154">此版本修正的問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-154">Issues fixed in this release</span></span>

* <span data-ttu-id="4daa4-155">當來源名稱包含空格時，VS/dotnet.exe/nuget.exe/msbuild.exe 資源未使用認證 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="4daa4-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="4daa4-156">LicenseAcceptanceWindow 與 LicenseFileWindow 協助工具問題 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="4daa4-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="4daa4-157">修正 DateTime.Parse 中來自 DateTimeConverter 的 FormatException - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="4daa4-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="4daa4-158">此 4.9.2 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="4daa4-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="4daa4-159">已知問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="4daa4-160">dotnet nuget push --interactive 在 Mac 上發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="4daa4-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="4daa4-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="4daa4-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="4daa4-162">問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-162">Issue</span></span>
<span data-ttu-id="4daa4-163">`--interactive` 引數未由 dotnet cli 轉送並導致錯誤 `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="4daa4-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="4daa4-164">因應措施</span><span class="sxs-lookup"><span data-stu-id="4daa4-164">Workaround</span></span>
<span data-ttu-id="4daa4-165">使用互動式選項 (例如 `dotnet restore --interactive`) 執行任何其他 dotnet 命令並驗證。</span><span class="sxs-lookup"><span data-stu-id="4daa4-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="4daa4-166">驗證接著可能會由認證提供者快取。</span><span class="sxs-lookup"><span data-stu-id="4daa4-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="4daa4-167">接著，執行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="4daa4-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="4daa4-168">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="4daa4-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="4daa4-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="4daa4-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="4daa4-170">問題</span><span class="sxs-lookup"><span data-stu-id="4daa4-170">Issue</span></span>
<span data-ttu-id="4daa4-171">使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="4daa4-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="4daa4-172">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="4daa4-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="4daa4-173">因應措施</span><span class="sxs-lookup"><span data-stu-id="4daa4-173">Workaround</span></span>
<span data-ttu-id="4daa4-174">透過將 `RestoreAdditionalProjectSources` 設定為空無一物以停用後援資料夾的使用。</span><span class="sxs-lookup"><span data-stu-id="4daa4-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="4daa4-175">`<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。</span><span class="sxs-lookup"><span data-stu-id="4daa4-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
