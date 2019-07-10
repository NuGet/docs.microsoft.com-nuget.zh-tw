---
title: 使用 nuget.exe CLI 管理 NuGet 套件
description: 使用 nuget.exe CLI 以處理 NuGet 套件的指示。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427373"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>使用 nuget.exe CLI 管理套件

CLI 工具可讓您輕鬆地在專案和解決方案中更新及還原 NuGet 套件。 此工具會在 Windows 上提供所有的 NuGet 功能，在 Mono 底下執行時也在 Mac 和 Linux 上提供大部分功能。

Nuget.exe CLI 適用於您的 .NET Framework 專案和非 SDK 樣式專案 (例如，以 .NET Standard 程式庫為目標的專案)。 如果您使用已移轉到 `PackageReference` 的非 SDK 樣式專案，請改為使用 dotnet CLI。 NuGet CLI 需要 [packages.config](../reference/packages-config.md) 檔案來進行套件參考。

> [!NOTE]
> 在大部分情況下，我們建議將使用 `packages.config` 的[非 SDK 樣式專案移轉](../reference/migrate-packages-config-to-package-reference.md)至 PackageReference，然後您便可以使用 dotnet CLI 而不是 `nuget.exe` CLI。 移轉目前不適用於 C++ 和 ASP.NET 專案。

本文顯示一些最常用 nuget.exe CLI 命令的基本使用方式。 針對這些命令的大部分，CLI 工具會在目前的目錄中尋找專案檔，除非在命令中指定專案檔。 如需您可以使用的命令和引數完整清單，請參閱 [nuget.exe CLI 參考](../tools/nuget-exe-cli-reference.md)。

## <a name="prerequisites"></a>必要條件

- 安裝 `nuget.exe` CLI，作法是從 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下載它、將該 `.exe` 檔案儲存至適當的資料夾，然後將該資料夾新增至您的 PATH 環境變數。

## <a name="install-a-package"></a>安裝套件

[install](../tools/cli-ref-install.md) 命令會下載並安裝套件至專案，預設為目前的資料夾，且使用指定的套件來源。 請將新套件安裝到專案根目錄中的 *packages* 資料夾。

> [!IMPORTANT]
> `install` 命令不會修改專案檔或 *packages.config*；如此，它類似於 `restore`，因為它只會將套件新增至磁碟，但不會變更專案的相依性。 若要新增相依性，請在 Visual Studio 中透過套件管理員 UI 或主控台來新增套件，或是修改 *packages.config*，然後執行 `install` 或 `restore`。

1. 開啟命令列並切換至包含您專案檔的目錄。

2. 使用下列命令，將 NuGet 套件安裝到 *packages* 資料夾。

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    若要將 `Newtonsoft.json` 套件安裝到 *packages* 資料夾，請使用下列命令：

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

或者，您可以使用下列命令，使用現有的 `packages.config` 檔案將 NuGet 套件安裝到 *packages* 資料夾。 這不會將套件新增至您的專案相依性，但會將它安裝在本機。

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>安裝特定版本的套件

如果當您使用 [install](../tools/cli-ref-install.md) 命令時未指定版本，NuGet 會安裝最新版的套件。 您也可以安裝特定版本的 NuGet 套件：

```cli
nuget install <packageID | configFilePath> -Version <version>
```

例如，若要新增 12.0.1 版的 `Newtonsoft.json` 套件，請使用此命令：

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

如需 `install` 限制和行為的詳細資訊，請參閱[安裝套件](#install-a-package)。

## <a name="remove-a-package"></a>移除套件

若要刪除一或多個套件，請從 *packages* 資料夾刪除您想要移除的套件。

如果您想要重新安裝套件，請使用 `restore` 或 `install` 命令。

## <a name="list-packages"></a>列出套件

您可以使用 [list](../tools/cli-ref-list.md) 命令顯示來自指定來源的套件清單。 使用 `-Source` 選項以限制搜尋。

```cli
nuget list -Source <source>
```

例如，列出 *packages* 資料夾中的套件。

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

如果您使用搜尋字詞，搜尋會包含套件名稱、標籤和套件描述。

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>更新個別套件

除非您指定套件版本，否則當您使用 `install` 命令時 NuGet 會安裝最新版套件。

## <a name="update-all-packages"></a>更新所有套件

使用 [update](../tools/cli-ref-update.md) 命令來更新所有套件。 將專案中的所有套件 (使用 `packages.config`) 更新為最新可用版本。 建議您先執行 `restore`，再執行 `update`。

```cli
nuget update
```

## <a name="restore-packages"></a>還原套件

使用 [restore](../tools/cli-ref-restore.md) 命令，它會下載並安裝 *packages* 資料夾遺漏的任何套件。

`restore` 只會將套件新增至磁碟，但不會變更專案的相依性。 若要還原專案相依性，請修改 `packages.config`，然後使用 `restore` 命令。

使用 `restore` 還原套件：

```cli
nuget restore MySolution.sln
```