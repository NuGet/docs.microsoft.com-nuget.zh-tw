---
title: 如何在 NuGet 中管理全域套件、快取、暫存資料夾
description: 如何管理全域套件安裝資料夾、套件快取，以及安裝、還原和更新套件時存在電腦上的暫存資料夾。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 354a8ec80e2ba20abe27746dec8c8aaae9b6c96c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>管理全域套件、快取和暫存資料夾

當您安裝、更新或還原套件時，NuGet 會管理專案結構之外數個資料夾中的套件和套件資訊：

| 名稱 | 描述和位置 (依使用者)|
| --- | --- |
| global&#8209;packages | *global-packages* 資料夾是 NuGet 安裝下載套件的位置。 每個套件已經完全展開至符合套件識別碼和版本號碼的子資料夾。 使用 PackageReference 格式的專案一律使用直接從這個資料夾取得的套件。 當使用 `packages.config` 時，套件會安裝到 *global-packages* 資料夾，然後複製到專案的 `packages` 資料夾。<br/><ul><li>Windows：`%userprofile%\.nuget\packages`</li><li>Mac/Linux：`~/.nuget/packages`</li><li>使用 NUGET_PACKAGES 環境變數、`globalPackagesFolder` 或 `repositoryPath` [組態設定](../reference/nuget-config-file.md#config-section) (當分別使用 PackageReference 和 `packages.config` 時)，或 `RestorePackagesPath` MSBuild 屬性 (僅限 MSBuild) 來覆寫。 環境變數的優先性高於組態設定。</li></ul> |
| http&#8209;cache | Visual Studio 套件管理員 (NuGet 3.x+) 和 `dotnet` 工具會將下載的套件複本存放在此快取中 (另存為 `.dat` 檔案)，並組織到每個套件來源的子資料夾。 套件不會展開，而且快取的到期時間為 30 分鐘。<br/><ul><li>Windows：`%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux：`~/.local/share/NuGet/v3-cache`</li><li>使用 NUGET_HTTP_CACHE_PATH 環境變數來覆寫。</li></ul> |
| temp | NuGet 在其各種作業期間存放暫存檔的資料夾。<br/><li>Windows：`%temp%\NuGetScratch`</li><li>Mac/Linux：`/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 和更早版本使用的是 *packages-cache*，而非位於 `%localappdata%\NuGet\Cache` 中的 *http-cache*。

NuGet 通常可使用快取和 *global-packages* 資料夾，以避免下載已經存在於電腦上的套件，藉此改善安裝、更新及還原作業的效能。 當使用 PackageReference 時，*global-packages* 資料夾也可避免將下載的套件保留在專案資料夾內 (以免可能會不小心新增到原始檔控制中)，並降低 NuGet 對電腦儲存體的整體影響。

NuGet 需要擷取套件時，首先會尋找 *global-packages* 資料夾。 如果套件的正確版本不存在，NuGet 便會檢查所有非 HTTP 套件來源。 如果仍然找不到套件，除非您使用 `dotnet.exe` 命令指定 `--no-cache`或使用 `nuget.exe` 命令指定 `-NoCache`，否則 NuGet 會尋找 *http-cache* 中的套件。 如果套件不在快取中，或者未使用快取，則 NuGet 會透過 HTTP 擷取套件。

如需詳細資訊，請參閱[安裝套件時會發生什麼事](ways-to-install-a-package.md#what-happens-when-a-package-is-installed)。

## <a name="viewing-folder-locations"></a>檢視資料夾位置

您可以使用 [dotnet nuget locals 命令](/dotnet/core/tools/dotnet-nuget-locals) 來檢視資料夾位置：

```cli
dotnet nuget locals all --list
```

一般輸出 (Mac/Linux；"user1" 是目前使用者名稱)：

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

若要顯示單一資料夾的位置，請使用 `http-cache`、`global-packages` 或 `temp`，不要使用 `all`。 

您也可以使用 [nuget locals 命令](../tools/cli-ref-locals.md)來檢視位置：

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

一般輸出 (Windows；"user1" 是目前使用者名稱)：

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` 使用於 NuGet 2.x 中，並在 NuGet 3.5 及更早版本中出現)。

## <a name="clearing-local-folders"></a>清除本機資料夾

如果遇到套件安裝問題，或想要確保安裝的是遠端資源庫的套件，請使用 `locals --clear` 選項 (dotnet.exe) 或 `locals -clear` (nuget.exe)，指定要清除的資料夾，或 `all` 以清除所有資料夾：

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

目前在 Visual Studio 中開啟且由專案使用的任何套件不會從 *global-packages* 資料夾清除。

在 Visual Studio 2017 中，使用 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令，然後選取 [清除所有 NuGet 快取]。 目前無法透過套件管理員主控台來管理快取。 在 Visual Studio 2015 中，請改用 CLI 命令。

![用來清除快取的 NuGet 選項命令](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>疑難排解錯誤

使用 `nuget locals` 或 `dotnet nuget locals` 時，可能會發生下列錯誤：

- 錯誤：「處理序無法存取檔案 <package> 因為其他處理序正在使用它」，或者「清除本機資源失敗：無法刪除一或多個檔案」

    其他處理序正在使用資料夾內的一或多個檔案；例如，Visual Studio 專案已開啟，其中參照 *global-packages* 資料夾中的套件。 關閉這些處理序，並再試一次。

- 錯誤：「存取路徑 <path> 遭到拒絕」或者「目錄不是空的」

    您沒有刪除此快取中檔案的權限。 如果可能，請變更資料夾權限，並再試一次。 否則，請洽詢系統管理員。

- 錯誤：「指定的路徑、檔案名稱或兩者都太長。完整的檔名必須少於 260 個字元，並且目錄名稱必須少於 248 個字元。」

    請縮短資料夾名稱，並再試一次。
