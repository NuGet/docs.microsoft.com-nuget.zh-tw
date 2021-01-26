---
title: NuGet 2.7 版本資訊
description: NuGet 2.7 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780393"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 版本資訊

[適用于 WebMatrix 的 NuGet 2.6.1 版本](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  資訊[NuGet 2.7.1 版本](../release-notes/nuget-2.7.1.md)資訊

NuGet 2.7 已于2013年8月22日發行。

## <a name="acknowledgements"></a>通知

我們想要感謝下列外部參與者對 NuGet 2.7 的重大貢獻：

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss)) 
    - 列出套件和詳細資訊時顯示授權 url。
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - [#1956](http://nuget.codeplex.com/workitem/1956) -將 developmentDependency 屬性新增至 `packages.config` ，並在 pack 命令中使用它，只包含執行時間封裝
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael)) 
    - 避免 nuget.exe pack 命令中出現重複的屬性索引鍵。
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan)) 
    - [#2610](http://nuget.codeplex.com/workitem/2610) -將電腦快取大小增加至200。
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel)) 
    - [#3217](http://nuget.codeplex.com/workitem/3217) -修正在錯誤索引標籤中顯示更新的 NuGet 對話方塊
    - 修正專案。 TargetFramework 在 ProjectManager 中可以是 null
    - [#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById 將會在不存在的 packageId 上失敗
6. [Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) () 的古柯 [@kevfromireland](https://twitter.com/kevfromireland)
    - [#3234](http://nuget.codeplex.com/workitem/3234) -啟用 Nomad 專案的支援
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie)) 
    - [#3252](http://nuget.codeplex.com/workitem/3252) -修正推送命令失敗，並在檔案不存在時結束代碼0。
8. [聖馬丁 Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -當專案參考資料庫專案時，使用 Add-BindingRedirect 命令修正 bug。
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos)) 
    - [#2891](http://nuget.codeplex.com/workitem/2891) -修正 nuget 的錯誤。套件的 ' exclude ' 屬性中的萬用字元剖析不正確。
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981)) 
     - [#3307](http://nuget.codeplex.com/workitem/3307) -修正 bug `NuGet.targets` 時，不會在還原套件時將 $ (Platform) 傳遞給 nuget.exe。
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -修正 nuget.exe package 命令中的 bug，此命令可讓您新增名稱相同但大小寫不同的檔案，最後會導致「專案已存在」例外狀況。
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu)) 
     - [#2990](http://nuget.codeplex.com/workitem/2990) -將 Version 屬性新增至 NetPortableProfile 類別。
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -如果 requireApiKey = true，但標頭 X-NUGET-APIKEY 不存在，請修正 bug NullReferenceException
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism)) 
     - [#3278](https://nuget.codeplex.com/workitem/3278) -將 NuGet. 組建目標檔案修正為可在 MonoDevelop 上正確運作
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km)) 
     - 藉由增加平行處理來改善還原命令效能

## <a name="notable-features-in-the-release"></a>版本中的值得注意功能

### <a name="package-restore-by-default-with-implicit-consent"></a>依預設，封裝還原 (與隱含同意) 

NuGet 2.7 引進了封裝還原的新方法，也克服了重大的障礙：套件還原同意現在預設為開啟！ 新方法和隱含同意的組合將大幅簡化套件還原案例。

#### <a name="implicit-consent"></a>隱含同意

使用 NuGet 2.0、2.1、2.2、2.5 和2.6 版時，使用者需要明確允許 NuGet 在組建期間下載遺漏的套件。 如果未明確指定此同意，則已啟用套件還原的方案將無法建立，直到使用者同意為止。

從 NuGet 2.7 開始，套件還原同意預設為開啟，但允許使用者視需要明確 *退出宣告* 套件還原，方法是使用 NuGet 設定中的 [Visual Studio] 核取方塊。 這項隱含同意變更會影響下列環境中的 NuGet：

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line 公用程式

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 中的自動套件還原

從 NuGet 2.7 開始，即使尚未針對方案明確啟用套件還原，NuGet 仍會在 Visual Studio 中的組建期間自動下載遺漏的套件。 當您建立專案或方案時，但在叫用 MSBuild 之前，會在 Visual Studio 中進行此自動封裝還原。 這會產生一些重要的優點：

1. 不再需要使用解決方案上的「啟用 NuGet 套件還原」手勢
1. 專案不需要修改，且 NuGet 不會對您的專案進行變更，以確保已啟用套件還原
1. 所有 NuGet 套件（包括包含 .props/目標檔案的 MSBuild 匯入）將在叫用 msbuild *之前* 還原，以確保在組建期間可正確辨識這些 .props/目標

若要在 Visual Studio 中使用自動套件還原，您只需要在) 動作中執行一個 (：

1. 不要簽入您的 `packages` 資料夾

有幾種方式可以 `packages` 從原始檔控制中省略您的資料夾。 如需詳細資訊，請參閱 [封裝和原始檔控制](../consume-packages/packages-and-source-control.md) 主題。

雖然所有使用者都會隱含地加入宣告自動套件還原同意，但您可以輕鬆地選擇 Visual Studio 中的封裝管理員設定。

![封裝管理員設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>從 Command-Line 簡化套件還原

NuGet 2.7 引進 nuget.exe 的新功能： `nuget.exe restore`

這個新的 Restore 命令可讓您輕鬆地使用單一命令來還原解決方案的所有套件，方法是接受方案檔或資料夾做為引數。 此外，當目前的資料夾中只有一個方案時，也會隱含該引數。 這表示下列所有工作都是從包含單一方案檔的資料夾 (Csharpconsoleapp) ：

1. nuget.exe 還原 Csharpconsoleapp .sln
1. nuget.exe 還原。
1. nuget.exe 還原

Restore 命令會開啟方案檔，並尋找方案中的所有專案。 從該處，它會尋找 `packages.config` 每個專案的檔案，並還原所有找到的封裝。 它也會還原檔案中找到的方案層級套件 `.nuget\packages.config` 。 有關 [新增還原] 命令的詳細資訊，可以在 [命令列參考](../reference/cli-reference/cli-ref-restore.md)中找到。

#### <a name="the-new-package-restore-workflow"></a>新的封裝還原工作流程

我們對封裝還原的這些變更很興奮，因為它引進了新的工作流程。 如果您想要從原始檔控制省略套件，則不會認可 `packages` 資料夾。 開啟並建立解決方案的 Visual Studio 使用者會看到自動還原的套件。 若是命令列組建，只要叫用 `nuget.exe restore` 再叫用 `msbuild` 。 您不再需要記得在解決方案上使用「啟用 NuGet 套件還原」手勢，我們將不再需要修改您的專案來改變組建。 此外，這也能為包含 MSBuild 匯入的套件帶來更佳的體驗，特別是透過 NuGet 最近的功能新增的匯入，可自動從 \build 資料夾匯 [入 .props/目標](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) 檔案。

除了我們自行完成的工作之外，我們也會與一些重要的夥伴合作，將這個新方法四捨五入。這兩種情況下都沒有具體的時程表，但每個合作夥伴都很興奮，因為這是新的方法。

* Team Foundation Service-它們正在將的呼叫整合到 `nuget.exe restore` 預設的組建案例中。
* Windows Azure 網站-這些網站可讓您將專案推送至 Azure，並在建立網站 `nuget.exe restore` 之前呼叫。
* TeamCity-他們正在更新其適用于 TeamCity 8.x 的 NuGet 安裝程式外掛程式
* AppHarbor-它們正在運作，可讓您將存放庫推送至 AppHarbor，並在 `nuget.exe restore` 您的解決方案建立之前呼叫。

在上述每個合作夥伴中，他們會使用自己的 nuget.exe 複本，而且您不需要在解決方案中攜帶 nuget.exe。

#### <a name="known-issues"></a>已知問題

nuget.exe restore 和初始2.7 版本有兩個已知的問題，但在9/6/2013 上已修正，並已更新 Nuget.exe 的 [命令列套件](http://www.nuget.org/packages/NuGet.CommandLine/)。  您也可以在 CodePlex 上的 [NuGet 2.7 下載頁面](https://nuget.codeplex.com/releases/view/107605) 上取得這項更新。  執行 `nuget.exe update -self` 會更新至最新版本。

修正的情況如下：

1. [使用 .SLN 檔案時，新的封裝還原不適用於 Mono](https://nuget.codeplex.com/workitem/3596)
1. [新的套件還原不適用於 Wix 專案](https://nuget.codeplex.com/workitem/3598)

此外，新的封裝還原工作流程也有已知的問題， [自動套件還原不適用於方案資料夾底下的專案](https://nuget.codeplex.com/workitem/3625)。 此問題已在 NuGet 2.7.1 中修正。

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>專案重定目標和升級組建錯誤/警告

在重定目標或升級您的專案之後，您會發現某些 NuGet 套件未正常運作。 可惜的是，這並不表示這一點，因此沒有解決方法的指引。 使用 NuGet 2.7，我們現在會使用一些 Visual Studio 事件，以在您已將專案重定目標或升級時，以影響已安裝之 NuGet 套件的方式來辨識。

如果我們偵測到任何套件受到重定目標或升級的影響，我們會產生立即的組建錯誤，讓您知道。 除了立即組建錯誤之外，我們也會在您的檔案 `requireReinstallation="true"` 中保存 `packages.config` 受重定目標影響之所有套件的旗標，且 Visual Studio 中的每個後續組建都會引發這些封裝的組建警告。

雖然 NuGet 無法採取自動動作來重新安裝受影響的套件，但我們希望此指示和警告會引導您在需要重新安裝套件時所發現的資訊。 我們也正在進行 [套件重新安裝指引檔](../consume-packages/reinstalling-and-updating-packages.md) ，這些錯誤訊息會將您導向至。

### <a name="nuget-configuration-defaults"></a>NuGet 設定預設值

許多公司都是在內部使用 NuGet，但卻很難讓開發人員使用內部套件來源，而不是 nuget.org。NuGet 2.7 引進了設定預設功能，可讓您針對下列各項指定全電腦的預設值：

1. 啟用的套件來源
1. 已註冊但已停用的套件來源
1. 預設 nuget.exe 推送來源

這兩個檔案現在都可以在位於的檔案內進行設定 `%ProgramData%\NuGet\NuGetDefaults.Config` 。 如果這個設定檔指定封裝來源，則預設的 nuget.org 套件來源將不會自動註冊， `NuGetDefaults.Config` 而會改為註冊在中。

雖然不需要使用這項功能，但我們預期公司會 `NuGetDefaults.Config` 使用群組原則來部署檔案。

*請注意，此功能絕不會導致從開發人員的 NuGet 設定中移除套件來源。這表示，如果開發人員已使用 NuGet，因此已註冊 nuget.org 套件來源，則在建立檔案後將不會移除它 `NuGetDefaults.Config` 。*

如需這項功能的詳細資訊，請參閱 [NuGet 設定預設值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) 。

### <a name="renaming-the-default-package-source"></a>重新命名預設封裝來源

NuGet 一律會註冊稱為「NuGet 官方套件來源」的預設套件來源，其指向 nuget.org。該名稱是 verbose，也未指定它實際指向的位置。 為了解決這兩個問題，我們已將此套件來源重新命名為簡單的 UI 中的 "nuget.org"。 套件來源的 URL 也已變更為包含 "www"。 前置詞。 使用 NuGet 2.7 之後，您現有的「NuGet 正式套件來源」將會自動更新為 "nuget.org" 作為其名稱和 " <https://www.nuget.org/api/v2/> " 作為其 URL。

### <a name="performance-improvements"></a>效能改進

我們已在2.7 中改善效能，這會產生較小的記憶體耗用量、磁片使用量較少，且套件安裝的速度較快。 我們也對以 OData 為基礎的摘要進行了更聰明的查詢，這會減少整體承載。

### <a name="new-extensibility-apis"></a>新的擴充性 Api

我們已將一些新的 Api 新增至擴充性服務，以填滿舊版中遺失之功能的差距。

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

### <a name="development-only-dependencies"></a>Development-Only 相依性

這項功能是由 [Adam Ralph](https://twitter.com/adamralph) 所提供，可讓套件作者宣告只在開發期間使用的相依性，而不需要套件相依性。 `developmentDependency="true"`將屬性新增至中的封裝 `packages.config` ， `nuget.exe pack` 就不會再包含該封裝作為相依性。

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>已移除 Visual Studio 2010 Express for Windows Phone 的支援

2.7 中新的封裝還原模型是由不同于主要 NuGet VSPackage 的新 VSPackage 所執行。 由於技術問題，這個新的 VSPackage 在 Windows Phone SKU 的 *Visual Studio 2010 Express* 中無法正常運作，因為我們與其他支援的 Visual Studio sku 共用相同的程式碼基底。 因此，從 NuGet 2.7 開始，我們會從已發佈的延伸模組中卸載 *Visual Studio 2010 Express for Windows Phone* 的支援。 *Visual Studio 2010 Express For Web* 的支援仍包含在發佈至 Visual Studio 擴充功能資源庫的主要延伸模組中。

由於我們不確定在該版本/版本的 Visual Studio 中，仍有多少開發人員仍在使用 NuGet，所以我們會特別為這些使用者發佈個別的 Visual Studio 擴充功能，並將其發佈到 CodePlex (，而不是 Visual Studio 擴充資源庫) 。 我們不打算繼續維護該延伸模組，但如果這會影響您，請在 CodePlex 上提出問題，讓我們知道。

若要下載適用于 Windows Phone) Visual Studio 2010 Express 的 NuGet 封裝管理員 (，請造訪 [nuget 2.7 下載](https://nuget.codeplex.com/releases/view/107605) 頁面。

### <a name="bug-fixes"></a>Bug 修正

除了這些功能之外，此版本的 NuGet 也包含許多其他 bug 修正。 發行中已解決的問題總數為97。 如需 NuGet 2.7 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。
