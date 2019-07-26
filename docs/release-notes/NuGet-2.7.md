---
title: NuGet 2.7 版本資訊
description: NuGet 2.7 的版本資訊, 包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317073"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 版本資訊

[Nuget 2.6.1 for WebMatrix 版本](../release-notes/nuget-2.6.1-for-webmatrix.md) | 資訊[nuget 2.7.1 版本](../release-notes/nuget-2.7.1.md)資訊

NuGet 2.7 已于2013年8月22日發行。

## <a name="acknowledgements"></a>謝誌

我們想要感謝下列外部參與者對 NuGet 2.7 的重大貢獻:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss)([@mxrss](https://twitter.com/mxrss))
    - 列出套件和詳細資訊時, 顯示授權 url。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph)([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -將 developmentDependency 屬性新增`packages.config`至, 並在 pack 命令中使用它, 只包含執行時間封裝
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael)([@tkrafael](https://twitter.com/tkrafael))
    - 避免在 nuget.exe pack 命令中出現重複的屬性索引鍵。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan)([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -將電腦快取大小增加至200。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel)([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修正在錯誤索引標籤中顯示更新的 NuGet 對話方塊
    - 修正專案。在 ProjectManager 中, TargetFramework 可以是 null
    - [#3248](http://nuget.codeplex.com/workitem/3248)修正 SharedPackageRepository FindPackage/FindPackagesById 將會在不存在的 packageId 上失敗
6. [古柯 Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG)([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -啟用 Nomad 專案的支援
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie)([@corinblaikie](https://twitter.com/corinblaikie))
    - 當檔案不存在時, [#3252](http://nuget.codeplex.com/workitem/3252)修正推送命令會失敗, 並出現結束代碼0。
8. [聖馬丁 Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -當專案參考資料庫專案時, 使用 BindingRedirect 命令修正 bug。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos)([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -修正 nuget 的錯誤。套件的 ' exclude ' 屬性中的萬用字元剖析錯誤。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981)([@zippy1981](https://twitter.com/zippy1981))
     - [](http://nuget.codeplex.com/workitem/3307)在還原套件時`NuGet.targets` , #3307 修正錯誤 (bug) 不會將 $ (Platform) 傳遞至 nuget.exe。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -修正 nuget.exe package 命令中的 bug, 這會允許加入具有相同名稱但大小寫不同的檔案, 最後造成「專案已存在」例外狀況。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino)([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -將版本屬性新增至 NetPortableProfile 類別。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -修正 requireApiKey = true 時的 bug NullReferenceException, 但標頭 X-APIKEY 不存在
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism)([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -修正 NuGet. 組建目標檔案, 使其在 MonoDevelop 上正常運作
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm)([@pranav_km](https://twitter.com/pranav_km))
     - 藉由增加平行處理來改善還原命令效能

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>預設封裝還原 (具有隱含同意)

NuGet 2.7 引進封裝還原的新方法, 同時也克服了一大障礙:套件還原同意現在預設為開啟! 新方法和隱含同意的結合, 可大幅簡化封裝還原案例。

#### <a name="implicit-consent"></a>隱含同意

使用 NuGet 版本2.0、2.1、2.2、2.5 和2.6 時, 使用者需要明確允許 NuGet 在組建期間下載遺漏的套件。 如果未明確指定此同意, 則已啟用封裝還原的解決方案將無法建立, 直到使用者授與同意為止。

從 NuGet 2.7 開始, 封裝還原同意預設為開啟, 並允許使用者在需要時使用 NuGet 設定 Visual Studio 中的核取方塊, 明確*退出宣告*套件還原。 這項隱含同意變更會影響下列環境中的 NuGet:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 命令列公用程式

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的自動套件還原

從 NuGet 2.7 開始, NuGet 會在 Visual Studio 組建期間自動下載遺漏的套件, 即使尚未針對解決方案明確啟用套件還原也一樣。 當您建立專案或方案時, 但在叫用 MSBuild 之前, 會在 Visual Studio 中進行這項自動封裝還原。 這會產生幾個重要的優點:

1. 不再需要在您的解決方案上使用 [啟用 NuGet 套件還原] 手勢
1. 不需要修改專案, NuGet 也不會對您的專案進行變更, 以確保已啟用封裝還原
1. 所有 NuGet 套件 (包括包含 .props/目標檔案的 MSBuild 匯入) 都將在叫用 msbuild*之前*還原, 以確保在組建期間能夠正確辨識這些 .props/目標

若要在 Visual Studio 中使用自動封裝還原, 您只需要採取一個 (in) 動作:

1. 不要簽入您`packages`的資料夾

有數種方式可以從原始`packages`檔控制中省略您的資料夾。 如需詳細資訊, 請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)主題。

雖然所有使用者都會隱含地加入宣告自動套件還原同意, 但是您可以輕鬆地透過 Visual Studio 中的套件管理員設定來退出。

![套件管理員設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>從命令列簡化套件還原

NuGet 2.7 引進了適用于 nuget.exe 的新功能:`nuget.exe restore`

這個新的 Restore 命令可讓您使用單一命令, 輕鬆還原解決方案的所有套件, 方法是接受方案檔案或資料夾做為引數。 此外, 當目前的資料夾中只有一個方案時, 就會隱含該引數。 這表示下列所有工作都是從包含單一方案檔 (Csharpconsoleapp .sln) 的資料夾中執行:

1. nuget.exe restore Csharpconsoleapp .sln
1. nuget.exe 還原。
1. nuget.exe 還原

Restore 命令會開啟方案檔, 並尋找方案中的所有專案。 它會從該處尋找每個`packages.config`專案的檔案, 並還原所有找到的套件。 它也會還原在檔案中找到的`.nuget\packages.config`解決方案層級封裝。 如需新的 Restore 命令的詳細資訊, 請參閱[命令列參考](../reference/cli-reference/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的封裝還原工作流程

我們對套件還原的這些變更很興奮, 因為它引進了新的工作流程。 如果您想要從原始檔控制中省略封裝, 您只需`packages`認可資料夾。 開啟並建立解決方案 Visual Studio 使用者會看到套件已自動還原。 針對命令列組建, 只需`nuget.exe restore` `msbuild`在叫用前叫用。 您不再需要記得在解決方案上使用 [啟用 NuGet 套件還原] 手勢, 而且我們不再需要修改您的專案來改變組建。 此外, 這也為包含 MSBuild 匯入的套件提供了更好的體驗, 特別是透過 NuGet 最近功能新增的匯入, 以自動從 \build 資料夾匯[入 .props/目標](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)檔案。

除了我們自己完成的工作之外, 我們也會與一些重要的合作夥伴合作, 將這種新方法舍入。我們尚無具體的時程表, 但每個夥伴都是我們對新方法的興奮。

* Team Foundation Service-他們正在努力將的呼叫`nuget.exe restore`整合到預設的組建案例中。
* Windows Azure 網站-他們正致力於讓您將專案推送至 Azure, 並`nuget.exe restore`在建立網站之前呼叫。
* TeamCity-他們正在更新其 TeamCity 8.x 的 NuGet 安裝程式外掛程式
* AppHarbor-他們正致力於讓您將存放庫推送至 AppHarbor, 並`nuget.exe restore`在您的解決方案建立之前呼叫。

在上述每個合作夥伴中, 他們會使用自己的 nuget.exe 複本, 而且您不需要在解決方案中攜帶 nuget.exe。

#### <a name="known-issues"></a>已知問題

使用初始2.7 版本進行 nuget.exe 還原有兩個已知問題, 但在9/6/2013 上已修正[nuget. 命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)的更新。  此更新也適用于 CodePlex 上的[NuGet 2.7 下載頁面](https://nuget.codeplex.com/releases/view/107605)。  執行`nuget.exe update -self`會更新至最新版本。

修正的內容為:

1. [使用 SLN 檔案時, 新的套件還原無法在 Mono 上使用](https://nuget.codeplex.com/workitem/3596)
1. [新的封裝還原不適用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)

新的封裝還原工作流程也有一個已知的問題, 也就是[自動封裝還原不適用於解決方案資料夾下的專案](https://nuget.codeplex.com/workitem/3625)。 此問題已在 NuGet 2.7.1 中修正。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>專案重定和升級組建錯誤/警告

在重定或升級您的專案之後, 您發現部分 NuGet 套件無法正常運作。 可惜的是, 這並不表示這種情況, 因此不提供如何解決此情況的指引。 使用 NuGet 2.7, 我們現在會使用一些 Visual Studio 事件來辨識您的專案是以影響已安裝之 NuGet 套件的方式重定或升級。

如果我們偵測到您的任何套件受到重定或升級影響, 我們將會產生立即的組建錯誤, 讓您知道。 除了立即組建錯誤之外, 我們也會在您`requireReinstallation="true"` `packages.config`的檔案中保存受重定影響之所有封裝的旗標, 而 Visual Studio 中的每個後續組建都會引發這些封裝的組建警告。

雖然 NuGet 無法採取自動動作來重新安裝受影響的套件, 但我們希望此指示和警告會引導您瞭解何時需要重新安裝套件。 我們也會使用[套件重新安裝指引檔](../consume-packages/reinstalling-and-updating-packages.md), 這些錯誤訊息會引導您前往。

### <a name="nuget-configuration-defaults"></a>NuGet 設定預設值

許多公司都在內部使用 NuGet, 但是已經很難引導其開發人員使用內部套件來源, 而不是 nuget.org。NuGet 2.7 引進了設定預設功能, 可針對下列各項指定全電腦的預設值:

1. 已啟用套件來源
1. 已註冊但已停用套件來源
1. 預設的 nuget.exe 推送來源

您現在可以在位於`%ProgramData%\NuGet\NuGetDefaults.Config`的檔案內設定這些檔案。 如果此設定檔指定封裝來源, 則預設的 nuget.org 封裝來源將不會自動註冊, 而且中`NuGetDefaults.Config`的將會改為註冊。

雖然不需要使用這項功能, 但我們預期公司會`NuGetDefaults.Config`使用群組原則來部署檔案。

*請注意, 這項功能永遠不會使套件來源從開發人員的 NuGet 設定中移除。這表示, 如果開發人員已使用 NuGet, 因此已註冊 nuget.org 套件來源, 則在檔案建立`NuGetDefaults.Config`後不會將它移除。*

如需這項功能的詳細資訊, 請參閱[NuGet 設定預設值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)。

### <a name="renaming-the-default-package-source"></a>重新命名預設封裝來源

NuGet 一律會註冊名為「NuGet 官方套件來源」的預設套件來源, 其指向 nuget.org。該名稱是 verbose, 而且也沒有指定實際指向的位置。 為了解決這兩個問題, 我們已將此套件來源重新命名為 UI 中的 "nuget.org"。 套件來源的 URL 也已變更為包含 "www"。 前置詞的「套件組合識別碼」。 使用 NuGet 2.7 之後, 您現有的「NuGet 官方套件來源」將自動更新為「nuget.org」, 作為其 URL 的<https://www.nuget.org/api/v2/>名稱和「」。

### <a name="performance-improvements"></a>效能改進

我們在2.7 中做了一些效能改進, 這會產生較小的記憶體耗用量、磁片使用量較少, 以及更快速的套件安裝。 我們也對以 OData 為基礎的摘要進行了更聰明的查詢, 這將會減少整體裝載。

### <a name="new-extensibility-apis"></a>新的擴充性 Api

我們已在擴充性服務中新增一些新的 Api, 以填補舊版中遺漏功能的差距。

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

### <a name="development-only-dependencies"></a>僅限開發的相依性

這項功能是由[Adam Ralph](https://twitter.com/adamralph)所提供, 可讓套件作者宣告只在開發階段使用, 而不需要封裝相依性的相依性。 藉由將`developmentDependency="true"`屬性新增至中`packages.config`的封裝`nuget.exe pack` , 將不再包含該封裝做為相依性。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>已移除 Visual Studio 2010 Express for Windows Phone 的支援

2\.7 中新的封裝還原模型是由與主要 NuGet VSPackage 不同的新 VSPackage 所執行。 由於技術問題的緣故, 這個新的 VSPackage 在 Windows Phone SKU 的*Visual Studio 2010 Express*中無法正常運作, 因為我們與其他支援的 Visual Studio sku 共用相同的程式碼基底。 因此, 從 NuGet 2.7 開始, 我們將從已發行的延伸模組中卸載*Visual Studio 2010 Express Windows Phone*的支援。 *Visual Studio 2010 Express For Web*的支援仍包含在發行至 Visual Studio 延伸模組資源庫的主要延伸模組中。

由於我們不確定有多少開發人員仍在該版本/版的 Visual Studio 中使用 NuGet, 因此我們會特別發佈個別的 Visual Studio 延伸模組, 供這些使用者使用, 並在 CodePlex 上發佈 (而不是 Visual Studio 的延伸模組資源庫). 我們不打算繼續維護該延伸模組, 但如果這會影響您, 請在 CodePlex 上提出問題以讓我們知道。

若要下載 NuGet 套件管理員 (適用于 Windows Phone 的 Visual Studio 2010 Express), 請造訪[nuget 2.7 下載](https://nuget.codeplex.com/releases/view/107605)頁面。

### <a name="bug-fixes"></a>錯誤修正

除了這些功能之外, 這一版的 NuGet 也包含其他許多 bug 修正。 發行中解決了97的總問題。 如需 NuGet 2.7 中已修正之工作專案的完整清單, 請參閱[此版本的 NuGet 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
