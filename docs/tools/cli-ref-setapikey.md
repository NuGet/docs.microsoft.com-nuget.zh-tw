---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549216"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令 (NuGet CLI)

**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有

將 API 金鑰儲存到指定的伺服器 url `NuGet.Config` ，讓它不需要輸入後續命令。

## <a name="usage"></a>使用量

```cli
nuget setapikey <key> -Source <url> [options]
```

何處`<source>`識別的伺服器和`<key>`是索引鍵或儲存的密碼。 如果`<source>`已省略，nuget.org 會假設。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
