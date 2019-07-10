---
title: NuGet 套件還原
description: NuGet 如何還原專案相依套件的概觀，包括如何停用還原和限制版本。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467801"
---
# <a name="package-restore"></a>套件還原

為了提倡更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會依專案檔或 `packages.config` 中所列，安裝專案的所有相依性。 .NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令會執行自動套件還原。 Visual Studio 可以在建置專案時自動還原套件，您可以隨時透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild 來還原套件。

套件還原會確認專案的所有相依性都可用，而不必將它們儲存在原始檔控制中。 若要設定原始程式碼控制存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。 

## <a name="package-restore-overview"></a>套件還原概觀

套件還原會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。

如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。 如果套件不在快取中，NuGet 會嘗試從清單中的所有已啟用來源下載套件，位置是 Visual Studio 中的 [工具]   > [選項]   > [NuGet 套件管理員]   > [套件來源]  。 在還原程序中，NuGet 會忽略套件來源的順序，且使用任一個最先回應要求的來源。 如需 NuGet 運作方式的詳細資訊，請參閱[常用的 NuGet 組態](Configuring-NuGet-Behavior.md)。 

> [!Note]
> 在所有來源檢查完畢前，NuGet 不會指出還原套件失敗。 到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。 這項錯誤表示套件未出現在其他「任何」  來源上，即使那些來源都未個別出現錯誤亦然。

您可以用下列任一方式來觸發套件還原：

- **dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令，利用 [PackageReference](../consume-packages/package-references-in-project-files.md) 來還原專案檔中所列套件。 使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 命令自動完成還原。  

- **套件管理員**：在 Windows 上的 Visual Studio，套件還原會自動在您從範本建立專案或建置專案時自動進行，且受限於[啟用和停用套件還原](#enable-and-disable-package-restore)中的選項。 在 NuGet 4.0+ 中，還原也會在對 .NET Core SDK 專案進行變更時自動進行。

    若要手動還原套件，請以滑鼠右鍵按一下 [方案總管]  中的解決方案，然後選取 [還原 NuGet 套件]  。 如果一或多個個別套件仍未正確安裝，則 [方案總管]  會顯示錯誤圖示。 以滑鼠右鍵按一下並選取 [管理 NuGet 套件]  ，且使用 [套件管理員]  先解除安裝再重新安裝受影響的套件。 如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)

    如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore)。 另請參閱[針對套件還原進行疑難排解](Package-restore-troubleshooting.md)。

- **nuget.exe CLI**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令來還原專案或解決方案檔或 `packages.config` 中所列的套件。 

- **MSBuild**：使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令，利用 PackageReference 來還原專案檔中所列套件。 這個命令只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017 和更新版本)。 `nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。

- **Azure Pipelines**：在 Azure Pipelines 中建立組建定義時，在定義中於任何建置工作之前包含 NuGet [還原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)或 .NET Core [還原](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages)工作。 根據預設，一些建置範本已包含還原工作。

- **Azure DevOps Server**：Azure DevOps Server 和 TFS 2013 及更新版本會在建置期間自動還原套件，前提是您使用 TFS 2013 或更新版本的 Team Build 範本。 針對較舊的 TFS 版本，您可以包含一個建置步驟來執行命令列還原選項，或選擇性地將建置範本移轉至較新版本。 如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原設定](../consume-packages/team-foundation-build.md)。

## <a name="enable-and-disable-package-restore"></a>啟用和停用套件還原

在 Visual Studio 中，您主要是透過 [工具]   > [選項]   > [NuGet 套件管理員]  來控制套件還原：

![透過 NuGet 套件管理員選項控制套件還原](media/Restore-01-AutoRestoreOptions.png)

- **允許 NuGet 下載遺漏的套件**會藉由變更 `NuGet.Config` 檔案 (在 Windows 上為 `%AppData%\NuGet\`，在 Mac/Linux 上則為 `~/.nuget/NuGet/`) [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 設定，控制所有形式的套件還原。 此設定也會啟用 Visual Studio 中解決方案操作功能表上的 [還原 NuGet 套件]  命令。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > 在啟動 Visual Studio 或啟動組建之前，若要全域覆寫 `packageRestore/enabled` 設定，可以用值 True 或 False 來設定 **EnableNuGetPackageRestore** 環境變數。

- **在 Visual Studio 建置期間自動檢查遺漏的套件**會藉由變更 `NuGet.Config` 檔案 [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 設定來控制自動還原。 將此選項設為 True 時，從 Visual Studio 中執行組建會自動還原任何遺漏的套件。 此設定不會影響從 MSBuild 命令列執行的組建。

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

若要針對電腦上的所有使用者啟用或停用套件還原，開發人員或公司可以將組態設定新增到全域 `nuget.config` 檔案。 全域 `nuget.config` 是在 Windows 中的 `%ProgramData%\NuGet\Config`，有時在特定 `\{IDE}\{Version}\{SKU}\` Visual Studio 資料夾中，或在 Mac/Linux 的 `~/.local/share`。 個別使用者接著可以視需要選擇性地啟用專案層級的還原。 如需 NuGet 如何排定多個組態檔優先順序的詳細資料，請參閱[常見的 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

> [!Important]
> 如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓 [選項]  對話方塊顯示目前的值。

## <a name="constrain-package-versions-with-restore"></a>使用還原來限制套件版本

NuGet 透過任何方法還原套件時，會使用 `packages.config` 或專案檔中所指定的任何條件約束：

- 在 `packages.config` 中，您可以在相依性的 `allowedVersion` 屬性中指定版本範圍。 如需詳細資訊，請參閱[限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如：

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- 在專案檔中，您可以使用 PackageReference 來直接指定相依性的範圍。 例如：

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。

## <a name="force-restore-from-package-sources"></a>強制從套件來源還原

根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有描述。

若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：

- 使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾。
- 使用下列其中一種方法，在還原作業之前暫時變更 *global-packages* 資料夾的位置：
  - 將 NUGET_PACKAGES 環境變數設定為不同資料夾。
  - 建立將 `globalPackagesFolder` (如果使用 PackageReference) 或 `repositoryPath` (如果使用 `packages.config`) 設定為不同資料夾的 `NuGet.Config` 檔案。 如需詳細資訊，請參閱[組態設定](../reference/nuget-config-file.md#config-section)。
  - 僅限 MSBuild：使用 `RestorePackagesPath` 屬性來指定不同資料夾。

若要避免使用 HTTP 來源的快取，請執行下列任一步驟：

- 使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。 這些選項不會影響透過 Visual Studio 套件管理員或主控台進行的還原作業。
- 使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。
- 暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。

## <a name="troubleshooting"></a>疑難排解

請參閱[針對套件還原進行疑難排解](package-restore-troubleshooting.md)。
