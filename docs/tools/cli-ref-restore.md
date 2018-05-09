---
title: NuGet CLI restore 命令
description: Nuget.exe 還原命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dd0a74c9ed9b879643ed24cbddacff87310dfd6b
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2018
---
# <a name="restore-command-nuget-cli"></a>restore 命令 (NuGet CLI)

**適用於：**封裝耗用量&bullet;**支援的版本：** 2.7 +

下載並安裝任何遺漏的套件`packages`資料夾。 搭配 NuGet 4.0 + 及 PackageReference 格式使用時，會產生`<project>.nuget.props`檔案，如有需要在`obj`資料夾。 （從原始檔控制可以省略檔案）。

在 Mac OSX 與 Linux 上 Mono CLI 與，還原封裝不支援 PackageReference。

## <a name="usage"></a>使用量

```cli
nuget restore <projectPath> [options]
```

其中`<projectPath>`指定方案的位置或`packages.config`檔案。 請參閱[備註](#remarks)下方的行為的詳細資料。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| DirectDownload | *（4.0 +)* 下載套件，直接但不填入任何二進位檔或中繼資料快取。 |
| DisableParallelProcessing | 還原多個封裝，以平行方式停用。 |
| FallbackSource | *（3.2 +)* 作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。 |
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| MSBuildPath | *（4.0 +)* 指定之路徑的 MSBuild 命令，優先於使用`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要搭配此命令使用 MSBuild 的版本。 支援的值為 4，12，14，15。 根據預設，在路徑中的 MSBuild 會挑出，否則，預設為最高的已安裝版本的 MSBuild。 |
| 無快取記憶體 | NuGet 可防止使用快取的封裝。 請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| OutputDirectory | 指定在其中安裝封裝的資料夾。 如果沒有指定資料夾，則會使用目前的資料夾。 必要時還原`packages.config`檔案除非`PackagesDirectory`或`SolutionDirectory`用。|
| PackageSaveMode | 指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| PackagesDirectory | 與 `OutputDirectory` 相同。 必要時還原`packages.config`檔案除非`OutputDirectory`或`SolutionDirectory`用。 |
| Project2ProjectTimeOut | 以秒為單位來解析專案對專案參考的逾時。 |
| 遞迴 | *（4.0 +)* 還原所有參考的專案，適用於 UWP 和.NET Core 專案。 不適用於使用專案`packages.config`。 |
| RequireConsent | 確認一次還原封裝才能下載和安裝封裝。 如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定的方案資料夾。 還原解決方案的封裝時，則不正確。 必要時還原`packages.config`檔案除非`PackagesDirectory`或`OutputDirectory`用。 |
| 原始程式檔 | 指定封裝來源清單 （Url) 要用於還原。 如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 |
| 詳細資訊 |> 指定輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="remarks"></a>備註

還原命令會執行下列步驟：

1. 判斷作業模式的 restore 命令。

   | projectPath 檔案類型 | 行為 |
   | --- | --- |
   | 方案 （資料夾） | 尋找 NuGet`.sln`檔案，並有找到，否則將會提供錯誤的使用。 `(SolutionDir)\.nuget` 做為起始的資料夾。 |
   | `.sln` 檔案 | 還原方案; 所識別的封裝如果將會提供錯誤`-SolutionDirectory`用。 `$(SolutionDir)\.nuget` 做為起始的資料夾。 |
   | `packages.config` 或專案檔 | 還原檔案，解決和安裝相依性中所列的封裝。 |
   | 其他檔案類型 | 檔案被假設為`.sln`檔案做為上述; 如果不是方案時，發生錯誤的 NuGet 提供。 |
   | (未指定 projectPath) | <ul><li>NuGet 會尋找目前的資料夾中的方案檔。 如果找到單一檔案，則使用該還原封裝。如果找不到多個方案，NuGet 會提供錯誤。</li><li>如果沒有方案檔案，NuGet 會尋找`packages.config`並使用該值來還原封裝。</li><li>如果沒有解決方案或`packages.config`找不到檔案，NuGet 會產生錯誤。</ul> |

2. 判斷使用下列優先順序 （NuGet 如果找不到任何這些資料夾會顯示錯誤） 的封裝資料夾：

    - 使用指定的資料夾`-PackagesDirectory`。
    - `repositoryPath`值中的，此值 `Nuget.Config`
    - 使用指定的資料夾 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 還原時的方案套件，NuGet 會執行下列作業：
    - 載入方案檔案。
    - 還原方案層級中所列的套件`$(SolutionDir)\.nuget\packages.config`到`packages`資料夾。
    - 還原封裝中所列`$(ProjectDir)\packages.config`到`packages`資料夾。 指定每一個封裝，還原以平行方式封裝除非`-DisableParallelProcessing`指定。

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
