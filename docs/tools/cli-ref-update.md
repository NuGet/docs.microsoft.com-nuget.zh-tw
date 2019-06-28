---
title: NuGet CLI 更新命令
description: Nuget.exe 更新命令參考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425912"
---
# <a name="update-command-nuget-cli"></a>update 命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 所有

更新專案中的所有封裝 (使用`packages.config`) 為最新可用版本。 建議您執行['restore'](cli-ref-restore.md)再執行`update`。 (若要更新個別的封裝，請使用[ `nuget install` ](cli-ref-install.md)但未指定版本號碼，寫 NuGet 會安裝最新版本。)

注意：`update`不適用於下執行，Mono （Mac OSX 或 Linux） 或使用 PackageReference 格式時的 CLI。

`update`命令也會更新專案檔中的組件參考，前提是這些參考已經存在。 已更新的封裝已加入之組件，新的參考是否*不*加入。 新的套件相依性也不需要加入其組件參考。 若要更新的組件中包含這些作業，請更新 Visual Studio 中使用套件管理員 UI 或套件管理員主控台中的封裝。

此命令也可用來更新本身的 nuget.exe 使用 *-自我*旗標。

## <a name="usage"></a>使用量

```cli
nuget update <configPath> [options]
```

何處`<configPath>`識別其中`packages.config`或列出專案的相依性的方案檔。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| FileConflictAction | 指定當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。 值為*覆寫，請忽略無*。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| Help | 顯示說明命令的資訊。 |
| ID | 指定封裝識別碼，以更新的清單。 |
| MSBuildPath | *（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為 4、 12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7，15.8、 15.9。 根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 發行前版本 | 可讓更新為發行前版本。 更新已安裝的發行前版本套件時，則不需要此旗標。 |
| RepositoryPath | 指定已安裝套件的本機資料夾。 |
| 安全 | 指定，只會更新與在相同的主要和次要版本內可用的最高版本將會安裝已安裝的套件。 |
| 自助 | Nuget.exe 更新為最新的版本;所有其他引數會被忽略。 |
| Source | 指定封裝來源清單 （Url) 若要使用的更新。 如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)。 |
| Verbosity | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 一個套件識別碼搭配使用時，指定要更新之封裝的版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
