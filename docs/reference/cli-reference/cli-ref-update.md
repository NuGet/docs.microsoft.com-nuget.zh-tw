---
title: NuGet CLI 更新命令
description: nuget.exe update 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323644"
---
# <a name="update-command-nuget-cli"></a> (NuGet CLI 更新命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 全部

將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。 建議您先執行「 [還原](cli-ref-restore.md) 」，再執行 `update` 。  (若要更新個別套件，請使用 [`nuget install`](cli-ref-install.md) 但不指定版本號碼，在此情況下，NuGet 會安裝最新版本。 ) 

注意： `update` 無法使用在 Mono (MAC OSX 或 Linux) 下執行的 CLI，或使用 PackageReference 格式時。

此 `update` 命令也會更新專案檔中的元件參考，前提是這些參考已存在。 如果更新的封裝具有已加入的元件，則 *不* 會加入新的參考。 新的封裝相依性也不會新增其元件參考。 若要在更新過程中包含這些作業，請使用封裝管理員 UI 或封裝管理員主控台更新 Visual Studio 中的套件。

此命令也可以用來使用 *-self* 旗標來更新 nuget.exe 本身。

## <a name="usage"></a>使用方式

```cli
nuget update <configPath> [options]
```

其中 `<configPath>` 會識別列出專案相依性的 `packages.config` 或方案檔。

## <a name="options"></a>選項

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  指定要使用之相依性套件的版本，它可以是下列其中一項：<br/><ul><li>*最低* (預設) ：最低版本</li><li>*HighestPatch*：最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*：最低主要、最小次要、最高修補程式的版本</li><li>*最高*：最高版本</li><li>*略* 過：將不會使用任何相依性套件</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  當封裝中的檔案已經存在於目標專案時，指定預設動作。 設定為 [ `Overwrite` 永遠覆寫檔案]。 設定為 `Ignore` 以略過檔案。

  `PromptUser`除非提供或，否則動作（預設值）會提示您輸入每個衝突的檔案 `OverwriteAll` `IgnoreAll` ，這些檔案將會套用到所有剩餘的檔案。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-Id`**

  指定要更新之套件識別碼的清單。

- **`-MSBuildPath`**

  *(4.0 +)* 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  *(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-PreRelease`**

  允許更新為發行前版本。 更新已安裝的發行前版本套件時，不需要此旗標。

- **`-RepositoryPath`**

  指定安裝封裝的本機資料夾。

- **`-Safe`**

  指定在安裝套件的主要和次要版本中，只會安裝具有最高版本的更新。

- **`-Self`**

  `nuget.exe`最新版本的更新。 `-Source` 可以使用，但會忽略所有其他引數。 如果未提供任何來源，則會檢查是否 `nuget.org` 有更新，不論 `NuGet.Config` 設定為何。

- **`-Source`**

  指定要用於更新的 Url)  (套件來源的清單。 如果省略，此命令會使用設定檔中提供的來源，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

- **`-Version`**

  與一個封裝識別碼搭配使用時，會指定要更新的封裝版本。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
