---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383965"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令（NuGet CLI）

**適用物件：** 套件耗用量、發行 &bullet;**支援的版本：** 全部

將指定伺服器 URL 的 API 金鑰儲存至 `NuGet.Config`，讓它不需要針對後續命令輸入。

## <a name="usage"></a>使用

```cli
nuget setapikey <key> -Source <url> [options]
```

其中 `<source>` 會識別伺服器，而 `<key>` 則是要儲存的金鑰或密碼。 如果省略 `<source>`，則會假設為 nuget.org。

> [!NOTE]
> API 金鑰不會用來向私人摘要進行驗證。 請參閱[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，以管理用來驗證來源的認證。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | *（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 說明 | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
