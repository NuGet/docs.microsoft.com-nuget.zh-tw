---
title: NuGet CLI 刪除命令
description: Nuget.exe delete 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548506"
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**適用於：** 封裝發行&bullet;**支援的版本：** 所有

刪除或取消列出套件從套件來源。 對於 nuget.org，delete 命令[取消列出套件](../policies/deleting-packages.md)。

## <a name="usage"></a>使用量

```cli
nuget delete <packageID> <packageVersion> [options]
```

何處`<packageID>`和`<packageVersion>`找出要刪除或取消列出確切的套件。 確切行為取決於來源。 對於本機資料夾，比方說，已經刪除套件;對於 nuget.org 的套件不會列出。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在，則會使用組態檔中所指定。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 原始程式檔 | 指定伺服器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 對於私用摘要，取代主機名稱，例如 *%hostname%/api/v3*。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
