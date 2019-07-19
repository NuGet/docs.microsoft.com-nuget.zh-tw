---
title: NuGet CLI 區域變數命令
description: Nuget.exe 區域變數命令的參考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327805"
---
# <a name="locals-command-nuget-cli"></a>locals 命令 (NuGet CLI)

**適用于:** 套件耗&bullet;用量**支援的版本:** 3.3+

清除或列出本機 NuGet 資源, 例如*HTTP*快取、*全域封裝*資料夾和 temp 資料夾。 `locals`命令也可以用來顯示這些位置的清單。 如需詳細資訊, 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。

## <a name="usage"></a>使用量

```cli
nuget locals <folder> [options]
```

其中`<folder>` `all`, 是`plugins-cache` 、 `global-packages` `temp`    、(3.5 和更早版本)、、(3.4 +) 和 (4.8 +) 其中之一。 `packages-cache` `http-cache`

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| 清除 | 清除指定的資料夾。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| 清單 | 列出指定之資料夾的位置, 或所有資料夾與*all*一起使用時的位置。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

如需其他範例, 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。
