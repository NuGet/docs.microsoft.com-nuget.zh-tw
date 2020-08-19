---
title: NuGet CLI 鏡像命令
description: nuget.exe 鏡像命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622963"
---
# <a name="mirror-command-nuget-cli"></a>NuGet CLI (的鏡像命令) 

**適用于：** 套件發行 &bullet; **支援的版本：** 已在 3.2 + 中淘汰

將封裝及其相依性從指定的來源存放庫鏡像至目標存放庫。

> [!NOTE]
> 先前在 NuGet 2.x (中支援這個命令 NuGet.ServerExtensions.dll 和 NuGet-Signed.exe 將無法再重新命名 NuGet-Signed.exe 至 nuget.exe) 。 若要使用類似的命令，請嘗試 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。

## <a name="usage"></a>使用方式

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中 `<packageID>` 是要鏡像的封裝，或 `<configFilePath>` 識別 `packages.config` 列出要鏡像之套件的檔案。

會 `<listUrlTarget>` 指定來源存放庫，並 `<publishUrlTarget>` 指定目標存放庫。

如果您的目標儲存機制是在執行 `https://machine/repo` [nuget.exe](../../hosting-packages/nuget-server.md)的電腦上，則清單和推送 url 會 `https://machine/repo/nuget` 分別為和 `https://machine/repo/api/v2/package` 。

## <a name="options"></a>選項。

- **`-ApiKey`**

  目標儲存機制的 API 金鑰。 如果不存在，則會使用設定檔中指定的 (`%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) # A5。

- **`-Help`**

  顯示命令的說明資訊。

- **`-NoCache`**

  防止 NuGet 使用快取的封裝。 請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。

- **`-Noop`**

  記錄會執行的動作，但不會執行動作。假設推送作業成功。

- **`-PreRelease`**

  在鏡像作業中包含發行前版本套件。

- **`-Source`**

  要鏡像的封裝來源清單。 如果未指定任何來源，則會使用在設定檔中定義的 ApiKey， (查看上述) ，如果未指定，則預設為 nuget.org。

- **`-Timeout`**

  指定推送至伺服器的超時時間（以秒為單位）。 預設值是 300 秒 (5 分鐘)。

- **`-Version`**

  要安裝之套件的版本。 如果未指定，則會鏡像最新版本。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
