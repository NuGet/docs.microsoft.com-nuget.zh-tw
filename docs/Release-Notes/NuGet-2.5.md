---
title: "NuGet 2.5 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.5 的已知的問題、 錯誤修正、 新增的功能，以及 Dcr 包括版本資訊。"
keywords: "NuGet 2.5 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 版本資訊

[NuGet 2.2.1 版本資訊](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md)

NuGet 2.5 已於 2013 年 4 月 25 日發行。 此版本太大，我們被迫略過 2.3 和 2.4 版本 ！ 若要到目前為止，這是我們之前 nuget，與最大版本透過[160 工作項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)版本中。

## <a name="acknowledgements"></a>謝誌

我們想要感謝下列外部參與者的重要為 NuGet 2.5:

1. [奧 Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [# 2847年](https://nuget.codeplex.com/workitem/2847)-新增 MonoAndroid、 MonoTouch 和 MonoMac 已知的目標 framework 識別碼的清單。
1. [安德列斯 G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [# 2865年](https://nuget.codeplex.com/workitem/2865)-修正拼字`NuGet.targets`for 區分大小寫的 OS
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - 請 Mono 上建置方案。
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - 修正 Mono 上失敗的單元測試。
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe 套件命令不會傳播至 MSBuild 屬性
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 1511年](https://nuget.codeplex.com/workitem/1511)-修改的 XML 處理程式碼與保留的格式。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 加入自訂字典，以允許 build.cmd 才能成功辨識的字。
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 在當地語系化的 VS 中執行時，請修正單元測試。
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 從 PackageService 擷取的介面
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -處理封裝作業時的專案相依性
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支援純文字密碼時在 nuget.cofig 檔案中儲存封裝來源的認證
1. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修正取得封裝的說明描述

我們也歡迎下列人員找出錯誤與 NuGet 2.5 Beta/RC 已核准與之前的最後發行版本修正：

1. [Tong 牆](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 中斷且最新 NuGet 2.4 和 2.5 的組建

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允許使用者覆寫已存在的內容檔案

其中一個最常要求的功能的所有時間已經過覆寫已存在時包含在 NuGet 套件中的磁碟的內容檔案的能力。 NuGet 2.5 從開始，這些衝突會識別，系統會提示您覆寫檔案，而先前這些檔案永遠略過。

![覆寫內容檔案](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe 更新' 和 'Install-package' 現在都有新的選項 '-FileConflictAction' 來設定一些預設命令列的案例。

從封裝檔案已存在目標專案中時，請設定預設動作。 設定為 [覆寫]，永遠覆寫檔案。 設為 [忽略] 略過檔案。 如果未指定，它會提示輸入每個衝突的檔案。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>自動匯入的 MSBuild 目標與 props 檔案

在最上層的 NuGet 封裝已建立新的傳統資料夾。  等`\lib`， `\content`，和`\tools`，您現在可以包含`\build`在封裝中的資料夾。  在這個資料夾中，您可以將兩個檔案，具有固定的名稱放`{packageid}.targets`或`{packageid}.props`。 這兩個檔案可以是直接在`build`或架構特定的資料夾，就像其他資料夾底下。 挑選最相符的 framework 資料夾的規則是完全相同的。

當 NuGet 封裝安裝 \build 檔案時，它會將加入 MSBuild`<Import>`指向專案檔中的項目`.targets`和`.props`檔案。 `.props`檔案加入在頂端，而`.targets`檔案新增到下方。

### <a name="specify-different-references-per-platform-using-references-element"></a>指定每個平台使用不同參考`<References/>`項目

2.5 之前, 在`.nuspec`檔案，使用者只可以指定要加入所有 framework 相同的檔案參考。 現在使用者可以利用此在 2.5 的新功能，撰寫`<reference/>`每個支援的平台，例如項目：

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

以下是如何 NuGet 加入基礎專案的參考流程`.nuspec`檔案：

1. 尋找`lib`資料夾，適用於目標架構，並從該資料夾中取得的組件清單
1. 個別找到適合的目標 framework 的參考群組，並從該群組取得組件清單。 沒有指定目標 framework 的參考群組為後援的群組。
1. 尋找交集處的兩個清單中，並以在其中做為參考加入

這項新功能可讓封裝作者使用 [參考] 功能，否則它們需要在多個執行重複的組件時，將組件子集套用到不同的架構`lib`資料夾。

注意： 您必須現在使用 nuget.exe 套件使用這項功能。NuGet 封裝總管 還不支援它。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>更新所有的按鈕，以允許立即更新所有的封裝

知道有關 「 更新套件 」 的 PowerShell 指令程式來更新所有封裝。現在是可以輕鬆地透過 UI 以及執行這項操作。

若要試用此功能：

1. 建立新的 ASP.NET MVC 應用程式
1. 啟動 [管理 NuGet 套件] 對話方塊
1. 選取 '更新'
1. 按一下 [全部更新] 按鈕

![更新對話方塊中的所有按鈕](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe 套件的改良的專案參考支援

現在 nuget.exe 套件命令處理程序會參考專案的下列規則：

1. 如果參考的專案具有對應`.nuspec`檔案中，例如沒有名為的檔案`proj1.nuspec`相同資料夾中`proj1.csproj`、 然後此專案會加入做為相依性套件，並使用識別碼和版本讀取`.nuspec`檔案。
1. 否則，參考專案的檔案會集結到套件中。 然後您會使用 sames 規則以遞迴方式來處理這個專案所參考的專案。
1. 所有 DLL， `.pdb`，和`.exe`檔案加入。
1. 所有其他內容的檔案會加入。
1. 會合併所有的相依性。

這可讓參考的專案，如果沒有，被視為相依`.nuspec`檔案中，否則它會變成套件的一部分。

這裡有更多詳細資料： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>將 ' 至少 NuGet Version' 屬性加入封裝

新的中繼資料屬性，稱為 'minClientVersion' 現在可以指出使用封裝所需的最小 NuGet 用戶端版本。

這項功能可協助封裝作者以指定只有在特定版本的 NuGet 之後，封裝將正常運作。 當新`.nuspec`功能後加入 NuGet 2.5，封裝將無法宣告的最小的 NuGet 版本。

```xml
<metadata minClientVersion="2.6">
```

如果使用者已安裝的 NuGet 2.5，封裝會被識別為需要 2.6 視覺提示將會提供給使用者指出無法安裝套件中。 然後將更新自己版本的 NuGet 會引導使用者。

這可以改善時若要安裝，但失敗，表示無法辨識的結構描述版本已識別封裝的開始位置的現有體驗。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>相依性不會再不必要地更新套件安裝

NuGet 2.5 之前時已安裝的套件相依於已安裝在專案中，封裝的相依性會更新新的安裝，即使現有版本符合相依性。

如果已符合相依性版本起 NuGet 2.5，相依性將不會更新其他封裝的安裝期間。

**案例：**

1. 來源儲存機制包含封裝 B 1.0.0 和 1.0.2 版。 它也包含封裝 A 會相依於 B (> = 1.0.0)。
1. 假設目前的專案已有封裝 B 版本 1.0.0 已安裝。 現在您想要安裝封裝 a。

**2.2 和較舊的 NuGet： 中**

* 當安裝的封裝，NuGet 會自動更新 B 為 1.0.2，即使現有的版本 1.0.0 已滿足相依性版本條件約束，也就是 > = 1.0.0。

**在 NuGet 2.5 和更新版本：**

* 因為它偵測到現有的版本 1.0.0 符合相依性版本條件約束，NuGet 就不再更新 B。

如需這項變更的詳細背景，讀取詳細[工作項目](http://nuget.codeplex.com/workitem/1681)以及相關[討論](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 輸出 http 要求，以及詳細的詳細資訊

如果您正在疑難排解 nuget.exe 或只知道哪些發出 HTTP 要求會在作業期間，'-詳細等級的詳細 ' 參數現在會輸出所做的所有 HTTP 要求。

![Nuget.exe 的 HTTP 輸出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送現可支援 UNC 和資料夾的來源

之前 NuGet 2.5，如果您嘗試執行 'nuget.exe 推送' 上的 UNC 路徑或本機資料夾，為基礎的封裝來源推播會失敗。 使用最近加入的階層式組態功能，它變得很常見的 nuget.exe 需要為目標的資料夾 UNC/來源或以 HTTP 為基礎的 NuGet Gallery。

如果 nuget.exe 識別 UNC/資料夾來源起 NuGet 2.5，就會執行檔案複製到來源。

下列命令能否正常運作：

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支援明確指定的組態檔

nuget.exe 命令的存取設定 （除了 '規格' 和 '組件' 全部） 現在支援新的 '-ConfigFile' 選項，強制執行特定的組態檔可用於取代 %appdata%\nuget\nuget.config 預設組態檔。

範例：

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>原生專案的支援

以 NuGet 2.5 NuGet 工具現在是適用於 Visual Studio 中的原生專案。 我們預期最原生封裝會利用上述的 MSBuild 匯入功能使用工具所建立[CoApp 專案](http://coapp.org)。 如需詳細資訊，請參閱[工具的相關詳細資料](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 網站上。

「 原生 」 的目標 framework 名稱被引進的封裝時所要包括檔案 \build、 \content，和 \tools 封裝安裝到原生專案。  \`Lib' 資料夾不能用於原生專案。
