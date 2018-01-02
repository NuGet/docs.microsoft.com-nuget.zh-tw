---
title: "什麼是 NuGet？它有哪些功能？ | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "何謂 NuGet 和其功能的完整介紹"
keywords: "NuGet 套件管理員、使用、套件建立、套件裝載"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29dcedf33a54e249fe0b6acf588e4aafde28304f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="an-introduction-to-nuget"></a>NuGet 簡介

任何現代化開發平台的基本工具都是一種機制，而開發人員可以透過此機制建立、共用和使用有用的程式碼程式庫。 這類程式庫通常稱為「套件」，因為它們可以包含已編譯程式碼 (如 DLL) 以及其他使用這些程式庫之專案中可能需要的內容。

針對 .NET，共用程式碼的機制是 **NuGet**，其定義如何建立、裝載和使用 .NET 的套件，並提供所有這些角色的工具。 

簡言之，NuGet 套件就是副檔名為 `.nupkg` 的單一 ZIP 檔案，內含已編譯程式碼 (DLL)、其他與該程式碼相關的檔案，以及包含套件版本號碼這類資訊的描述性資訊清單。 程式庫開發人員建立套件檔案，並將其發行至主機。 套件取用者會收到這些套件，並將它們新增至其專案，然後在其專案程式碼中呼叫該程式庫功能。 NuGet 本身接著會處理所有中間詳細資料。

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>建立者、主機和取用者之間的套件流程

NuGet 的角色是主機，因此本身會在 [nuget.org](https://www.nuget.org) 維護超過 60,000 個唯一公開可用套件的中央存放庫。每天都會有數百萬位 .NET 開發人員採用這些套件。 NuGet 也可讓您在雲端、私人網路甚至只在本機檔案系統中私下裝載套件。 如此一來，只有特定組織或客戶群組內的開發人員才能使用這些套件。 [裝載您自己的 NuGet 摘要](Hosting-Packages/Overview.md)會說明這些選項。

不管其本質為何，主機都是作為套件「建立者」與套件「取用者」之間的連線點。 建立者會建置有用的 NuGet 套件，並將其發行至主機。 取用者接著會搜尋可存取主機上的實用和相容套件，並下載這些套件且將其包含在專案中。 一旦安裝於專案，套件的 API 就可供專案程式碼的其餘部分使用。

![套件建立者、套件主機與套件取用者之間的關聯性](media/nuget-roles.png)

在此情況下，「相容」套件表示它包含針對與取用中專案目標架構相容的至少一個目標 .NET Framework 所建置的組件。 若要可讓套件廣泛相容，其建立者會編譯各種目標架構的不同組件，並將它們全部併入相同的套件中。 取用者安裝該套件時，NuGet 只會擷取專案所需的組件。 在該專案所產生的最終應用程式和 (或) 組件中，這可將套件的用量降到最低。

## <a name="nuget-tools"></a>NuGet 工具

除了裝載支援之外，NuGet 也提供建立者和取用者所使用的各種工具：

| 工具 | 平台 | 適用的案例 | 說明 |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | 全部 | 建立、使用 | 提供所有 NuGet 功能，而且有些命令專門套用至套件建立者、有些命令只套用至取用者，其他命令則套用至兩者。 例如，套件建立者使用 `nuget pack` 命令以從各種組件和相關檔案建立套件、套件取用者使用 `nuget install` 以將套件納入專案，而每個人都使用 `nuget config` 來設定 NuGet 組態變數。  |
| [套件管理員 UI](Tools/Package-Manager-UI.md) | Windows 上的 Visual Studio | 使用 | 提供易用 UI，以在 .NET 專案中安裝和管理套件。 | 
| [管理 NuGet UI](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 使用 | 提供易用 UI，以在 .NET 專案中安裝和管理套件。 |
| [套件管理員主控台](Tools/Package-Manager-Console.md) | Windows 上的 Visual Studio | 使用 | 提供 [PowerShell 命令](Tools/Powershell-Reference.md)，以在 .NET 專案中安裝和管理套件。 | 
| [dotnet CLI](Tools/dotnet-Commands.md) | 全部 | 建立、使用 | 在 .NET Core 工具鏈內，直接提供特定 NuGet CLI 功能。 |
| [ MSBuild](Schema/msbuild-targets.md) | Windows | 建立、使用 | 可以建立套件，以及還原透過 MSBuild 工具鏈直接用於專案的套件。 |

如您所見，用來處理 NuGet 的工具大部分取決於建立 (和發行) 套件還是使用套件，以及您所工作的平台。 在[套件建立工作流程](Create-Packages/Overview-and-Workflow.md)和[套件使用工作流程](Consume-Packages/Overview-and-Workflow.md)主題，以及這些章節中的其他主題，可以找到更具體的詳細資料。 

套件建立者通常也是取用者，因為他們是以其他 NuGet 套件的現有功能為建置基礎。 當然，這些套件可能接著會與其他項目相依。

## <a name="managing-dependencies"></a>管理相依性

以其他人的工作為基礎輕鬆進行建置的能力，是讓套件管理系統功能強大的其中一項。 因此，大部分 NuGet 功能都會代表您的專案來管理相依性樹狀結構或「圖形」。 簡言之，您只需要讓自己關注在專案中直接使用的套件。 如果所有這些套件本身都使用其他套件 (其可使用套件)，則 NuGet 會負責所有這些下層相依性。

下圖顯示與五個套件相依的專案，而這五個套件接著與許多其他套件相依。  

![.NET 專案的範例 NuGet 相依性圖形](media/dependency-graph.png)

請注意，在相依性圖形中，有些套件會出現多次。 例如，套件 B 有三個不同的取用者，而每個取用者也可能為該套件 (未顯示) 指定不同的版本。 因為這經常發生，所以 NuGet 幸運地會執行所有困難的工作，以確切判斷哪個版本的套件 B 符合其所有取用者。 不管相依性圖形的深度為何，NuGet 接著都會對所有其他套件執行相同作業。

如需 NuGet 如何執行這項服務的詳細資料，請參閱[相依性解析](Consume-Packages/Dependency-Resolution.md)。

## <a name="tracking-references-and-restoring-packages"></a>追蹤參考和還原套件

因為專案可以輕鬆地在開發人員電腦、原始檔控制存放庫、組建伺服器等等之間移動，所以極適合保留來自直接繫結至專案之 NuGet 套件的二進位組件。 這不僅會讓專案的每個複本不必要的膨脹 (因而浪費原始檔控制存放庫中的空間)，也會很難將套件二進位檔更新為較新版本，因為這需要跨專案的所有複本來完成。 

相反地，NuGet 只會維護專案所相依之套件的參考清單 (包含最上層和下層相依性)，並提供方法，以在要求時還原所有參考的套件，如[套件還原](Consume-Packages/Package-Restore.md)中所述。 也就是說，只要您將套件從某個主機安裝至專案，NuGet 就會在此參考清單中記錄套件識別碼和版本號碼  (當然，解除安裝套件會將它從清單中移除)。 

![在套件安裝時會建立 NuGet 參考清單，並且可以用來在其他位置還原套件](media/nuget-restore.png)

只有參考清單時，NuGet 稍後隨時可以從公用和 (或) 私用主機重新安裝 (即還原) 所有這些套件  (因此，nuget.org 不允許永久刪除已發行的套件，但可以將它們隱藏；請參閱[刪除套件](Policies/deleting-packages.md))。將專案認可到原始檔控制或以某種其他方式進行共用時，只需要包含參考清單，而且不需要包含任何套件二進位檔 (請參閱[套件和原始檔控制](Consume-Packages/Packages-and-Source-Control.md))。

接收專案的電腦 (例如，在自動部署系統期間取得專案複本的組建伺服器) 只會要求 NuGet 在必要時還原相依性。 針對這個確切的用途，Visual Studio Team Services 這類組建系統會提供「NuGet 還原」步驟。 同樣地，如果開發人員取得專案的複本 (複製存放庫時)，然後在 Visual Studio 中開啟專案並執行建置，則 Visual Studio 會自動還原必要的 NuGet 套件。 開發人員也可以隨時在套件管理員主控台中使用 `nuget restore` CLI 命令或 `Install-Package` Cmdlet，告知 NuGet 還原套件。

清楚的是，開發人員所關注的 NuGet 主要角色將會代表您的專案維護該參考清單，並提供方式，以有效率地還原 (和更新) 這些參考的套件。

其確切運作方式已歷經不同版本的 NuGet，因而導致數個*套件管理格式*，它們稱為：

- [`packages.config`](Schema/packages-config.md)：*(NuGet 1.0+)* 一個 XML 檔案，維護專案中所有相依性的一般清單，內含其他已安裝套件的相依性。 
- [`project.json`](Schema/project-json.md)：*(NuGet 3.0+)* 一個 JSON 檔案，維護相關檔案 `project.lock.json` 中專案與整體套件圖形的相依性清單。 此結構提供的效能優於[相依性解析](Consume-Packages/Dependency-Resolution.md) (包含可轉移還原) 中所述的 `packages.config`，但其本身一般已取代為下面的 PackageReference。
- [專案檔中的套件參考](Consume-Packages/Package-References-in-Project-Files.md) (也稱為 "PackageReference") | *(NuGet 4.0+)* 直接維護專案檔內的專案最上層相依性清單，因此不需要個別檔案。 動態產生相關聯的檔案 `project.assets.json` (例如 `project.lock.json`) 來管理整體相依性圖形。

任何指定專案中所使用的專案管理格式都取決於專案類型，以及可用的 NuGet 和 Visual Studio 版本。 若要檢查正在使用的格式，只需要在安裝第一個套件之後，於專案根目錄中尋找 `packages.config` 或 `project.json`。 如果您看不到其中一個檔案，請直接查看 &lt;PackageReference&gt; 項目的專案檔。

例如，在 Visual Studio 2017 中，大部分專案類型都會使用 `packages.config`，但使用 PackageReference 的 UWP C# 和 .NET Core 專案。 

## <a name="what-else-does-nuget-do"></a>NuGet 還有其他功能嗎？

總而言之，NuGet 提供 (以其裝載角色) nuget.org 中央存放庫，並支援私用裝載。 NuGet 提供開發人員建立、發行和使用套件所需的工具。 最重要的是，NuGet 會維護專案中所用套件的參考清單，而且可以用來從該清單中還原和更新這些套件。

為了讓這些程序有效率地運作，NuGet 會在幕後進行一些最佳化。 最值得注意的是，NuGet 管理整個電腦和專案特定套件快取，以建立安裝和重新安裝的捷徑。 如果關注整個電腦的快取，則任何您在專案中下載並安裝的套件都會儲存在快取中，這樣在另一個專案中安裝相同的套件時就不需要再次進行下載。 當您經常還原大量套件時 (例如在組建伺服器上)，這十分有幫助。 如需機制和其使用方式的詳細資料，請參閱[管理 NuGet 快取](Consume-Packages/Managing-the-Nuget-Cache.md)。

在個別專案內，NuGet 會執行許多工作，來管理整體相依性圖形  (使用 `project.json` 或 &lt;PackageReference&gt; 時，NuGet 會將該資訊分別保留在稱為 `project.lock.json` 和 `project.assets.json` 的次要檔案中)。這同樣地包含解析相同套件之不同版本的多個參考。

也就是說，專案經常需要採用與一或多個本身具有相同相依性之套件的相依性。 例如，許多其他套件都會使用 nuget.org 上的一些最實用公用程式套件。 在整個相依性圖形中，您可以輕鬆地擁有相同套件之不同版本的十個不同參考。 不過，您不會想要將該套件的多個版本帶入應用程式本身，因此 NuGet 找出每個人都可以使用的單一版本  (如需本主題的詳細資訊，請參閱[相依性解析](Consume-Packages/Dependency-Resolution.md))。

此外，NuGet 會維護所有與套件建構方式相關的規格 (包含[當地語系化](Create-Packages/Creating-Localized-Packages.md)和[偵錯符號](Create-Packages/Symbol-Packages.md)) 和其參考方式 (包含[版本範圍](reference/package-versioning.md#version-ranges-and-wildcards)和[發行前版本](create-packages/Prerelease-Packages.md))。NuGet 也針對認證提供者 (適用於存取私用主機) 以及撰寫 Visual Studio 延伸模組和專案範本的開發人員提供 API。

請花一點時間瀏覽本文件的目錄，而您會在那裏看到所有呈現的功能，以及回溯到 NuGet 開始的版本資訊。

## <a name="comments-contributions-and-issues"></a>意見、參與和問題

最後，我們十分歡迎對本文件的意見和參與&mdash;只要選取任何頁面上的 [意見] 和 [編輯] 命令，或瀏覽 GitHub 上的[文件存放庫](https://github.com/NuGet/docs.microsoft.com-nuget/)和[文件問題清單](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。

我們也歡迎透過[各種 GitHub 存放庫](https://github.com/NuGet/Home)來參與 NuGet 本身；在 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues) 上可以找到 NuGet 問題。

享受 NuGet 體驗！
