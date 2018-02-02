---
title: "NuGet CLI init 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe init 命令參考"
keywords: "nuget init 參考，初始化命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="init-command-nuget-cli"></a>初始化命令 (NuGet CLI)

**適用於：**封裝建立&bullet;**支援的版本：** 3.3 +

將所有封裝從一般資料夾都複製到目的資料夾，如所述，使用以階層配置[將命令加入](cli-ref-add.md)。 也就使用`init`相當於使用`add`命令上的資料夾中的每個封裝。

如同`add`，目的地必須是本機資料夾或 UNC 路徑。不支援 HTTP 封裝儲存機制，例如 nuget.org 或私用的伺服器。

## <a name="usage"></a>使用量

```cli
nuget init <source> <destination> [options]
```

其中`<source>`是包含封裝的資料夾和`<destination>`是本機資料夾或封裝複製到其中的 UNC 路徑名稱。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| Expand | 將所有檔案新增至套件來源; 每個封裝中與相同`-Expand`與`add`命令。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
