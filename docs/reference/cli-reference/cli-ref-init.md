---
title: NuGet CLI init 命令
description: Nuget.exe init 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327775"
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI)

**適用于:** 套件建立&bullet; **支援的版本:** 3.3+

使用階層式配置, 將所有封裝從一般資料夾複製到目的地資料夾, 如[add 命令](cli-ref-add.md)所述。 也就是說, 使用`init`相當於在資料夾中的`add`每個封裝上使用命令。

`add`如同, 目的地必須是本機資料夾或 UNC 路徑;不支援 HTTP 封裝存放庫 (例如 nuget.org 或私用伺服器)。

## <a name="usage"></a>使用量

```cli
nuget init <source> <destination> [options]
```

其中`<source>`是包含封裝的資料夾, `<destination>`而是要將封裝複製到其中的本機資料夾或 UNC 路徑名稱。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Expand | 新增每個封裝中新增至封裝來源的所有檔案;`-Expand` 與`add`命令相同。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
