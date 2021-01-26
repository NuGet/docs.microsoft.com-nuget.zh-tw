---
title: NuGet CLI 區域變數命令
description: nuget.exe 區域變數命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779198"
---
# <a name="locals-command-nuget-cli"></a> (NuGet CLI 的區域變數命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 3.3 +

清除或列出本機 NuGet 資源，例如 *HTTP* 快取、 *全域套件* 資料夾和 temp 資料夾。 `locals`命令也可以用來顯示這些位置的清單。 如需詳細資訊，請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。

## <a name="usage"></a>使用方式

```cli
nuget locals <folder> [options]
```

其中 `<folder>` 是 `all` 、 `http-cache` 、 `packages-cache` *(3.5 和較早的)*、 `global-packages` `temp` *(3.4 +)*，以及 `plugins-cache` *(4.8 +)*。

## <a name="options"></a>選項。

- **`-Clear`**

  清除指定的資料夾。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-List`**

  列出指定之資料夾的位置，或與 *所有* 資料夾一起使用時的位置。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

如需其他範例，請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。
