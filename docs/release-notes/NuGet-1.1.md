---
title: NuGet 1.0 和1.1 版本資訊
description: NuGet 1.1 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384693"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 和1.1 版本資訊

[NuGet 1.2 版本資訊](../release-notes/nuget-1.2.md)

NuGet 1.0 已于2011年1月13日發行。  NuGet 1.1 已于2011年2月12日發行。

## <a name="overview"></a>概觀

本檔包含根據主要預覽版本分組的各種 NuGet 1.0 版本的版本資訊。

NuGet 包含下列元件：

* 包含下列各項的*NuGet. Tools .vsix* *：
  * [**新增程式庫套件] 對話方塊*** 對話方塊內用來流覽及安裝套件的 Visual Studio。
  * **套件管理員主控台*** Visual Studio 中的 Powershell 型主控台。
* *NuGet 命令列工具** 用來建立（並最終發佈）封裝的工具。

NuGet 工具 Visual Studio 擴充功能（*nuget.exe*）需要：

* Visual Studio 2010 或 Visual Web Developer 2010 Express。

NuGet 命令列工具需要：

* .NET Framework 第4版

## <a name="installation"></a>安裝

若要使用這個[最新版本](http://nuget.codeplex.com/releases/view/52018)：

* 先卸載舊版的組建。 您必須以系統管理員身分執行 VS，才能執行此動作。
* 移除您擁有的所有現有摘要。
* 加入指向 <https://go.microsoft.com/fwlink/?LinkId=206669>的新摘要。

## <a name="nuget-11"></a>NuGet 1.1

在此版本中修正的問題清單[可以在這裡找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

自 RC 起，RTM 已修正一個問題。

* [問題474：移除封裝會影響方案中的所有專案](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>候選版本

以下是自 CTP 2 之後，此發行候選版本中所做的變更。 請流覽問題追蹤程式，以查看錯誤的完整清單。

* [從主控台更新套件並不會更新相依性。](http://nuget.codeplex.com/workitem/443)
* [新增套件拾取-不套件參考（CTP1）](http://nuget.codeplex.com/workitem/442)
* [更新套件會保留中斷的參考](http://nuget.codeplex.com/workitem/440)
* [取得套件-在對話方塊中或在主控台中選取了 [全部] 匯總來源時，更新會失敗](http://nuget.codeplex.com/workitem/439)
* [取得套件驗證錯誤](http://nuget.codeplex.com/workitem/426)
* [當無法從 [新增套件] 對話方塊安裝套件時警告使用者](http://nuget.codeplex.com/workitem/425)
* [取得套件-更新大量套件時，會擲回更新](http://nuget.codeplex.com/workitem/424)
* [改善 nuspec 檔案撰寫錯誤時的錯誤處理](http://nuget.codeplex.com/workitem/423)
* [Nuget 套件忽略指定的檔案](http://nuget.codeplex.com/workitem/422)
* [移除第二個到最後一個套件來源，然後按一下 [下移] 當機與](http://nuget.codeplex.com/workitem/418)
* [安裝封裝時移除元件參考](http://nuget.codeplex.com/workitem/413)
* [開啟 [設定] 對話方塊時 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [套件管理員主控台中套件來源的存取金鑰無法使用](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 設定對話方塊存取金鑰會將焦點放在錯誤的欄位](http://nuget.codeplex.com/workitem/409)
* [封裝識別碼 intellisense 不應查詢太多專案](http://nuget.codeplex.com/workitem/404)
* [無法在專案名稱中使用點字元將封裝新增至專案](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中指定檔案的問題](http://nuget.codeplex.com/workitem/400)
* [使用較新的組建時，應該會註冊正確的官方摘要](http://nuget.codeplex.com/workitem/399)
* [標記應該使用空格，而不是#](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少一些有用的資訊](http://nuget.codeplex.com/workitem/388)
* [將報告不當內容連結新增至對話方塊](http://nuget.codeplex.com/workitem/386)
* [使用 App_Data 解壓縮封裝會中斷 Visual Studio](http://nuget.codeplex.com/workitem/380)
* [執行標記](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 允許建立不具相依性的空封裝](http://nuget.codeplex.com/workitem/373)
* [封裝的 [新增擁有者] 欄位](http://nuget.codeplex.com/workitem/365)
* [更新 VSIX 資訊清單，以說是 NuGet 套件管理員，而不是 VSIX 工具](http://nuget.codeplex.com/workitem/364)
* [當選取所有來源時，取得封裝命令會擲回錯誤](http://nuget.codeplex.com/workitem/359)
* [允許在 [選項] 對話方塊中排序套件來源](http://nuget.codeplex.com/workitem/356)
* [更新-套件不會移除較舊的版本](http://nuget.codeplex.com/workitem/352)
* [執行相依性的版本範圍規格](http://nuget.codeplex.com/workitem/347)
* [按一下 [新增套件] 時 Visual Studio 損毀](http://nuget.codeplex.com/workitem/346)
* [在 [新增套件] 對話方塊中顯示下載和分級](http://nuget.codeplex.com/workitem/345)
* [在對話方塊中的套件來源之間變更不會更新作用中的來源](http://nuget.codeplex.com/workitem/344)
* [移除套件管理員主控台視窗的金鑰系結](http://nuget.codeplex.com/workitem/339)
* [安裝-套件無法辨識為 Cmdlet 的名稱 .。。](http://nuget.codeplex.com/workitem/338)
* [從本機摘要安裝套件不會解析一般摘要的相依性](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 應該略過仍在使用中的相依性](http://nuget.codeplex.com/workitem/331)
* [如果取消頁面導覽，則當原始頁面要求傳回時，使用者無法流覽至其他頁面](http://nuget.codeplex.com/workitem/325)
* [調查 NuPack 的效能，以提供大量套件的摘要。](http://nuget.codeplex.com/workitem/324)
* [第二次篩選套件時，它會使用「新增」套件來源，而不是先前選取的來源。](http://nuget.codeplex.com/workitem/321)
* [選取對話方塊上的 [線上] 索引標籤時，應選取 [預設封裝來源]。](http://nuget.codeplex.com/workitem/320)
* [清單套件預設應該會顯示已安裝的套件](http://nuget.codeplex.com/workitem/309)
* [元件參考 HintPaths](http://nuget.codeplex.com/workitem/294)
* [開啟封裝管理員主控台時發生例外狀況](http://nuget.codeplex.com/workitem/268)
* [主控台 intellisense 下載整個摘要](http://nuget.codeplex.com/workitem/259)
* [「預設」套件來源應重新命名為 ' Active '](http://nuget.codeplex.com/workitem/258)
* [套件來源 UI：如果名稱/來源欄位不是空白，按下 [確定] 應該會新增新的來源](http://nuget.codeplex.com/workitem/257)
* [當已安裝的套件數目很大時，對話方塊會變得非常慢](http://nuget.codeplex.com/workitem/243)
* [支援強式命名元件的系結重新導向](http://nuget.codeplex.com/workitem/238)
* [新增封裝參考 .。。要包含套件來源下拉的 UI](http://nuget.codeplex.com/workitem/226)
* [NuPack 必須支援設定檔案名稱的設定轉換 agnostically](http://nuget.codeplex.com/workitem/224)
* [允許在 NuPack 中覆寫 BasePath](http://nuget.codeplex.com/workitem/222)
* [封裝來源回復行為](http://nuget.codeplex.com/workitem/204)
* [GUI 上的損毀](http://nuget.codeplex.com/workitem/201)
* [新增排序選項以新增封裝對話方塊](http://nuget.codeplex.com/workitem/179)
* [用來清除套件管理員主控台的快速鍵](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 導致 NuPack 主控台失敗](http://nuget.codeplex.com/workitem/166)
* [[主控台] 和 [新增套件] 對話方塊應該在要求中設定使用者代理程式](http://nuget.codeplex.com/workitem/141)
* [在組建中設定 VSIX 和 NuPack 的版本號碼。](http://nuget.codeplex.com/workitem/134)
* [隱藏一般 PowerShell 參數來源-？](http://nuget.codeplex.com/workitem/118)
* [新增主控台命令的詳細說明](http://nuget.codeplex.com/workitem/110)
* [[新增封裝] 對話方塊應允許選擇目前的封裝來源](http://nuget.codeplex.com/workitem/88)
* [將 NuPack 類別移至不同的命名空間](http://nuget.codeplex.com/workitem/50)
* [將說明新增至 Cmdlet](http://nuget.codeplex.com/workitem/23)
* [在套件下載之後驗證摘要中的雜湊](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

以下是 CTP 2 中最重要的變更：

* 將套件摘要從 ATOM 切換到 OData 服務端點：如果您升級至 CTP2 版本的 NuGet，請務必將下列 URL 新增為封裝來源： `https://feed.nuget.org/ctp2/odata/v1/`。
* 將 [新增套件] 命令重新命名為*Install-package*。
* 已更新 `.nuspec` 格式。 `.nuspec` 格式現在包含*iconUrl*欄位，可用於指定會顯示在 [新增封裝] 對話方塊中的 32x32 png 圖示。 因此，請務必將其設定為區分您的套件。 `.nuspec` 格式也包含新的*projectUrl*欄位，您可以用它來指向提供封裝詳細資訊的網頁。

這個組建無法搭配舊的 `.nupkg` 檔案使用。 如果您收到 null 參考例外狀況，則會使用舊的 `.nupkg` 檔案，而且需要使用更新的[NuGet 命令列工具](http://nuget.codeplex.com/releases/52017/download/165468)來重建它。

以下是針對 NuGet CTP 2 修正的功能和 bug 清單（不包含次要程式碼清除等的錯誤）。

* [指定元件的 TargetFramework 時，解壓縮封裝元件時發生錯誤。](http://nuget.codeplex.com/workitem/10)
* [讓 NuPack 主控台視窗更容易探索](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack .exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的錯誤/例外狀況處理](http://nuget.codeplex.com/workitem/24)
* [[Nupack]： PackageManager 應正常處理饋送相關的錯誤](http://nuget.codeplex.com/workitem/28)
* [需要新的主控台圖示](http://nuget.codeplex.com/workitem/29)
* [在對話方塊中將字串當地語系化](http://nuget.codeplex.com/workitem/38)
* [NuPack 快取已下載的 NuPack 檔案于記憶體中](http://nuget.codeplex.com/workitem/40)
* [NuPack 主控台：變更顯示主控台的預設快捷方式](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 應該支援通用屬性的預設值](http://nuget.codeplex.com/workitem/49)
* [在只有一個 nuspec 檔案的資料夾中執行 nupack，應該使用該 nuspec](http://nuget.codeplex.com/workitem/52)
* [即使沒有載入任何專案/方案，[專案] 功能表也會顯示](http://nuget.codeplex.com/workitem/54)
* [build。 cmd 在程式碼基底的全新複製上失敗](http://nuget.codeplex.com/workitem/56)
* [更新可用的功能](http://nuget.codeplex.com/workitem/57)
* [對話方塊：透過對話方塊新增封裝會移除主控台中的提示](http://nuget.codeplex.com/workitem/73)
* [按一下 [安裝] 來新增封裝通常會變慢，且沒有視覺效果的意見反應](http://nuget.codeplex.com/workitem/80)
* [無法探索哪些已安裝的套件具有更新。](http://nuget.codeplex.com/workitem/82)
* [無法在對話方塊中更新已安裝的封裝。](http://nuget.codeplex.com/workitem/83)
* [沒有任何方法可在對話方塊中卸載已安裝的套件](http://nuget.codeplex.com/workitem/84)
* [&ldquo;[新增套件參考]&hellip;&rdquo; 會出現在已安裝參考的內容功能表上](http://nuget.codeplex.com/workitem/85)
* [從主控台更新套件之後，它會顯示已安裝的舊版本和新版本](http://nuget.codeplex.com/workitem/86)
* [使用對話方塊時，主控台中的活動會在使用後消失](http://nuget.codeplex.com/workitem/87)
* [Nupack 中的清除命令列剖析](http://nuget.codeplex.com/workitem/89)
* [為套件來源新增易記名稱](http://nuget.codeplex.com/workitem/98)
* [更新. nuspec 以支援包含套件圖示](http://nuget.codeplex.com/workitem/103)
* [摘要 UI 不允許複製 URL](http://nuget.codeplex.com/workitem/105)
* [更好的移除-封裝錯誤處理。](http://nuget.codeplex.com/workitem/107)
* [在主控台視窗中輸入取決於游標焦點](http://nuget.codeplex.com/workitem/112)
* [錯誤訊息看起來非常複雜](http://nuget.codeplex.com/workitem/116)
* [未安裝之封裝的移除封裝效能不正確](http://nuget.codeplex.com/workitem/117)
* [當沒有套件來源時，移除封裝會失敗](http://nuget.codeplex.com/workitem/119)
* [當套件來源無法使用時，移除封裝會失敗](http://nuget.codeplex.com/workitem/120)
* [將標題新增至套件中繼資料和摘要。](http://nuget.codeplex.com/workitem/125)
* [將-Source 參數新增回新增封裝](http://nuget.codeplex.com/workitem/127)
* [清單套件應具有-Source 參數](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack 以要求 NuPack 使用者代理程式下載套件](http://nuget.codeplex.com/workitem/142)
* [[接受授權] 對話方塊必須列出需要接受的所有相依性的授權](http://nuget.codeplex.com/workitem/145)
* [當封裝在摘要中擲回時，記錄錯誤](http://nuget.codeplex.com/workitem/150)
* [NuPack 不應允許空白的 &lt;licenseurl&gt; 元素](http://nuget.codeplex.com/workitem/152)
* [將清單套件重新命名為-Package、Add-Package to Install-package 和 Remove-Package to Uninstall](http://nuget.codeplex.com/workitem/155)
* [使用解決方案導覽器中的 [加入套件參考] 功能表項目損毀 Visual Studio](http://nuget.codeplex.com/workitem/158)
* [[可用的套件來源] 標籤缺少冒號](http://nuget.codeplex.com/workitem/160)
* [Make. nuspec xml 元素大小寫一致的 camel 大寫](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX 的資訊清單必須開啟 ' admin ' 位](http://nuget.codeplex.com/workitem/162)
* [如果您執行不含摘要的清單套件，則會收到 null ref 錯誤](http://nuget.codeplex.com/workitem/164)
* [nuget.exe：指定目的地路徑](http://nuget.codeplex.com/workitem/171)
* [在 Test-winxp 上開啟套件管理主控台時發生 Powershell 錯誤](http://nuget.codeplex.com/workitem/175)
* [嘗試載入封裝清單時，VS 損毀](http://nuget.codeplex.com/workitem/176)
* [允許中繼封裝（沒有檔案，僅限相依性）](http://nuget.codeplex.com/workitem/180)
* [將 Powershell 腳本轉換成 Powershell 2.0 模組](http://nuget.codeplex.com/workitem/181)
* [當指定 target 時，PathResolver 應該捨棄前面萬用字元的路徑部分](http://nuget.codeplex.com/workitem/183)
* [無相關性](http://nuget.codeplex.com/workitem/186)
* [安裝 Elmah 時發生錯誤](http://nuget.codeplex.com/workitem/192)
* [設定轉換無法與 &lt;configsections 一起正常運作&gt;](http://nuget.codeplex.com/workitem/194)
* [無法抓取變數 ' $global:p rojectCache '，因為它尚未設定](http://nuget.codeplex.com/workitem/203)
* [新增用於建立 NuPack 套件的 MSBuild 工作](http://nuget.codeplex.com/workitem/205)
* [清單-封裝需要支援搜尋/篩選](http://nuget.codeplex.com/workitem/206)
* [如果封裝作者提供授權 URL，一律顯示授權的連結](http://nuget.codeplex.com/workitem/208)
* [具有移除封裝的偶爾「拒絕存取」例外狀況](http://nuget.codeplex.com/workitem/213)
* [單元測試失敗： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [如果找不到特定 framework 版本，則允許一組回溯/預設的檔案](http://nuget.codeplex.com/workitem/223)
* [新增封裝參考 .。。UI 無法移除封裝](http://nuget.codeplex.com/workitem/225)
* [卸載一個或多個專案時，新增封裝參考當機](http://nuget.codeplex.com/workitem/228)
* [設定轉換在 web.config 檔案上似乎沒有作用](http://nuget.codeplex.com/workitem/229)
* [在自訂封裝上未引發 init. ps1](http://nuget.codeplex.com/workitem/237)
* [將路徑新增至 feedlist 時，[預設值] 按鈕會設定為 [確定]，因此，如果我按 ENTER 鍵，它會自動關閉](http://nuget.codeplex.com/workitem/240)
* [嘗試卸載相依性將會在資料列中嘗試2次時損毀 VS](http://nuget.codeplex.com/workitem/241)
* [在 [新增套件] 對話方塊中顯示專案 URL](http://nuget.codeplex.com/workitem/253)
* [將 [新增套件] 對話方塊預設為已安裝的套件](http://nuget.codeplex.com/workitem/254)
* [[變更新增封裝] 對話方塊功能表項目。](http://nuget.codeplex.com/workitem/261)
* [重新命名命名空間和元件](http://nuget.codeplex.com/workitem/274)
* [將 NuPack 專案重新命名為 NuGet](http://nuget.codeplex.com/workitem/282)
* [在相依性清單底下新增下列文字](http://nuget.codeplex.com/workitem/288)
* [變更 [接受授權] 對話方塊中的 [接受授權] 文字](http://nuget.codeplex.com/workitem/291)
* [變更套件清單上方 [接受授權] 對話方塊中的文字](http://nuget.codeplex.com/workitem/292)
* [OData 不適用於 fwlink URL](http://nuget.codeplex.com/workitem/304)
* [套件管理員 UI：透過積極快取用於分頁的封裝計數](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet-&gt; 套件管理員主控台錯誤](http://nuget.codeplex.com/workitem/335)
* [[新增套件] 對話方塊會顯示已安裝之已封裝的授權接受](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

以下是針對 NuGet CTP 1 修正的功能和 bug 清單。

* [封裝延伸模組應重新命名為. nupack](http://nuget.codeplex.com/workitem/1)
* [將封裝檔案移至資料夾](http://nuget.codeplex.com/workitem/2)
* [合併安裝 &amp; 新增 PS 命令](http://nuget.codeplex.com/workitem/3)
* [建立動詞-名詞 Cmdlet 的別名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切換方案時，NuPack 會混淆](http://nuget.codeplex.com/workitem/6)
* [根據預設，我們應該隱藏 [套件] 方案資料夾](http://nuget.codeplex.com/workitem/11)
* [新增在內容專案中取代權杖的支援。](http://nuget.codeplex.com/workitem/12)
* [NuPack 應該使用 Register-packagesource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack]： PackageManager 會在安裝套件之前將它們標示為已安裝](http://nuget.codeplex.com/workitem/27)
* [從方案中刪除預設專案仍然會將已刪除的專案顯示為預設值](http://nuget.codeplex.com/workitem/30)
* [新的-封裝失敗，並出現「無法為指定的 URI 新增部分，因為它已經在封裝中。」](http://nuget.codeplex.com/workitem/32)
* [從 Visual Studio GUI 移除 "NuPack" 字串](http://nuget.codeplex.com/workitem/35)
* [將 Apache 標頭新增至著作權 .txt 檔案](http://nuget.codeplex.com/workitem/36)
* [移除 Register-packagesource 命令](http://nuget.codeplex.com/workitem/37)
* [載入設定檔擲回例外狀況時，套件管理員無法使用](http://nuget.codeplex.com/workitem/39)
* [init ps1，install. ps1 和 uninstall 必須接收其他狀態](http://nuget.codeplex.com/workitem/41)
* [將主控台和 GUI 套件合併成一個套件](http://nuget.codeplex.com/workitem/42)
* [Xml 轉換邏輯不適用於不在根目錄的 XML](http://nuget.codeplex.com/workitem/43)
* [[管理封裝來源設定] 對話方塊未更新 NuPack 主控台](http://nuget.codeplex.com/workitem/44)
* [NuPack 主控台 UI：將 [套件摘要] 下拉式清單重新命名為 [套件來源]](http://nuget.codeplex.com/workitem/45)
* [NuPack 主控台選項：將 [存放庫 UI] 重新命名為與 NuPack 主控台一致](http://nuget.codeplex.com/workitem/46)
* [針對從 IIS 或 URL 開啟的網站，新增封裝失敗](http://nuget.codeplex.com/workitem/53)
* [套件管理員來源無法與 FwLink 搭配使用](http://nuget.codeplex.com/workitem/55)
* [設定預設封裝來源](http://nuget.codeplex.com/workitem/59)
* [在選項中新增封裝來源時，如果只提供一個來源，則假設它是預設值。](http://nuget.codeplex.com/workitem/60)
* [對話方塊 UI 會顯示假的「最近」套件](http://nuget.codeplex.com/workitem/62)
* [選項：按一下 [取消] 並不會取消變更](http://nuget.codeplex.com/workitem/63)
* [[新增套件參考] 對話方塊搜尋應該不區分大小寫](http://nuget.codeplex.com/workitem/65)
* [修正 AssemblyInfo.cs 檔中的公司中繼資料](http://nuget.codeplex.com/workitem/67)
* [VSIX 的版本號碼](http://nuget.codeplex.com/workitem/71)
* [移除-封裝：使用-？顯示 [說明] 兩次](http://nuget.codeplex.com/workitem/72)
* [執行專案層級封裝的安裝/卸載套件](http://nuget.codeplex.com/workitem/74)
* [當一個 nupack 驗證失敗時，伺服器無法建立摘要](http://nuget.codeplex.com/workitem/90)
* [需要取代 NuPack 圖示](http://nuget.codeplex.com/workitem/94)
* [NTLM HTTP proxy 不會向套件摘要進行驗證。](http://nuget.codeplex.com/workitem/96)
* [對話方塊不一定會在 VS 視窗中以中央方式啟動](http://nuget.codeplex.com/workitem/100)
* [封裝詳細資料中的許多欄位並未在對話方塊中填入](http://nuget.codeplex.com/workitem/102)
* [對話方塊 UI 不會顯示作者的名稱](http://nuget.codeplex.com/workitem/108)
* [原因-移除套件的版本](http://nuget.codeplex.com/workitem/113)
* [移除對話方塊 UI 上的 [最近] 索引標籤](http://nuget.codeplex.com/workitem/115)
* [在開啟對話方塊 UI 至少一個之後，以滑鼠右鍵按一下方案資料夾時，VS 損毀。](http://nuget.codeplex.com/workitem/126)
* [將清單套件的-Local 參數變更為-已安裝](http://nuget.codeplex.com/workitem/129)
* [將套件 .xml 重新命名為 NuPack。](http://nuget.codeplex.com/workitem/132)
* [主控台強制游標在行尾](http://nuget.codeplex.com/workitem/135)
* [移除-封裝 intellisense 已中斷](http://nuget.codeplex.com/workitem/136)
* [將 RequireLicenseAcceptance 旗標新增至. nuspec 和 Feed](http://nuget.codeplex.com/workitem/137)
* [將 LicenseUrl 新增至 nuspec 格式和封裝摘要](http://nuget.codeplex.com/workitem/138)
* [針對需要接受的套件按一下 [安裝] 應該會顯示 [接受] 對話方塊](http://nuget.codeplex.com/workitem/139)
* [將免責聲明文字新增至 [新增封裝] 對話方塊](http://nuget.codeplex.com/workitem/140)
* [第一次執行套件主控台時新增免責聲明](http://nuget.codeplex.com/workitem/143)
* [在主控台中安裝套件後顯示免責聲明](http://nuget.codeplex.com/workitem/144)
* [將 nupack 副檔名重新命名為 nupkg。](http://nuget.codeplex.com/workitem/146)