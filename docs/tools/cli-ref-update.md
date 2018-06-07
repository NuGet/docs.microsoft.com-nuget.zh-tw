---
title: NuGet CLI 更新命令
description: Nuget.exe 更新命令的參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817703"
---
# <a name="update-command-nuget-cli"></a>update 命令 (NuGet CLI)

**適用於：** 封裝耗用量&bullet;**支援的版本：** 所有

更新專案中的所有封裝 (使用`packages.config`) 為其最新可用版本。 建議您執行['restore'](cli-ref-restore.md)再執行`update`。 (若要更新個別的封裝，請使用[ `nuget install` ](cli-ref-install.md)但未指定版本號碼，case NuGet 會安裝最新版本。)

注意：`update`不適用於 CLI 下執行，單聲道 （Mac OSX 或 Linux） 或使用 PackageReference 格式時。

`update`命令也會更新專案檔中的組件參考、 提供的參考已經存在。 如果已更新的封裝加入組件，新的參考是*不*加入。 新的封裝相依性也不需要加入其組件參考。 若要更新的組件中包含這些作業，請更新 Visual Studio 中使用封裝管理員 UI 或 Package Manager Console 中的封裝。

此命令也可用來更新本身 nuget.exe 使用 *-自我*旗標。

## <a name="usage"></a>使用量

```cli
nuget update <configPath> [options]
```

其中`<configPath>`識別其中`packages.config`或列出專案的相依性的方案檔。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| FileConflictAction | 指定當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。 值為*覆寫，忽略無*。 |
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| ID | 指定封裝識別碼，以更新的清單。 |
| MSBuildPath | *（4.0 +)* 指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要搭配此命令使用 MSBuild 的版本。 支援的值為 4，12，14，15。 根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 發行前版本 | 可讓更新的發行前版本。 更新已安裝的套件發行前版本時，則不需要此旗標。 |
| RepositoryPath | 指定已安裝的套件的本機資料夾。 |
| 安全 | 指定，只更新相同的主要和次要版本中可用的最高版本時已安裝的封裝將會安裝。 |
| 自我 | Nuget.exe 更新為最新版本。所有其他引數會被忽略。 |
| 原始程式檔 | 指定封裝來源清單 （Url) 若要使用的更新。 如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 一個封裝識別碼搭配使用時，指定要更新之封裝的版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
