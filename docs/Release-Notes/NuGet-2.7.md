---
title: NuGet 2.7 版本資訊 |Microsoft 文件
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.7。
keywords: NuGet 2.7 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 71ced70af127c8219001069739a6cec59d7d1684
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 版本資訊

[如需 WebMatrix 版本資訊的 NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md)

NuGet 2.7 已於 2013 年 8 月 22 日發行。

## <a name="acknowledgements"></a>謝誌

我們想要感謝下列外部 NuGet 2.7 其顯著比重的參與者：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - 當詳細列出封裝和詳細資訊會顯示授權 url。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [# 1956年](http://nuget.codeplex.com/workitem/1956)-新增要 developmentDependency 屬性`packages.config`並使其只包含執行階段封裝組件命令中使用它
1. [Rafael-salas.com Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - 避免重複 nuget.exe 套件命令的屬性索引鍵。
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [# 2610年](http://nuget.codeplex.com/workitem/2610)-machine 快取大小增加到 200。
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修正 NuGet 對話方塊顯示在 [錯誤] 索引標籤中的更新
    - 修正 Project.TargetFramework 可以是 null ProjectManager 中
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById 上不存在 packageId，將會失敗
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -啟用遊牧專案支援
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -檔案不存在時，修正發送命令失敗，並結束程式碼 0。
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -使用專案參考資料庫專案時加入 BindingRedirect 命令修正 bug。
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 2891年](http://nuget.codeplex.com/workitem/2891)-修正 bug 的 nuget.pack 不正確剖析 'exclude' 屬性中的萬用字元。
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -修正 bug`NuGet.targets`不 $(Platform) 時傳遞至 nuget.exe 還原封裝。
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe 套件] 命令會讓加入具有相同名稱但不同大小寫，最後導致 「 項目已經存在 」 的例外狀況的檔案中的修正 bug。
1. [奧 Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [# 2990年](http://nuget.codeplex.com/workitem/2990)-新增版本] 屬性，NetPortableProfile 類別。
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -如果修正 bug NullReferenceException requireApiKey = true，但標頭 X-NUGET-APIKEY 不存在
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -修正 NuGet.Build 目標檔案，讓它 MonoDevelop 上正常運作
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - 還原命令的效能改善藉由增加平行化作業

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="package-restore-by-default-with-implicit-consent"></a>封裝還原預設 （與隱含地同意）

NuGet 2.7 導入了新的封裝還原，方法，也能夠克服大障礙： 封裝還原同意現在預設為開啟 ！ 新的方法和隱含地同意的組合會大幅簡化封裝還原實例。

#### <a name="implicit-consent"></a>隱含地同意

與 NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6，明確地允許 NuGet 下載遺漏的封裝時所需的使用者來建立。 如果不在此同意已明確指定為，則必須啟用封裝還原的方案會無法建立，直到使用者已獲得同意。

從開始 NuGet 2.7，封裝還原同意預設為 ON 同時允許使用者明確*退出*的封裝還原，如有需要，在 Visual Studio 中的 NuGet 的設定中使用核取方塊。 隱含地同意此變更會影響 NuGet 在下列環境：

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe 命令列公用程式

#### <a name="automatic-package-restore-in-visual-studio"></a>在 Visual Studio 中的自動封裝還原

NuGet 2.7 從開始，NuGet 會自動下載缺少的套件 Visual Studio 中，在建置期間即使封裝還原尚未明確啟用方案。 這個自動封裝還原，發生在 Visual Studio 中，當您建置專案或方案，但是叫用 MSBuild 之前。 這會產生幾個重要的優點：

1. 不再需要在您的方案使用的 「 啟用 NuGet 封裝還原 」 的筆勢
1. 專案不需要修改，並 NuGet 將不會變更您的專案，確定已啟用封裝還原
1. 所有的 NuGet 封裝，包括包含 props/目標檔案的 MSBuild 匯入將會還原*之前*MSBuild 會叫用，確保在建置期間，正確辨識這些 props/目標

若要在 Visual Studio 中，使用自動封裝還原，您只需要採取動作 （中） 的其中一個：

1. 請勿核取 [您`packages`資料夾

有幾種方式可以省略您`packages`從原始檔控制的資料夾。 如需詳細資訊，請參閱[封裝和原始檔控制](../consume-packages/packages-and-source-control.md)主題。

雖然所有使用者都是隱含選擇加入自動封裝還原同意，您也可以輕鬆地退出透過 Visual Studio 中 [套件管理員設定。

![封裝管理員設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>簡化的封裝還原，從命令列

NuGet 2.7 導入了 nuget.exe 的新功能： `nuget.exe restore`

這個新的還原命令可讓您輕鬆地還原所有的套件在方案中使用單一命令中，接受的解決方案檔案或資料夾做為引數。 此外，目前的資料夾中僅有單一的解決方案時，就會隱含該引數。 這表示從包含單一方案檔 (MySolution.sln) 的資料夾的所有下列都工作：

1. nuget.exe restore MySolution.sln
1. nuget.exe 還原。
1. nuget.exe 還原

還原命令會開啟方案檔，並尋找方案中的所有專案。 它會從該處找到`packages.config`針對每個專案和封裝的所有找到的還原的檔案。 它也會還原方案層級中找不到封裝`.nuget\packages.config`檔案。 可以找到新的 Restore 命令的詳細資訊，在[命令列參照](../tools/cli-ref-restore.md)。

#### <a name="the-new-package-restore-workflow"></a>新的封裝還原工作流程

很高興有關這些變更封裝還原，因為它導入了新的工作流程。 如果您想要省略您從原始檔控制的封裝。 您只需不認可`packages`資料夾。 Visual Studio 使用者開啟並建置此方案將會看見自動還原封裝。 命令列組建，直接叫用`nuget.exe restore`叫用之前`msbuild`。 您不再需要使用 「 啟用 NuGet 封裝還原 」 筆勢在您的方案，請記住，我們不再需要修改您要更改組建的專案。 這也會產生包含 MSBuild 匯入，特別是針對匯入透過 NuGet 的新功能加入封裝以改良過的體驗和[自動匯入 props/目標檔案](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 資料夾中。

除了我們已經完成自己的工作，我們也正在使用一些重要的夥伴，來補足這種新方法。我們沒有具體的時間軸的其中任何棒的是，但每個夥伴為高興，因為我們新的方法。

* Team Foundation Service-他們正在處理整合到呼叫`nuget.exe restore`到預設建置案例。
* Windows Azure Web Sites-他們正在處理可讓您將您的專案推送至 Azure，並讓`nuget.exe restore`建置您的網站之前呼叫。
* TeamCity-它們會更新其 NuGet 安裝程式的外掛程式 TeamCity 8.x
* AppHarbor-他們正在處理可讓您以 AppHarbor 推送您的儲存機制，並讓`nuget.exe restore`建置方案之前呼叫。

與每一個上述協力電腦，就可以使用他們自己的 nuget.exe 的複本，您不需要執行 nuget.exe 方案中。

#### <a name="known-issues"></a>已知問題

有一些 nuget.exe 還原初始 2.7 版中，兩個已知的問題，但它們在 9/6/2013 的更新與已修正[NuGet.CommandLine 封裝](http://www.nuget.org/packages/NuGet.CommandLine/)。  此更新也會提供在[NuGet 2.7 下載頁面](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。  執行`nuget.exe update -self`會更新為最新版本。

固定所示：

1. [新的封裝還原不適用於的 Mono 時使用 SLN 檔案](https://nuget.codeplex.com/workitem/3596)
1. [新的封裝還原不適合用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)

另外還有新的封裝還原工作流程的已知的問題，[自動封裝還原不適用於專案的方案資料夾下](https://nuget.codeplex.com/workitem/3625)。 NuGet 2.7.1 中已修正此問題。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>專案重定目標 」 和 「 升級建置錯誤/警告

多次之後重定目標或升級您的專案，您發現部分 NuGet 封裝不正常運作。 不幸的是，沒有這個指示，則沒有任何指引，如何處理它。 NuGet 2.7，我們現在使用某些 Visual Studio 事件來辨識重定目標或升級的方式會影響安裝的 NuGet 套件中的專案時。

如果我們偵測到任何封裝已受到重定目標或升級，我們將會產生立即建置錯誤，讓您知道。 除了立即的建置錯誤，我們也會保留存`requireReinstallation="true"`加上旗標您`packages.config`檔案 for Visual Studio 中的受影響的重定目標，且每個後續的所有封裝都組建將會引發這些封裝的都建置警告。

雖然 NuGet 無法採取自動動作，以重新安裝受影響的封裝，我們希望此指示和警告會引導協助您找出當您需要重新安裝套件。 我們也正在[封裝重新安裝指引文件](../consume-packages/reinstalling-and-updating-packages.md)這些錯誤訊息引導您。

### <a name="nuget-configuration-defaults"></a>NuGet 組態預設值

許多公司在內部使用 NuGet，但有難引導他們的開發人員，可以使用內部的封裝來源而不是 nuget.org。NuGet 2.7 引進了組態預設值的功能，可讓指定的整部機器的預設值：

1. 已啟用的封裝來源
1. 已註冊，但是已停用封裝來源
1. 預設 nuget.exe 推送來源

其中每一項現在位於檔案內設定`%ProgramData%\NuGet\NuGetDefaults.Config`。 如果此組態檔指定封裝來源，則不會自動登錄的預設 nuget.org 的封裝來源中的項目和`NuGetDefaults.Config`將改為註冊。

雖然不需要使用這項功能，但我們預期公司部署`NuGetDefaults.Config`檔案所使用的群組原則。

*請注意，這項功能將會永遠不會導致從開發人員的 NuGet 設定中移除的封裝來源。這表示如果開發人員已經使用 NuGet 和因此 nuget.org 的封裝來源註冊，將不會移除它建立之後`NuGetDefaults.Config`檔案。*

請參閱[NuGet 組態預設值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)如需有關這項功能。

### <a name="renaming-the-default-package-source"></a>重新命名的預設封裝來源

NuGet 一律已註冊預設稱為 「 NuGet 官方封裝來源 」 指向 nuget.org 的封裝來源。該名稱的詳細資訊，它也未指定位置的實際指向。 若要解決這些兩個問題，我們已重新命名只要"nuget.org 」 在 UI 中此封裝來源。 封裝來源的 URL 也已變更為包含"www"。 前置詞的「套件組合識別碼」。 使用 NuGet 2.7 之後, 您現有 「 NuGet 官方封裝來源 」 會自動更新為"nuget.org"做為其名稱和"https://www.nuget.org/api/v2/"做為其 URL。

### <a name="performance-improvements"></a>效能改善

我們在將會產生較小的記憶體使用量、 較少的磁碟使用量和更快的套件安裝 2.7 進行一些效能改進。 我們也對 OData 摘要會減少整體裝載更佳的查詢。

### <a name="new-extensibility-apis"></a>新的擴充性 Api

我們加入一些新 Api 至我們的擴充性服務，以填滿遺漏功能的差距，在先前的版本。

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

### <a name="development-only-dependencies"></a>開發階段專用的相依性

這項功能已由造成[Adam Ralph](https://twitter.com/adamralph)並可讓封裝作者以宣告只能用在開發階段的相依性的時間，且不需要的套件相依性。 藉由新增`developmentDependency="true"`屬性中的封裝`packages.config`，`nuget.exe pack`將不再包含該封裝做為相依性。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>移除 Visual Studio 2010 Express 適用於 Windows Phone 的支援

2.7 中新的封裝還原模型是由新的 VSPackage 主要 NuGet VSPackage 的不同實作。 因為技術問題，這個新的 VSPackage 正確地在無法運作*Visual Studio 2010 Express for Windows Phone* SKU 為我們與其他共用相同的程式碼基底支援 Visual Studio Sku。 因此，從 NuGet 2.7 開始，我們會卸除支援*Visual Studio 2010 Express for Windows Phone*來自已發行的延伸模組。 支援*Visual Studio 2010 Express for Web*仍然包含在發行至 Visual Studio 延伸模組組件庫的主要延伸模組。

因為我們不確定如何許多開發人員仍在使用 NuGet 在該版本/版本的 Visual Studio 中，我們所發佈個別的 Visual Studio 擴充功能，特別是為那些使用者和發佈 CodePlex （而非 Visual Studio 擴充程式庫）. 我們不打算繼續維持該擴充功能，但如果這會影響您，請讓我們知道藉由在 CodePlex 上提出問題。

若要下載 NuGet 封裝管理員 （適用於 Visual Studio 2010 Express for Windows Phone)，請瀏覽[NuGet 2.7 下載](https://nuget.codeplex.com/releases/view/107605)頁面。

### <a name="bug-fixes"></a>Bug 修正

除了這些功能，此版本的 NuGet 也包含許多其他 bug 修正。 有一些版本中解決的 97 總問題。 如需完整的工作清單項目固定在 NuGet 2.7，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
