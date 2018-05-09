---
title: NuGet CLI [區域變數] 命令
description: Nuget.exe 區域變數命令參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>[區域變數] 命令 (NuGet CLI)

**適用於：**封裝耗用量&bullet;**支援的版本：** 3.3 +

清除或列出本機 NuGet 資源，例如*http 快取*，*全域封裝*資料夾以及暫存資料夾。 `locals`命令也可用來顯示這些位置的清單。 如需詳細資訊，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>使用量

```cli
nuget locals <folder> [options]
```

其中`<folder>`是其中一個`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 清除 | 清除指定的資料夾。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 清單 | 列出指定的資料夾位置或搭配使用時的所有資料夾的位置*所有*。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

如需其他範例，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。
