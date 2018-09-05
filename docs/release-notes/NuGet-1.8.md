---
title: NuGet 1.8 的版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.8 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546617"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="c56c4-103">NuGet 1.8 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="c56c4-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="c56c4-104">[NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md) | [NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="c56c4-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="c56c4-105">NuGet 1.8 已於 2012 5 月 23 日發行。</span><span class="sxs-lookup"><span data-stu-id="c56c4-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="c56c4-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="c56c4-106">Known Installation Issue</span></span>
<span data-ttu-id="c56c4-107">如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。</span><span class="sxs-lookup"><span data-stu-id="c56c4-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="c56c4-108">因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="c56c4-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c56c4-109">請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="c56c4-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="c56c4-110">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="c56c4-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="c56c4-111">NuGet 1.8 相容 Windows xp 中，發行的 hotfix</span><span class="sxs-lookup"><span data-stu-id="c56c4-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="c56c4-112">NuGet 1.8 發行不久之後，我們已了解 1.8 的密碼編譯變更中斷使用者，在 Windows XP 上。</span><span class="sxs-lookup"><span data-stu-id="c56c4-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="c56c4-113">我們因為已發行 hotfix 來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="c56c4-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="c56c4-114">藉由更新透過 Visual Studio 延伸模組組件庫的 NuGet，您會收到此 hotfix。</span><span class="sxs-lookup"><span data-stu-id="c56c4-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="c56c4-115">功能</span><span class="sxs-lookup"><span data-stu-id="c56c4-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="c56c4-116">當地語系化資源的附屬套件</span><span class="sxs-lookup"><span data-stu-id="c56c4-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="c56c4-117">NuGet 1.8 現在支援建立個別的封裝，如需當地語系化的資源，類似於.NET Framework 的附屬組件功能的能力。</span><span class="sxs-lookup"><span data-stu-id="c56c4-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="c56c4-118">附屬套件會在相同的方式，加上一些慣例的任何其他 NuGet 套件的形式建立：</span><span class="sxs-lookup"><span data-stu-id="c56c4-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="c56c4-119">附屬套件識別碼和檔案名稱應包含符合標準的其中一個尾碼[文化特性 .NET Framework 所使用字串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c56c4-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="c56c4-120">在其`.nuspec`檔案，附屬套件應該定義語言項目具有相同識別碼使用的文化特性字串</span><span class="sxs-lookup"><span data-stu-id="c56c4-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="c56c4-121">附屬套件應該定義中的相依性及其`.nuspec`其核心封裝，也就是只要使用相同的識別碼，減去語言字尾封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="c56c4-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="c56c4-122">核心封裝必須可成功安裝的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="c56c4-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="c56c4-123">若要將套件安裝當地語系化的資源，開發人員明確選取當地語系化的套件儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="c56c4-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="c56c4-124">目前，NuGet 資源庫不會提供任何一種特殊處理，就可以附屬套件。</span><span class="sxs-lookup"><span data-stu-id="c56c4-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![使用當地語系化 pacakges 套件管理員 對話方塊](./media/dlg-w-loc-packs.png)

<span data-ttu-id="c56c4-126">附屬套件列出其核心封裝的相依性，因為在附屬和核心套件會提取至 NuGet 套件資料夾，並安裝。</span><span class="sxs-lookup"><span data-stu-id="c56c4-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![封裝資料夾中，使用當地語系化的套件](./media/fldr-loc-packs.png)

<span data-ttu-id="c56c4-128">此外，在安裝附屬套件，NuGet 也會辨識的文化特性的字串命名慣例，然後將當地語系化的資源組件複製到核心封裝內的正確子資料夾，以便它可以挑選由.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="c56c4-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![核心封裝資料夾中，使用複製的資源資料夾](./media/fldr-copied-loc.png)

<span data-ttu-id="c56c4-130">一個現有的 bug，要特別注意的附屬套件是 NuGet 不會複製至的當地語系化的資源`bin`適用於網站專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c56c4-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="c56c4-131">在 NuGet 的下一個版本中，將會修正此問題。</span><span class="sxs-lookup"><span data-stu-id="c56c4-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="c56c4-132">如需示範如何建立和使用附屬套件的完整範例，請參閱 < [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。</span><span class="sxs-lookup"><span data-stu-id="c56c4-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="c56c4-133">套件還原同意</span><span class="sxs-lookup"><span data-stu-id="c56c4-133">Package Restore Consent</span></span>
<span data-ttu-id="c56c4-134">在 NuGet 1.8 中，我們打造出支援套件還原以保護使用者隱私權的一個重要限制。</span><span class="sxs-lookup"><span data-stu-id="c56c4-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="c56c4-135">此條件約束需要開發人員在建置專案和方案明確地同意套件還原用套件還原的上線設定的套件來源下載套件。</span><span class="sxs-lookup"><span data-stu-id="c56c4-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="c56c4-136">有 2 種方式可提供此同意。</span><span class="sxs-lookup"><span data-stu-id="c56c4-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="c56c4-137">第一個可在 [套件管理員設定] 對話方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c56c4-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="c56c4-138">這個方法主要是供開發人員電腦。</span><span class="sxs-lookup"><span data-stu-id="c56c4-138">This method is primarily intended for developer machines.</span></span>

![套件管理員 設定對話方塊](./media/pr-consent-configdlg.png)

<span data-ttu-id="c56c4-140">第二種方法是將環境變數"EnableNuGetPackageRestore 」 設為值"true"。</span><span class="sxs-lookup"><span data-stu-id="c56c4-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="c56c4-141">這個方法適用於無人看管的電腦，例如 CI 或組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="c56c4-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="c56c4-142">現在，如上所述，我們有只打造出這項功能在 NuGet 1.8。</span><span class="sxs-lookup"><span data-stu-id="c56c4-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="c56c4-143">實際上，這表示，雖然我們已新增所有的邏輯，以啟用功能，它目前未強制執行在此版本。</span><span class="sxs-lookup"><span data-stu-id="c56c4-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="c56c4-144">將會啟用，不過，在下一個版本的 NuGet，因此我們想要讓您知道它儘速，以便您可以適當地設定您的環境，並因此不會影響我們啟動時強制使用同意條件約束。</span><span class="sxs-lookup"><span data-stu-id="c56c4-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="c56c4-145">如需詳細資訊，請參閱[小組部落格文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)這項功能。</span><span class="sxs-lookup"><span data-stu-id="c56c4-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="c56c4-146">nuget.exe 的效能改進</span><span class="sxs-lookup"><span data-stu-id="c56c4-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="c56c4-147">藉由修改安裝命令，下載及並行安裝套件，NuGet 1.8 會提供大幅的效能增強功能 nuget.exe-to 和 by 延伸模組套件還原。</span><span class="sxs-lookup"><span data-stu-id="c56c4-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="c56c4-148">高的層級測試顯示為 6 的套件安裝至專案的效能改善在 NuGet 1.8 約 35%。</span><span class="sxs-lookup"><span data-stu-id="c56c4-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="c56c4-149">增加到 25 的套件數目，顯示約 60%的效能提高。</span><span class="sxs-lookup"><span data-stu-id="c56c4-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c56c4-150">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="c56c4-150">Bug Fixes</span></span>
<span data-ttu-id="c56c4-151">NuGet 1.8 會包含相當多的 bug 修正，並強調的套件管理員主控台和套件還原工作流程，特別是與封裝還原同意與 Windows 8 Express 整合。</span><span class="sxs-lookup"><span data-stu-id="c56c4-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="c56c4-152">如需完整的工作清單項目中已修正 NuGet 1.8，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="c56c4-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
