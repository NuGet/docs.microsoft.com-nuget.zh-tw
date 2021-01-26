---
title: NuGet 4.9 RTM 版本資訊
description: NuGet 4.9 版本資訊，包含已知問題、錯誤 (Bug) 修正、新功能與 DCR。
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780150"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="57738-103">NuGet 4.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="57738-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="57738-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="57738-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="57738-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="57738-105">NuGet version</span></span> | <span data-ttu-id="57738-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="57738-106">Available in Visual Studio version</span></span>| <span data-ttu-id="57738-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="57738-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="57738-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="57738-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="57738-109">Visual Studio 2017 版本15.9。0</span><span class="sxs-lookup"><span data-stu-id="57738-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="57738-110">2.1.500、2.2.100</span><span class="sxs-lookup"><span data-stu-id="57738-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="57738-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="57738-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="57738-112">n/a</span><span class="sxs-lookup"><span data-stu-id="57738-112">n/a</span></span> | <span data-ttu-id="57738-113">n/a</span><span class="sxs-lookup"><span data-stu-id="57738-113">n/a</span></span> |
| [<span data-ttu-id="57738-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="57738-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="57738-115">Visual Studio 2017 版本15.9。4</span><span class="sxs-lookup"><span data-stu-id="57738-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="57738-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="57738-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="57738-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="57738-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="57738-118">Visual Studio 2017 版本15.9.6 版</span><span class="sxs-lookup"><span data-stu-id="57738-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="57738-119">2.1.504、2.2.104</span><span class="sxs-lookup"><span data-stu-id="57738-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="57738-120">摘要：4.9.0 的新功能</span><span class="sxs-lookup"><span data-stu-id="57738-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="57738-121">簽署：讓 ClientPolicies 要求使用一組受信任的作者和儲存機制，NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961)列于[blog 文章](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)中。</span><span class="sxs-lookup"><span data-stu-id="57738-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="57738-122">建立 ".snupkg" 檔案以在套件中包含符號 -- 加強推送以了解 nuget 通訊協定以接受符號伺服器的 snupkg 檔案 - [#6878](https://github.com/NuGet/Home/issues/6878)、[部落格文章](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="57738-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="57738-123">NuGet 認證外掛程式 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="57738-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="57738-124">自封式 NuGet 套件 - 授權 - [#4628](https://github.com/NuGet/Home/issues/4628)、[公告](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="57738-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="57738-125">啟用 PackageReference 上的選擇性加入 "GeneratePathProperty" 中繼資料以產生每個套件的 MSBuild 屬性到 "Foo.Bar\1.0\" 目錄 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="57738-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="57738-126">使用 NuGet 作業改進客戶成功 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="57738-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="57738-127">使用鎖定檔案啟用可重複的套件還原 - [#5602](https://github.com/NuGet/Home/issues/5602)、[公告](https://github.com/NuGet/Announcements/issues/28)、[部落格文章](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="57738-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="57738-128">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="57738-128">Issues fixed in this release</span></span>

* <span data-ttu-id="57738-129">由 PackageExtraction 引發的警告提升為錯誤 (透過 WarnAsErrors) 不應該留下擷取的套件 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="57738-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="57738-130">錯誤簽署的套件最後不應該存在於全域套件資料夾中 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="57738-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="57738-131">繫結重新導向產生不應該跳過 facade 組件 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="57738-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="57738-132">VersionRange Equals 無法比較浮點數範圍 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="57738-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="57738-133">還原：使用新的 .NET Core 2.1 HTTP 堆疊的效能迴歸 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="57738-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="57738-134">套件的更新不應該修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="57738-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="57738-135">簽署：若套件有太多套件項目 (>65534)，簽署應該失敗 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="57738-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="57738-136">"dotnet nuget push" 程式碼路徑應該支援新的認證提供者 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="57738-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="57738-137">支援執行具有不因文化特性而異的外掛程式 (如 Docker 中所發生) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="57738-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="57738-138">nuget sources add 不應該從 NuGet.config 刪除認證 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="57738-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="57738-139">安裝 devDependency PackageReference 不應該預設為 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="57738-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="57738-140">修正移轉程式選項以針對所有專案顯示並在專案不相容時顯示錯誤 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="57738-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="57738-141">"dotnet add package" 應該認可它對資產檔案所執行的還原 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="57738-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="57738-142">簽署：改進簽署相關錯誤訊息 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="57738-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="57738-143">[測試失敗][zh-TW]套件管理器主控台上的 "Package Manager Console" 字串未當地語系化 - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="57738-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="57738-144">有關「找不到專案資訊」的錯誤訊息在 VS 內應該更確切一點 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="57738-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="57738-145">不正確地使用 nuget 套件的 nuspec 版本標記時沒有幫助的錯誤訊息 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="57738-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="57738-146">DCR - 簽署：支援 NuGet 通訊協定：RepositorySignatures/4.9.0 資源 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="57738-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="57738-147">DCR - 現在將會在套件擷取期間建立 .nupkg.metadata 檔案 - 包含 "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="57738-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="57738-148">DCR - 在 Mono 上執行時跳過外掛程式的 Authenticode 驗證 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="57738-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="57738-149">此 4.9.0 版中修更的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="57738-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="57738-150">摘要：4.9.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="57738-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="57738-151">新增透過新的命令受信任簽署者將寫入項目讀取到 nuget.config 的支援 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="57738-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="57738-152">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="57738-152">Issues fixed in this release</span></span>

* <span data-ttu-id="57738-153">修正授權連結產生 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="57738-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="57738-154">用於驗證簽章的錯誤碼迴歸 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="57738-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="57738-155">NuGet.Build.Tasks.Pack 套件沒有授權資訊 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="57738-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="57738-156">此 4.9.1 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="57738-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="57738-157">摘要：4.9.2 的新功能</span><span class="sxs-lookup"><span data-stu-id="57738-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="57738-158">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="57738-158">Issues fixed in this release</span></span>

* <span data-ttu-id="57738-159">當來源名稱包含空格時，VS/dotnet.exe/nuget.exe/msbuild.exe 資源未使用認證 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="57738-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="57738-160">LicenseAcceptanceWindow 與 LicenseFileWindow 協助工具問題 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="57738-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="57738-161">修正 DateTime.Parse 中來自 DateTimeConverter 的 FormatException - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="57738-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="57738-162">此 4.9.2 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="57738-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="57738-163">摘要：4.9.3 的新功能</span><span class="sxs-lookup"><span data-stu-id="57738-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="57738-164">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="57738-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="57738-165">「使用鎖定檔案的可重複的套件還原」問題</span><span class="sxs-lookup"><span data-stu-id="57738-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="57738-166">針對先前的已快取套件，未以雜湊方式運作的鎖定模式計算錯誤 - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="57738-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="57738-167">還原會解析為與 `packages.lock.json` 檔案中所定義之版本不同的版本 - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="57738-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="57738-168">'--locked-mode / RestoreLockedMode' 導致可疑的還原失敗 (當涉及 ProjectReferences 時) - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="57738-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="57738-169">MSBuild SDK 解析程式嘗試驗證 SDK 套件的 SHA (在使用 packages.lock.json 時，此套件還原失敗) - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="57738-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="57738-170">「使用可設定的信任原則鎖定您的相依性」問題</span><span class="sxs-lookup"><span data-stu-id="57738-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="57738-171">簽署不支援的套件時，dotnet.exe 不應該評估信任的簽署者 - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="57738-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="57738-172">設定檔中 trustedSigners 的順序會影響信任評估 - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="57738-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="57738-173">無法實作 ISettings [由重構 API 設定以支援信任原則功能引起] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="57738-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="57738-174">「改良的偵錯體驗」問題</span><span class="sxs-lookup"><span data-stu-id="57738-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="57738-175">無法為 .NET Core 全域工具發行符號套件 - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="57738-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="57738-176">「自封式 NuGet 套件 - 授權」問題</span><span class="sxs-lookup"><span data-stu-id="57738-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="57738-177">使用內嵌授權檔案時，建置符號 .snupkg 套件發生錯誤 - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="57738-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="57738-178">此 4.9.3 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="57738-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="57738-179">摘要：4.9.4 的新功能</span><span class="sxs-lookup"><span data-stu-id="57738-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="57738-180">安全性修正：在 ~/.nuget 內建立之檔案的許可權太過開啟 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="57738-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="57738-181">已知問題</span><span class="sxs-lookup"><span data-stu-id="57738-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="57738-182">dotnet nuget push --interactive 在 Mac 上發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="57738-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="57738-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="57738-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="57738-184">問題</span><span class="sxs-lookup"><span data-stu-id="57738-184">Issue</span></span>
<span data-ttu-id="57738-185">`--interactive` 引數未由 dotnet cli 轉送並導致錯誤 `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="57738-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="57738-186">因應措施</span><span class="sxs-lookup"><span data-stu-id="57738-186">Workaround</span></span>
<span data-ttu-id="57738-187">使用互動式選項 (例如 `dotnet restore --interactive`) 執行任何其他 dotnet 命令並驗證。</span><span class="sxs-lookup"><span data-stu-id="57738-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="57738-188">驗證接著可能會由認證提供者快取。</span><span class="sxs-lookup"><span data-stu-id="57738-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="57738-189">然後執行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="57738-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="57738-190">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="57738-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="57738-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="57738-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="57738-192">問題</span><span class="sxs-lookup"><span data-stu-id="57738-192">Issue</span></span>
<span data-ttu-id="57738-193">使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="57738-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="57738-194">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="57738-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="57738-195">因應措施</span><span class="sxs-lookup"><span data-stu-id="57738-195">Workaround</span></span>
<span data-ttu-id="57738-196">透過將 `RestoreAdditionalProjectSources` 設定為空無一物以停用後援資料夾的使用。</span><span class="sxs-lookup"><span data-stu-id="57738-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="57738-197">`<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。</span><span class="sxs-lookup"><span data-stu-id="57738-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
