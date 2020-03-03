---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231223"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令（NuGet CLI）

**適用物件：** 套件耗用量、發行 &bullet;**支援的版本：** 全部

將指定伺服器 URL 的 API 金鑰儲存至 `NuGet.Config`，讓它不需要針對後續命令輸入。

## <a name="usage"></a>使用量

```cli
nuget setapikey <key> -Source <url> [options]
```

其中 `<source>` 會識別伺服器，而 `<key>` 則是要儲存的金鑰。 如果省略 `<source>`，則會假設為 nuget.org。 

> [!NOTE]
> API 金鑰不會用來向私人摘要進行驗證。 請參閱[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，以管理用來驗證來源的認證。
> 您可以從個別的 NuGet 伺服器取得 API 金鑰。 若要建立和管理 nuget.org 的 APIKeys，請參閱[發佈-api-金鑰](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>選項。

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | *（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 説明 | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| 詳細程度 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
