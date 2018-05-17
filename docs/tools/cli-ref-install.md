---
title: NuGet CLI 安裝命令
description: Nuget.exe 安裝命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 615f2beca1eb288417f2345fcdf25e323942d300
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="install-command-nuget-cli"></a>install 命令 (NuGet CLI)

**適用於：** 封裝耗用量&bullet;**支援的版本：** 所有

下載並安裝到專案，將預設為目前的資料夾，使用指定的封裝來源的封裝。

> [!Tip]
> 若要下載的封裝，直接在專案內容之外，請瀏覽封裝的頁面上[nuget.org](https://www.nuget.org)選取**下載**連結。

如果未不指定任何來源，列出全域組態檔中， `%appdata%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，會使用。 請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)如需詳細資訊。

如果未不指定任何特定的封裝，`install`將列在專案中的所有封裝都安裝`packages.config`檔案，讓它變成類似[ `restore` ](cli-ref-restore.md)。

`install`命令不會修改專案檔或`packages.config`; 如此一來，類似於`restore`，只能將封裝新增至磁碟，但不會變更專案的相依性。

若要加入相依性，請在 Visual Studio 中，將透過封裝管理員 UI 或主控台專案，或是修改`packages.config`，然後執行 `install`或`restore`。

## <a name="usage"></a>使用量

```cli
nuget install <packageID | configFilePath> [options]
```

其中`<packageID>`名稱 （使用最新版本） 來安裝封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要安裝的封裝。 您可以指定特定版本與`-Version`選項。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| DependencyVersion | *（4.4 +)* 指定特定版本，覆寫預設相依性解析行為。 |
| DisableParallelProcessing | 安裝多個封裝，以平行方式停用。 |
| ExcludeVersion | 會封裝安裝到名為與封裝名稱和版本號碼。 |
| FallbackSource | *（3.2 +)* 作為後援，萬一主要中找不到封裝的封裝來源的清單或預設的來源。 |
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 架構 | *（4.4 +)* 用於選取的相依性的目標 framework。 預設值是 'Any' 如果未指定。 |
| 說明 | 顯示說明命令的資訊。 |
| 無快取記憶體 | NuGet 可防止使用快取的封裝。 請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| OutputDirectory | 指定在其中安裝封裝的資料夾。 如果沒有指定資料夾，則會使用目前的資料夾。 |
| PackageSaveMode | 指定要儲存封裝的安裝後的檔案類型： 其中一個`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| 發行前版本 | 允許安裝的套件發行前版本。 還原的封裝時，不需要此旗標`packages.config`。 |
| RequireConsent | 確認一次還原封裝才能下載和安裝封裝。 如需詳細資訊，請參閱[封裝還原，](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要還原封裝方案的根資料夾。 |
| 原始程式檔 | 指定封裝來源清單 （Url) 使用。 如果省略，則此命令會使用組態檔中提供的來源，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |
| 版本 | 指定要安裝之封裝的版本。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
