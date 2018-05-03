---
title: NuGet 1.8 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.8 的版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1801d62b786717c088429fbeca6f1f72f5ab6b4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="e4771-103">NuGet 1.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="e4771-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="e4771-104">[NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md) | [NuGet 2.0 版本資訊](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="e4771-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="e4771-105">NuGet 1.8 已於 2012 月 23 日發行。</span><span class="sxs-lookup"><span data-stu-id="e4771-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="e4771-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="e4771-106">Known Installation Issue</span></span>
<span data-ttu-id="e4771-107">如果您正在執行 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您有安裝較舊的版本。</span><span class="sxs-lookup"><span data-stu-id="e4771-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="e4771-108">因應措施是只要解除安裝 NuGet，然後再從 VS 擴充功能庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="e4771-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="e4771-109">請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="e4771-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="e4771-110">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕會停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="e4771-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="e4771-111">NuGet 1.8 相容 Windows XP 中，發行的 hotfix</span><span class="sxs-lookup"><span data-stu-id="e4771-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="e4771-112">NuGet 1.8 很快發行之後，我們所了解密碼編譯中的變更 1.8 中斷使用者，在 Windows XP 上。</span><span class="sxs-lookup"><span data-stu-id="e4771-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="e4771-113">我們已因為已發行 hotfix，以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="e4771-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="e4771-114">透過更新 Visual Studio 延伸模組組件庫中透過 NuGet，您會收到此 hotfix。</span><span class="sxs-lookup"><span data-stu-id="e4771-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="e4771-115">功能</span><span class="sxs-lookup"><span data-stu-id="e4771-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="e4771-116">當地語系化資源的附屬項目封裝</span><span class="sxs-lookup"><span data-stu-id="e4771-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="e4771-117">NuGet 1.8 現在支援建立個別的封裝，當地語系化的資源，類似於.NET Framework 的附屬組件功能的能力。</span><span class="sxs-lookup"><span data-stu-id="e4771-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="e4771-118">加上一些慣例的任何其他 NuGet 封裝為相同的方式建立附屬項目封裝：</span><span class="sxs-lookup"><span data-stu-id="e4771-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="e4771-119">附屬項目封裝識別碼和檔案名稱應該包含符合其中一個標準的後置詞[文化特性使用的.NET Framework 字串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e4771-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="e4771-120">在其`.nuspec`檔案，附屬封裝應該定義語言項目具有相同識別碼中使用的文化特性字串</span><span class="sxs-lookup"><span data-stu-id="e4771-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="e4771-121">附屬項目封裝應該定義中的相依性及其`.nuspec`核心封裝，也就是減去語言尾碼相同的識別碼與封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="e4771-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="e4771-122">此核心套件必須能夠使用成功安裝的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="e4771-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="e4771-123">若要安裝當地語系化的資源的封裝，開發人員明確選取當地語系化的封裝儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="e4771-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="e4771-124">目前，在 NuGet gallery 所提供的任何一種特殊處理，附屬封裝。</span><span class="sxs-lookup"><span data-stu-id="e4771-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![與當地語系化 pacakges 封裝管理員 對話方塊](./media/dlg-w-loc-packs.png)

<span data-ttu-id="e4771-126">附屬項目封裝列出其核心封裝的相依性，因為附屬和核心封裝並提取到 [NuGet 封裝] 資料夾，因此安裝。</span><span class="sxs-lookup"><span data-stu-id="e4771-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![當地語系化的封裝與封裝資料夾](./media/fldr-loc-packs.png)

<span data-ttu-id="e4771-128">此外，安裝附屬套件，NuGet 也能辨識的文化特性的字串命名慣例，而且，讓它可以由.NET Framework 中選取，然後將當地語系化的資源組件複製到核心封裝內的正確子資料夾。</span><span class="sxs-lookup"><span data-stu-id="e4771-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![核心封裝資料夾與複製的資源資料夾](./media/fldr-copied-loc.png)

<span data-ttu-id="e4771-130">要注意與附屬封裝一個現有的 bug 會 NuGet 當地語系化的資源不會複製`bin`適用於網站專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e4771-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="e4771-131">NuGet 的下一個版本中，將會修正此問題。</span><span class="sxs-lookup"><span data-stu-id="e4771-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="e4771-132">如需示範如何建立及使用附屬項目封裝的完整範例，請參閱[ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。</span><span class="sxs-lookup"><span data-stu-id="e4771-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="e4771-133">封裝還原同意</span><span class="sxs-lookup"><span data-stu-id="e4771-133">Package Restore Consent</span></span>
<span data-ttu-id="e4771-134">在 NuGet 1.8 我們打造支援來保護使用者隱私權的封裝還原的一個重要限制。</span><span class="sxs-lookup"><span data-stu-id="e4771-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="e4771-135">此條件約束需要開發人員在建置專案和方案用來明確地同意封裝還原封裝還原的上線從設定的封裝來源下載套件。</span><span class="sxs-lookup"><span data-stu-id="e4771-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="e4771-136">有 2 種方式來提供此同意。</span><span class="sxs-lookup"><span data-stu-id="e4771-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="e4771-137">第一個位於 [套件管理員設定] 對話方塊如下所示。</span><span class="sxs-lookup"><span data-stu-id="e4771-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="e4771-138">這個方法主要是用於開發人員電腦。</span><span class="sxs-lookup"><span data-stu-id="e4771-138">This method is primarily intended for developer machines.</span></span>

![封裝管理員的組態對話方塊](./media/pr-consent-configdlg.png)

<span data-ttu-id="e4771-140">第二種方法是將設定環境變數"EnableNuGetPackageRestore"值"true"。</span><span class="sxs-lookup"><span data-stu-id="e4771-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="e4771-141">這個方法適用於無人看管的電腦，例如 CI 或組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="e4771-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="e4771-142">現在，如上所述，我們已於 NuGet 1.8 中只配置這項功能的基礎。</span><span class="sxs-lookup"><span data-stu-id="e4771-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="e4771-143">實際上，這表示，雖然我們新增了所有的邏輯，以啟用功能，它會目前未強制執行此版本中。</span><span class="sxs-lookup"><span data-stu-id="e4771-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="e4771-144">會啟用它，不過，在下一個版本的 NuGet，因此我們想要讓您知道它儘速使您可以適當地設定您的環境，並因此不會影響我們啟動時，強制使用同意條件約束。</span><span class="sxs-lookup"><span data-stu-id="e4771-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="e4771-145">如需詳細資訊，請參閱[小組部落格文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)這項功能。</span><span class="sxs-lookup"><span data-stu-id="e4771-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="e4771-146">nuget.exe 的效能改進</span><span class="sxs-lookup"><span data-stu-id="e4771-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="e4771-147">藉由修改安裝命令，以下載並安裝封裝，以平行方式，NuGet 1.8 帶來重大的效能改進 nuget.exe – 和擴充功能封裝還原。</span><span class="sxs-lookup"><span data-stu-id="e4771-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="e4771-148">高的層級測試顯示 6 封裝安裝到專案的效能改善大約在 NuGet 1.8 35%。</span><span class="sxs-lookup"><span data-stu-id="e4771-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="e4771-149">增加到 25 的套件數目，顯示大約 60%的效能提高。</span><span class="sxs-lookup"><span data-stu-id="e4771-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e4771-150">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="e4771-150">Bug Fixes</span></span>
<span data-ttu-id="e4771-151">NuGet 1.8 包含很多 bug 修正，特別強調的封裝管理員主控台和封裝還原工作流程，特別是在關聯於封裝還原同意和 Windows 8 Express 整合。</span><span class="sxs-lookup"><span data-stu-id="e4771-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="e4771-152">如需完整的工作清單項目固定在 NuGet 1.8，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="e4771-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
