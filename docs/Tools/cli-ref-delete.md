---
title: "NuGet CLI delete 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe delete 命令的參考"
keywords: "nuget 刪除參考，則刪除套件 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**適用於：**封裝發行&bullet;**支援的版本：**所有

刪除或 unlists 從套件來源的封裝。 為 delete 命令，nuget.org [unlists 封裝](../policies/deleting-packages.md)。

## <a name="usage"></a>使用量

```cli
nuget delete <packageID> <packageVersion> [options]
```

其中`<packageID>`和`<packageVersion>`識別要刪除或 unlist 確切的封裝。 確切行為取決於來源。 針對本機資料夾，例如，已經刪除套件;nuget.org 的封裝未列出。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫 API 金鑰。 如果不存在，則會使用組態檔中所指定。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 原始程式檔 | 指定伺服器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 私用的摘要，替代的主機名稱，例如*%hostname%/api/v3*。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
