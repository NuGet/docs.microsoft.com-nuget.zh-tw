---
title: NuGet CLI 還原命令
description: nuget.exe restore 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622825"
---
# <a name="restore-command-nuget-cli"></a> (NuGet CLI 還原命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 2.7 +

下載並安裝資料夾中遺失的任何套件 `packages` 。 與 NuGet 4.0 + 和 PackageReference 格式搭配使用時，會 `<project>.nuget.props` 在資料夾中產生檔案（如有需要） `obj` 。  (可以從原始檔控制省略檔案。 ) 

在 Mac OSX 和 Linux 上搭配使用 CLI 與 Mono，PackageReference 不支援還原套件。

## <a name="usage"></a>使用方式

```cli
nuget restore <projectPath> [options]
```

其中 `<projectPath>` 指定方案或檔案的位置 `packages.config` 。 如需行為詳細資料，請參閱下面的 [備註](#remarks) 。

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-DirectDownload`**

  * (4.0 +) * 直接下載套件，而不將任何二進位檔或中繼資料填入快取。

- **`-DisableParallelProcessing`**

   停用平行還原多個封裝。

- **`-FallbackSource`**

  * (3.2 +) * 在主要或預設來源中找不到封裝時，用來做為回盒的封裝來源清單。 使用分號來分隔清單專案。

- **`-Force`**

  在以 PackageReference 為基礎的專案中，即使上次還原成功，仍會強制解析所有相依性。 指定此旗標與刪除檔案類似 `project.assets.json` 。 這不會略過 HTTP 快取。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-ForceEvaluate`**

  強制還原重新評估所有的相依性，即使鎖定檔案已存在也一樣。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-LockFilePath`**

  寫入專案鎖定檔案的輸出位置。 根據預設，這是 `PROJECT_ROOT\packages.lock.json`。

- **`-LockedMode`**

  不允許更新專案鎖定檔案。

- **`-MSBuildPath`**

   * (4.0 +) * 指定要搭配命令使用的 MSBuild 路徑，優先順序高於 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  * (3.2 +) * 指定要搭配此命令使用的 MSBuild 版本。 支援的值為4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 依預設，會挑選路徑中的 MSBuild，否則會預設為 MSBuild 的最高安裝版本。

- **`-NoCache`**

  防止 NuGet 使用快取的封裝。 請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-OutputDirectory`**

  指定安裝封裝的資料夾。 如果未指定資料夾，則會使用目前的資料夾。 `packages.config`除非 `PackagesDirectory` 使用或，否則使用檔案還原時為必要項 `SolutionDirectory` 。

- **`-PackageSaveMode`**

  指定封裝安裝之後要儲存的檔案類型：、或的其中一個 `nuspec` `nupkg` `nuspec;nupkg` 。

- **`-PackagesDirectory`**

  與 `OutputDirectory` 相同。 `packages.config`除非 `OutputDirectory` 使用或，否則使用檔案還原時為必要項 `SolutionDirectory` 。

- **`-Project2ProjectTimeOut`**

  解析專案對專案參考的時間（秒）。

- **`-Recursive`**

  * (4.0 +) * 還原 UWP 和 .NET Core 專案的所有參考專案。 不會套用至使用 `packages.config` 的專案。

- **`-RequireConsent`**

  確認在下載及安裝封裝之前，已啟用還原的封裝。 如需詳細資訊，請參閱 [封裝還原](../../consume-packages/package-restore.md)。

- **`-SolutionDirectory`**

  指定方案資料夾。 還原解決方案的封裝時無效。 `packages.config`除非 `PackagesDirectory` 使用或，否則使用檔案還原時為必要項 `OutputDirectory` 。

- **`-Source`**

  將套件來源的清單指定為用於還原的 Url)  (。 如果省略，此命令會使用設定檔中提供的來源，請參閱設定 [NuGet 行為](../../consume-packages/configuring-nuget-behavior.md)。 使用分號來分隔清單專案。

- **`-UseLockFile`**

  可產生專案鎖定檔案並與還原一起使用。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="remarks"></a>備註

Restore 命令會執行下列步驟：

1. 判斷還原命令的操作模式。

   | projectPath 檔案類型 | 行為 |
   | --- | --- |
   | 方案 (資料夾)  | NuGet 會尋找檔案 `.sln` 並使用該檔案（如果找到的話），否則會產生錯誤。 `(SolutionDir)\.nuget` 會當做起始資料夾使用。 |
   | `.sln` 檔案 | 還原解決方案所識別的封裝;如果 `-SolutionDirectory` 使用，則會提供錯誤。 `$(SolutionDir)\.nuget` 會當做起始資料夾使用。 |
   | `packages.config` 或專案檔 | 還原檔案中列出的封裝，並解析和安裝相依性。 |
   | 其他檔案類型 | 檔案會假設為上述的檔案 `.sln` ; 如果不是解決方案，NuGet 會提供錯誤。 |
   | 未指定 (projectPath)  | <ul><li>NuGet 會在目前的資料夾中尋找方案檔。 如果找到單一檔案，則會使用該檔案來還原套件;如果找到多個解決方案，NuGet 會提供錯誤。</li><li>如果沒有解決方案檔，NuGet 會尋找 `packages.config` 並使用該檔案來還原封裝。</li><li>如果找不到任何解決方案或檔案 `packages.config` ，NuGet 會提供錯誤。</ul> |

2. 使用下列優先權順序判斷套件資料夾 (如果找不到這些資料夾) ，NuGet 會產生錯誤：

    - 使用指定的資料夾 `-PackagesDirectory` 。
    - `repositoryPath`中的值`Nuget.Config`
    - 使用指定的資料夾 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 還原解決方案的套件時，NuGet 會執行下列動作：
    - 載入方案檔。
    - 將中列出的方案層級封裝還原 `$(SolutionDir)\.nuget\packages.config` 到 `packages` 資料夾中。
    - 將列出的封裝還原 `$(ProjectDir)\packages.config` 到 `packages` 資料夾中。 針對指定的每個封裝，以平行方式還原封裝，除非 `-DisableParallelProcessing` 指定了。

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
