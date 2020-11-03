---
title: NuGet 2.5 版本資訊
description: NuGet 2.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237075"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 版本資訊

[NuGet 2.2.1 版本](../release-notes/nuget-2.2.1.md)  |  資訊[NuGet 2.6 版本](../release-notes/nuget-2.6.md)資訊

NuGet 2.5 已于2013年4月25日發行。 這一版的功能很大，我們認為可以略過2.3 和2.4 版！ 到目前為止，這是我們針對 NuGet 所擁有的最大版本，內含超過160個在發行中的 [工作專案](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 。

## <a name="acknowledgements"></a>通知

我們想要感謝下列外部參與者對 NuGet 2.5 的重大貢獻：

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted)) 
    - [#2847](https://nuget.codeplex.com/workitem/2847) -將 MonoAndroid、Monotouch.dll 和 MonoMac 新增至已知的目標 framework 識別碼清單。
2. [Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte)) 
    - [#2865](https://nuget.codeplex.com/workitem/2865) -修正區分 `NuGet.targets` 大小寫作業系統的拼寫
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl)) 
    - 在 Mono 上建立解決方案。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken)) 
    - 修正 Mono 上的單元測試失敗。
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool)) 
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack 命令不會將屬性傳播至 MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos)) 
    - [#1511](https://nuget.codeplex.com/workitem/1511) 修改過的 XML 處理常式代碼，以保留格式化。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - 已將可辨識的單字新增至自訂字典，以允許組建成功。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 修正在當地語系化與中執行時的單元測試
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 已從 PackageService 解壓縮介面
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou)) 
     - [#936](https://nuget.codeplex.com/workitem/936) -在封裝時處理專案相依性
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster)) 
     - [#2991](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) 支援在 cofig 檔案中儲存套件來源認證時的純文字密碼
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj)) 
     - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修正 Get-Package 說明描述

我們也感謝下列個人在最終發行版本之前，用來尋找 NuGet 2.5 搶鮮版（Beta/RC）的 bug：

1. [Tony 牆](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief)) 
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 與最新 NuGet 2.4 和2.5 組建中斷

## <a name="notable-features-in-the-release"></a>版本中的值得注意功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允許使用者覆寫已經存在的內容檔案

所有時間最常被要求的功能之一，就是能夠覆寫 NuGet 套件中所含磁片上已存在的內容檔案。 從 NuGet 2.5 開始，系統會識別這些衝突並提示您覆寫檔案，但先前一律會略過這些檔案。

![覆寫內容檔案](./media/NuGet-2.5/overwrite-file.png)

「nuget.exe 更新」和「安裝套件」現在都有新的選項 '-FileConflictAction '，可針對命令列案例設定一些預設值。

當封裝中的檔案已經存在於目標專案時，設定預設動作。 設定為 [覆寫] 以永遠覆寫檔案。 設定為 [略過] 以略過檔案。 如果未指定，則會提示輸入每個衝突的檔案。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>自動匯入 MSBuild 目標和 .props 檔案

在 NuGet 套件的最上層建立了新的傳統資料夾。  `\lib` `\content` `\tools` 您現在可以將 `\build` 資料夾包含在套件中，以做為、和的對等。  您可以在此資料夾下放置兩個具有固定名稱的檔案， `{packageid}.targets` 或 `{packageid}.props` 。 這兩個檔案可以直接在 `build` 架構特定資料夾下或下，就像其他資料夾一樣。 挑選最符合之架構資料夾的規則與在這些資料夾中的方式完全相同。

當 NuGet 安裝具有 \build 檔案的套件時，會 `<Import>` 在指向和檔案的專案檔中新增 MSBuild 元素 `.targets` `.props` 。 檔案 `.props` 會新增至頂端，而檔案 `.targets` 會新增至底部。

### <a name="specify-different-references-per-platform-using-references-element"></a>使用元素指定每個平臺的不同參考 `<References/>`

在2.5 之前的檔案中 `.nuspec` ，使用者只能指定要為所有架構新增的參考檔案。 現在有了2.5 的這項新功能，使用者可以 `<reference/>` 為每個支援的平臺撰寫元素，例如：

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

以下是 NuGet 如何根據檔案新增專案參考的流程 `.nuspec` ：

1. 尋找 `lib` 適用于目標 framework 的資料夾，並從該資料夾取得元件清單
1. 個別尋找適用于目標 framework 的參考群組，並從該群組取得元件清單。 未指定目標 framework 的參考群組是 fallback 群組。
1. 找出兩個清單的交集，然後使用該清單作為要加入的參考

這項新功能可讓封裝作者使用 [參考] 功能，將元件的子集套用至不同的架構，而這些元件在其他情況下需要在多個資料夾中攜帶重複的元件 `lib` 。

注意：您目前必須使用 nuget.exe 套件才能使用此功能;NuGet 套件 Explorer 尚未支援。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>全部更新按鈕以允許一次更新所有套件

許多人都知道「更新套件」 PowerShell Cmdlet 來更新所有套件;現在也有一個簡單的方法可以透過 UI 來執行此動作。

若要試用這項功能：

1. 建立新的 ASP.NET MVC 應用程式
1. 啟動 [管理 NuGet 套件] 對話方塊
1. 選取 [更新]
1. 按一下 [全部更新] 按鈕

![對話方塊中的 [全部更新] 按鈕](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>改善 nuget.exe 套件的專案參考支援

現在 nuget.exe pack 命令會處理參考的專案，但有下列規則：

1. 如果參考的專案有對應的檔案 `.nuspec` ，例如在與 `proj1.nuspec` 相同的資料夾中呼叫檔案， `proj1.csproj` 則會使用從檔案讀取的識別碼和版本，將此專案新增為套件的相依性 `.nuspec` 。
1. 否則，會將參考專案的檔案配套到套件中。 然後，將會以遞迴方式使用相同規則來處理這個專案所參考的專案。
1. 所有 DLL、 `.pdb` 和檔案 `.exe` 都會加入。
1. 新增所有其他內容檔案。
1. 所有相依性都會合並。

如果有檔案，則這可將參考的專案視為相依性 `.nuspec` ，否則它會成為封裝的一部分。

詳細資訊請參閱： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>將「最低 NuGet 版本」屬性新增至套件

名為 ' minClientVersion ' 的新中繼資料屬性現在可以指出取用封裝所需的最低 NuGet 用戶端版本。

這項功能可協助封裝作者指定套件只在特定版本的 NuGet 之後才能運作。 當您在 `.nuspec` NuGet 2.5 之後新增新功能時，套件將能夠索取最低的 nuget 版本。

```xml
<metadata minClientVersion="2.6">
```

如果使用者已安裝 NuGet 2.5 且將套件識別為需要2.6，則會提供視覺提示給使用者，指出將無法安裝該套件。 然後，系統會引導使用者更新其 NuGet 版本。

這將會在套件開始安裝的現有體驗上改善，但會在找不到可辨識的架構版本時失敗。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>在套件安裝期間，不再必要地更新相依性

在 NuGet 2.5 之前，當安裝的套件相依于已安裝在專案中的套件時，會在新的安裝過程中更新相依性，即使現有的版本已滿足相依性。

從 NuGet 2.5 開始，如果已符合相依性版本，則不會在其他套件安裝期間更新相依性。

**案例：**

1. 來源存放庫包含1.0.0 版和1.0.2 版的套件 B。 它也包含相依于 B ( # B0 = 1.0.0) 的封裝 A。
1. 假設目前的專案已安裝套件 B 1.0.0 版。 現在您想要安裝封裝 A。

**在 NuGet 2.2 及更舊版本中：**

* 安裝套件 A 時，NuGet 會自動將 B 更新為1.0.2，即使現有的1.0.0 版已經滿足相依性版本的條件約束，也就是 >= 1.0.0。

**在 NuGet 2.5 和更新版本中：**

* NuGet 將不再更新 B，因為它會偵測到現有的1.0.0 版符合相依性版本條件約束。

如需這項變更的詳細背景，請閱讀詳細的 [工作專案](http://nuget.codeplex.com/workitem/1681) 以及相關的 [討論執行緒](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 輸出具有詳細詳細資訊的 HTTP 要求

如果您要針對 nuget.exe 進行疑難排解，或只想知道在作業期間提出的 HTTP 要求，「-詳細程度詳細」參數現在會輸出發出的所有 HTTP 要求。

![nuget.exe 的 HTTP 輸出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送現在支援 UNC 和資料夾來源

在 NuGet 2.5 之前，如果您嘗試對以 UNC 路徑或本機資料夾為基礎的套件來源執行 ' nuget.exe push '，推送會失敗。 在最近新增的階層式設定功能中，nuget.exe 需要以 UNC/資料夾來源或以 HTTP 為基礎的 NuGet 資源庫為目標，是很常見的情況。

從 NuGet 2.5 開始，如果 nuget.exe 識別 UNC/資料夾來源，則會對來源執行檔案複製。

下列命令現在可運作：

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支援明確指定的設定檔

存取設定 (除了 ' spec ' 和 ' pack ' 以外的 nuget.exe 命令 ) 現在支援新的 '-get-help ' 選項，這會強制使用特定的設定檔來取代位於% AppData% \nuget\Nuget.Config 的預設設定檔。

範例：

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>原生專案的支援

使用 NuGet 2.5，NuGet 工具現在可用於 Visual Studio 中的原生專案。 我們預期大部分的原生封裝會利用上述的 MSBuild 匯入功能，並使用 [CoApp 專案](http://coapp.org)所建立的工具。 如需詳細資訊，請參閱 coapp.org 網站上的 [工具詳細資料](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) 。

將套件安裝到原生專案時，會針對套件引進「原生」的目標 framework 名稱以包含 \build、\content 和 \tools 中的檔案。  \`Lib 的資料夾不會用於原生專案。
