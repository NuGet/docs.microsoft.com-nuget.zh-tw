---
title: 使用 NuGet 套件的概觀和工作流程 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/22/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 在專案中使用 NuGet 套件之程序的概觀，以及程序之其他特定部分的連結。
keywords: NuGet 套件使用, NuGet 使用概觀, NuGet 使用工作流程, 套件使用工作流程, 套件使用概觀
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e79b09fe8131f25c6bbed650e1927425dcc5d409
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="5bf33-104">套件使用工作流程</span><span class="sxs-lookup"><span data-stu-id="5bf33-104">Package consumption workflow</span></span>

<span data-ttu-id="5bf33-105">在 nuget.org 與您組織可建立的私人套件庫之間，您可以找到數以萬計的高可用套件，以在您的應用程式和服務中使用。</span><span class="sxs-lookup"><span data-stu-id="5bf33-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="5bf33-106">但是不論來源為何，使用套件會遵循相同的一般工作流程。</span><span class="sxs-lookup"><span data-stu-id="5bf33-106">But regardless of the source, consuming a package follows the same general workflow.</span></span>

![移至套件來源、尋找套件、將它安裝至專案，然後新增 using 陳述式和套件 API 呼叫的流程](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="5bf33-108">\* _僅限 Visual Studio 和 dotnet.ex\`。Muget 安裝命令不會修改專案檔或 packages.config，項目必須手動管理。_</span><span class="sxs-lookup"><span data-stu-id="5bf33-108">\* _Visual Studio and dotnet.ex\` only. The nuget install command does not modify project files or packages.config; entries must be managed manually._</span></span>

<span data-ttu-id="5bf33-109">如需詳細資訊，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)和[安裝 NuGet 套件的不同方式](ways-to-install-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf33-109">For further details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

<span data-ttu-id="5bf33-110">NuGet 會記住每個已安裝套件的身分識別和版本號碼，並將其記錄在 [`packages.config`](../reference/packages-config.md) 或專案檔中 (使用 [PackageReference](../consume-packages/package-references-in-project-files.md))，端視專案類型和 NuGet 版本而定。</span><span class="sxs-lookup"><span data-stu-id="5bf33-110">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file (using [PackageReference](../consume-packages/package-references-in-project-files.md)), depending on project type and your version of NuGet.</span></span> <span data-ttu-id="5bf33-111">使用 NuGet 4.0+ 時，儘管這可在 Visual Studio 中透過[套件管理員 UI 選項](../tools/package-manager-ui.md)來設定，但最好是使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="5bf33-111">With NuGet 4.0+, PackageReference is preferred, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="5bf33-112">在任何情況下，您隨時都可以查看適當的檔案，以查看您專案的完整相依性清單。</span><span class="sxs-lookup"><span data-stu-id="5bf33-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="5bf33-113">最好一律檢查您要在軟體中使用之每個套件的授權。</span><span class="sxs-lookup"><span data-stu-id="5bf33-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="5bf33-114">在 nuget.org 上，您可以在每個套件的描述頁面右側找到 [授權資訊] 連結。</span><span class="sxs-lookup"><span data-stu-id="5bf33-114">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="5bf33-115">如果套件未指定授權條款，請使用套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="5bf33-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="5bf33-116">Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf33-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="5bf33-117">安裝套件時，NuGet 通常會檢查是否已經可以從其快取中使用套件。</span><span class="sxs-lookup"><span data-stu-id="5bf33-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="5bf33-118">您可以從命令列手動清除此快取，如[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="5bf33-118">You can manually clear this cache from the command line, as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="5bf33-119">NuGet 也會確保套件所支援的目標架構與您的專案相容。</span><span class="sxs-lookup"><span data-stu-id="5bf33-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="5bf33-120">如果套件未包含相容的組件，則 NuGet 會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bf33-120">If the package does not contain compatible assemblies, NuGet displays an error.</span></span> <span data-ttu-id="5bf33-121">請參閱[解決不相容的套件錯誤](dependency-resolution.md#resolving-incompatible-package-errors)。</span><span class="sxs-lookup"><span data-stu-id="5bf33-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="5bf33-122">將專案程式碼新增至來源存放庫時，您通常不會包含 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="5bf33-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="5bf33-123">如果人員稍後複製存放庫或取得專案，其中包含 Visual Studio Team Services 這類系統上組建代理程式，則必須先還原必要套件，再執行組建置：</span><span class="sxs-lookup"><span data-stu-id="5bf33-123">Those who later clone the repository or otherwise acquire the project, including build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![複製存放庫並使用還原命令來還原 NuGet 套件的流程](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="5bf33-125">[套件還原](../consume-packages/package-restore.md)使用專案檔或 `packages.config` 中的資訊來重新安裝所有相依性。</span><span class="sxs-lookup"><span data-stu-id="5bf33-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="5bf33-126">請注意，所含的程序會有些差異，如[相依性解析](../consume-packages/dependency-resolution.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="5bf33-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span> <span data-ttu-id="5bf33-127">此外，上圖中未顯示套件管理員主控台的還原命令，因為您使用的是已在 Visual Studio 內容中的主控台，這通常會自動還原套件，並提供解決方案層級的命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5bf33-127">Also, the diagram above does not show a restore command for the Package Manager Console because you're with the Console you're already in the context of Visual Studio, which typically restores packages automatically and provides the solution-level command as shown.</span></span>

<span data-ttu-id="5bf33-128">偶爾需要重新安裝已包含在專案中的套件，這也可能會重新安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="5bf33-128">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="5bf33-129">使用 `nuget reinstall` 命令或 NuGet 套件管理員主控台，就可以輕鬆做到這項作業。</span><span class="sxs-lookup"><span data-stu-id="5bf33-129">This is easy to do using the `nuget reinstall` command or the NuGet Package Manager Console.</span></span> <span data-ttu-id="5bf33-130">如需詳細資料，請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf33-130">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="5bf33-131">最後，NuGet 的行為是透過 `Nuget.Config` 檔案所驅動。</span><span class="sxs-lookup"><span data-stu-id="5bf33-131">Finally, NuGet's behavior is driven by `Nuget.Config` files.</span></span> <span data-ttu-id="5bf33-132">可以使用多個檔案來集中管理不同層級的特定設定，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)所述。</span><span class="sxs-lookup"><span data-stu-id="5bf33-132">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="5bf33-133">使用 NuGet 套件享受具生產力的程式碼！</span><span class="sxs-lookup"><span data-stu-id="5bf33-133">Enjoy your productive coding with NuGet packages!</span></span>
