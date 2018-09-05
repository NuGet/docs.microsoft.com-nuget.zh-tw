---
title: NuGet CLI locals 命令
description: Nuget.exe locals 命令參考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545024"
---
# <a name="locals-command-nuget-cli"></a>locals 命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 3.3 +

清除或列出本機 NuGet 資源，例如*http 快取*，*全域套件*資料夾，然後 [temp] 資料夾。 `locals`命令也可用來顯示這些位置的清單。 如需詳細資訊，請參閱 <<c0> [ 管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>使用量

```cli
nuget locals <folder> [options]
```

何處`<folder>`是其中一個`all`， `http-cache`， `packages-cache` *（3.5 和更早版本）*， `global-packages`， `temp` *（3.4 +）*，以及`plugins-cache` *（4.8 +）*。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 清除 | 清除指定的資料夾。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| 清單 | 列出指定的資料夾的位置或搭配使用時的所有資料夾的位置*所有*。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

如需其他範例，請參閱 <<c0> [ 管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。
