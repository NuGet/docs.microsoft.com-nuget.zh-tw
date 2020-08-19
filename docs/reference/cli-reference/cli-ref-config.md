---
title: NuGet CLI config 命令
description: nuget.exe config 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622872"
---
# <a name="config-command-nuget-cli"></a> (NuGet CLI 的設定命令) 

**適用于：** 所有 &bullet; **支援的版本**：全部

取得或設定 NuGet 設定值。 如需其他使用方式，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 如需允許的金鑰名稱的詳細資訊，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。

## <a name="usage"></a>使用方式

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中 `<name>` 並 `<value>` 指定要在設定中設定的機碼值組。 您可以視需要指定任意數量的配對。 若要移除值，請指定名稱和 `=` 正負號，但不指定值。

如需允許的金鑰名稱，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。

在 NuGet 3.4 + 中， `<value>` 可以使用 [環境變數](cli-ref-environment-variables.md)。

## <a name="options"></a>選項。


- **`AsPath`**

  以路徑形式傳回設定值，使用時會忽略 `-Set` 。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Set`**

  一個要在 config 中設定的索引鍵/值組。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

### <a name="examples"></a>範例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
