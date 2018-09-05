---
title: NuGet CLI 還原命令
description: Nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 06e3a26863761b7e7a42752866e7fe369f5be4ef
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550348"
---
# <a name="restore-command-nuget-cli"></a>restore 命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 2.7 +

下載並安裝任何遺漏的套件`packages`資料夾。 NuGet 4.0 + 和 PackageReference 格式搭配使用時，會產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。 （從原始檔控制可以省略檔案）。

Mac OSX 和 Linux 上使用 CLI 在 Mono 上，還原套件不支援使用 PackageReference。

## <a name="usage"></a>使用量

```cli
nuget restore <projectPath> [options]
```

何處`<projectPath>`指定方案的位置或`packages.config`檔案。 請參閱[備註](#remarks)下方的行為的詳細資料。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| DirectDownload | *（4.0 +)* 填入具有任何二進位檔或中繼資料的快取不直接下載套件。 |
| DisableParallelProcessing | 還原多個封裝，以平行方式停用。 |
| FallbackSource | *（3.2 +)* 作為後援，以防主要中找不到封裝的封裝來源清單或預設來源。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| MSBuildPath | *（4.0 +)* 指定要搭配命令，優先於使用 MSBuild 的路徑`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為 4、 12、 14、 15。 根據您的路徑中的 MSBuild 會挑出的預設值，否則，預設已安裝的最高的 MSBuild 版本。 |
| 無快取記憶體 | 禁止 NuGet 使用的快取的套件。 請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| OutputDirectory | 指定套件安裝所在的資料夾。 如果未不指定任何資料夾，則會使用目前的資料夾。 必要時以還原`packages.config`檔案，除非`PackagesDirectory`或`SolutionDirectory`用。|
| PackageSaveMode | 指定要在套件安裝之後儲存的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| PackagesDirectory | 與 `OutputDirectory` 相同。 必要時以還原`packages.config`檔案，除非`OutputDirectory`或`SolutionDirectory`用。 |
| Project2ProjectTimeOut | 以秒為單位來解析專案對專案參考的逾時。 |
| 遞迴 | *（4.0 +)* 還原適用於 UWP 和.NET Core 專案的所有參考專案。 不適用於使用專案`packages.config`。 |
| RequireConsent | 確認，然後再下載並安裝封裝中啟用還原套件。 如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定的方案資料夾。 還原套件的解決方案時，則不正確。 必要時以還原`packages.config`檔案，除非`PackagesDirectory`或`OutputDirectory`用。 |
| 原始程式檔 | 指定封裝來源清單 （Url) 要用於還原。 如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 |
| 詳細資訊 |> 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="remarks"></a>備註

Restore 命令會執行下列步驟：

1. 判斷 restore 命令的作業模式。

   | projectPath 檔案類型 | 行為 |
   | --- | --- |
   | 方案 （資料夾） | NuGet 會尋找`.sln`檔案，並使用，如未找到則會產生錯誤。 `(SolutionDir)\.nuget` 做為起始的資料夾。 |
   | `.sln` 檔案 | 還原方案中; 所識別的套件如果會顯示錯誤`-SolutionDirectory`用。 `$(SolutionDir)\.nuget` 做為起始的資料夾。 |
   | `packages.config` 或專案檔 | 還原在檔案中，解決並安裝相依性所列的套件。 |
   | 其他檔案類型 | 檔案會假設為`.sln`檔案儲存為上述的; 如果不是方案時，發生錯誤的 NuGet 提供。 |
   | (未指定 projectPath) | <ul><li>NuGet 會尋找目前資料夾中的方案檔。 如果找到單一檔案，則使用該還原套件;如果找到多個方案，則 NuGet 會顯示錯誤。</li><li>如果沒有方案檔案，NuGet 會尋找`packages.config`並使用它來還原套件。</li><li>如果沒有解決方案或`packages.config`找到檔案，NuGet 會產生錯誤。</ul> |

2. 決定使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的 [packages] 資料夾：

    - 使用指定的資料夾`-PackagesDirectory`。
    - `repositoryPath`值中的，此值 `Nuget.Config`
    - 使用指定的資料夾 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 當還原方案的套件，NuGet 會執行下列作業：
    - 載入方案檔。
    - 還原方案中所列的層級套件`$(SolutionDir)\.nuget\packages.config`成`packages`資料夾。
    - 還原套件中所列`$(ProjectDir)\packages.config`成`packages`資料夾。 指定每一個封裝還原以平行方式封裝除非`-DisableParallelProcessing`指定。

## <a name="examples"></a>範例

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
