---
title: NuGet CLI 鏡像命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 鏡像命令參考
keywords: nuget 鏡像參考，鏡像命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a>鏡像命令 (NuGet CLI)

**適用於：**封裝發行&bullet;**支援的版本：** 3.2 + 中已被取代

反映封裝及其相依性從指定的來源儲存機制的目標儲存機制。

> [!NOTE]
> 若要啟用此命令的 NuGet 版本 3.2 之前，請移至[ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)、 選取最新穩定版本，請下載`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`您的本機磁碟和重新命名`Nuget-Signed.exe`至`nuget.exe`。

## <a name="usage"></a>使用量

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>`是要建立鏡像的封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要鏡像的封裝。

`<listUrlTarget>`指定來源儲存機制和`<publishUrlTarget>`指定目標存放庫。

如果您的目標儲存機制位於`https://machine/repo`執行[NuGet.Server](../hosting-packages/nuget-server.md)，清單並推送 url 就是`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分別。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫 API 金鑰。 如果不存在，指定在組態檔中會使用 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。 |
| 說明 | 顯示說明命令的資訊。 |
| 無快取記憶體 | NuGet 可防止使用快取的封裝。 請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| Noop | 記錄項目會完成，但不會執行動作。假設推送作業成功。 |
| 發行前版本 | 鏡像作業中包含套件發行前版本。 |
| 原始程式檔 | 要鏡像的封裝來源清單。 如果未不指定任何來源中, 定義的組態檔 （請參閱上述 ApiKey） 使用，如果未指定任何 nuget.org 預設值。 |
| 等候逾時 | 指定在逾時，以秒為單位，可用於推入到伺服器。 預設值是 300 秒 （5 分鐘）。 |
| 版本 | 要安裝之封裝的版本。 如果未指定，則會鏡像的最新版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
