---
title: "使用 NuGet 套件的概觀和工作流程 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "在專案中使用 NuGet 套件之程序的概觀，以及程序之其他特定部分的連結。"
keywords: "NuGet 套件使用, NuGet 使用概觀, NuGet 使用工作流程, 套件使用工作流程, 套件使用概觀"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="6ac7d-104">套件使用工作流程</span><span class="sxs-lookup"><span data-stu-id="6ac7d-104">Package consumption workflow</span></span>

<span data-ttu-id="6ac7d-105">在 nuget.org 與您組織可建立的私人套件庫之間，您可以找到數以萬計的高可用套件，以在您的應用程式和服務中使用。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="6ac7d-106">但是，不論來源為何，使用套件都會遵循相同的一般工作流程，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-106">But regardless of the source, consuming a package follows the same general workflow as shown below.</span></span> <span data-ttu-id="6ac7d-107">如需詳細資料，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)和[使用套件快速入門](../quickstart/use-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-107">For details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and the [Use a Package quickstart](../quickstart/use-a-package.md).</span></span>

![移至套件來源、尋找套件、將它安裝至專案，然後新增 using 陳述式和套件 API 呼叫的流程](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="6ac7d-109">\* _但從命令列使用 `nuget install` 除外，在此情況下，需要手動編輯組態檔。請參閱 [install 命令參考](../tools/cli-ref-install.md)。_</span><span class="sxs-lookup"><span data-stu-id="6ac7d-109">\* _Except with `nuget install` from the command-line, in which case it's necessary to edit the configuration files by hand. See the [install command reference](../tools/cli-ref-install.md)._</span></span>

<span data-ttu-id="6ac7d-110">NuGet 會記住每個已安裝套件的身分識別和版本號碼，並將其記錄在 `packages.config`、專案檔，或專案根目錄中的 `project.json` 檔案 (視專案類型和 NuGet 版本而定)。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-110">NuGet remembers the identity and version number of each installed package, recording it in either `packages.config`, the project file, or a `project.json` file in your project root, depending on project type and your version of NuGet.</span></span> <span data-ttu-id="6ac7d-111">使用 NuGet 4.0+，[將相依性儲存至專案檔](../consume-packages/package-references-in-project-files.md)是預設值 (但目標設為 Windows 10 RS1 的 UWP 專案除外)。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-111">With NuGet 4.0+, [storing dependencies in the project file](../consume-packages/package-references-in-project-files.md) is the default (except for UWP projects targeting Windows 10 RS1).</span></span> <span data-ttu-id="6ac7d-112">在任何情況下，您隨時都可以查看適當的檔案，以查看您專案的完整相依性清單。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="6ac7d-113">最好一律檢查您要在軟體中使用之每個套件的授權。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="6ac7d-114">在 nuget.org 上，您可以在每個套件的描述頁面右側找到 [授權資訊] 連結。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-114">On nuget.org, you'll find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="6ac7d-115">如果套件未指定授權條款，請使用套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="6ac7d-116">Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="6ac7d-117">安裝套件時，NuGet 通常會檢查是否已經可以從其快取中使用套件。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="6ac7d-118">您可以從命令列手動清除此快取，如[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md)中述。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-118">You can manually clear this cache from the command line, as described on [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

<span data-ttu-id="6ac7d-119">NuGet 也會確保套件所支援的目標架構與您的專案相容。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="6ac7d-120">如果套件未包含相容的組件，則 NuGet 會提供錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-120">If the package does not contain compatible assemblies, NuGet will give you an error message.</span></span> <span data-ttu-id="6ac7d-121">請參閱[解決不相容的套件錯誤](dependency-resolution.md#resolving-incompatible-package-errors)。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="6ac7d-122">將專案程式碼新增至來源存放庫時，您通常不會包含 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="6ac7d-123">如果人員稍後複製包含 Visual Studio Team Services 這類系統上組建代理程式的存放庫，則必須先還原必要套件，再執行組建置：</span><span class="sxs-lookup"><span data-stu-id="6ac7d-123">Those who later clone the repository, which includes build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![複製存放庫並使用還原命令來還原 NuGet 套件的流程](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="6ac7d-125">[套件還原](../consume-packages/package-restore.md)使用 `packages.config`、`project.json` 專案檔中的資訊來重新安裝所有相依性。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file, `packages.config`, `project.json` to reinstall all dependencies.</span></span> <span data-ttu-id="6ac7d-126">請注意，所含的程序會有些差異，如[相依性解析](../consume-packages/dependency-resolution.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>

<span data-ttu-id="6ac7d-127">偶爾需要重新安裝已包含在專案中的套件，這也可能會重新安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-127">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="6ac7d-128">透過 NuGet 命令列或 NuGet 套件管理員主控台使用 `reinstall`，就可以輕鬆做到這項作業。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-128">This is easy to do using the `reinstall` command via the NuGet command line or the NuGet Package Manager Console.</span></span> <span data-ttu-id="6ac7d-129">如需詳細資料，請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-129">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="6ac7d-130">最後，NuGet 的行為是透過 `Nuget.Config` 組態檔所驅動。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-130">Finally, NuGet's behavior is driven by `Nuget.Config` configuration files.</span></span> <span data-ttu-id="6ac7d-131">可以使用多個檔案來集中管理不同層級的特定設定，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)所述。</span><span class="sxs-lookup"><span data-stu-id="6ac7d-131">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6ac7d-132">使用 NuGet 套件享受具生產力的程式碼！</span><span class="sxs-lookup"><span data-stu-id="6ac7d-132">Enjoy your productive coding with NuGet packages!</span></span>
