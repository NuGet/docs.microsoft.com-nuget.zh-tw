---
title: NuGet 2.7 版本資訊
description: 版本資訊適用於 NuGet 2.7 包括已知的問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550961"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 版本資訊

[NuGet 2.6.1 for WebMatrix 版本資訊](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md)

NuGet 2.7 已於 2013 年 8 月 22 日發行。

## <a name="acknowledgements"></a>謝誌

我們想要感謝下列外部參與者，NuGet 2.7 到重大貢獻：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 當詳細列出封裝和詳細資訊會顯示授權 url。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [# 1956年](http://nuget.codeplex.com/workitem/1956)-developmentDependency 將屬性新增至`packages.config`並使其只包含執行階段套件組件命令中使用它
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - 避免重複 nuget.exe pack 命令的屬性索引鍵。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [# 2610年](http://nuget.codeplex.com/workitem/2610)-machine 快取大小增加至 200。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修正 NuGet 對話方塊顯示 [錯誤] 索引標籤中的更新
    - 修正 Project.TargetFramework 在可以是 null ProjectManager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById 上不存在 packageId，將會失敗
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -啟用遊牧專案的支援
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -修正推送命令會失敗，並結束程式碼 0，當檔案不存在。
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -修正 bug，以新增 BindingRedirect 命令時參考資料庫專案的專案。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 2891年](http://nuget.codeplex.com/workitem/2891)-修正 bug 的 nuget.pack 不正確剖析 'exclude' 屬性中的萬用字元。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -修正 bug`NuGet.targets`不會通過 $ （platform） nuget.exe 還原套件時。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe package 命令，這可讓您新增具有相同名稱但大小寫不同的最終導致 「 項目已經存在 」 的例外狀況的檔案中的修正 bug。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [# 2990年](http://nuget.codeplex.com/workitem/2990)-NetPortableProfile 類別的 [新增版本] 屬性。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -如果修正錯誤 NullReferenceException requireApiKey = true，但標頭 X-NUGET-APIKEY 不存在
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -修正 NuGet.Build 目標檔案，以讓它 MonoDevelop 上正常運作
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - 改善還原命令效能增加平行處理

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>根據預設 （隱含地同意） 的套件還原

NuGet 2.7 導入了新的套件還原，方法，也能夠克服的主要障礙： 套件還原同意現在預設為開啟 ！ 新的方法和隱含地同意的組合會大幅簡化套件還原案例。

#### <a name="implicit-consent"></a>隱含地同意

NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6，明確地允許 NuGet 下載遺漏的套件期間所需的使用者來建立。 如果此同意有未被明確授，則必須啟用套件還原的解決方案無法建立，直到使用者已授與同意。

從 NuGet 2.7 開始，套件還原同意預設值是 ON 時明確地讓使用者能夠*退出*的套件還原，如有需要，在 Visual Studio 中的 NuGet 的設定中使用核取方塊。 隱含地同意此變更會影響 NuGet 在下列環境：

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 命令列公用程式

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的自動套件還原

從 NuGet 2.7 開始，NuGet 會自動下載遺漏的套件在 Visual Studio 建置期間即使套件還原尚未明確啟用的解決方案。 此自動套件還原會在 Visual Studio 中，當您建置專案或方案，但之前叫用 MSBuild。 這會產生幾個重要優點：

1. 不再需要在您的方案使用 [啟用 NuGet 封裝還原] 筆勢
1. 專案不需要進行修改，而且 NuGet 不會對您的專案，以確保啟用套件還原的變更
1. 所有的 NuGet 套件，包括包含 MSBuild 屬性/目標檔案的匯入將會還原*之前*MSBuild 會叫用，確保在建置期間，都會正確地辨識這些屬性/目標

若要在 Visual Studio 中，使用自動套件還原，您只需要接受下列其中一個 (in) 動作：

1. 未簽入您`packages`資料夾

有數種方式，以省略您`packages`從原始檔控制資料夾。 如需詳細資訊，請參閱 <<c0> [ 套件和原始檔控制](../consume-packages/packages-and-source-control.md)主題。

雖然所有使用者都是隱含加入自動套件還原的同意，您可以輕鬆地選擇退出透過 Visual Studio 中的套件管理員設定。

![套件管理員設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>從命令列的簡化的套件還原

NuGet 2.7 導入了 nuget.exe 的新功能： `nuget.exe restore`

這個新的還原命令可讓您輕鬆地還原所接受的解決方案檔案或資料夾，做為引數的 使用單一命令中，解決方案的所有封裝。 此外，在目前的資料夾只是單一的解決方案時，就會隱含該引數。 這表示從包含單一的方案檔 (MySolution.sln) 的資料夾的所有下列都工作：

1. nuget.exe restore MySolution.sln
1. nuget.exe restore。
1. nuget.exe restore

Restore 命令會開啟方案檔，並尋找方案內的所有專案。 從該處，就可以找出`packages.config`針對每個專案和還原的所有封裝所找到的檔案。 它也會還原位於方案層級套件`.nuget\packages.config`檔案。 新的 Restore 命令的詳細資訊可在[命令列參考](../tools/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的套件還原工作流程

我們很榮幸套件還原，這些變更的相關的因為它導入了新的工作流程。 如果您想要忽略您的套件，從原始檔控制您只需不認可`packages`資料夾。 Visual Studio 使用者開啟及建置方案會自動還原套件。 命令列建置，只需叫用`nuget.exe restore`叫用之前`msbuild`。 您不再需要在您的方案中，使用 [啟用 NuGet 封裝還原] 筆勢，請記得，我們不再需要修改您的專案，來改變組建。 這也會產生很多改善的套件，包括匯入的 MSBuild，特別是針對透過 NuGet 的最新功能新增匯入並[自動匯入屬性/目標檔案](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 資料夾中。

除了我們自行完成的工作，我們也正在使用一些重要的夥伴，若要完成這個新方法。我們目前沒有具體的時間表的任一，但每個夥伴相關的新方法正如我們的榮幸。

* Team Foundation Service-他們正在整合呼叫`nuget.exe restore`的預設建置案例。
* Windows Azure 網站-他們正在可讓您將您的專案推送至 Azure，並讓`nuget.exe restore`建置您的網站之前呼叫。
* TeamCity-它們會更新其 NuGet 安裝程式外掛程式的 TeamCity 8.x
* AppHarbor-他們正在可讓您將您的存放庫推送至 AppHarbor 還有`nuget.exe restore`建置您的解決方案之前呼叫。

與每個上述協力廠商，他們會使用自己的 nuget.exe 複本，以及您不需要在您的方案中執行 nuget.exe。

#### <a name="known-issues"></a>已知問題

發生初始 2.7 版本中，nuget.exe 還原兩個已知的問題，但它們在 9/6/2013 與更新已修正[NuGet.CommandLine 封裝](http://www.nuget.org/packages/NuGet.CommandLine/)。  此更新也是位於[NuGet 2.7 下載頁面](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。  執行`nuget.exe update -self`會更新至最新版本。

已修正所示：

1. [使用 SLN 檔案時，新的套件還原無法在 Mono 上運作](https://nuget.codeplex.com/workitem/3596)
1. [新的套件還原不適用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)

另外還有新的套件還原工作流程的已知的問題讓[自動套件還原不適用於專案的方案資料夾底下](https://nuget.codeplex.com/workitem/3625)。 在 NuGet 2.7.1 中已經修正這個問題。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>重定專案目標與升級組建錯誤/警告

多次之後重設目標或升級您的專案，您發現某些 NuGet 套件未正常運作。 不幸的是，這不表示，並就沒有指引如何處理它。 NuGet 2.7，我們現在使用某些 Visual Studio 事件來識別您已重設目標或升級您的專案中的方式會影響您已安裝的 NuGet 套件。

如果我們偵測到任何封裝的影響重設目標或升級，我們將會產生立即的建置錯誤，讓您知道。 除了立即的建置錯誤，我們也保存`requireReinstallation="true"`加上旗標在您`packages.config`檔案已受到重定目標，以及每個後續的所有套件建置在 Visual Studio 中將會引發這些套件的建置警告。

雖然 NuGet 無法採取自動動作來重新安裝受影響的套件，我們希望此指示和警告會引導協助您了解當您需要重新安裝套件。 我們也正在努力[套件重新安裝指引文件](../consume-packages/reinstalling-and-updating-packages.md)這些錯誤訊息引導您。

### <a name="nuget-configuration-defaults"></a>NuGet 組態預設值

許多公司就內部而言，使用 NuGet，但有難引導其開發人員若要使用內部的套件來源，而非 nuget.org。NuGet 2.7 引進了可讓整個電腦的預設值為指定的組態預設值功能：

1. 已啟用的套件來源
1. 已註冊，但已停用套件來源
1. 預設的 nuget.exe 推送來源

每一種現在位於檔案中設定`%ProgramData%\NuGet\NuGetDefaults.Config`。 如果此組態檔指定套件來源，則預設值 nuget.org 封裝來源不會自動登錄和中的虛擬機器`NuGetDefaults.Config`會改為註冊。

雖然不一定要使用這項功能，我們會預期要部署的公司`NuGetDefaults.Config`檔案所使用的群組原則。

*請注意，這項功能將會永遠不會導致從開發人員的 NuGet 設定中移除的套件來源。這表示如果開發人員已經使用 NuGet，且因此 nuget.org 套件來源註冊，它不會移除建立之後`NuGetDefaults.Config`檔案。*

請參閱[NuGet 組態預設值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)如需有關這項功能。

### <a name="renaming-the-default-package-source"></a>重新命名的預設套件來源

NuGet 一律已登錄呼叫 「 NuGet 官方封裝來源 」 指向 nuget.org 的預設套件來源。該名稱的詳細資訊，它也未指定，它實際上已指向。 若要解決這些兩個問題，我們已重新命名為只是"nuget.org"在 UI 中此套件來源。 套件來源 URL 也已變更為包含"www"。 前置詞的「套件組合識別碼」。 使用 NuGet 2.7 之後, 您現有 「 NuGet 官方封裝來源 」 會自動更新為"nuget.org"作為其名稱和"<https://www.nuget.org/api/v2/>」 做為其 URL。

### <a name="performance-improvements"></a>效能改善

我們將會產生較小的記憶體使用量、 較少的磁碟使用量和速度的套件安裝 2.7 中進行一些效能改進。 我們也對 OData 為基礎的摘要，用來減少整體的承載更聰明的查詢。

### <a name="new-extensibility-apis"></a>新的擴充性 Api

我們加入我們的擴充性服務來填補遺漏功能的差異，在舊版中的某些新的 Api。

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>僅限開發相依性

這項功能已由發表[Adam Ralph](https://twitter.com/adamralph) ，它可讓套件作者將宣告只用於在開發階段的相依性的時間，而且不需要套件相依性。 藉由新增`developmentDependency="true"`屬性中的封裝`packages.config`，`nuget.exe pack`將不會再包括該套件作為相依性。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>移除 Visual Studio 2010 Express for Windows Phone 的支援

新的套件還原模型，在 2.7 是由新的 VSPackage，不同於主要 NuGet VSPackage 實作。 因為技術問題，這個新的 VSPackage 無法正確運作*Visual Studio 2010 Express for Windows Phone* SKU，以與其他共用相同的程式碼基底支援 Visual Studio Sku。 因此，從 NuGet 2.7 開始，我們會卸除的支援*Visual Studio 2010 Express for Windows Phone*從已發佈的延伸模組。 支援*Visual Studio 2010 Express for Web*仍然包含在發行至 Visual Studio 延伸模組組件庫的主要延伸模組。

因為我們不確定如何許多開發人員仍在使用 NuGet 在該版本的 Visual Studio 中，我們所發佈個別的 Visual Studio 擴充功能，專為這些使用者，並將其發佈在 CodePlex （而不是 Visual Studio 延伸模組程式庫）. 我們不打算繼續維護該延伸模組，但如果這會影響您，請讓我們知道藉由在 CodePlex 上提出問題。

若要下載 NuGet 套件管理員 （適用於 Visual Studio 2010 Express for Windows Phone)，請瀏覽[NuGet 2.7 下載](https://nuget.codeplex.com/releases/view/107605)頁面。

### <a name="bug-fixes"></a>Bug 修正

除了這些功能，這一版的 NuGet 也會包含其他許多 bug 修正。 發生在版本中解決的 97 總問題。 如需完整的工作清單項目中已修正 NuGet 2.7，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
