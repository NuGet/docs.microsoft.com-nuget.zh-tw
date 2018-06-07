---
title: NuGet CLI 組態命令
description: Nuget.exe 組態命令的參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818161"
---
# <a name="config-command-nuget-cli"></a>組態命令 (NuGet CLI)

**適用於：** 所有&bullet;**支援的版本，**： 所有

取得或設定 NuGet 組態值。 對於其他使用方式，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。

## <a name="usage"></a>使用量

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中`<name>`和`<value>`指定要在組態中設定的索引鍵-值組。 您可以視需要指定多組。 若要移除的值，指定名稱和`=`號但沒有值。

如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。

在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AsPath | 傳回組態值做為路徑，會忽略時`-Set`用。 |
| ConfigFile | 要修改的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

### <a name="examples"></a>範例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
