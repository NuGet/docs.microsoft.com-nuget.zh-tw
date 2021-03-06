---
title: 尋找及選擇 NuGet 套件
description: 如何尋找和選擇專案之最佳 NuGet 套件的概觀，包含 NuGet 搜尋語法的詳細資料。
author: JonDouglas
ms.author: jodou
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 4ba51028c1a69a3466cec655db19c2c498e29d9b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775181"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>尋找和評估您專案的 NuGet 套件

啟動任何 .NET 專案時，或只要識別到您應用程式或服務的功能需求時，就可以使用滿足這項需求的現有 NuGet 套件來節省大量時間和麻煩。 這些套件可以來自 [nuget.org](https://www.nuget.org/packages/) 上的公用集合，或是您組織或其他協力廠商所提供的私人來源。

## <a name="finding-packages"></a>尋找套件

當您造訪 nuget.org 或在 Visual Studio 中開啟封裝管理員 UI 時，您會看到依相關性排序的套件清單。 這會顯示所有 .NET 專案內最廣泛使用的套件。 其中某些套件很有可能適合您自己的專案！

![顯示最常用套件的 nuget.org/套件的預設檢視](media/Finding-01-Popularity.png)

在 nuget.org 上，請注意頁面右上方的 [ **篩選** ] 按鈕。 按一下時，[先進搜尋] 面板會展開以顯示排序和篩選選項。

![nuget.org 上 'json' 的搜尋結果](media/Finding-02-SearchResults.png)

您可以使用 [ **封裝類型** ] 篩選來顯示特定類型的封裝：
- **`All types`**：這是預設行為。 它會顯示所有套件，不論其類型為何。
- **`Dependency`**：可安裝至您專案的一般 NuGet 套件。
- **`.NET tool`**：這會篩選至 [.net 工具](/dotnet/core/tools/global-tools)，這是包含主控台應用程式的 NuGet 套件。
- **`Template`**：這會篩選至 [.net 範本](/dotnet/core/install/templates)，可以用來建立使用命令的新專案 [`dotnet new`](/dotnet/core/tools/dotnet-new) 。

您可以使用 [ **排序依據** ] 選項來排序搜尋結果：
- **`Relevance`**：這是預設行為。 它會根據內部計分演算法來排序結果。
- **`Downloads`**：依下載總數（以遞減順序）排序搜尋結果。
- **`Recently updated`**：根據最新版本的建立日期，以遞減的時間順序排序搜尋結果。

在 [ **選項** ] 區段中，我們可以找到該 **`Include prerelease`** 核取方塊。
若有選取時，nuget.org 會顯示所有套件版本，包括發行前版本。 若只要顯示穩定的版本，請清除此選項。

若要套用搜尋篩選準則，請按一下 **`Apply`** 按鈕。 您隨時都可以按一下按鈕，回到預設行為 **`Reset`** 。

您也可以使用 [搜尋語法](#search-syntax) 來篩選標記、擁有者和封裝識別碼。

### <a name="does-the-package-support-my-projects-target-framework"></a>套件支援我專案的目標架構嗎？

只有在套件支援的架構包含專案的目標架構時，NuGet 才會將該套件安裝至專案  如果套件不相容，NuGet 就會發出錯誤。

部分套件會直接在 nuget.org 資源庫中列出其支援的架構，但因為不需要這類資料，所以許多套件都不會包含該清單。 目前沒有方法可以搜尋 nuget.org 中是否有支援特定目標架構的套件 (這項功能已列入考量，請參閱 [NuGet 問題 2936](https://github.com/NuGet/NuGetGallery/issues/2936))。

幸運的是，您可以透過其他兩種方法來判斷支援的架構：

1. 嘗試使用 NuGet 封裝管理員主控台中的命令，將套件安裝到專案 [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) 中。 如果套件不相容，則此命令會顯示套件所支援的架構。

1. 使用 [資訊] 下的 [手動下載] 連結，以從套件在 nuget.org 上的頁面下載套件。 將副檔名從 `.nupkg` 變更為 `.zip`，並開啟檔案來檢查其 `lib` 資料夾的內容。 您會在那裡看到每個所支援架構的子資料夾，其中使用目標 Framework Moniker (TFM；請參閱[目標 Framework](../reference/target-frameworks.md)) 來命名每個子資料夾。 如果您在 `lib` 下看不到任何子資料夾，而且只有單一 DLL，則必須嘗試將套件安裝至您的專案，以探索其相容性。

## <a name="pre-release-packages"></a>發行前套件

許多套件作者都會將預覽和搶鮮版 (Beta) 版本設為可用，因為他們會繼續進行改善並搜尋其最新版本的意見。

nuget.org 預設會在搜尋結果中顯示發行前套件。 若只要搜尋穩定的版本，請清除 [高級搜尋] 面板中的 [ **包含發行** 前版本] 選項，該選項可從頁面右上方的 [ **篩選** ] 按鈕存取。

![nuget.org 上的 [包含發行前版本] 核取方塊](media/Finding-06-include-prerelease.png)

在 Visual Studio 中，並且使用 NuGet 和 dotnet CLI 工具時，NuGet 預設不會包含發行前版本。 若要變更此行為，請執行下列步驟：

- **Visual Studio 中的套件管理員 UI**：在 [管理 NuGet 套件] UI 中，設定 [包含發行前版本] 方塊。 設定或清除此方塊時，會重新整理套件管理員 UI 以及您可以安裝的可用版本清單。

    ![Visual Studio 的 [包含發行前版本] 核取方塊](media/Prerelease_02-CheckPrerelease.png)

- **封裝管理員主控台**：使用 `-IncludePrerelease` 參數搭配、、 `Find-Package` `Get-Package` `Install-Package` 、 `Sync-Package` 和 `Update-Package` 命令。 請參閱 [PowerShell 參考](../reference/powershell-reference.md)。

- **nuget.exe CLI**：搭配 `-prerelease` `install` 、 `update` 、 `delete` 和命令使用參數 `mirror` 。 請參閱 [NuGet CLI 參考](../reference/nuget-exe-cli-reference.md)

- **dotnet.exe CLI** 使用 `-v` 引數指定確切的發行前版本。 請參閱 [dotnet 新增套件參考](/dotnet/core/tools/dotnet-add-package)。

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>原生 C++ 套件

NuGet 支援可在 Visual Studio 中用於 C++ 專案的原生 C++ 套件。 這會啟用專案的 [管理 NuGet 套件] 操作功能表命令、引進 `native` 目標架構，並提供 MSBuild 整合。

若要在 [nuget.org](https://www.nuget.org/packages) 上尋找原生套件，請使用 `tag:native` 進行搜尋。 這類套件一般會提供 `.targets` 和 `.props` 檔案，而 NuGet 會在將套件新增至專案時自動匯入這些檔案。

## <a name="evaluating-packages"></a>評估套件

評估套件實用性的最佳方法是下載套件並以您的代碼加以試用 (順帶一題，nuget.org 上的所有套件都會定期掃描病毒)。 畢竟，只有少數使用高度常用之套件的開發人員才能啟動高度常用的套件，而且您可能是早期採用者 

同時，使用 NuGet 套件表示與其相依，因此您想要確定其為穩定且可靠。 因為安裝和直接測試套件相當耗時，所以您也可以使用套件清單頁面上的資訊來深入了解套件品質：

- **下載統計資料**：在 nuget.org 的套件頁面上，[統計資料] 區段會顯示總下載次數、最新版的下載，以及每天的平均下載次數。 較大的數字指出許多其他開發人員都具有與套件的相依性，這表示它已證明它自己。

    ![下載套件清單頁面上的統計資料](media/Finding-03-Downloads.png)

- **消費者**：在 [套件] 頁面上，[ **消費者** ] 區段會列出相依于此套件的前5個最受歡迎的 NuGet.org 套件和熱門的 GitHub 存放庫。 相依于此套件的套件和存放庫可以稱為此封裝的「相依項」。 相依套件和存放庫可以視為此封裝的「簽署」，因為套件作者已選擇信任並相依于該套件。
  - 相依套件必須依存于此封裝的 *最新穩定版本* 中的 *任何版本*。 這項定義可確保顯示的相依套件是封裝作者決定要信任且相依于此套件的最新反映。 未列出預先發行版本相依性，因為它們尚未被視為全 hero endoresements。 請參閱下表中的範例：

    | 封裝版本 | 封裝 A 列為套件 B 的相依專案？ |
    |-|-|
    | 1.0.0 版<br>v 1.1.0 (最新的穩定) --> 套件 B<br>v 1.2.0-預覽 | TRUE，最新穩定版本取決於套件 B |
    | 1.0.0 版--> 套件 B<br>v 1.1.0 (最新的穩定) <br>v 1.2.0-預覽 | FALSE，最新的穩定版本不相依于套件 B |
    | 1.0.0 版--> 套件 B<br>v 1.1.0 (最新的穩定) <br>v 1.2.0-預覽--> 套件 B | FALSE，最新的穩定版本不相依于套件 B |

  - GitHub 存放庫的星星數目通常表示該存放庫與 GitHub 使用者的熱門程度 (更多星星通常表示較熱門的) 。 如需 GitHub 的星星和儲存機制排名系統的詳細資訊，請造訪 [github 的開始使用頁面](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) 。

    ![消費者](media/Used-By-section-Humanizer.png)

    > [!Note]
    > 區段所使用的套件會定期自動產生，而不需要個別存放庫的人工審核，而且僅供資訊性用途，以顯示相依于封裝的 NuGet.org 套件和熱門 GitHub 存放庫。

- **版本歷程記錄**：在 [套件] 頁面上，在 [ **資訊** ] 下方尋找最新的更新日期，並檢查 **版本歷程記錄**。 維護良好的套件具有新的更新和豐富的版本歷程記錄。 忽略的套件有幾個更新，而且有時通常尚未更新。

    ![套件清單頁面上的版本歷程記錄](media/Finding-04-VersionHistory.png)

- **最近安裝**：在 [封裝] 頁面的 [ **統計資料]** 底下，選取 [ **View full stats**]。[完整統計資料] 頁面會顯示過去六周的套件安裝（依版本號碼）。 其他開發人員主動使用的套件一般是比未使用的套件還適合的選擇。

- **支援**：在套件頁面的 [資訊] 下方，選取 [專案網站] \(如果有的話) 以查看作者提供的支援選項。 具有專用網站的專案通常有較佳的支援。

- **開發人員歷程記錄**：在套件頁面的 [擁有者] 下方，選取擁有者以查看他們已發行的其他套件。 具有多個套件的擁有者未來較可能繼續支援其工作。

- **開放原始碼參與**：開放原始碼存放庫會維護許多套件，因此與其相依的開發人員可以直接參與 Bug 修正和功能改善。 任何指定套件的參與歷程記錄也是有多少開發人員主動參與的不錯指標。

- **訪談擁有者**：可以肯定平均認可新的開發人員，以產生您可使用的不錯套件，讓它們有機會帶入 NuGet 生態系統的新項目。 請記住，透過清單頁面的 [資訊] 下方的 [連絡擁有者] 選項直接聯繫套件開發人員。 而且他們很樂意與您合作來滿足您的需求！

- **保留的套件識別碼首碼**：許多套件擁有者已申請並獲得 [保留的套件識別碼首碼](../nuget-org/id-prefix-reservation.md)。 當您在 [nuget.org](https://www.nuget.org/) 上或 Visual Studio 中看到套件識別碼旁出現視覺核取標記時，表示套件擁有者已符合我們的識別碼首碼保留[準則](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)。 這表示套件擁有者已明確識別自身及其套件。

> [!Note]
> 一律留意套件的授權條款，您可以在 nuget.org 上的套件清單頁面上選取 **授權資訊** 來查看套件的授權條款。如果封裝未指定授權條款，請使用 [封裝] 頁面上的 [ **連絡人擁有** 者] 連結，直接聯絡封裝擁有者。 Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。

## <a name="license-url-deprecation"></a>授權 URL 過時
當我們從 [licenseUrl](../reference/nuspec.md#licenseurl) 轉換到 [license](../reference/nuspec.md#license) 時，某些 NuGet 用戶端與 NuGet 摘要可能還沒有在某些案例中呈現授權資訊的能力。 為維護回溯相容性，授權 URL 會指向此文件，此文件說明如何在此案例中擷取授權資訊。

若按一下套件的授權 URL 將您帶向此頁面，即表示套件包含授權檔案且
* 您已連線到不知道如何解譯並呈現新授權資訊給用戶端的摘要 **或**
* 您正在使用還不知道如何解譯並讀取可能由摘要提供之新授權資訊的用戶端 **或**
* 上列兩者的組合

以下說明如何讀取套件內之授權檔案中包含的資訊：
1. 下載 NuGet 套件並將其內容解壓縮到資料夾。
1. 開啟位於資料夾根目錄的 `.nuspec` 檔案。
1. 它應該有如 `<license type="file">license\license.txt</license>` 的標記。 這意指授權檔案的名稱是 `license.txt` 且它位於稱為 `license` 的資料夾 (也位於資料夾的根目錄) 內。
1. 瀏覽到 `license` 資料夾並開啟 `license.txt` 檔案。

如果 MSBuild 相當於在 `.nuspec` 中設定授權，請參閱[封裝授權運算式或授權檔案](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)。

## <a name="search-syntax"></a>搜尋語法

在 nuget.org 上、從 NuGet CLI 中，以及 Visual Studio 的 NuGet 套件管理員延伸模組內，NuGet 套件搜尋的運作都相同。 一般而言，會將搜尋套用至關鍵字和套件描述。

- **篩選**：您可以使用不 `<property>:<term>` `<property>` 區分大小寫的 () 可以是 `id` 、、 `packageid` `version` 、 `title` `tags` `author` `description` `summary` `owner` 、、、、和的語法，將搜尋詞彙套用至特定屬性。 您可以同時搜尋多個屬性。 在屬性上搜尋會比對 `id` 子字串，而會 `packageid` `owner` 使用完全不區分大小寫的相符專案。 範例：

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
