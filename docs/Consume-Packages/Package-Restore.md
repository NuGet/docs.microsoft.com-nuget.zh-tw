---
title: "NuGet 套件還原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "描述 NuGet 如何還原專案所相依的套件，包含如何停用還原和限制版本。"
keywords: "NuGet 套件還原, NuGet 套件安裝, 安裝套件, 還原套件、相依性版本, 停用自動還原, 限制套件版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>套件還原

若要升級更乾淨的開發環境，以及降低存放庫大小，NuGet **套件還原**會先安裝所有參考的套件，再建置專案。 這項廣泛使用的功能可確保專案中具有所有相依性，而這些套件不需要儲存在原始檔控制中 (請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)，以了解如何設定存放庫排除套件二進位檔)。

本主題內容：
- [套件還原快速指南](#quick-guide-to-package-restore)
- [套件還原概觀](#package-restore-overview)
- [啟用和停用套件還原](#enabling-and-disabling-package-restore)
- [使用還原限制套件版本](#constraining-package-versions-with-restore)
- [命令列還原](#command-line-restore)，適用於所有版本的 NuGet
- [Visual Studio 中的自動還原](#automatic-restore-in-visual-studio)，適用於 NuGet 2.7 和更新版本。
- [Visual Studio 中的 MSBuild 整合還原](#msbuild-integrated-restore)，適用於 NuGet 2.6 和更早版本。
- [使用 Team Foundation Build 的套件還原](#package-restore-with-team-foundation-build)

還原行為會因版本而異；若要檢查 NuGet 版本，只需要在命令列上執行 `nuget.exe`，並查看輸出的第一行。

如需組建伺服器上套件還原的詳細資料，請參閱[使用 TFBuild 的套件還原](../consume-packages/team-foundation-build.md)。

> [!Note]
> 設定進行套件還原的專案也會與 Mono 上的 xbuild 搭配運作。

## <a name="quick-guide-to-package-restore"></a>套件還原快速指南

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> 如果您看到「此專案參考這部電腦上所缺少的 NuGet 套件」或「一或多個 NuGet 套件需要還原，但因未獲同意而無法進行」錯誤，請遵循[啟用和停用套件還原](#enabling-and-disabling-package-restore)下的指示來開啟自動還原。

## <a name="package-restore-overview"></a>套件還原概觀

首先，會使用下列其中一種套件管理格式來維護套件參考 (視專案類型和 NuGet 版本而定)  (請注意，NuGet 4 和 MSBuild 15.1 是與 Visual Studio 2017 一起安裝)。

| 方法 | NuGet 版本 | 描述 | 
| --- | --- | --- |
| `packages.config` | 2.x+ | 列出一組完整深層相依性。 新增至 `packages.config` 的套件也必須新增至專案檔，而且 [目標] 和 [屬性] 也必須新增至專案檔。 這是 NuGet 所有版本的基準方法，但與其他選項相較之下效能較慢。 (請參閱 [packages.config 結構描述](../schema/packages-config.md))。 | 
| `project.json` | 3.x+ | 預設只會與 UWP 專案搭配使用，但可以從 `packages.config` 轉換專案。 `project.json` 只會列出最上層相依性。 在建置期間會將參考、目標和屬性動態新增至專案，並與 `packages.config` 相較之下可產生更好的效能  (請參閱 [project.json 結構描述](../schema/project-json.md))。|
| PackageReference | 4.x+ | 直接在 `<PackageReference>` 節點以及 `<Reference>` 和 `<ProjectReference>` 的專案檔中列出相依性。 運作方式與 `project.json` 類似；請參閱[專案檔中的套件參考](../Consume-Packages/Package-References-in-Project-Files.md)。 |

其次，您透過各種方式，使用參考清單來開始還原：

從命令列或[套件管理員主控台](../tools/Package-Manager-Console.md)：

| 命令 | 適用的案例 |
| --- | --- | 
| `nuget restore` | 所有版本的 NuGet 和所有參考類型。 請參閱下方的[命令列還原](#command-line-restore)。 | 
| `dotnet restore` | 與 .NET Core 專案的 `nuget restore` 相同。 請參閱 [dotnet restore](/dotnet/articles/core/tools/dotnet-restore)。 |
| `msbuild /t:restore` | 僅限具有[專案檔中的套件參考](../Consume-Packages/Package-References-in-Project-Files.md)的 Nuget 4.x+ 和 MSBuild 15.1+。 `nuget restore` 和 `dotnet restore` 都會將這個命令用於適用的專案。 請參閱 [NuGet 封裝和還原為 MSBuild 目標 - 還原目標](../schema/msbuild-targets.md#restore-target)。|

Visual Studio 本身也會在不同的時間還原套件：

| 類型 | 進行還原的時機 |
| --- | --- |
| 範本還原 | 在建立新專案期間，某些範本與外部套件相依。 |
| 組建還原 | 為組建的第一個步驟。 |
| 方案還原 | 使用者以滑鼠右鍵按一下方案並選取 [還原 NuGet 套件] 時。 |
| 在專案變更時還原 | *(僅限 NuGet 4.x)* 使用 .NET Core SDK 專案時，包含專案狀態變更時。 |

## <a name="enabling-and-disabling-package-restore"></a>啟用和停用套件還原

套件還原主要是透過 Visual Studio 中的 [工具] > [選項] > [NuGet 套件管理員] 所啟用：

![透過 NuGet 套件管理員選項控制套件還原行為](media/Restore-01-AutoRestoreOptions.png)

- **允許 NuGet 下載遺漏的套件**：變更 `%AppData%\NuGet\NuGet.Config` 檔案中的 `packageRestore/enabled` 設定，以控制所有形式的套件還原，如下所示。

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
    

- **在 Visual Studio 建置期間自動檢查遺漏的套件**：變更 `%AppData%\NuGet\NuGet.Config` 檔案中的 `packageRestore/automatic` 設定，以控制 NuGet 2.7 和更新版本的自動還原，如下所示。
            
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

如需參考，請參閱 [NuGet 組態檔 - packageRestore 區段](../Schema/nuget-config-file.md#packagerestore-section)。

在某些情況下，根據預設，開發人員或公司可能想要啟用或停用電腦上所有使用者的套件還原。 做法是將上述相同設定新增至 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 的全域 NuGet 組態檔。 個別使用者接著可以視需要選擇性地啟用專案層級的還原。 如需 NuGet 如何設定多個組態檔優先順序的確切詳細資料，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

## <a name="constraining-package-versions-with-restore"></a>使用還原限制套件版本

NuGet 透過任何方法還原套件時，會使用 `packages.config`、`project.json` 或專案檔中所指定的任何條件約束：

- `packages.config`：指定相依性之 `allowedVersion` 屬性中的版本範圍。 請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如: 

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`：直接使用相依性的版本號碼來指定版本範圍。 例如: 

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- 專案檔中的套件參考：直接使用相依性的版本號碼來指定版本範圍。 例如: 
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

在所有情況下，都請使用[套件版本控制](../reference/package-versioning.md)中所述的標記法。

## <a name="command-line-restore"></a>命令列還原

針對 NuGet 2.7 和更新版本，使用 [Restore](../tools/cli-ref-restore.md) 命令，以還原方案中的所有套件 (無論是使用 `packages.config`、`project.json` 或是專案檔中的套件參考)。 針對 `c:\proj\app` 這類指定專案資料夾，其下的一般變異會還原套件：

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

針對 NuGet 4.0+ 和 MSBuild 15.1+，您也可以使用 `MSBuild /t:restore`，如 [NuGet 封裝和還原為 MSBuild 目標](../schema/msbuild-targets.md)中所述。

## <a name="build-time-restore-in-visual-studio"></a>Visual Studio 中的建置時間還原

Visual Studio 預設會在建置開始時自動還原遺漏的套件。 此行為的變更方式是清除 [工具] > [選項] > [NuGet 套件管理員] > [一般] > [在 Visual Studio 建置期間自動檢查遺漏的套件]。

啟用時，自動還原會如下運作：

1. 開始建置時，Visual Studio 會指示 NuGet 還原套件。
1. NuGet 會遞迴尋找方案中的所有 `packages.config` 檔案、尋找 `project.json` 或查看專案檔。
1. 針對參考檔案中所列的每個套件，NuGet 會檢查它是否已存在於方案中 (`packages` 資料夾、`project.lock.json` 或 `project.assets.json`，根據專案使用 `packages.config`、`project.json` 還是專案檔中的套件參考而定)。
1. 如果找不到套件，NuGet 會嘗試先從其快取擷取套件 (請參閱[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md))。 如果套件不在快取中，則 NuGet 會嘗試從 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 中所列的已啟用來源下載套件，而下載順序就是來源出現的順序。 在此情況下，除非已檢查所有來源，否則 NuGet 不會指出尋找套件失敗，而它在此時只會報告清單中最後一個來源的失敗。 這類錯誤也隱含表示套件未出現在任何其他來源上，即使未個別顯示這些來源的錯誤也是一樣。
1. 如果成功下載，則 NuGet 會快取套件，並將它安裝至方案 (同樣地安裝至 `packages` 資料夾、`project.lock.json` 或 `project.assets.json`)；否則 NuGet 會失敗，而且建置會失敗。

在此程序期間，您會看到內含取消套件還原選項的進度對話方塊。

## <a name="package-restore-with-team-foundation-build"></a>使用 Team Foundation Build 的套件還原

套件還原常用於在組建伺服器上建置專案時，與使用 Team Foundation Server (TFS) 和 Visual Studio Team Services 相同 (以及這裡未涵蓋的其他組建系統)。

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

在 Team Services 上建立組建定義時，只需要在定義中於任何建置工作之前包含「還原 NuGet 套件」工作。 在許多組建範本中，預設會包含此工作。

![Visual Studio Team Service 組建定義中的 NuGet 套件還原工作](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

使用 TFS 2013 和更新版本，在建置期間預設會自動還原套件，前提是您將 Team Build 範本用於 Team Foundation Server 2013 或更新版本。

如果您使用舊版的組建範本 (例如，在已從舊版 TFS 移轉的專案中)，則也需要將這些組建範本移轉至 TFS 2013。 這基本上表示使用原始檔控制 (TFVC 或 Git) 的適當範本來重建組建範本的自訂組件。

針對較早的 TFS 版本，您可以只包含可叫用[命令列還原](#command-line-restore)的建置步驟，如上所述。

如需詳細資料，請參閱[使用 Team Foundation Build 的套件還原逐步解說](../consume-packages/team-foundation-build.md)。    
