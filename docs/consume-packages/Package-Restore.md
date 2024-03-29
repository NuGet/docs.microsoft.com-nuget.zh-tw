---
title: NuGet 套件還原
description: NuGet 如何還原專案相依套件的概觀，包括如何停用還原和限制版本。
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 6cdc826c85f233c7108a53ad244aa8c47df0be67
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901833"
---
# <a name="restore-packages-using-package-restore"></a>使用套件還原還原套件

為了提倡更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原** 會依專案檔或 `packages.config` 中所列，安裝專案的所有相依性。 .NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令會執行自動套件還原。 Visual Studio 可以在建置專案時自動還原套件，您可以隨時透過 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild 來還原套件。

套件還原會確認專案的所有相依性都可用，而不必將它們儲存在原始檔控制中。 若要設定原始程式碼控制存放庫以排除套件二進位檔，請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。 

## <a name="package-restore-overview"></a>套件還原概觀

套件還原會先視需要安裝專案的直接相依性，然後在整個相依性關係圖中安裝那些套件的任何相依性。

如果尚未安裝套件，NuGet 會先嘗試從[快取](../consume-packages/managing-the-global-packages-and-cache-folders.md)中擷取它。 如果套件不在快取中，則 nuget 會嘗試從 [**工具**  >  **選項**]  >  **nuget 封裝管理員**  >  **套件來源** 的清單中的所有已啟用來源下載套件 Visual Studio。 在還原程序中，NuGet 會忽略套件來源的順序，且使用任一個最先回應要求的來源。 如需 NuGet 運作方式的詳細資訊，請參閱[常用的 NuGet 組態](Configuring-NuGet-Behavior.md)。 

> [!Note]
> 在所有來源檢查完畢前，NuGet 不會指出還原套件失敗。 到那時候，NuGet 只會針對清單中的最後一個來源回報失敗。 這項錯誤表示套件未出現在其他「任何」來源上，即使那些來源都未個別出現錯誤亦然。

## <a name="restore-packages"></a>還原套件

套件還原會嘗試將所有套件相依性安裝到符合專案檔 (*.csproj*) 或您的 *packages.config* 檔案中套件參考的正確狀態。 (在 Visual Studio 中，參考會出現在 [方案總管] 的 [相依性 \ NuGet] 或 [參考] 節點下。)

1. 如果專案檔中的套件參考是正確的，請使用您慣用的工具來還原套件。

   - [Visual Studio](#restore-using-visual-studio) ([自動還原](#restore-packages-automatically-using-visual-studio)或[手動還原](#restore-packages-manually-using-visual-studio))
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   如果專案檔 (*.csproj*) 或您的 *packages.config* 檔案中的套件參考不正確 (不符合您在套件還原之後所需的狀態)，則您需要改為安裝套件或更新套件。

   針對使用 PackageReference 的專案，在成功還原之後，套件應該會出現在 [global-packages] 資料夾中，而且 `obj/project.assets.json` 檔案會重新建立。 針對使用 `packages.config` 的專案，套件應該會出現在專案的 `packages` 資料夾中。 專案現在應可順利建置。 

2. 如果您在執行套件還原之後，仍然遇到缺少套件或套件相關的問題 (例如 Visual Studio 方案總管中的錯誤圖示)，建議您遵循[對套件還原錯誤進行疑難排解](package-restore-troubleshooting.md)中的指示，或者[重新安裝並更新套件](../consume-packages/reinstalling-and-updating-packages.md)。

   在 Visual Studio 中，套件管理員主控台提供幾個彈性的選項來重新安裝套件。 請參閱[使用 Package-Update](reinstalling-and-updating-packages.md#using-update-package)。

## <a name="restore-using-visual-studio"></a>使用 Visual Studio 進行還原

在 Windows 的 Visual Studio 中：

- 自動還原套件，或

- 手動還原套件

### <a name="restore-packages-automatically-using-visual-studio"></a>使用 Visual Studio 自動還原套件

套件還原會在您從範本建立專案或建置專案時自動進行，且受限於[啟用和停用套件還原](#enable-and-disable-package-restore-in-visual-studio)中的選項。 在 NuGet 4.0+ 中，還原也會在您變更 SDK 樣式專案 (通常是 .NET Core 或 .NET Standard 專案) 時自動進行。

1. 選擇 [**工具**  >  **選項**]  >  **NuGet 封裝管理員**，然後在 [**套件還原**] 下的 Visual Studio 中選取 [在 **組建期間自動檢查遺漏的套件**]，以啟用自動套件還原。

   針對非 SDK 樣式的專案，您必須先選取 [允許 NuGet 下載遺漏的套件 ] 以啟用自動還原選項。

1. 建置專案。

   如果一或多個個別套件仍未正確安裝，則 [方案總管] 會顯示錯誤圖示。 以滑鼠右鍵按一下並選取 [管理 NuGet 套件]，且使用 [套件管理員] 先解除安裝再重新安裝受影響的套件。 如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)

   如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore-in-visual-studio)。 針對較舊的專案，另請參閱[移轉至自動套件還原](#migrate-to-automatic-package-restore-visual-studio)。 另請參閱 [套件還原疑難排解](Package-restore-troubleshooting.md)。

### <a name="restore-packages-manually-using-visual-studio"></a>使用 Visual Studio 手動還原套件

1. 選擇 [**工具**  >  **選項**]  >  **NuGet 封裝管理員** 來啟用套件還原。 在 [套件還原] 選項下，選取 [允許 NuGet 下載遺漏的套件]。

1. 在 [方案總管] 中，請以滑鼠右鍵按一下解決方案，然後選取 [還原 NuGet 套件]。

   如果一或多個個別套件仍未正確安裝，則 [方案總管] 會顯示錯誤圖示。 以滑鼠右鍵按一下並選取 [管理 NuGet 套件]，然後使用 [套件管理員] 先解除安裝再重新安裝受影響的套件。 如需詳細資訊，請參閱[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)

   如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請[啟用自動還原](#enable-and-disable-package-restore-in-visual-studio)。 針對較舊的專案，另請參閱[移轉至自動套件還原](#migrate-to-automatic-package-restore-visual-studio)。 另請參閱 [套件還原疑難排解](Package-restore-troubleshooting.md)。

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>在 Visual Studio 中啟用及停用套件還原

在 Visual Studio 中，您主要是透過 [**工具**  >  **選項**]  >  **NuGet 封裝管理員** 來控制套件還原：

![透過 NuGet 套件管理員選項控制套件還原](media/Restore-01-AutoRestoreOptions.png)

- **允許 NuGet 下載遺漏的套件** 會藉由變更 `NuGet.Config` 檔案 (在 Windows 上為 `%AppData%\NuGet\`，在 Mac/Linux 上則為 `~/.nuget/NuGet/`) [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 設定，控制所有形式的套件還原。 此設定也會啟用 Visual Studio 中解決方案操作功能表上的 [還原 NuGet 套件] 命令。

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

- **在 Visual Studio 建置期間自動檢查遺漏的套件** 會藉由變更 `NuGet.Config` 檔案 [packageRestore 區段](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 設定來控制自動還原。 將此選項設為 True 時，從 Visual Studio 中執行組建會自動還原任何遺漏的套件。 此設定不會影響從 MSBuild 命令列執行的組建。

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
> 如果您 `packageRestore` 直接在中編輯設定 `nuget.config` ，請重新開機 Visual Studio，如此 [ **選項** ] 對話方塊就會顯示目前的值。

### <a name="choose-default-package-management-format"></a>選擇預設封裝管理格式

![透過 NuGet 封裝管理員選項來控制預設封裝管理格式](media/Restore-02-PackageFormatOptions.png)

NuGet 有兩種格式，可供專案使用套件： [`PackageReference`](package-references-in-project-files.md) 和 [`packages.config`](../reference/packages-config.md) 。 您可以從 **套件管理** 標題底下的下拉式清單中選取預設格式。 也可以使用在專案中安裝第一個套件時的提示選項。

> [!Note]
> 如果專案不支援這兩種套件管理格式，則使用的封裝管理格式將會是與專案相容的格式，因此可能不是選項中的預設設定。 此外，即使在 [選項] 視窗中選取了選項，NuGet 也不會在第一次安裝套件時提示您選擇。
>
> 如果使用封裝管理員主控台在專案中安裝第一個套件，即使在 [選項] 視窗中選取選項，NuGet 也不會提示選擇格式。

## <a name="restore-using-the-dotnet-cli"></a>使用 dotnet CLI 進行還原

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> 若要將遺漏的套件參考新增至專案檔，請使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)，這也會執行 `restore` 命令。

## <a name="restore-using-the-nugetexe-cli"></a>使用 nuget.exe CLI 進行還原

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> 此 `restore` 命令不會修改專案檔或 *packages.config*。若要加入相依性，請在 Visual Studio 中透過封裝管理員 UI 或主控台加入封裝，或修改 *packages.config* 然後執行 `install` 或 `restore` 。

## <a name="restore-using-msbuild"></a>使用 MSBuild 進行還原

使用 [msbuild-t:restore](../reference/msbuild-targets.md#restore-target) 命令來還原專案檔中所列的套件 (請參閱 [PackageReference](package-references-in-project-files.md)) 並開始使用 msbuild 16.5 +、 `packages.config` 專案。

 這個命令只適用於 NuGet 4.x+ 和 MSBuild 15.1+ (兩者均隨附於 Visual Studio 2017 和更新版本)。
從 MSBuild 16.5 + 開始，此命令也可以 `packages.config` 在執行時還原為基礎的專案 `-p:RestorePackagesConfig=true` 。

1. 開啟開發人員命令提示字元 (在 [搜尋] 方塊中，輸入 **開發人員命令提示字元**)。

   您通常想要從 [開始] 功能表啟動適用於 Visual Studio 的開發人員命令提示字元，因為它將使用適用於 MSBuild 的所有必要路徑來設定。

2. 切換至包含專案檔的資料夾，並輸入下列命令。

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. 輸入下列命令以重建專案。

   ```cmd
   msbuild
   ```

   確定 MSBuild 輸出會指出組建已順利完成。
   
> [!Note]
> msbuild 具有 `-restore` 會執行 `Restore` 、重載專案，然後建立的參數。 請參閱 [使用一個 MSBuild 命令來還原和建立](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command)。

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>使用 Azure Pipelines 進行還原

在 Azure Pipelines 中建立組建定義時，在定義中於任何建置工作之前包含 NuGet [還原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)或 .NET Core [還原](/azure/devops/pipelines/tasks/build/dotnet-core-cli)工作。 根據預設，一些建置範本已包含還原工作。

## <a name="restore-using-azure-devops-server"></a>使用 Azure DevOps Server 進行還原

Azure DevOps Server 和 TFS 2013 及更新版本會在建置期間自動還原套件，前提是您使用 TFS 2013 或更新版本的 Team Build 範本。 針對較舊的 TFS 版本，您可以包含一個建置步驟來執行命令列還原選項，或選擇性地將建置範本移轉至較新版本。 如需詳細資訊，請參閱[使用 Team Foundation Build 的套件還原設定](../consume-packages/team-foundation-build.md)。

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

在所有情況下，都請使用[套件版本控制](../concepts/package-versioning.md)中所述的標記法。

## <a name="force-restore-from-package-sources"></a>強制從套件來源還原

根據預設，NuGet 還原作業會使用來自 *global-packages* 和 *http-cache* 資料夾的套件，這在 [管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中有描述。

若要避免使用 *global-packages* 資料夾，請執行下列任一步驟：

- 使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除資料夾。
- 使用下列其中一種方法，在還原作業之前暫時變更 *全域套件* 資料夾的位置：
  - 將 NUGET_PACKAGES 環境變數設定為不同資料夾。
  - 建立將 `globalPackagesFolder` (如果使用 PackageReference) 或 `repositoryPath` (如果使用 `packages.config`) 設定為不同資料夾的 `NuGet.Config` 檔案。 如需詳細資訊，請參閱[組態設定](../reference/nuget-config-file.md#config-section)。
  - 僅限 MSBuild：請使用屬性指定不同的資料夾 `RestorePackagesPath` 。

若要避免使用 HTTP 來源的快取，請執行下列任一步驟：

- 使用 `-NoCache` 選項搭配 `nuget restore`，或 `--no-cache` 選項搭配 `dotnet restore`。 這些選項不會影響透過 Visual Studio 套件管理員或主控台進行的還原作業。
- 使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear`清除快取。
- 暫時將 NUGET_HTTP_CACHE_PATH 環境變數設定為不同資料夾。

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>遷移至自動套件還原 (Visual Studio)

針對 NuGet 2.6 和更早版本，先前支援的 MSBuild 整合套件還原已不再適用。 (通常是在 Visual Studio 中以滑鼠右鍵按一下解決方案，然後選取 [啟用 NuGet 套件還原] 來啟用)。 如果您的專案是使用整合 MSBuild 套件還原，請遷移至自動套件還原。

使用 MSBuild-Integrated 套件還原的專案通常會包含包含三個檔案的 *. nuget* 資料夾： *NuGet.config*、 *nuget.exe* 和 *nuget.exe*。 存在 *nuget .targets* 檔案時，會判斷 nuget 是否會繼續使用 MSBuild 整合的方法，因此必須在遷移期間移除此檔案。

若要遷移至自動套件還原：

1. 關閉 Visual Studio。
2. 刪除 *.nuget/nuget.exe* 和 *.nuget/NuGet.targets*。
3. 針對每個專案檔，移除 `<RestorePackages>` 元素，並移除任何對 *NuGet.targets* 的參考。

若要測試自動套件還原：

1. 將 [packages] 資料夾從解決方案中移除。
2. 在 Visual Studio 中開啟方案，並啟動建置。

   自動套件還原應該會下載並安裝每個相依性套件，而不會將他們新增至原始檔控制。

## <a name="troubleshooting"></a>疑難排解

請參閱[針對套件還原進行疑難排解](Package-restore-troubleshooting.md)。
