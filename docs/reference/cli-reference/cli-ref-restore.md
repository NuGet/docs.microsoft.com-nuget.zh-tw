---
title: NuGet CLI 還原命令
description: Nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 211f24ff67c06da00d6a014e679cc422d493d6d5
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959735"
---
# <a name="restore-command-nuget-cli"></a>restore 命令 (NuGet CLI)

**適用于:** 套件耗&bullet;用量**支援的版本:** 2.7+

下載並安裝資料夾中遺失的`packages`任何套件。 與 NuGet 4.0 + 和 PackageReference 格式搭配使用時, 會`<project>.nuget.props` `obj`在資料夾中產生檔案 (如有需要)。 (可以從原始檔控制省略檔案)。

在 Mac OSX 和 Linux 上使用 Mono 的 CLI, PackageReference 不支援還原封裝。

## <a name="usage"></a>使用量

```cli
nuget restore <projectPath> [options]
```

其中`<projectPath>`指定解決方案`packages.config`或檔案的位置。 如需行為詳細資料, 請參閱下面的[備註](#remarks)。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| DirectDownload | *(4.0 +)* 直接下載封裝, 而不需以任何二進位檔或中繼資料填入快取。 |
| DisableParallelProcessing | 停用平行還原多個封裝。 |
| FallbackSource | *(3.2 +)* 在主要或預設來源中找不到封裝時, 用來做為回退的套件來源清單。 請使用分號來分隔清單專案。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| MSBuildPath | *(4.0 +)* 指定要搭配命令使用之 MSBuild 的路徑, 其優先順序高於`-MSBuildVersion`。 |
| MSBuildVersion | *(3.2 +)* 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 根據預設, 會挑選路徑中的 MSBuild, 否則會預設為 MSBuild 的最高安裝版本。 |
| NoCache | 防止 NuGet 使用快取的套件。 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| OutputDirectory | 指定安裝封裝的資料夾。 如果未指定任何資料夾, 則會使用目前的資料夾。 使用檔案進行還原時`packages.config` , 除非`PackagesDirectory`使用`SolutionDirectory`或, 否則為必要。|
| PackageSaveMode | 指定封裝安裝後要儲存的檔案類型: `nuspec`、 `nupkg`或`nuspec;nupkg`其中之一。 |
| PackagesDirectory | 與 `OutputDirectory` 相同。 使用檔案進行還原時`packages.config` , 除非`OutputDirectory`使用`SolutionDirectory`或, 否則為必要。 |
| Project2ProjectTimeOut | 解析專案對專案參考的超時 (以秒為單位)。 |
| 式 | *(4.0 +)* 還原 UWP 和 .NET Core 專案的所有參考專案。 不適用於使用`packages.config`的專案。 |
| RequireConsent | 確認在下載並安裝封裝之前, 已啟用還原封裝。 如需詳細資訊, 請參閱[套件還原](../../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定解決方案資料夾。 還原方案的封裝時無效。 使用檔案進行還原時`packages.config` , 除非`PackagesDirectory`使用`OutputDirectory`或, 否則為必要。 |
| Source | 指定要用於還原的套件來源清單 (如 Url)。 如果省略, 此命令會使用設定檔中提供的來源, 請參閱設定[NuGet 行為](../../consume-packages/configuring-nuget-behavior.md)。 請使用分號來分隔清單專案。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="remarks"></a>備註

Restore 命令會執行下列步驟:

1. 判斷 restore 命令的操作模式。

   | projectPath 檔案類型 | 行為 |
   | --- | --- |
   | 解決方案 (資料夾) | NuGet 會尋找`.sln`檔案, 並在找到時使用該檔案, 否則會產生錯誤。 `(SolutionDir)\.nuget`會用來做為起始資料夾。 |
   | `.sln`文字檔 | 還原解決方案所識別的套件;如果`-SolutionDirectory`使用, 則會產生錯誤。 `$(SolutionDir)\.nuget`會用來做為起始資料夾。 |
   | `packages.config`或專案檔 | 還原檔案中列出的套件、解析和安裝相依性。 |
   | 其他檔案類型 | 檔案會假設`.sln`為上述檔案; 如果不是解決方案, NuGet 會提供錯誤。 |
   | (未指定 projectPath) | <ul><li>NuGet 會在目前的資料夾中尋找方案檔。 如果找到單一檔案, 則會使用該檔案來還原封裝;如果找到多個解決方案, NuGet 會提供錯誤。</li><li>如果沒有解決方案檔, NuGet 會尋找`packages.config` , 並使用它來還原套件。</li><li>如果找不到`packages.config`解決方案或檔案, NuGet 會提供錯誤。</ul> |

2. 使用下列優先順序來判斷套件資料夾 (如果找不到這些資料夾, 則 NuGet 會產生錯誤):

    - 使用`-PackagesDirectory`指定的資料夾。
    - 中`repositoryPath`的值`Nuget.Config`
    - 使用指定的資料夾`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 還原解決方案的套件時, NuGet 會執行下列動作:
    - 載入方案檔。
    - 將中列出的`$(SolutionDir)\.nuget\packages.config` `packages`方案層級封裝還原到資料夾中。
    - 將中列出的`$(ProjectDir)\packages.config` `packages`封裝還原到資料夾中。 針對每個指定的封裝, 請以平行方式`-DisableParallelProcessing`還原封裝, 除非指定了。

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
