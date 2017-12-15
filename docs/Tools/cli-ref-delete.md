---
title: "NuGet CLI delete 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete 命令的參考"
keywords: "nuget 刪除參考，則刪除套件 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**適用於：**封裝發行&bullet;**支援的版本：**所有

刪除或 unlists 從套件來源的封裝。 為 delete 命令，nuget.org [unlists 封裝](../policies/Deleting-Packages.md)。

## <a name="usage"></a>使用方式

```
nuget delete <packageID> <packageVersion> [options]
```

其中`<packageID>`和`<packageVersion>`識別要刪除或 unlist 確切的封裝。 確切行為取決於來源。 針對本機資料夾，例如，已經刪除套件;nuget.org 的封裝未列出。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| apiKey | 目標存放庫 API 金鑰。 如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。 |
| ConfigFile | *（2.5 +)* NuGet 組態檔來套用。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 來源 | 指定伺服器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 私用的摘要，替代的主機名稱，例如*%hostname%/api/v3*。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
