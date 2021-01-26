---
title: 安裝套件時會發生什麼事？
description: 套件安裝程序的詳細資訊
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 2a16c1cfe1ada0d1a78cefcdb2bdc69b9c6e84cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775091"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a><span data-ttu-id="83e5e-103">安裝 NuGet 套件時會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="83e5e-103">What happens when a NuGet package is installed?</span></span>

<span data-ttu-id="83e5e-104">簡單地說，不同的 NuGet 工具通常會在專案檔或 `packages.config` 中建立套件的參考，然後執行套件還原，從而有效地安裝套件。</span><span class="sxs-lookup"><span data-stu-id="83e5e-104">Simply said, the different NuGet tools typically create a reference to a package in the project file or `packages.config`, then perform a package restore, which effectively installs the package.</span></span> <span data-ttu-id="83e5e-105">例外狀況是 `nuget install`，它只會將套件展開到 `packages` 資料夾，且不會修改其他任何檔案。</span><span class="sxs-lookup"><span data-stu-id="83e5e-105">The exception is `nuget install`, which only expands the package into a `packages` folder and does not modify any other files.</span></span>

<span data-ttu-id="83e5e-106">一般程序如下：</span><span class="sxs-lookup"><span data-stu-id="83e5e-106">The general process is as follows:</span></span>

1. <span data-ttu-id="83e5e-107">(除 `nuget.exe` 外的所有工具) 將套件識別碼和版本記錄到專案檔或 `packages.config` 中。</span><span class="sxs-lookup"><span data-stu-id="83e5e-107">(All tools except `nuget.exe`) Record the package identifier and version into the project file or `packages.config`.</span></span>

   <span data-ttu-id="83e5e-108">如果安裝工具是 Visual Studio 或 dotnet CLI，則工具會先嘗試安裝套件。</span><span class="sxs-lookup"><span data-stu-id="83e5e-108">If the installation tool is Visual Studio or the dotnet CLI, the tool first attempts to install the package.</span></span> <span data-ttu-id="83e5e-109">如果不相容，則套件不會新增至專案檔或 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="83e5e-109">If it's incompatible, the package is not added to the project file or `packages.config`.</span></span>

2. <span data-ttu-id="83e5e-110">取得套件：</span><span class="sxs-lookup"><span data-stu-id="83e5e-110">Acquire the package:</span></span>
   - <span data-ttu-id="83e5e-111">檢查套件 (依據確切的識別碼和版本號碼) 是否已安裝在 *global-packages* 資料夾中，如 [管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="83e5e-111">Check if the package (by exact identifer and version number) is already installed in the *global-packages* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

   - <span data-ttu-id="83e5e-112">如果套件不在 [ *全域封裝* ] 資料夾中，請嘗試從 [設定檔](../consume-packages/Configuring-NuGet-Behavior.md)中所列的來源抓取。</span><span class="sxs-lookup"><span data-stu-id="83e5e-112">If the package is not in the *global-packages* folder, attempt to retrieve it from the sources listed in the [configuration files](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> <span data-ttu-id="83e5e-113">針對線上來源，除非已使用 `nuget.exe` 命令指定 `-NoCache`，或已使用 `dotnet restore` 指定 `--no-cache`，否則會先嘗試從 HTTP 快取擷取套件。</span><span class="sxs-lookup"><span data-stu-id="83e5e-113">For online sources, attempt first to retrieve the package from the HTTP cache unless `-NoCache` is specified with `nuget.exe` commands or `--no-cache` is specified with `dotnet restore`.</span></span> <span data-ttu-id="83e5e-114"> (Visual Studio，且 `dotnet add package` 一律使用快取。 ) 如果從快取使用封裝，輸出中就會出現 "cache"。</span><span class="sxs-lookup"><span data-stu-id="83e5e-114">(Visual Studio and `dotnet add package` always use the cache.) If a package is used from the cache, "CACHE" appears in the output.</span></span> <span data-ttu-id="83e5e-115">快取的到期時間為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="83e5e-115">The cache has an expiration time of 30 minutes.</span></span>

   - <span data-ttu-id="83e5e-116">如果封裝是使用 [浮動版本](../consume-packages/Package-References-in-Project-Files.md#floating-versions)指定，或沒有最低版本，則 NuGet *會* 聯繫所有來源，以找出最符合的結果。</span><span class="sxs-lookup"><span data-stu-id="83e5e-116">If the package has been specified using a [floating version](../consume-packages/Package-References-in-Project-Files.md#floating-versions), or without a minimum version, NuGet *will* contact all sources to figure out the best match.</span></span>
   <span data-ttu-id="83e5e-117">範例： `1.*` ， `(, 2.0.0]` 。</span><span class="sxs-lookup"><span data-stu-id="83e5e-117">Example: `1.*`, `(, 2.0.0]`.</span></span>

   - <span data-ttu-id="83e5e-118">如果套件不在 HTTP 快取中，則會嘗試從組態中所列的來源下載套件。</span><span class="sxs-lookup"><span data-stu-id="83e5e-118">If the package is not in the HTTP cache, attempt to download it from the sources listed in the configuration.</span></span> <span data-ttu-id="83e5e-119">如果已下載套件，輸出中會出現 "GET" 和 "OK"。</span><span class="sxs-lookup"><span data-stu-id="83e5e-119">If a package is downloaded, "GET" and "OK" appear in the output.</span></span> <span data-ttu-id="83e5e-120">NuGet 會記錄正常詳細程度的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="83e5e-120">NuGet logs http traffic on normal verbosity.</span></span>

   - <span data-ttu-id="83e5e-121">如果無法從任何來源成功取得套件，此時安裝會失敗，並出現錯誤，例如 [NU1103](../reference/errors-and-warnings/NU1103.md)。</span><span class="sxs-lookup"><span data-stu-id="83e5e-121">If the package cannot be successfully acquired from any sources, installation fails at this point with an error such as [NU1103](../reference/errors-and-warnings/NU1103.md).</span></span> <span data-ttu-id="83e5e-122">請注意，來自 `nuget.exe` 命令的錯誤只會顯示所檢查的最後一個來源，但表示無法從任何來源使用套件。</span><span class="sxs-lookup"><span data-stu-id="83e5e-122">Note that errors from `nuget.exe` commands show only the last source checked, but implies that the package wasn't available from any source.</span></span>

   <span data-ttu-id="83e5e-123">取得套件時，可能套用 NuGet 組態中的來源順序為：</span><span class="sxs-lookup"><span data-stu-id="83e5e-123">When acquiring the package, the order of sources in the NuGet configuration may apply:</span></span>

   - <span data-ttu-id="83e5e-124">NuGet 會先檢查來源本機資料夾和網路共用，然後才檢查 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="83e5e-124">NuGet checks sources local folder and network shares before checking HTTP sources.</span></span>

3. <span data-ttu-id="83e5e-125">將套件複本和其他資訊儲存在 *http-cache* 資料夾中，如 [管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="83e5e-125">Save a copy of the package and other information in the *http-cache* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

4. <span data-ttu-id="83e5e-126">如果已下載，則將套件安裝到每個使用者的 *global-packages* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="83e5e-126">If downloaded, install the package into the per-user *global-packages* folder.</span></span> <span data-ttu-id="83e5e-127">NuGet 會針對每個套件識別碼建立子資料夾，然後針對每個已安裝的套件版本建立子資料夾。</span><span class="sxs-lookup"><span data-stu-id="83e5e-127">NuGet creates a subfolder for each package identifier, then creates subfolders for each installed version of the package.</span></span>

5. <span data-ttu-id="83e5e-128">NuGet 會視需要安裝套件相依性。</span><span class="sxs-lookup"><span data-stu-id="83e5e-128">NuGet installs package dependencies as required.</span></span> <span data-ttu-id="83e5e-129">此程序可能更新流程中的套件版本，如[相依性解析](../concepts/dependency-resolution.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="83e5e-129">This process might update package versions in the process, as described in [Dependency Resolution](../concepts/dependency-resolution.md).</span></span>

6. <span data-ttu-id="83e5e-130">更新其他專案檔和資料夾：</span><span class="sxs-lookup"><span data-stu-id="83e5e-130">Update other project files and folders:</span></span>

    - <span data-ttu-id="83e5e-131">針對使用 PackageReference 的專案，更新儲存在 `obj/project.assets.json` 中的套件相依性關係圖。</span><span class="sxs-lookup"><span data-stu-id="83e5e-131">For projects using PackageReference, update the package dependency graph stored in `obj/project.assets.json`.</span></span> <span data-ttu-id="83e5e-132">套件內容本身不會複製到任何專案資料夾中。</span><span class="sxs-lookup"><span data-stu-id="83e5e-132">Package contents themselves are not copied into any project folder.</span></span>
    - <span data-ttu-id="83e5e-133">如果套件使用[來源和組態檔轉換](../create-packages/source-and-config-file-transformations.md)，則更新 `app.config` 和/或 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="83e5e-133">Update `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>

7. <span data-ttu-id="83e5e-134">(僅限 Visual Studio) 在 Visual Studio 視窗中顯示套件的讀我檔案 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="83e5e-134">(Visual Studio only) Display the package's readme file, if available, in a Visual Studio window.</span></span>

<span data-ttu-id="83e5e-135">使用 NuGet 套件享受具生產力的程式碼！</span><span class="sxs-lookup"><span data-stu-id="83e5e-135">Enjoy your productive coding with NuGet packages!</span></span>
