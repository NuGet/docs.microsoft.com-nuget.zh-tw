---
title: NuGet CLI 鏡像命令
description: Nuget.exe 鏡像命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550202"
---
# <a name="mirror-command-nuget-cli"></a>mirror 命令 (NuGet CLI)

**適用於：** 封裝發行&bullet;**支援的版本：** 3.2 + 中已被取代

鏡像處理封裝和目標存放庫從指定的來源存放庫及其相依性。

> [!NOTE]
> 若要啟用此命令的 NuGet 版本 3.2 之前，請移至[ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)、 選取最新穩定版本，請下載`NuGet.ServerExtensions.dll`並`Nuget-Signed.exe`您的本機磁碟和重新命名`Nuget-Signed.exe`至`nuget.exe`。

## <a name="usage"></a>使用量

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

何處`<packageID>`是要建立鏡像的套件或`<configFilePath>`識別`packages.config`檔案，其中列出要鏡像的封裝。

`<listUrlTarget>`指定的來源存放庫和`<publishUrlTarget>`指定目標存放庫。

如果您的目標存放庫位於`https://machine/repo`執行[NuGet.Server](../hosting-packages/nuget-server.md)，清單和推送 url 會`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分別。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在，組態檔中指定會使用一個 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。 |
| 說明 | 顯示說明命令的資訊。 |
| 無快取記憶體 | 禁止 NuGet 使用的快取的套件。 請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| Noop | 記錄項目會完成，但不會執行動作;假設推送作業成功。 |
| 發行前版本 | 包含發行前版本套件中的鏡像作業。 |
| 原始程式檔 | 鏡像的套件來源清單。 如果未不指定任何來源中, 定義的組態檔 （請參閱上述的 ApiKey） 使用，如果未指定，將預設為 nuget.org。 |
| 等候逾時 | 指定的逾時 （秒），推送至伺服器。 預設值為 300 秒 （5 分鐘）。 |
| 版本 | 要安裝的套件版本。 如果未指定，則被鏡像的最新版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
