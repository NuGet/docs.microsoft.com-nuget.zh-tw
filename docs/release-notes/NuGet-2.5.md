---
title: NuGet 2.5 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.5 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550479"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 版本資訊

[NuGet 2.2.1 版本資訊](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md)

NuGet 2.5 已於 2013 年 4 月 25 日發行。 此版本中已太大了，我們被迫以略過 2.3 和 2.4 版 ！ 若要到目前為止，這是最大規模的發行，我們已推出適 NuGet，與透過[160 工作項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)版本中。

## <a name="acknowledgements"></a>謝誌

我們想要感謝下列的外部參與者重大貢獻到 NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [# 2847年](https://nuget.codeplex.com/workitem/2847)-新增 MonoAndroid MonoTouch，且 MonoMac 已知的目標 framework 識別碼的清單。
2. [Andres G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [# 2865年](https://nuget.codeplex.com/workitem/2865)-修正拼字`NuGet.targets`區分大小寫的 os
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - 請在 Mono 上建置的解決方案。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - 修正在 Mono 上失敗的單元測試。
5. [撰文 Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe pack 命令不會傳播至 MSBuild 屬性
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 1511年](https://nuget.codeplex.com/workitem/1511)-修改 XML 處理程式碼以保留的格式。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 加入自訂字典，以便成功的 build.cmd 辨識出的字詞。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 在當地語系化的 VS 中執行時，請修正單元測試。
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 從 PackageService 擷取的介面
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -封裝時，處理專案相依性
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支援純文字密碼將套件來源的認證儲存在 nuget.cofig 檔案時
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-封裝說明描述

我們也歡迎下列人員，找出錯誤使用 NuGet 2.5 Beta/RC 已核准並修正之前的最後發行版本：

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -以最新 NuGet 2.4 及 2.5 組建中斷的 MSTest

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允許使用者覆寫已存在的內容檔案

其中一個最常要求的功能的所有時間，而能夠覆寫已存在時 NuGet 套件中包含的磁碟的內容檔案。 開始使用 NuGet 2.5，這些衝突會識別，而且系統會提示您覆寫檔案，而先前這些檔案已一律略過。

![覆寫內容檔案](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe 更新' 和 'Install-package' 現在都有新的選項 '-FileConflictAction' 設定一些預設的命令列的案例。

從封裝檔案已存在目標專案中時，請設定預設動作。 設定為 [覆寫]，永遠覆寫檔案。 設為 [忽略] 以略過檔案。 如果未指定，它會提示輸入每個衝突的檔案。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>自動匯入的 MSBuild 目標與 props 檔案

在 NuGet 套件的最上層已建立新的傳統資料夾。  為對等`\lib`， `\content`，並`\tools`，您現在可以包含`\build`套件中的資料夾。  在此資料夾中，您可以將具有固定名稱，兩個檔案放`{packageid}.targets`或`{packageid}.props`。 這兩個檔案可以是直接在`build`或架構特有資料夾，就像其他資料夾底下。 挑選最相符的 framework 資料夾的規則正是這些相同。

當 NuGet 使用 \build 檔案安裝的套件時，它會將新增 MSBuild`<Import>`指向的專案檔中的項目`.targets`和`.props`檔案。 `.props`檔案加入在頂端，而`.targets`檔案新增至底部。

### <a name="specify-different-references-per-platform-using-references-element"></a>指定每個平台上使用的不同參考`<References/>`項目

2.5 之前在`.nuspec`檔案，使用者只可以指定要加入所有的架構相同的檔案參考。 現在使用者可以利用此 2.5 的新功能，來撰寫`<reference/>`的每個支援的平台，例如項目：

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

以下是如何 NuGet 將參考加入至專案為基礎的流程`.nuspec`檔案：

1. 尋找`lib`適合的目標 framework，並從該資料夾中取得的組件清單的資料夾
1. 個別尋找適合的目標 framework 參考群組，並從該群組取得組件清單。 參考群組，而指定的目標 framework 不會是後援的群組。
1. 尋找兩份清單中，交集，並使用它做為參考來新增

這項新功能可讓套件作者可使用 「 參考 」 功能，它們必須在多個執行重複的組件時，將組件子集套用到不同的架構`lib`資料夾。

注意： 您必須目前使用 nuget.exe 組件來使用這項功能;NuGet 封裝總管 還不支援它。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>更新所有的按鈕，以允許同時更新所有封裝

許多人了解 「 更新套件 」 PowerShell cmdlet，來更新所有封裝;現在是透過 UI 以及執行簡單的方法。

若要試用這項功能：

1. 建立新的 ASP.NET MVC 應用程式
1. 啟動 [管理 NuGet 套件] 對話方塊
1. 選取 「 更新 」
1. 按一下 [更新全部] 按鈕

![更新對話方塊中的所有按鈕](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe 組件的改良的專案參考支援

現在 nuget.exe 組件命令處理程序會參考專案的下列規則：

1. 如果參考的專案具有對應`.nuspec`檔案中，例如沒有名為的檔案`proj1.nuspec`相同的資料夾中`proj1.csproj`，然後此專案會加入為相依性套件，並使用識別碼和版本讀取`.nuspec`檔案。
1. 否則，請參考專案的檔案已包含的封裝。 然後您會使用相同的規則以遞迴方式來處理這個專案所參考的專案。
1. 所有的 DLL `.pdb`，和`.exe`檔案會新增。
1. 所有其他內容的檔案會加入。
1. 會合併所有的相依性。

這可讓參考的專案，如果沒有，被視為相依性`.nuspec`檔案中，否則它會變成套件的一部分。

更多詳細資料： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>將 ' 至少 NuGet Version' 屬性新增至套件

新的中繼資料屬性，稱為 'minClientVersion' 現在可以指出使用套件所需的最低 NuGet 用戶端版本。

這項功能有助於封裝作者以指定封裝能夠只在特定版本的 NuGet 之後。 當新`.nuspec`功能後面會加 NuGet 2.5，封裝可以宣告的最小的 NuGet 版本。

```xml
<metadata minClientVersion="2.6">
```

如果使用者已安裝的 NuGet 2.5，封裝便會被視為需要 2.6 視覺提示會提供給使用者指出封裝不會安裝中。 更新 NuGet 的版本，然後會引導使用者。

這會改善現有套件何處開始安裝，但無法指出無法辨識的結構描述版本已識別出的體驗。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>在套件安裝期間不會再進行不必要更新的相依性

NuGet 2.5 之前已安裝套件相依於已安裝在專案中，封裝相依性會更新為新安裝期間，即使現有版本符合相依性。

如果已符合相依性版本，則為，從開始使用 NuGet 2.5，相依性將不會更新其他套件安裝期間。

**案例：**

1. 來源存放庫包含套件 B 版本 1.0.0 和 1.0.2。 它也包含套件 A 在 B 具有相依性 (> = 1.0.0)。
1. 假設目前的專案已經有套件 B 版本 1.0.0 的安裝。 現在您想要安裝套件 a。

**在 NuGet 2.2 和較舊版本：**

* 安裝時的封裝，NuGet 會自動更新 B 至 1.0.2，即使現有版本 1.0.0 已符合相依性版本條件約束，也就是 > = 1.0.0。

**Nuget 2.5 和更新版本：**

* 因為它偵測到現有的版本 1.0.0 符合相依性版本條件約束，NuGet 就不再會更新 B。

如需更多有關這項變更的詳細背景，閱讀詳細[工作項目](http://nuget.codeplex.com/workitem/1681)以及相關[討論](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 會輸出 http 要求，以及詳細的詳細資訊

如果您正在疑難排解 nuget.exe 或只想知道哪些 HTTP 要求都是在作業期間，'-詳細的詳細資訊 ' 參數現在會輸出所做的所有 HTTP 要求。

![Nuget.exe HTTP 輸出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送現在支援 UNC 和資料夾的來源

NuGet 2.5 之前如果您嘗試執行 'nuget.exe push' 至套件來源，依據 UNC 路徑或本機資料夾，就會失敗的推播。 使用最近加入的階層式組態功能，它變得很常見的 nuget.exe 需要以 UNC/資料夾的來源或以 HTTP 為基礎的 NuGet 資源庫為目標。

如果 nuget.exe 識別 UNC/資料夾的來源，使用 NuGet 2.5，從開始，它會執行檔案複製到來源。

下列命令能否正常運作：

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支援明確指定設定檔

nuget.exe 命令存取組態 （全部 '規格' 和 '組件' 除外） 現在支援新的 '-ConfigFile' 選項，強制執行特定的組態檔來代替預設組態檔位於 %appdata%\nuget\nuget.config。

範例：

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>原生專案的支援

使用 NuGet 2.5 NuGet 工具現已供 Visual Studio 中的原生專案。 我們預期最原生套件將會利用 MSBuild 匯入功能，以上版本，使用所建立的工具[CoApp 專案](http://coapp.org)。 如需詳細資訊，請參閱[工具的詳細](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 網站上。

「 原生 」 的目標架構名稱引進 \build、 \content 和 \tools 中包含檔案，當封裝安裝到原生專案的封裝。  \`Lib' 資料夾不能用於原生專案。
