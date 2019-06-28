---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8088c6dcb7d453650950c219e1cc4dd047a64417
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426000"
---
# <a name="install-command-nuget-cli"></a>install 命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 所有

下載並安裝至專案時，預設為目前的資料夾中，使用指定的封裝來源。

> [!Tip]
> 若要下載封裝，以直接在專案的內容之外，請瀏覽套件頁面上[nuget.org](https://www.nuget.org) ，然後選取**下載**連結。

如果未不指定任何來源，所列在 全域設定檔中， `%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，會使用。 請參閱[常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)如需詳細資訊。

如果未不指定任何特定的套件，`install`會安裝在專案中所列出的所有套件`packages.config`檔案，讓它變成類似[ `restore` ](cli-ref-restore.md)。

`install`命令不會修改專案檔或`packages.config`; 如此一來，類似於`restore`，因為它只會將套件新增至磁碟，但不會變更專案的相依性。

若要加入相依性，請在 Visual Studio 中，新增套件，以透過套件管理員 UI 或主控台，或是修改`packages.config`，然後執行`install`或`restore`。

## <a name="usage"></a>使用量

```cli
nuget install <packageID | configFilePath> [options]
```

何處`<packageID>`名稱來安裝 （使用最新版本），或`<configFilePath>`識別`packages.config`檔案，其中列出要安裝的套件。 您可以指定特定版本`-Version`選項。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| DependencyVersion | *（4.4 +)* 的相依性套件使用，它可以是下列其中一種版本：<br/><ul><li>*最低*（預設值）： 最低版本</li><li>*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</li><li>*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</li><li>*最高*： 最高版本</li></ul> |
| DisableParallelProcessing | 安裝多個封裝，以平行方式停用。 |
| ExcludeVersion | 安裝封裝到資料夾，名為封裝名稱和版本號碼。 |
| FallbackSource | *（3.2 +)* 作為後援，以防主要中找不到封裝的封裝來源清單或預設來源。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 架構 | *（4.4 +)* 用於選取相依性的目標 framework。 預設值是 'Any' 如果未指定。 |
| Help | 顯示說明命令的資訊。 |
| NoCache | 禁止 NuGet 使用的快取的套件。 請參閱[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| OutputDirectory | 指定套件安裝所在的資料夾。 如果未不指定任何資料夾，則會使用目前的資料夾。 |
| PackageSaveMode | 指定要在套件安裝之後儲存的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| 發行前版本 | 允許發行前版本套件進行安裝。 還原套件時，不需要此旗標`packages.config`。 |
| RequireConsent | 確認，然後再下載並安裝封裝中啟用還原套件。 如需詳細資訊，請參閱 <<c0> [ 套件還原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要還原套件解決方案的根資料夾。 |
| Source | 指定封裝來源清單 （Url) 來使用。 如果省略，則此命令會使用組態檔中提供的來源，請參閱 <<c0> [ 常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)。 |
| Verbosity | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 指定要安裝的套件版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
