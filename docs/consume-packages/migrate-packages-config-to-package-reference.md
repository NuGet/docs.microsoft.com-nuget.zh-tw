---
title: 從 packages.config 遷移至 PackageReference 格式
description: 詳細說明如何將專案從 packages.config 管理格式遷移至 NuGet 4.0 + 和 VS2017 和 .NET Core 2.0 所支援的 PackageReference
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8161f4a39d4adfdb9efb25bcb840b20b85a58e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774782"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>從 package.config 移轉到 PackageReference

Visual Studio 2017 15.7 版和更新版本支援將專案從 [packages.config](../reference/packages-config.md) 管理格式移轉到 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的優點

* **在一個位置管理所有專案** 相依性：就像專案對專案參考和元件參考一樣，使用節點)  (的 NuGet 套件參考 `PackageReference` 會直接在專案檔內進行管理，而不是使用個別的 packages.config 檔。
* **最上層相依性的整齊觀點**：不同于 packages.config，PackageReference 只會列出您直接安裝在專案中的 NuGet 套件。 因此，NuGet 套件管理員 UI 和專案檔不會因包含下層相依性而變得雜亂。
* **效能改進**：使用 PackageReference 時，套件會保留在 *全域套件* 資料夾中 (如 [管理全域封裝和](../consume-packages/managing-the-global-packages-and-cache-folders.md) 快取資料夾，而不是在方案內的資料夾中所述 `packages` 。 因此，PackageReference 執行較快，且耗用較少磁碟空間。
* **對相依性和內容流程的精確控制**：使用 MSBuild 的現有功能，可讓您有 [條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ，並為每個目標 framework、設定、平臺或其他透視表選擇套件參考。
* **PackageReference 正在進行開發**：請參閱 [GitHub 上的 PackageReference 問題](https://aka.ms/nuget-pr-improvements)。 packages.config 已不再進行開發。

### <a name="limitations"></a>限制

* 在 Visual Studio 2015 與更早版本中，無法使用 NuGet PackageReference。 已移轉專案只能在 Visual Studio 2017 與更新版本中開啟。
* 移轉目前不適用於 C++ 和 ASP.NET 專案。
* 某些套件可能無法與 PackageReference 完全相容。 如需詳細資訊，請參閱[套件相容性問題](#package-compatibility-issues)。

此外，相較于 packages.config，PackageReferences 的運作方式會有一些差異。例如，PackageReference 不會 supprted [限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) ，但會新增 [浮動版本](../consume-packages/package-references-in-project-files.md#floating-versions)的支援。

### <a name="known-issues"></a>已知問題

1. 滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項 

#### <a name="issue"></a>問題 
 
當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。 這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。 

#### <a name="workaround"></a>因應措施 

執行以下任何一個 NuGet 動作： 
* 開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...` 
* 開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console` 
* 執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages` 
* 建置專案也會觸發 NuGet 還原 

您現在應該可以看到移轉選項。 請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。 

## <a name="migration-steps"></a>移轉步驟

> [!Note]
> 移轉開始之前，Visual Studio 會建立專案的備份，以允許您在必要時[復原到 packages.config](#how-to-roll-back-to-packagesconfig)。

1. 開啟包含使用 `packages.config` 之專案的解決方案。

1. 在 [方案總管] 中，以滑鼠右鍵按一下 [參考] 節點或 `packages.config` 檔案，然後選取 [將 packages.config 移轉至 PackageReference]。

1. 移轉程式會分析專案的 NuGet 套件參考，並嘗試將它們分類成 **頂層相依性** (您直接安裝的 NuGet 套件) 與 **可轉移的相依性** (已安裝為頂層套件相依性的套件)。

   > [!Note]
   > PackageReference 支援可轉移套件還原，且會動態地解析相依性，這表示不需要明確地安裝可轉移的相依性。

1. (選擇性) 您可以選取 NuGet 套件的 [頂層] 選項，將套件分類為頂層可轉移的相依性。 針對包含無法轉移的資產 (在 `build`、`buildCrossTargeting`、`contentFiles` 或 `analyzers` 資料夾中) 的套件，以及標示為開發相依性 (`developmentDependency = "true"`) 的套件，系統會自動為它們設定此選項。

1. 檢閱任何[套件相容性問題](#package-compatibility-issues)。

1. 選取 [確定] 來開始移轉。

1. 當移轉結束時，Visual Studio 會提供一份報告，其中包含備份的路徑、已安裝套件的清單 (頂層相依性)、參考為可轉移相依性之套件的清單，以及在開始移轉時識別出的相容性問題。 報表會儲存至 [backup] 資料夾。

1. 驗證解決方案可建置並執行。 如果您遇到問題，請[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何復原為 packages.config

1. 關閉已移轉專案。

1. 將專案檔與 `packages.config` 從備份 (通常在 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 複製到專案資料夾。 如果 obj 資料夾存在於專案根目錄中，請將它刪除。

1. 開啟專案。

1. 使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 功能表命令來開啟 [套件管理器主控台]。

1. 在主控台中，執行下列命令：

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>移轉之後建立套件

完成移轉之後，建議您新增 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) \(英文\) nuget 套件的參考，然後使用 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) 來建立套件。 雖然在某些情況下，您可以使用 `dotnet.exe pack` 而不是 `msbuild -t:pack`，但不建議這麼做。

## <a name="package-compatibility-issues"></a>套件相容性問題

PackageReference 中不支援某些在 packages.config 中支援的層面。 移轉程式會分析並偵測此類問題。 有一或多個下列問題的任何套件，在移轉之後可能不會如預期般運作。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>當套件是在移轉之後安裝時，系統會忽略 "install. ps1" 指令碼

| | |
| --- | --- |
| **說明** | 使用 PackageReference 時，在安裝套件或將套件解除時，不會執行 install.ps1 與 uninstall.ps1 PowerShell 指令碼。 |
| **潛在影響** | 相依於這些指令碼以在目的專案中設定某些行為的套件，可能無法如預期般運作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>當套件是在移轉之後安裝時，會無法使用「內容」資產

| | |
| --- | --- |
| **說明** | PackageReference 不支援在套件的 `content` 資料夾中的資產，因此系統會忽略它們。 PackageReference 新增對 `contentFiles` 的支援，以獲得更好的可轉移支援和共用內容。  |
| **潛在影響** | `content` 中的資產未複製到專案中，且依賴那些資產存在的專案程式碼必須重構。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>當套件是在升級後安裝時，不會套用 XDT 轉換

| | |
| --- | --- |
| **說明** | PackageReference 不支援 XDT 轉換，而且在安裝套件或將套件解除安裝時，系統會忽略 `.xdt` 檔案。   |
| **潛在影響** | XDT 轉換不會套用至任何專案 XML 檔案，最常見的是 `web.config.install.xdt` 與 `web.config.uninstall.xdt`，這表示專案的 ` web.config` 檔案，沒有在安裝套件或將套件解除安裝時更新。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>當套件是在遷移之後安裝時，系統會忽略 lib 根目錄中的組件

| | |
| --- | --- |
| **說明** | 使用 PackageReference 時，系統會忽略出現在 `lib` 資料夾根目錄且沒有目標架構特定子資料夾的組件。 NuGet 會尋找與專案目標 Framework 對應之目標 Framework Moniker (TFM) 相符的子資料夾，並將相符的元件安裝到專案中。 |
| **潛在影響** | 若套件沒有與專案目標架構對應之目標 Framework Moniker (TFM) 相符的子資料夾，在移轉之後可能無法如預期般運作，或可能在移轉期間安裝失敗 |

## <a name="found-an-issue-report-it"></a>發現問題嗎？ 請回報！

如果您遇到移轉體驗的問題，請[在 NuGet GitHub 存放庫中提出問題](https://github.com/NuGet/Home/issues/) \(英文\)。
