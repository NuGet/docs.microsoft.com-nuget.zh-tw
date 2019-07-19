---
title: NuGet CLI 鏡像命令
description: Nuget.exe 鏡像命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327665"
---
# <a name="mirror-command-nuget-cli"></a>mirror 命令 (NuGet CLI)

**適用于:** 套件發行&bullet; **支援的版本:** 3.2 + 中已淘汰

將封裝及其相依性從指定的來源存放庫鏡像到目標儲存機制。

> [!NOTE]
> 若要在3.2 之前的 NuGet 版本啟用此命令, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)請移至, 選取最新的`NuGet.ServerExtensions.dll` 穩定`Nuget-Signed.exe` 版本, 將和下載到`Nuget-Signed.exe` 您`nuget.exe` 的本機磁片, 並將重新命名為。

## <a name="usage"></a>使用量

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>`是要鏡像的封裝, 或`<configFilePath>`識別`packages.config`列出要鏡像之封裝的檔案。

會指定來源存放庫, 並`<publishUrlTarget>`指定目標存放庫。 `<listUrlTarget>`

如果您的目標存放庫`https://machine/repo`是在執行[nuget.exe](../../hosting-packages/nuget-server.md)的上, 則清單和推播 url 會`https://machine/repo/nuget`分別`https://machine/repo/api/v2/package`是和。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在, 則會使用設定檔中指定的檔案 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。 |
| Help | 顯示命令的說明資訊。 |
| NoCache | 防止 NuGet 使用快取的套件。 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| Noop | 記錄哪些作業會完成, 但不會執行動作;假設推送作業成功。 |
| 版 | 包括鏡像作業中的發行前版本套件。 |
| Source | 要鏡像的封裝來源清單。 如果未指定任何來源, 則會使用設定檔中所定義的來源 (如上面的 ApiKey), 預設為 nuget.org (如果未指定)。 |
| 逾時 | 指定推送至伺服器的超時時間 (以秒為單位)。 預設值為300秒 (5 分鐘)。 |
| 版本 | 要安裝的封裝版本。 如果未指定, 則會鏡像最新版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
