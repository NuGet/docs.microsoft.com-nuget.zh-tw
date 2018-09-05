---
title: NuGet CLI init 命令
description: Nuget.exe init 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551406"
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI)

**適用於：** 封裝建立&bullet;**支援的版本：** 3.3 +

所有的封裝複製到如所述，使用以階層配置的目的地資料夾的一般資料夾[將命令加入](cli-ref-add.md)。 也就使用`init`相當於使用`add`命令的資料夾中的每個套件。

如同`add`，目的地必須是本機資料夾或 UNC 路徑;不支援 HTTP 套件存放庫，例如 nuget.org 或私用的伺服器。

## <a name="usage"></a>使用量

```cli
nuget init <source> <destination> [options]
```

何處`<source>`是包含封裝的資料夾和`<destination>`是本機資料夾或封裝複製到其中的 UNC 路徑名稱。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| Expand | 將所有檔案新增至套件來源; 每個封裝中與相同`-Expand`與`add`命令。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
