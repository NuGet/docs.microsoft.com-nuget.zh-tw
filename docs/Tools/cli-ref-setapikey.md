---
title: "NuGet CLI setapikey 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe setapikey 命令參考"
keywords: "nuget setapikey 參考 setapikey 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令 (NuGet CLI)

**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有

將 API 金鑰儲存到給定的伺服器 url`NuGet.Config`使它不需要輸入後續命令。

## <a name="usage"></a>使用量

```cli
nuget setapikey <key> -Source <url> [options]
```

其中`<source>`識別伺服器並`<key>`是索引鍵或儲存的密碼。 如果`<source>`已省略，則會假設 nuget.org。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要修改的 NuGet 設定檔。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
