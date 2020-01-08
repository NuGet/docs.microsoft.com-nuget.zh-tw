---
title: NuGet 1.8 版本資訊
description: NuGet 1.8 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383457"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="fd731-103">NuGet 1.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="fd731-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="fd731-104">[Nuget 1.7 版本](../release-notes/nuget-1.7.md)資訊 | [nuget 2.0 版本](../release-notes/nuget-2.0.md)資訊</span><span class="sxs-lookup"><span data-stu-id="fd731-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="fd731-105">NuGet 1.8 已于2012年5月23日發行。</span><span class="sxs-lookup"><span data-stu-id="fd731-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="fd731-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="fd731-106">Known Installation Issue</span></span>
<span data-ttu-id="fd731-107">如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd731-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="fd731-108">因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="fd731-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="fd731-109">如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>，或[直接移至 VS 提供程式](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="fd731-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="fd731-110">注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="fd731-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="fd731-111">NuGet 1.8 與 Windows XP 不相容，已發行的修補程式</span><span class="sxs-lookup"><span data-stu-id="fd731-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="fd731-112">在 NuGet 1.8 發行後不久，我們已瞭解1.8 中的密碼編譯變更會中斷 Windows XP 上的使用者。</span><span class="sxs-lookup"><span data-stu-id="fd731-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="fd731-113">我們已發行解決此問題的修正程式。</span><span class="sxs-lookup"><span data-stu-id="fd731-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="fd731-114">藉由 Visual Studio 延伸模組資源庫來更新 NuGet，您會收到此修補程式。</span><span class="sxs-lookup"><span data-stu-id="fd731-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="fd731-115">功能</span><span class="sxs-lookup"><span data-stu-id="fd731-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="fd731-116">當地語系化資源的附屬套件</span><span class="sxs-lookup"><span data-stu-id="fd731-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="fd731-117">NuGet 1.8 現在支援針對當地語系化的資源建立個別的封裝，類似于 .NET Framework 的附屬元件功能。</span><span class="sxs-lookup"><span data-stu-id="fd731-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="fd731-118">附屬套件的建立方式與任何其他 NuGet 套件相同，並加入幾個慣例：</span><span class="sxs-lookup"><span data-stu-id="fd731-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="fd731-119">附屬套件識別碼和檔案名應包含尾碼，以符合 .NET Framework 所使用的其中一個標準[文化特性字串](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。</span><span class="sxs-lookup"><span data-stu-id="fd731-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).</span></span>
* <span data-ttu-id="fd731-120">在它的 `.nuspec` 檔案中，附屬套件應使用識別碼中所用的相同文化特性字串來定義語言元素。</span><span class="sxs-lookup"><span data-stu-id="fd731-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="fd731-121">附屬套件應定義其 `.nuspec` 檔案中的相依性至其核心套件，這只是識別碼減去語言尾碼的套件。</span><span class="sxs-lookup"><span data-stu-id="fd731-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="fd731-122">核心套件必須在存放庫中提供，才能成功安裝。</span><span class="sxs-lookup"><span data-stu-id="fd731-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="fd731-123">若要安裝具有當地語系化資源的套件，開發人員會從存放庫明確選取當地語系化的封裝。</span><span class="sxs-lookup"><span data-stu-id="fd731-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="fd731-124">目前，NuGet 資源庫不會對附屬套件提供任何一種特殊的處理方式。</span><span class="sxs-lookup"><span data-stu-id="fd731-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![具有當地語系化套件的 [套件管理員] 對話方塊](./media/dlg-w-loc-packs.png)

<span data-ttu-id="fd731-126">因為附屬套件會列出其核心套件的相依性，所以附屬和核心套件都會提取至 NuGet 套件資料夾並安裝。</span><span class="sxs-lookup"><span data-stu-id="fd731-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![具有當地語系化套件的封裝資料夾](./media/fldr-loc-packs.png)

<span data-ttu-id="fd731-128">此外，在安裝附屬套件時，NuGet 也會辨識文化特性字串命名慣例，然後將當地語系化的資源元件複製到核心套件中正確的子資料夾，以供 .NET Framework 挑選。</span><span class="sxs-lookup"><span data-stu-id="fd731-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![已複製資源資料夾的核心封裝資料夾](./media/fldr-copied-loc.png)

<span data-ttu-id="fd731-130">要注意的附屬套件有一個現有的錯誤，就是 NuGet 不會將當地語系化的資源複製到網站專案的 `bin` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd731-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="fd731-131">此問題將在下一版的 NuGet 中修正。</span><span class="sxs-lookup"><span data-stu-id="fd731-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="fd731-132">如需示範如何建立和使用附屬套件的完整範例，請參閱[https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)。</span><span class="sxs-lookup"><span data-stu-id="fd731-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="fd731-133">套件還原同意</span><span class="sxs-lookup"><span data-stu-id="fd731-133">Package Restore Consent</span></span>
<span data-ttu-id="fd731-134">在 NuGet 1.8 中，我們已為支援封裝還原的重要條件約束奠定基礎，以保護使用者隱私權。</span><span class="sxs-lookup"><span data-stu-id="fd731-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="fd731-135">此條件約束需要開發人員建立專案和解決方案，使用套件還原來明確同意封裝還原上線，以從設定的套件來源下載套件。</span><span class="sxs-lookup"><span data-stu-id="fd731-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="fd731-136">有2種方式可提供這種同意。</span><span class="sxs-lookup"><span data-stu-id="fd731-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="fd731-137">第一個可在 [套件管理員設定] 對話方塊中找到，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd731-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="fd731-138">這個方法主要是供開發人員機器。</span><span class="sxs-lookup"><span data-stu-id="fd731-138">This method is primarily intended for developer machines.</span></span>

![[套件管理員設定] 對話方塊](./media/pr-consent-configdlg.png)

<span data-ttu-id="fd731-140">第二種方法是將環境變數 "EnableNuGetPackageRestore" 設定為值 "true"。</span><span class="sxs-lookup"><span data-stu-id="fd731-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="fd731-141">此方法適用于自動機器，例如 CI 或組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd731-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="fd731-142">如先前所述，我們只在 NuGet 1.8 中為這項功能奠定了基礎。</span><span class="sxs-lookup"><span data-stu-id="fd731-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="fd731-143">實際上，這表示雖然我們已新增所有邏輯來啟用此功能，但目前並不會在此版本中強制執行。</span><span class="sxs-lookup"><span data-stu-id="fd731-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="fd731-144">不過，它會在下一版的 NuGet 中啟用，因此我們想要讓您儘快知道它，以便您可以適當地設定環境，並在我們開始強制執行同意條件約束時不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="fd731-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="fd731-145">如需詳細資訊，請參閱這項功能的[小組博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)。</span><span class="sxs-lookup"><span data-stu-id="fd731-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="fd731-146">nuget.exe 效能改進</span><span class="sxs-lookup"><span data-stu-id="fd731-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="fd731-147">藉由修改 install 命令來以平行方式下載和安裝套件，NuGet 1.8 針對 nuget.exe –和擴充套件還原帶來了顯著的效能改進。</span><span class="sxs-lookup"><span data-stu-id="fd731-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="fd731-148">高階測試顯示將6個套件安裝到專案中的效能，在 NuGet 1.8 中可改善大約35%。</span><span class="sxs-lookup"><span data-stu-id="fd731-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="fd731-149">將封裝數目增加為25會顯示大約60% 的效能提升。</span><span class="sxs-lookup"><span data-stu-id="fd731-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="fd731-150">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="fd731-150">Bug Fixes</span></span>
<span data-ttu-id="fd731-151">NuGet 1.8 包含很多 bug 修正，著重于套件管理員主控台和套件還原工作流程，特別是與套件還原同意和 Windows 8 Express 整合相關。</span><span class="sxs-lookup"><span data-stu-id="fd731-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="fd731-152">如需 NuGet 1.8 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="fd731-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
