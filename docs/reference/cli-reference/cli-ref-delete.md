---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327835"
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**適用于:** 套件發行&bullet; **支援的版本:** 全部

從封裝來源刪除或取消列出封裝。 針對 nuget.org, delete 命令會[取消列出套件](../../nuget-org/policies/deleting-packages.md)。

## <a name="usage"></a>使用量

```cli
nuget delete <packageID> <packageVersion> [options]
```

其中`<packageID>` , `<packageVersion>`和會識別要刪除或取消列出的確切封裝。 確切的行為視來源而定。 例如, 針對本機資料夾, 會刪除封裝;針對 nuget.org, 封裝為未列出。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在, 則會使用設定檔中指定的檔案。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Source | 指定伺服器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 若是私人摘要, 請以主機名稱取代, 例如 *% hostname%/api/v3*。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
