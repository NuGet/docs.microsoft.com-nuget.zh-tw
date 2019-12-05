---
title: 如何在 NuGet 中管理全域套件、快取、暫存資料夾
description: 如何管理全域套件安裝資料夾、套件快取，以及安裝、還原和更新套件時存在電腦上的暫存資料夾。
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825202"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="0f597-103">管理全域套件、快取和暫存資料夾</span><span class="sxs-lookup"><span data-stu-id="0f597-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="0f597-104">當您安裝、更新或還原套件時，NuGet 會管理專案結構之外數個資料夾中的套件和套件資訊：</span><span class="sxs-lookup"><span data-stu-id="0f597-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="0f597-105">Name</span><span class="sxs-lookup"><span data-stu-id="0f597-105">Name</span></span> | <span data-ttu-id="0f597-106">描述和位置 (依使用者)</span><span class="sxs-lookup"><span data-stu-id="0f597-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="0f597-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="0f597-107">global&#8209;packages</span></span> | <span data-ttu-id="0f597-108">*global-packages* 資料夾是 NuGet 安裝下載套件的位置。</span><span class="sxs-lookup"><span data-stu-id="0f597-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="0f597-109">每個套件已經完全展開至符合套件識別碼和版本號碼的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f597-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="0f597-110">使用 [PackageReference](package-references-in-project-files.md) 格式的專案一律使用直接從此資料夾取得的套件。</span><span class="sxs-lookup"><span data-stu-id="0f597-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="0f597-111">當使用 [packages.config](../reference/packages-config.md) 時，套件會安裝到 *global-packages* 資料夾，然後複製到專案的 `packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f597-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="0f597-112">Windows：`%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="0f597-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="0f597-113">Mac/Linux：`~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="0f597-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="0f597-114">使用 NUGET_PACKAGES 環境變數、`globalPackagesFolder` 或 `repositoryPath` [組態設定](../reference/nuget-config-file.md#config-section) (當分別使用 PackageReference 和 `packages.config` 時)，或 `RestorePackagesPath` MSBuild 屬性 (僅限 MSBuild) 來覆寫。</span><span class="sxs-lookup"><span data-stu-id="0f597-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="0f597-115">環境變數的優先性高於組態設定。</span><span class="sxs-lookup"><span data-stu-id="0f597-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="0f597-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="0f597-116">http&#8209;cache</span></span> | <span data-ttu-id="0f597-117">Visual Studio 套件管理員 (NuGet 3.x+) 和 `dotnet` 工具會將下載的套件複本存放在此快取中 (另存為 `.dat` 檔案)，並組織到每個套件來源的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f597-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="0f597-118">套件不會展開，而且快取的到期時間為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="0f597-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="0f597-119">Windows：`%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="0f597-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="0f597-120">Mac/Linux：`~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="0f597-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="0f597-121">使用 NUGET_HTTP_CACHE_PATH 環境變數來覆寫。</span><span class="sxs-lookup"><span data-stu-id="0f597-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="0f597-122">temp</span><span class="sxs-lookup"><span data-stu-id="0f597-122">temp</span></span> | <span data-ttu-id="0f597-123">NuGet 在其各種作業期間存放暫存檔的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f597-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="0f597-124">Windows：`%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="0f597-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="0f597-125">Mac/Linux：`/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="0f597-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="0f597-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="0f597-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="0f597-127">NuGet 在此資料夾中儲存來自作業宣告要求的結果。</span><span class="sxs-lookup"><span data-stu-id="0f597-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="0f597-128">Windows：`%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="0f597-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="0f597-129">Mac/Linux：`~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="0f597-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="0f597-130">使用 NUGET_PLUGINS_CACHE_PATH 環境變數來覆寫。</span><span class="sxs-lookup"><span data-stu-id="0f597-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="0f597-131">NuGet 3.5 和更早版本使用的是 *packages-cache*，而非位於 `%localappdata%\NuGet\Cache` 中的 *http-cache*。</span><span class="sxs-lookup"><span data-stu-id="0f597-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="0f597-132">NuGet 通常可使用快取和 *global-packages* 資料夾，以避免下載已經存在於電腦上的套件，藉此改善安裝、更新及還原作業的效能。</span><span class="sxs-lookup"><span data-stu-id="0f597-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="0f597-133">當使用 PackageReference 時，*global-packages* 資料夾也可避免將下載的套件保留在專案資料夾內 (以免可能會不小心新增到原始檔控制中)，並降低 NuGet 對電腦儲存體的整體影響。</span><span class="sxs-lookup"><span data-stu-id="0f597-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="0f597-134">NuGet 需要擷取套件時，首先會尋找 *global-packages* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f597-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="0f597-135">如果套件的正確版本不存在，NuGet 便會檢查所有非 HTTP 套件來源。</span><span class="sxs-lookup"><span data-stu-id="0f597-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="0f597-136">如果仍然找不到套件，除非您使用 `dotnet.exe` 命令指定 `--no-cache`或使用 `nuget.exe` 命令指定 `-NoCache`，否則 NuGet 會尋找 *http-cache* 中的套件。</span><span class="sxs-lookup"><span data-stu-id="0f597-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="0f597-137">如果套件不在快取中，或者未使用快取，則 NuGet 會透過 HTTP 擷取套件。</span><span class="sxs-lookup"><span data-stu-id="0f597-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="0f597-138">如需詳細資訊，請參閱[安裝套件後會發生什麼事](../concepts/package-installation-process.md)。</span><span class="sxs-lookup"><span data-stu-id="0f597-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="0f597-139">檢視資料夾位置</span><span class="sxs-lookup"><span data-stu-id="0f597-139">Viewing folder locations</span></span>

<span data-ttu-id="0f597-140">您可以使用 [nuget locals 命令](../reference/cli-reference/cli-ref-locals.md)來檢視位置：</span><span class="sxs-lookup"><span data-stu-id="0f597-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="0f597-141">一般輸出 (Windows；"user1" 是目前使用者名稱)：</span><span class="sxs-lookup"><span data-stu-id="0f597-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="0f597-142">(`package-cache` 使用於 NuGet 2.x 中，並在 NuGet 3.5 及更早版本中出現)。</span><span class="sxs-lookup"><span data-stu-id="0f597-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="0f597-143">您可以使用 [dotnet nuget locals 命令](/dotnet/core/tools/dotnet-nuget-locals)來檢視資料夾位置：</span><span class="sxs-lookup"><span data-stu-id="0f597-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="0f597-144">一般輸出 (Mac/Linux；"user1" 是目前使用者名稱)：</span><span class="sxs-lookup"><span data-stu-id="0f597-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="0f597-145">若要顯示單一資料夾的位置，請使用 `http-cache`、`global-packages`、`temp` 或 `plugins-cache`，不要使用 `all`。</span><span class="sxs-lookup"><span data-stu-id="0f597-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="0f597-146">清除本機資料夾</span><span class="sxs-lookup"><span data-stu-id="0f597-146">Clearing local folders</span></span>

<span data-ttu-id="0f597-147">如果遇到套件安裝問題，或想要確保安裝的是遠端資源庫的套件，請使用 `locals --clear` 選項 (dotnet.exe) 或 `locals -clear` (nuget.exe)，指定要清除的資料夾，或 `all` 以清除所有資料夾：</span><span class="sxs-lookup"><span data-stu-id="0f597-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="0f597-148">目前在 Visual Studio 中開啟且由專案使用的任何套件不會從 *global-packages* 資料夾清除。</span><span class="sxs-lookup"><span data-stu-id="0f597-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="0f597-149">在 Visual Studio 2017 中啟動，使用 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令，然後選取 [清除所有 NuGet 快取]。</span><span class="sxs-lookup"><span data-stu-id="0f597-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="0f597-150">目前無法透過套件管理員主控台來管理快取。</span><span class="sxs-lookup"><span data-stu-id="0f597-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="0f597-151">在 Visual Studio 2015 中，請改用 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="0f597-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![用來清除快取的 NuGet 選項命令](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="0f597-153">疑難排解錯誤</span><span class="sxs-lookup"><span data-stu-id="0f597-153">Troubleshooting errors</span></span>

<span data-ttu-id="0f597-154">使用 `nuget locals` 或 `dotnet nuget locals` 時，可能會發生下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0f597-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="0f597-155">錯誤：「處理序無法存取檔案 <package> 因為其他處理序正在使用它」，或者「清除本機資源失敗：無法刪除一或多個檔案」</span><span class="sxs-lookup"><span data-stu-id="0f597-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="0f597-156">其他處理序正在使用資料夾內的一或多個檔案；例如，Visual Studio 專案已開啟，其中參照 *global-packages* 資料夾中的套件。</span><span class="sxs-lookup"><span data-stu-id="0f597-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="0f597-157">關閉這些處理序，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="0f597-157">Close those processes and try again.</span></span>

- <span data-ttu-id="0f597-158">錯誤：「存取路徑 <path> 遭到拒絕」或者「目錄不是空的」</span><span class="sxs-lookup"><span data-stu-id="0f597-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="0f597-159">您沒有刪除此快取中檔案的權限。</span><span class="sxs-lookup"><span data-stu-id="0f597-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="0f597-160">如果可能，請變更資料夾權限，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="0f597-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="0f597-161">否則，請洽詢系統管理員。</span><span class="sxs-lookup"><span data-stu-id="0f597-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="0f597-162">*錯誤：指定的路徑、檔案名或兩者都太長。完整檔案名必須小於260個字元，且目錄名稱必須小於248個字元。*</span><span class="sxs-lookup"><span data-stu-id="0f597-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="0f597-163">請縮短資料夾名稱，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="0f597-163">Shorten the folder names and try again.</span></span>
