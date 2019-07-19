---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327785"
---
# <a name="install-command-nuget-cli"></a>install 命令 (NuGet CLI)

**適用于:** 套件耗&bullet;用量**支援的版本:** 全部

使用指定的套件來源, 將套件下載並安裝到專案中, 並預設為目前的資料夾。

> [!Tip]
> 若要直接在專案內容之外下載套件, 請流覽[nuget.org](https://www.nuget.org)上的套件頁面, 然後選取 [**下載**] 連結。

如果未指定任何來源, 則會使用全域設定檔`%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 中所列的來源。 如需其他詳細資料, 請參閱[常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。

如果未指定特定套件, `install`會安裝`packages.config`專案檔案中列出的所有套件[`restore`](cli-ref-restore.md), 使其類似。

此命令不會修改專案檔或`packages.config`, 其`restore`方式類似于, 因為它只會將套件新增至磁片, 但不會變更專案的相依性。 `install`

若要新增相依性, 請在 Visual Studio 中透過套件管理員 UI 或主控台新增封裝, 或修改`packages.config` , 然後`install`執行或`restore`。

## <a name="usage"></a>使用量

```cli
nuget install <packageID | configFilePath> [options]
```

其中`<packageID>`的名稱是要安裝的封裝 (使用最新版本) `<configFilePath>` , 或`packages.config`識別列出要安裝之套件的檔案。 您可以使用`-Version`選項來指定特定版本。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| DependencyVersion | *(4.4 +)* 要使用的相依性套件版本, 它可以是下列其中一項:<br/><ul><li>*最低*(預設值): 最低版本</li><li>*HighestPatch*: 具有最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*: 具有最低主要、最高次要、最高修補程式的版本</li><li>*最高*: 最高版本</li></ul> |
| DisableParallelProcessing | 停用平行安裝多個套件。 |
| ExcludeVersion | 將套件安裝到名為的資料夾, 只包含套件名稱, 而不是版本號碼。 |
| FallbackSource | *(3.2 +)* 在主要或預設來源中找不到封裝時, 用來做為回退的套件來源清單。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 架構 | *(4.4 +)* 用來選取相依性的目標架構。 如果未指定, 則預設為「任何」。 |
| Help | 顯示命令的說明資訊。 |
| NoCache | 防止 NuGet 使用快取的套件。 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| OutputDirectory | 指定安裝封裝的資料夾。 如果未指定任何資料夾, 則會使用目前的資料夾。 |
| PackageSaveMode | 指定封裝安裝後要儲存的檔案類型: `nuspec`、 `nupkg`或`nuspec;nupkg`其中之一。 |
| 版 | 允許安裝發行前版本套件。 使用`packages.config`還原套件時, 不需要此旗標。 |
| RequireConsent | 確認在下載並安裝封裝之前, 已啟用還原封裝。 如需詳細資訊, 請參閱[套件還原](../../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要還原封裝之方案的根資料夾。 |
| Source | 指定要使用的套件來源清單 (如 Url)。 如果省略, 此命令會使用設定檔中提供的來源, 請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |
| 版本 | 指定要安裝的封裝版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
