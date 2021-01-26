---
title: NuGet CLI 安裝命令
description: nuget.exe install 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779263"
---
# <a name="install-command-nuget-cli"></a> (NuGet CLI 安裝命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 全部

使用指定的套件來源，將套件下載並安裝到專案中，預設為目前的資料夾。

> [!Tip]
> 若要直接在專案內容外下載套件，請造訪套件在 [nuget.org](https://www.nuget.org) 上的頁面，然後選取 **下載** 連結。

如果未指定任何來源，則會使用全域設定檔中所列的 `%appdata%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。 如需其他詳細資料，請參閱 [常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md) 設定。

如果未指定特定的封裝，則會 `install` 安裝專案檔案中列出的所有套件 `packages.config` ，使其類似 [`restore`](cli-ref-restore.md) 。

此 `install` 命令不會修改專案檔，或者， `packages.config` 它類似于 `restore` ，它只會將套件新增至磁片，但不會變更專案的相依性。

若要加入相依性，請在 Visual Studio 中透過封裝管理員 UI 或主控台加入封裝，或修改 `packages.config` 然後執行 `install` 或 `restore` 。

## <a name="usage"></a>使用方式

```cli
nuget install <packageID | configFilePath> [options]
```

`<packageID>`使用最新版本) 將套件命名為安裝 (，或 `<configFilePath>` 識別 `packages.config` 列出要安裝之套件的檔案。 您可以使用選項來指出特定版本 `-Version` 。

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-DependencyVersion`**

  *(4.4 +)* 要使用之相依性套件的版本，它可以是下列其中一項：<br/><ul><li>*最低* (預設) ：最低版本</li><li>*HighestPatch*：最低主要、最低次要、最高修補程式的版本</li><li>*HighestMinor*：最低主要、最小次要、最高修補程式的版本</li><li>*最高*：最高版本</li><li>*略* 過：將不會使用任何相依性套件</li></ul>

- **`-DirectDownload`**

  直接下載，但不填入任何具有中繼資料或二進位檔的快取。

- **`-DisableParallelProcessing`**

  停用平行安裝多個套件。

- **`-x|-ExcludeVersion`**

  將套件安裝至僅具有套件名稱的資料夾，而不是版本號碼。

- **`-FallbackSource`**

  *(3.2 +)* 在主要或預設來源中找不到封裝時，用來做為回盒的封裝來源清單。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-Framework`**

  *(4.4 +)* 用來選取相依性的目標架構。 如果未指定，則預設為 ' Any '。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NoCache`**

  防止 NuGet 使用快取的封裝。 請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-OutputDirectory`**

  指定安裝封裝的資料夾。 如果未指定資料夾，則會使用目前的資料夾。

- **`-PackageSaveMode`**

  指定封裝安裝之後要儲存的檔案類型：、或的其中一個 `nuspec` `nupkg` `nuspec;nupkg` 。

- **`-PreRelease`**

  允許安裝發行前版本套件。 使用還原封裝時，不需要此旗標 `packages.config` 。

- **`-RequireConsent`**

  確認在下載及安裝封裝之前，已啟用還原的封裝。 如需詳細資訊，請參閱 [封裝還原](../../consume-packages/package-restore.md)。

- **`-SolutionDirectory`**

  指定要還原封裝之方案的根資料夾。

- **`-Source`**

   指定) 要使用的 Url (套件來源的清單。 如果省略，此命令會使用設定檔中提供的來源，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

- **`-Version`**

  指定要安裝的封裝版本。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
