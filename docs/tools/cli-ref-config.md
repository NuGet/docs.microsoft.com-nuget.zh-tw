---
title: NuGet CLI git-config 命令
description: Nuget.exe git-config 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546474"
---
# <a name="config-command-nuget-cli"></a>組態命令 (NuGet CLI)

**適用於：** 所有&bullet;**支援的版本**： 所有

取得或設定 NuGet 組態值。 額外的使用量，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。

## <a name="usage"></a>使用量

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

何處`<name>`和`<value>`指定要在組態中設定的索引鍵 / 值組。 您可以指定多個組所需。 若要移除的值，指定名稱和`=`號但沒有值。

如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。

在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AsPath | 傳回組態值做為路徑，會忽略時`-Set`用。 |
| ConfigFile | 要修改的 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

### <a name="examples"></a>範例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
