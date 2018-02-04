---
title: "NuGet CLI 區域變數命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 區域變數命令參考"
keywords: "nuget 區域變數的參考，[區域變數] 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>[區域變數] 命令 (NuGet CLI)

**適用於：**封裝耗用量&bullet;**支援的版本：** 3.3 +

清除或列出本機 NuGet 資源，例如 http 要求的快取、 封裝快取，而 [全機器全域 packages] 資料夾。 `locals`命令也可用來顯示這些位置的清單。 如需詳細資訊，請參閱[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md)。

## <a name="usage"></a>使用量

```cli
nuget locals <cache> [options]
```

其中`<cache>`是其中一個`all`， `http-cache`， `packages-cache`， `global-packages`，和`temp` *（3.4 +）*。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 清除 | 清除指定的快取。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 清單 | 列出指定的快取的位置或搭配使用時，所有快取位置*所有*。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget locals all -list
nuget locals http-cache -clear
```
