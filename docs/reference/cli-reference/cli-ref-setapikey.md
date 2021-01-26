---
title: NuGet CLI setapikey 命令
description: nuget.exe setapikey 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780021"
---
# <a name="setapikey-command-nuget-cli"></a> (NuGet CLI 的 setapikey 命令) 

**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部

將指定的伺服器 URL 的 API 金鑰儲存在中 `NuGet.Config` ，如此一來，就不需要針對後續命令輸入它。

## <a name="usage"></a>使用方式

```cli
nuget setapikey <key> -Source <url> [options]
```

`<source>`識別伺服器的位置，以及 `<key>` 要儲存的金鑰。 如果 `<source>` 省略，則會假設為 nuget.org。 

> [!NOTE]
> API 金鑰不會用來向私人摘要進行驗證。 請參閱[ `nuget sources` 命令](../cli-reference/cli-ref-sources.md)來管理用來驗證來源的認證。
> 您可以從個別的 NuGet 伺服器取得 API 金鑰。 若要建立和管理 nuget.org 的 >apikeys.cs，請參閱 [取得---api 金鑰](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-src|-Source`**

  API 金鑰有效的伺服器 URL。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
