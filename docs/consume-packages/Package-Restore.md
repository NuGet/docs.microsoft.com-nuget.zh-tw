---
title: NuGet 套件還原
description: 概述 NuGet 如何還原專案相依的套件，包括如何停用還原和限制版本。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 6a8a2f1c5ced956f18b623f112756cdd2fab22f5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="package-restore"></a>套件還原

為了升級更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會依專案檔或 `packages.config`中所列，安裝所有專案的相依性。 Visual Studio 可在建置專案時自動還原套件。 `dotnet build` 和 `dotnet run` 命令 (.NET Core 2.0 +) 也會執行自動還原。 您也可以透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild，隨時還原套件。

套件還原會確認所有專案的相依性是可用的，而不用將那些套件儲存在原始檔控制中。 有關如何設定存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。

## <a name="package-restore-overview"></a>套件還原概觀

還原套件會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。

如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。 如果套件不在快取中，則 NuGet 會嘗試從所有已啟用的來源下載套件 (請參閱[設定 NuGet 行為](Configuring-NuGet-Behavior.md)；來源也會出現在 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 中)。 在還原過程中，NuGet 會忽略套件來源的順序，而使用任一個最先回應要求的來源。

> [!Note]
> 在所有來源檢查完畢前，NuGet 不會指出還原套件的失敗。 到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。 這項錯誤表示套件未出現在其他*任何*來源上，即使那些來源都未個別出現錯誤亦然。

套件還原會以下列方式觸發：

- **dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../consume-packages/package-references-in-project-files.md)) 中所列的套件。 使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。

- **套件管理員 UI (Windows 上的 Visual Studio)**：從範本建立專案時，以及建置專案時，會自動還原套件 (受限於[啟用和停用套件還原](#enabling-and-disabling-package-restore)中所述的選項)。 在 NuGet 4.0+ 中，還原也會在對 .NET Core SDK 型專案進行變更時自動進行。

    若要手動還原，請以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [還原 NuGet 套件]。 如有一或多個個別套件仍未正確安裝 (表示方案總管顯示錯誤圖示)，則使用套件管理員 UI 來解除安裝並重新安裝受影響的套件。 請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)

    如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請遵循[啟用和停用套件還原](#enabling-and-disabling-package-restore)下的指示來開啟自動還原。 另請參閱[套件還原疑難排解](Package-restore-troubleshooting.md)。

- **NuGet CLI**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令來還原專案檔或 `packages.config`中所列的套件。 您也可以指定方案檔。

- **MSBuild**：使用 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 命令來還原專案檔中所列的套件 (僅限 PackageReference)。 只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017)。 `nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。

- **Visual Studio Team Services**：在 Team Services 上建立組建定義時，在定義中於任何建置工作之前包含 [NuGet 還原](/vsts/build-release/tasks/package/nuget#restore-nuget-packages)或 [.NET Core 還原](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages)工作。 在許多組建範本中，預設會包含此工作。

- **Team Foundation Server**：TFS 2013 和更新版本會在建置期間自動還原套件，前提是您使用的是適用於 TFS 2013 或更新版本的 Team Build 範本。 針對較早的 TFS 版本，您可以包含一個建置步驟來叫用上述其中一個命令列還原選項。 您可以選擇性地將建置範本移轉至 TFS 2013。 如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原逐步解說](../consume-packages/team-foundation-build.md)。

## <a name="enabling-and-disabling-package-restore"></a>啟用和停用套件還原

套件還原主要是透過 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] 所啟用：

![透過 NuGet 套件管理員選項控制套件還原行為](media/Restore-01-AutoRestoreOptions.png)

- **允許 NuGet 下載遺漏的套件**：變更 `NuGet.Config` 檔案中的 `packageRestore/enabled` 設定，以控制所有形式的套件還原，如下所示 (在 Windows 上為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。 在 Visual Studio 中，此設定可讓解決方案操作功能表上的 [還原 NuGet 套件] 命令運作。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  在啟動 Visual Studio 或啟動組建之前，可以設定稱為 **EnableNuGetPackageRestore** 且值為 TRUE 或 FALSE 的環境變數，以全域覆寫 `packageRestore/enabled` 設定。

- **在 Visual Studio 建置期間自動檢查遺漏的套件**：變更 `NuGet.Config` 檔案中的 `packageRestore/automatic` 設定，以控制自動還原，如下所示 (在 Windows 上為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。 設定此選項時，從 Visual Studio 中執行組建，會自動還原任何遺漏的套件。 此選項不會影響使用 MSBuild 從命令列執行的組建。

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

如需參考，請參閱 [NuGet 組態檔 - packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)。

在某些情況下，開發人員或公司可能想要針對電腦上的所有使用者啟用或停用套件還原。 若要這麼做，請將上述相同設定新增到全域 NuGet 組態檔中，此檔案位於 `%ProgramData%\NuGet\Config` (Windows，可能位於 Visual Studio 的特定 `\{IDE}\{Version}\{SKU}\` 資料夾下) 或 `~/.local/share` (Mac/Linux)。 個別使用者接著可以視需要選擇性地啟用專案層級的還原。 如需 NuGet 如何設定多個組態檔優先順序的確切詳細資料，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

> [!Important]
> 如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。

## <a name="constraining-package-versions-with-restore"></a>使用還原限制套件版本

透過任何方法還原套件時，NuGet 會遵循 `packages.config` 或專案檔中所指定的任何條件約束：

- `packages.config`：指定相依性之 `allowedVersion` 屬性中的版本範圍。 請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如: 

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- 專案檔 (PackageReference)：直接使用相依性的版本號碼來指定版本範圍。 例如: 

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。

## <a name="forcing-restore-from-package-sources"></a>強制從套件來源還原

根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有說明。

若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：

- 使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾
- 使用下列方法其中之一，在還原作業之前暫時變更 *global-packages* 資料夾的位置：
  - 將 NUGET_PACKAGES 環境變數設定為不同資料夾。
  - 建立將 `globalPackagesFolder` (如果使用 PackageReference) 或 `repositoryPath` (如果使用 `packages.config`) 設定為不同資料夾的 `NuGet.Config` 檔案 (請參閱[組態設定](../reference/nuget-config-file.md#config-section)
  - 僅限 MSBuild：使用 `RestorePackagesPath` 屬性來指定不同資料夾。

若要避免使用 HTTP 來源的快取，請執行下列任一步驟：

- 使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。 這些選項不會影響透過 Visual Studio 套件管理員 UI 或主控台進行的還原作業。
- 使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。
- 暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。

## <a name="troubleshooting"></a>疑難排解

請參閱[針對套件還原進行疑難排解](package-restore-troubleshooting.md)。