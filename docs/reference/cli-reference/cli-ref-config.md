---
title: NuGet CLI config 命令
description: Nuget.exe config 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433311"
---
# <a name="config-command-nuget-cli"></a>config 命令 (NuGet CLI)

**適用于:** 所有&bullet; **支援的版本**: 全部

取得或設定 NuGet 設定值。 如需其他用法, 請參閱[一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 如需可允許金鑰名稱的詳細資訊, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。

## <a name="usage"></a>使用量

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中`<name>` , `<value>`並指定要在設定中設定的機碼值組。 您可以指定所需數量的配對。 若要移除值, 請指定名稱和`=`正負號, 但沒有值。

如需允許的金鑰名稱, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。

在 NuGet 3.4 + 中`<value>` , 可以使用[環境變數](cli-ref-environment-variables.md)。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| AsPath | 傳回設定值做為路徑, 並在使用`-Set`時予以忽略。 |
| ConfigFile | 要修改的 NuGet 設定檔案。 如果未指定, 則會使用預設檔案-`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.config/NuGet/NuGet.Config` (Mac/Linux) 或`~/.nuget/NuGet/NuGet.Config` (依 OS 散發而有所不同)。|
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*] 、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

### <a name="examples"></a>範例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
