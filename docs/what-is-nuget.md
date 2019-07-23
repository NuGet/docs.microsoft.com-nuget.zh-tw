---
title: 什麼是 NuGet？它有哪些功能？
description: 何謂 NuGet 和其功能的完整介紹
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: e11eed5c614a7634fa578ebc84c3ab2068522fe2
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842196"
---
# <a name="an-introduction-to-nuget"></a>NuGet 簡介

任何新式開發平台的基本工具都是一種機制，而開發人員可以透過此機制建立、共用和使用實用的程式碼。 這類程式碼通常會打包成「套件」，其中包含已編譯程式碼 (如 DLL)，以及在取用這些套件之專案中所需的其他內容。

針對 .NET (包括 .NET Core)，Microsoft 支援的共用程式碼機制是 **NuGet**，它定義如何建立、裝載和取用 .NET 套件，並為這些角色的每一個[提供工具](install-nuget-client-tools.md)。

簡言之，NuGet 套件就是副檔名為 `.nupkg` 的單一 ZIP 檔案，內含已編譯程式碼 (DLL)、其他與該程式碼相關的檔案，以及包含套件版本號碼這類資訊的描述性資訊清單。 擁有要共用之程式碼的開發人員會建立套件，並將它們發行至公用或私人主機。 套件取用者會從適當的主機取得那些套件、將它們新增至其專案，然後在其專案程式碼中呼叫套件的功能。 NuGet 本身接著會處理所有中間詳細資料。

由於 NuGet 同時支援私人主機和公用 nuget.org 主機，因此，您可以使用 NuGet 套件來共用組織或工作群組專屬的程式碼。 您也可以使用 NuGet 套件作為一種簡便方式來建構自己的程式碼，僅供您自己的專案使用。 簡言之，NuGet 套件是一個可共用的程式碼單位，但不需要也不會暗示任何特殊的共用方式。

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>建立者、主機和取用者之間的套件流程

NuGet 的角色是公用主機，因此本身會在 [nuget.org](https://www.nuget.org) \(英文\) 維護具有超過 100,000 個獨特套件的中央存放庫。每天都會有數百萬位 .NET/.NET Core 開發人員採用這些套件。 NuGet 也讓您能夠在雲端 (例如在 Azure DevOps 上)、私人網路或甚至只是在本機檔案系統中，私下裝載套件。 如此一來，那些套件就只能供可存取該主機的開發人員使用，讓特定的取用者群組能夠使用套件。 [裝載您自己的 NuGet 摘要](hosting-packages/overview.md)會說明這些選項。 透過設定選項，您也可以完全控制哪些主機可以透過任何指定的電腦來存取，以確定可從諸如 nuget.org 之公用存放庫以外的特定來源取得套件。

不管其本質為何，主機都是作為套件「建立者」  與套件「取用者」  之間的聯繫點。 建立者會建置有用的 NuGet 套件，並將其發行至主機。 取用者接著會搜尋可存取主機上的實用和相容套件，並下載這些套件且將其包含在專案中。 一旦安裝於專案，套件的 API 就可供專案程式碼的其餘部分使用。

![套件建立者、套件主機與套件取用者之間的關聯性](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>套件目標相容性

「相容」套件表示它所包含的組件，是針對與取用專案之目標 Framework 相容的至少一個目標 .NET Framework 所建置的。 開發人員可以建立某種架構特有的套件 (就像使用 UWP 控制項)，或者，它們可以支援範圍更廣泛的目標。 開發人員為了讓套件有最大的相容性，會將目標設為所有 .NET 和 .NET Core 專案均可取用的 [.NET Standard](/dotnet/standard/net-standard)。 這對建立者與取用者而言是最有效率的方法，因為單一套件 (通常包含單一組件) 適用於所有取用專案。

相反地，需要 .NET Standard 以外之 API 的套件開發人員，會針對他們想要支援的不同目標 Framework 建立個別組件，並在相同套件中包含所有的那些組件 (稱為「多目標」)。 當取用者安裝這類套件時，NuGet 只會擷取專案所需的組件。 在該專案所產生的最終應用程式和 (或) 組件中，這可將套件的用量降到最低。 當然，多目標套件對其建立者而言就更難維護了。

> [!Note]
> 將目標設為 .NET Standard 會取代先前使用各種可攜式類別庫 (PCL) 目標的方法。 因此，本文件著重在如何建立適用於 .NET Standard 的套件。

## <a name="nuget-tools"></a>NuGet 工具

除了裝載支援之外，NuGet 也提供建立者和取用者都能使用的各種工具。 請參閱[安裝 NuGet 用戶端工具](install-nuget-client-tools.md)了解如何取得特定的工具。

| 工具 | 平台 | 適用的案例 | 說明 |
| --- | --- | --- | --- |
| [dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md) | All | 建立、使用 | 適用於 .NET Core 與 .NET Standard 程式庫，以及以 .NET Framework 為目標之 [SDK 樣式專案](resources/check-project-format.md)的 CLI 工具。 在 .NET Core 工具鏈內，直接提供特定 NuGet CLI 功能。 就像 NuGet CLI，dotnet CLI 不會與 Visual Studio 專案互動。 |
| [nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md) | All | 建立、使用 | 適用於 .NET Framework 程式庫與以 .NET Standard 程式庫為目標之[非 SDK 樣式專案](resources/check-project-format.md)的 CLI 工具。 提供所有 NuGet 功能，而且有些命令專門套用至套件建立者、有些命令只套用至取用者，其他命令則套用至兩者。 例如，套件建立者使用 `nuget pack` 命令以從各種組件和相關檔案建立套件、套件取用者使用 `nuget install` 以將套件納入專案資料夾，而每個人都使用 `nuget config` 來設定 NuGet 組態變數。 作為無從驗證平台的工具，NuGet CLI 不會與 Visual Studio 專案互動。 |
| [套件管理員主控台](tools/package-manager-console.md) | Windows 上的 Visual Studio | 使用 | 提供 [PowerShell 命令](tools/Powershell-Reference.md)，以在 Visual Studio 專案中安裝和管理套件。 |
| [套件管理員 UI](tools/package-manager-ui.md) | Windows 上的 Visual Studio | 使用 | 提供易於使用的 UI，以在 Visual Studio 專案中安裝和管理套件。 |
| [管理 NuGet UI](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 使用 | 提供易於使用的 UI，以在 Visual Studio for Mac 專案中安裝和管理套件。 |
| [MSBuild](reference/msbuild-targets.md) | Windows | 建立、使用 | 提供能夠建立套件，以及還原透過 MSBuild 工具鏈直接用於專案的套件的能力。 |

如您所見，您所使用的 NuGet 工具大部分取決於您是否正在建立、取用或發行套件，以及您的工作所在平台。 套件建立者通常也是取用者，因為他們是以其他 NuGet 套件的現有功能為建置基礎。 當然，這些套件可能接著會與其他項目相依。

如需詳細資訊，請從[套件建立工作流程](create-packages/Overview-and-Workflow.md)和[套件使用工作流程](consume-packages/Overview-and-Workflow.md)文章開始。

## <a name="managing-dependencies"></a>管理相依性

以其他人的工作為基礎輕鬆進行建置的能力，是套件管理系統中最強大的功能之一。 因此，大部分 NuGet 功能都為代表專案來管理相依性樹狀結構或「圖形」。 簡言之，您只需要讓自己關注在專案中直接使用的套件。 如果任何那些套件本身都取用其他套件 (其接著仍取用其他套件)，則 NuGet 會負責所有那些下層相依性。

下圖顯示與五個套件相依的專案，而這五個套件接著與許多其他套件相依。

![.NET 專案的範例 NuGet 相依性圖形](media/dependency-graph.png)

請注意，在相依性圖形中，有些套件會出現多次。 例如，套件 B 有三個不同的取用者，而每個取用者也可能為該套件 (未顯示) 指定不同的版本。 這種狀況經常發生，特別是針對廣泛使用的套件。 還好 NuGet 會執行所有困難的工作，以確切判斷哪個版本的套件 B 可滿足所有取用者。 不管相依性關係圖的深度為何，NuGet 接著都會對所有其他套件執行相同作業。

如需 NuGet 如何執行這項服務的詳細資料，請參閱[相依性解析](consume-packages/dependency-resolution.md)。

## <a name="tracking-references-and-restoring-packages"></a>追蹤參考和還原套件

因為專案可以輕鬆地在開發人員電腦、原始檔控制存放庫、組建伺服器等等之間移動，所以讓 NuGet 套件的二進位組件直接繫結至專案是不切實際的作法。 這樣做會使得專案的每個複本產生不必要的膨脹 (因而浪費原始檔控制存放庫中的空間)。 此外，也會使得它很難將套件二進位檔更新為較新版本，因為更新必須跨專案的所有複本加以套用。

NuGet 會改為維護專案相依之套件的簡單參考清單，包括最上層和最下層的相依性。 也就是說，只要您將套件從某個主機安裝至專案，NuGet 就會在參考清單中記錄套件識別碼和版本號碼 (當然，解除安裝套件會將它從清單中移除)。NuGet 接著提供方法，在收到要求時還原所有參考的套件，如[套件還原](consume-packages/package-restore.md)中所述。

![在套件安裝時會建立 NuGet 參考清單，並且可以用來在其他位置還原套件](media/nuget-restore.png)

只有參考清單時，NuGet 稍後隨時都可從公用和/或私人主機重新安裝&mdash;即「還原」  &mdash;所有的那些套件。 將專案認可到原始檔控制，或以某種其他方式進行共用時，只需包含參考清單，並排除任何套件二進位檔 (請參閱[套件和原始檔控制](consume-packages/packages-and-source-control.md))。

接收專案的電腦 (例如，在自動部署系統期間取得專案複本的組建伺服器) 只會要求 NuGet 在必要時還原相依性。 而建置像是 Azure DevOps 系統，可為此確切之目的，提供 "NuGet restore" 步驟。 同樣地，當開發人員取得專案複本時 (像是在複製存放庫時)，可以叫用類似 `nuget restore` (NuGet CLI)、`dotnet restore` (dotnet CLI) 或 `Install-Package` (套件管理員主控台) 的命令來取得所有必要的套件。 在建置專案時，Visual Studio 會自動還原套件 (假設已啟用自動還原，如[套件還原](consume-packages/package-restore.md)中所述)。

清楚的是，開發人員所關注的 NuGet 主要角色將會代表您的專案維護該參考清單，並提供方式，以有效率地還原 (和更新) 這些參考的套件。 此清單會以兩種「套件管理格式」  (呼叫它們時) 之一來維護：

- [PackageReference](consume-packages/package-references-in-project-files.md) (或「專案檔中的套件參考」) | *(NuGet 4.0+)* 直接維護專案檔內的專案最上層相依性清單，因此不需要個別檔案。 相關聯的 `obj/project.assets.json` 檔案是動態產生的，用途是管理專案所使用套件的整體相依性關係圖以及所有下層相依性。 PackageReference 一律由 .NET Core 專案使用。

- [`packages.config`](reference/packages-config.md)： *(NuGet 1.0+)* 一個 XML 檔案，其維護專案中所有相依性的一般清單，內含其他已安裝套件的相依性。 已安裝或已還原的套件會儲存在 `packages` 資料夾中。

任何指定專案中採用的套件管理格式都取決於專案類型，以及 NuGet (和/或 Visual Studio) 的可用版本。 若要檢查正在使用的格式，只需在安裝第一個套件之後，於專案根目錄中尋找 `packages.config`。 如果您沒有該檔案，請直接在專案檔中查看是否有 \<PackageReference\> 元素。

如果您可以選擇，建議使用 PackageReference。 `packages.config` 是為了舊版考量而保留，已不再積極開發中。

> [!Tip]
> 各種 `nuget.exe` CLI 命令 (例如 `nuget install`) 不會自動將套件新增到參考清單中。 在透過 Visual Studio 套件管理員 (UI 或主控台) 和透過 `dotnet.exe` CLI 安裝套件時，才會更新清單。

## <a name="what-else-does-nuget-do"></a>NuGet 還有其他功能嗎？

到目前為止，您已了解 NuGet 的下列特性：

- NuGet 提供 nuget.org 中央存放庫，並支援私人裝載。
- NuGet 提供開發人員建立、發行和使用套件所需的工具。
- 最重要的是，NuGet 會維護專案中所用套件的參考清單，而且能夠從該清單還原和更新那些套件。

為了讓這些程序有效率地運作，NuGet 會在幕後進行一些最佳化。 最重要的是，NuGet 會管理套件快取和全域套件資料夾，以方便安裝和重新安裝。 快取可避免下載已安裝在電腦上的套件。 全域套件資料夾可讓多個專案共用相同的已安裝套件，藉此降低 NuGet 在電腦上的整體使用量。 當您經常還原大量套件時 (例如在組建伺服器上)，快取和全域套件資料夾也十分有幫助。 如需這些機制的詳細資訊，請參閱[管理全域套件和快取資料夾](consume-packages/managing-the-global-packages-and-cache-folders.md)。

在個別專案中，NuGet 會管理整體相依性關係圖，同樣包含將多個參考解析為相同套件的不同版本。 專案經常需要採用與一或多個本身具有相同相依性之套件的相依性。 許多其他套件都會採用 nuget.org 上的一些最實用公用程式套件。 在整個相依性關係圖中，您接著就能輕鬆地擁有相同套件之不同版本的十個不同參考。 為了避免將該套件的多個版本帶入應用程式本身，NuGet 會找出所有取用者都可使用的單一版本 (如需詳細資訊，請參閱[相依性解析](consume-packages/dependency-resolution.md))。

此外，NuGet 會維護所有與套件建構方式相關的規格 (包含[當地語系化](create-packages/creating-localized-packages.md)和[偵錯符號](create-packages/symbol-packages.md)) 和其參考方式 (包含[版本範圍](reference/package-versioning.md#version-ranges-and-wildcards)和[發行前版本](create-packages/prerelease-packages.md))。NuGet 提供各種 API 供其他應用程式以程式設計方式使用其服務，並為撰寫 Visual Studio 擴充功能和專案範本的開發人員提供支援。

請花一點時間瀏覽此文件的目錄，您會在那裡看到所有呈現的功能，以及回溯到 NuGet 開始的版本資訊。

## <a name="comments-contributions-and-issues"></a>意見、參與和問題

最後，我們十分歡迎對本文件的意見和參與&mdash;只要選取任何頁面頂端的 [意見反應]  和 [編輯]  命令，或瀏覽 GitHub 上的[文件存放庫](https://github.com/NuGet/docs.microsoft.com-nuget/) \(英文\) 和[文件問題清單](https://github.com/NuGet/docs.microsoft.com-nuget/issues) \(英文\)。

我們也歡迎透過[各種 GitHub 存放庫](https://github.com/NuGet/Home) \(英文\) 來參與 NuGet 本身；在 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues) \(英文\) 可以找到 NuGet 問題。

享受 NuGet 體驗！
