---
title: NuGet CLI 更新命令
description: Nuget.exe update 命令的參考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327505"
---
# <a name="update-command-nuget-cli"></a>update 命令 (NuGet CLI)

**適用于:** 套件耗&bullet;用量**支援的版本:** 全部

將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。 建議先執行「[還原](cli-ref-restore.md)」, 然後再`update`執行。 (若要更新個別的封裝, [`nuget install`](cli-ref-install.md)請使用, 而不指定版本號碼, 在此情況下, NuGet 會安裝最新版本)。

注意: `update`不會使用在 Mono (Mac OSX 或 Linux) 下執行的 CLI, 或使用 PackageReference 格式時。

如果`update`參考已經存在, 此命令也會更新專案檔中的元件參考。 如果更新的封裝有已加入的元件, 則*不*會加入新的參考。 新的封裝相依性也不會新增其元件參考。 若要將這些作業納入做為更新的一部分, 請使用套件管理員 UI 或套件管理員主控台, 更新 Visual Studio 中的封裝。

此命令也可以用來使用 *-self*旗標來更新 nuget.exe 本身。

## <a name="usage"></a>使用量

```cli
nuget update <configPath> [options]
```

其中`<configPath>` , 會識別`packages.config`列出專案相依性的或方案檔。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| FileConflictAction | 指定當系統提示您覆寫或忽略專案所參考的現有檔案時, 所要採取的動作。 值為*overwrite、ignore、none*。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| ID | 指定要更新之套件識別碼的清單。 |
| MSBuildPath | *(4.0 +)* 指定要搭配命令使用之 MSBuild 的路徑, 其優先順序高於`-MSBuildVersion`。 |
| MSBuildVersion | *(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 根據預設, 會挑選路徑中的 MSBuild, 否則會預設為 MSBuild 的最高安裝版本。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| PreRelease | 允許更新為發行前版本。 更新已安裝的發行前版本套件時, 不需要此旗標。 |
| RepositoryPath | 指定安裝封裝的本機資料夾。 |
| Safe | 指定只會安裝與已安裝的封裝在相同的主要和次要版本中可用的最高版本更新。 |
| Self | 將 nuget.exe 更新為最新版本;所有其他引數都會被忽略。 |
| Source | 指定要用於更新的套件來源清單 (如 Url)。 如果省略, 此命令會使用設定檔中提供的來源, 請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]、[無訊息]、[*詳細*]。 |
| Version | 與一個封裝識別碼搭配使用時, 會指定要更新的封裝版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
