---
title: NuGet 4.9 RTM 版本資訊
description: NuGet 4.9 版本資訊，包含已知問題、錯誤 (Bug) 修正、新功能與 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453768"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="ac5b4-103">NuGet 4.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="ac5b4-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="ac5b4-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 NuGet 4.9.0 功能。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="ac5b4-105">相同的功能也有命令列版本可供使用：</span><span class="sxs-lookup"><span data-stu-id="ac5b4-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="ac5b4-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="ac5b4-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="ac5b4-108">摘要：4.9.0 的新功能</span><span class="sxs-lookup"><span data-stu-id="ac5b4-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="ac5b4-109">簽署：讓 ClientPolicies 要求使用 NuGet.Config 中所列的一組受信任作者與存放庫 - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="ac5b4-110">建立 ".snupkg" 檔案以在套件中包含符號 -- 加強推送以了解 nuget 通訊協定以接受符號伺服器的 snupkg 檔案 - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="ac5b4-111">NuGet 認證外掛程式 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="ac5b4-112">自封式 NuGet 套件 - 授權 - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="ac5b4-113">啟用 PackageReference 上的選擇性加入 "GeneratePathProperty" 中繼資料以產生每個套件的 MSBuild 屬性到 "Foo.Bar\1.0\" 目錄 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="ac5b4-114">使用 NuGet 作業改進客戶成功 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ac5b4-115">此版本已修正的問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-115">Issues fixed in this release</span></span>

* <span data-ttu-id="ac5b4-116">由 PackageExtraction 引發的警告提升為錯誤 (透過 WarnAsErrors) 不應該留下擷取的套件 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="ac5b4-117">錯誤簽署的套件最後不應該存在於全域套件資料夾中 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="ac5b4-118">繫結重新導向產生不應該跳過 facade 組件 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="ac5b4-119">VersionRange Equals 無法比較浮點數範圍 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="ac5b4-120">還原：使用新的 .NET Core 2.1 HTTP 堆疊的效能迴歸 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="ac5b4-121">套件的更新不應該修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="ac5b4-122">簽署：若套件有太多套件項目 (>65534)，簽署應該失敗 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="ac5b4-123">"dotnet nuget push" 程式碼路徑應該支援新的認證提供者 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="ac5b4-124">支援執行具有不因文化特性而異的外掛程式 (如 Docker 中所發生) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="ac5b4-125">nuget sources add 不應該從 NuGet.config 刪除認證 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="ac5b4-126">安裝 devDependency PackageReference 不應該預設為 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="ac5b4-127">修正移轉程式選項以針對所有專案顯示並在專案不相容時顯示錯誤 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="ac5b4-128">"dotnet add package" 應該認可它對資產檔案所執行的還原 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="ac5b4-129">簽署：改進簽署相關錯誤訊息 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="ac5b4-130">[測試失敗][zh-TW]套件管理器主控台上的 "Package Manager Console" 字串未當地語系化 - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="ac5b4-131">有關「找不到專案資訊」的錯誤訊息在 VS 內應該更確切一點 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="ac5b4-132">不正確地使用 nuget 套件的 nuspec 版本標記時沒有幫助的錯誤訊息 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="ac5b4-133">DCR - 簽署：支援 NuGet 通訊協定：RepositorySignatures/4.9.0 資源 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="ac5b4-134">DCR - 現在將會在套件擷取期間建立 .nupkg.metadata 檔案 - 包含 "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="ac5b4-135">DCR - 在 Mono 上執行時跳過外掛程式的 Authenticode 驗證 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="ac5b4-136">此 4.9.0 版中修更的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="ac5b4-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="ac5b4-137">摘要：4.9.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="ac5b4-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="ac5b4-138">新增透過新的命令受信任簽署者將寫入項目讀取到 nuget.config 的支援 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ac5b4-139">此版本已修正的問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-139">Issues fixed in this release</span></span>

* <span data-ttu-id="ac5b4-140">修正授權連結產生 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="ac5b4-141">用於驗證簽章的錯誤碼迴歸 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="ac5b4-142">NuGet.Build.Tasks.Pack 套件沒有授權資訊 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="ac5b4-143">此 4.9.1 版本修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="ac5b4-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="ac5b4-144">已知問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="ac5b4-145">當來源名稱包含空格時，dotnet.exe/nuget.exe 未使用認證 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="ac5b4-146">問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-146">Issue</span></span>
<span data-ttu-id="ac5b4-147">當來源名稱中包含空格時，nuget.exe 擲回如 `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` 的錯誤</span><span class="sxs-lookup"><span data-stu-id="ac5b4-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ac5b4-148">因應措施</span><span class="sxs-lookup"><span data-stu-id="ac5b4-148">Workaround</span></span>
<span data-ttu-id="ac5b4-149">變更來源名稱，使其不包含空格。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ac5b4-150">dotnet nuget push --interactive 在 Mac 上發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ac5b4-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="ac5b4-152">問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-152">Issue</span></span>
<span data-ttu-id="ac5b4-153">`--interactive` 引數未由 dotnet cli 轉送並導致錯誤 `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="ac5b4-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ac5b4-154">因應措施</span><span class="sxs-lookup"><span data-stu-id="ac5b4-154">Workaround</span></span>
<span data-ttu-id="ac5b4-155">使用互動式選項 (例如 `dotnet restore --interactive`) 執行任何其他 dotnet 命令並驗證。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ac5b4-156">驗證接著可能會由認證提供者快取。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ac5b4-157">接著，執行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="ac5b4-158">LicenseAcceptanceWindow 與 LicenseFileWindow 協助工具問題 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="ac5b4-159">問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-159">Issue</span></span>
<span data-ttu-id="ac5b4-160">授權接受視窗與授權檔案視窗有鍵盤瀏覽與使用螢幕助讀程式和 JAWS 朗讀方面的協助工具問題。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ac5b4-161">因應措施</span><span class="sxs-lookup"><span data-stu-id="ac5b4-161">Workaround</span></span>
<span data-ttu-id="ac5b4-162">沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ac5b4-163">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ac5b4-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ac5b4-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="ac5b4-165">問題</span><span class="sxs-lookup"><span data-stu-id="ac5b4-165">Issue</span></span>
<span data-ttu-id="ac5b4-166">使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ac5b4-167">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ac5b4-168">因應措施</span><span class="sxs-lookup"><span data-stu-id="ac5b4-168">Workaround</span></span>
<span data-ttu-id="ac5b4-169">透過將 `RestoreAdditionalProjectSources` 設定為空無一物以停用後援資料夾的使用。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ac5b4-170">`<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。</span><span class="sxs-lookup"><span data-stu-id="ac5b4-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
