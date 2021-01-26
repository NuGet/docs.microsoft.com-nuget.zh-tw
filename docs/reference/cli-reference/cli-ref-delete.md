---
title: NuGet CLI 刪除命令
description: nuget.exe delete 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775953"
---
# <a name="delete-command-nuget-cli"></a> (NuGet CLI 刪除命令) 

**適用于：** 套件發行 &bullet; **支援的版本：** 全部

從套件來源刪除或取消列出套件。 若為 nuget.org，delete 命令會 [取消列出封裝](../../nuget-org/policies/deleting-packages.md)。

## <a name="usage"></a>使用方式

```cli
nuget delete <packageID> <packageVersion> [options]
```

， `<packageID>` 並 `<packageVersion>` 識別要刪除或取消列出的確切套件。 確切的行為取決於來源。 舉例來說，如果是本機資料夾，則會刪除封裝;若為 nuget.org，則不會列出套件。

## <a name="options"></a>選項。

- **`-ApiKey`**

  目標儲存機制的 API 金鑰。 如果不存在，則會使用設定檔中指定的。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

 - **`-np|-NoPrompt`**

   刪除時不要提示。

 - **`-NoServiceEndpoint`** 不會將 "api/v2/套件" 附加至來源 URL。

- **`-src|-Source`**

  指定伺服器 URL。 Nuget.org 的 URL 是 `https://api.nuget.org/v3/index.json` 。 若為私用摘要，請取代主機名稱，例如 *% hostname%/api/v3*。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
