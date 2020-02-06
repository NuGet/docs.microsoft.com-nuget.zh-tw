---
title: NuGet CLI 安裝命令
description: Nuget.exe install 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036938"
---
# <a name="install-command-nuget-cli"></a>安裝命令（NuGet CLI）

**適用物件：** 套件耗用量 &bullet;**支援的版本：** 全部

使用指定的套件來源，將套件下載並安裝到專案中，並預設為目前的資料夾。

> [!Tip]
> 若要直接在專案內容之外下載套件，請流覽[nuget.org](https://www.nuget.org)上的套件頁面，然後選取 [**下載**] 連結。

如果未指定任何來源，則會使用全域設定檔中所列的 `%appdata%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。 如需其他詳細資料，請參閱[常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。

如果未指定特定的封裝，`install` 會安裝專案的 `packages.config` 檔案中列出的所有套件，使其類似于[`restore`](cli-ref-restore.md)。

`install` 命令不會修改專案檔或 `packages.config`;如此一來，它就類似于 `restore`，因為它只會將套件新增至磁片，但不會變更專案的相依性。

若要新增相依性，請在 Visual Studio 中透過套件管理員 UI 或主控台新增封裝，或修改 `packages.config` 然後執行 `install` 或 `restore`。

## <a name="usage"></a>使用方式

```cli
nuget install <packageID | configFilePath> [options]
```

其中 `<packageID>` 為要安裝的套件命名（使用最新版本），或 `<configFilePath>` 識別列出要安裝之套件的 `packages.config` 檔案。 您可以使用 `-Version` 選項來指定特定版本。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| DependencyVersion | *（4.4 +）* 要使用的相依性套件版本，它可以是下列其中一項：<br/><ul><li>*最低*（預設值）：最低版本</li><li>*HighestPatch*：具有最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*：具有最低主要、最高次要、最高修補程式的版本</li><li>*最高*：最高版本</li><li>*忽略*：不會使用任何相依性套件</li></ul> |
| DisableParallelProcessing | 停用平行安裝多個套件。 |
| ExcludeVersion | 將套件安裝到名為的資料夾，只包含套件名稱，而不是版本號碼。 |
| FallbackSource | *（3.2 +）* 在主要或預設來源中找不到封裝時，用來做為回退的套件來源清單。 |
| ForceEnglishOutput | *（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 架構 | *（4.4 +）* 用來選取相依性的目標架構。 如果未指定，則預設為「任何」。 |
| 說明 | 顯示命令的說明資訊。 |
| NoCache | 防止 NuGet 使用快取的套件。 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| OutputDirectory | 指定安裝封裝的資料夾。 如果未指定任何資料夾，則會使用目前的資料夾。 |
| PackageSaveMode | 指定封裝安裝後要儲存的檔案類型： `nuspec`、`nupkg`或 `nuspec;nupkg`的其中一個。 |
| PreRelease | 允許安裝發行前版本套件。 還原具有 `packages.config`的封裝時，不需要此旗標。 |
| RequireConsent | 確認在下載並安裝封裝之前，已啟用還原封裝。 如需詳細資訊，請參閱[套件還原](../../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要還原封裝之方案的根資料夾。 |
| 來源 | 指定要使用的套件來源清單（如 Url）。 如果省略，此命令會使用設定檔中提供的來源，請參閱[一般的 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 |
| 詳細程度 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |
| 版本 | 指定要安裝的封裝版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
