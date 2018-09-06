---
title: 1.0 和 1.1 版的 NuGet 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.1 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547017"
---
# <a name="nuget-10-and-11-release-notes"></a>1.0 和 1.1 版的 NuGet 版本資訊

[NuGet 1.2 版本資訊](../release-notes/nuget-1.2.md)

NuGet 1.0 已於 2011 年 1 月 13 日發行。  NuGet 1.1 版已於 2011 年 2 月 12 日發行。

## <a name="overview"></a>總覽

本文件包含各種群組根據主要的預覽版本的 NuGet 1.0 版本的版本資訊。

NuGet 會包含下列元件：

* *NuGet.Tools.vsix* * 所組成：
  * **新增程式庫封裝對話方塊*** 用來瀏覽及安裝套件的 Visual Studio 中的對話方塊。
  * **套件管理員主控台*** Powershell 型的 Visual Studio 中的主控台。
* *NuGet 命令列工具** 工具用來建立 （和最後發行） 套件。

NuGet 工具 Visual Studio 擴充功能 (*NuGet.Tools.vsix*) 需要：

* Visual Studio 2010 或 Visual Web Developer 2010 Express。

NuGet 命令列工具需要：

* .NET framework 第 4 版

## <a name="installation"></a>安裝

若要使用此[最新版本](http://nuget.codeplex.com/releases/view/52018):

* 先解除安裝舊的組建。 您需要執行這項操作的系統管理員身分執行 VS。
* 移除您所擁有的所有現有摘要。
* 新增指向摘要[ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669)。

## <a name="nuget-11"></a>NuGet 1.1

在此版本中修正的問題清單[可以在這裡找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

自 RC 起，有一項問題已修正 rtm。

* [問題 474： 移除套件會影響方案中的所有專案](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>發行候選版本

以下是自 CTP 2 這個 Release candidate 所做的變更。 請瀏覽問題追蹤程式，以查看錯誤的完整清單。

* [更新套件，從主控台不會更新相依性。](http://nuget.codeplex.com/workitem/443)
* [新增套件取用 bin 不套件參考 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [更新套件離開中斷的參考](http://nuget.codeplex.com/workitem/440)
* [取得封裝-更新失敗時，在對話方塊中，或在主控台中選取 '所有' 彙總的來源](http://nuget.codeplex.com/workitem/439)
* [取得封裝驗證錯誤](http://nuget.codeplex.com/workitem/426)
* [無法安裝套件，從 [新增套件] 對話方塊，警告使用者](http://nuget.codeplex.com/workitem/425)
* [取得封裝-更新大量套件時，更新會擲回](http://nuget.codeplex.com/workitem/424)
* [改善錯誤處理不正確地撰寫 nuspec 檔案時](http://nuget.codeplex.com/workitem/423)
* [Nuget 套件會忽略指定的檔案](http://nuget.codeplex.com/workitem/422)
* [移除第二個倒數第二個套件來源，然後按一下 [下移] 損毀 VS](http://nuget.codeplex.com/workitem/418)
* [安裝套件時移除組件參考](http://nuget.codeplex.com/workitem/413)
* [開啟 [設定] 對話方塊時的 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [在 套件管理員主控台中的套件來源的存取金鑰無法運作](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 設定對話方塊存取的索引鍵將焦點提供給錯誤的欄位](http://nuget.codeplex.com/workitem/409)
* [套件識別碼 intellisense 不應該查詢項目太多](http://nuget.codeplex.com/workitem/404)
* [將封裝加入至專案與專案名稱中的點字元時失敗](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中的指定檔案的問題](http://nuget.codeplex.com/workitem/400)
* [使用較新的組建時，應該取得註冊正確的官方摘要](http://nuget.codeplex.com/workitem/399)
* [標記應該使用空格而不是 #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少某些實用的資訊](http://nuget.codeplex.com/workitem/388)
* [將報告不當內容的連結新增至對話方塊](http://nuget.codeplex.com/workitem/386)
* [若要解壓縮封裝符號，Visual Studio 中的使用 App_Data](http://nuget.codeplex.com/workitem/380)
* [實作標記](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 允許建立不含相依性的空白封裝](http://nuget.codeplex.com/workitem/373)
* [加入封裝的擁有者欄位](http://nuget.codeplex.com/workitem/365)
* [更新到 NuGet 套件管理員，而不是 VSIX 工具的 VSIX 資訊清單](http://nuget.codeplex.com/workitem/364)
* [取得封裝命令在選取所有的來源時，會擲回錯誤](http://nuget.codeplex.com/workitem/359)
* [允許 [選項] 對話方塊中的套件來源的排序](http://nuget.codeplex.com/workitem/356)
* [更新套件不會移除舊的版本](http://nuget.codeplex.com/workitem/352)
* [相依性的實作版本範圍規格](http://nuget.codeplex.com/workitem/347)
* [按一下 [新增新的封裝] 時，visual Studio 損毀](http://nuget.codeplex.com/workitem/346)
* [顯示 [新增套件] 對話方塊中的 下載和評等](http://nuget.codeplex.com/workitem/345)
* [在對話方塊中的封裝來源之間的變更不會更新使用中的來源](http://nuget.codeplex.com/workitem/344)
* [移除套件管理員主控台 視窗中的索引鍵繫的結](http://nuget.codeplex.com/workitem/339)
* [安裝套件無法辨識為 cmdlet 名稱...](http://nuget.codeplex.com/workitem/338)
* [從本機摘要的相依性規則的摘要安裝套件就不會解析](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 應該略過仍在使用的相依性](http://nuget.codeplex.com/workitem/331)
* [如果取消頁面導覽，使用者無法瀏覽至不同的網頁原始頁面要求會傳回](http://nuget.codeplex.com/workitem/325)
* [調查效能 NuPack.Server 提供摘要給使用大量的封裝。](http://nuget.codeplex.com/workitem/324)
* [封裝的第二次我要篩選它會使用 [新增] 的封裝來源，而不是先前選取的來源。](http://nuget.codeplex.com/workitem/321)
* [選取對話方塊上的 [上線] 索引標籤時，就應該選取預設套件來源。](http://nuget.codeplex.com/workitem/320)
* [列出封裝應該依預設會顯示已安裝的套件](http://nuget.codeplex.com/workitem/309)
* [組件參考 HintPaths](http://nuget.codeplex.com/workitem/294)
* [開啟套件管理員主控台時的例外狀況](http://nuget.codeplex.com/workitem/268)
* [主控台 intellisense 下載整個摘要](http://nuget.codeplex.com/workitem/259)
* ['Default' 套件來源應該重新命名為 「 作用中 」](http://nuget.codeplex.com/workitem/258)
* [封裝來源 UI： 按下 [確定] 應該加入新的來源，如果名稱/來源欄位不可空白](http://nuget.codeplex.com/workitem/257)
* [對話方塊在已安裝的套件數目很大時速度超慢](http://nuget.codeplex.com/workitem/243)
* [支援強式名稱組件繫結重新導向](http://nuget.codeplex.com/workitem/238)
* [新增套件參考...UI 來包含向下的卸除，套件來源](http://nuget.codeplex.com/workitem/226)
* [NuPack 需要支援 agnostically 的組態檔名稱的組態轉換](http://nuget.codeplex.com/workitem/224)
* [可讓要覆寫在 NuPack.exe BasePath](http://nuget.codeplex.com/workitem/222)
* [封裝來源後援行為](http://nuget.codeplex.com/workitem/204)
* [GUI 損毀](http://nuget.codeplex.com/workitem/201)
* [加入排序選項，以新增套件 對話方塊](http://nuget.codeplex.com/workitem/179)
* [若要清除 Package Manager Console 攠摝坫](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 會導致失敗的 NuPack 主控台](http://nuget.codeplex.com/workitem/166)
* [主控台和新增套件 對話方塊應該在要求中設定使用者代理程式](http://nuget.codeplex.com/workitem/141)
* [在組建中，設定 VSIX 和 NuPack.exe 版本號碼。](http://nuget.codeplex.com/workitem/134)
* [隱藏常用 PowerShell 參數，從-？](http://nuget.codeplex.com/workitem/118)
* [新增-主控台命令的詳細的說明](http://nuget.codeplex.com/workitem/110)
* [新增套件 對話方塊應該可讓您選擇目前的封裝來源](http://nuget.codeplex.com/workitem/88)
* [將 NuPack.Core 類別移至不同的命名空間](http://nuget.codeplex.com/workitem/50)
* [新增至 cmdlet 的說明](http://nuget.codeplex.com/workitem/23)
* [在 套件下載後確認從摘要的雜湊](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

在 CTP 2 中所做的重大變更如下：

* 切換至 OData 服務端點從 ATOM 摘要的套件： 如果您升級到 CTP2 版本的 NuGet，請務必將下列 URL 新增為套件來源： `https://feed.nuget.org/ctp2/odata/v1/`。
* 已新增套件命令，以重新命名*Install-package*。
* 更新`.nuspec`格式。 `.nuspec`格式現在包含*iconUrl*欄位指定 32 x 32 png 圖示，此圖示就會顯示在 [新增套件] 對話方塊。 因此請務必設定，來區分您的套件。 `.nuspec`格式也包含新*projectUrl*欄位可用來指向提供您套件的詳細資訊的網頁。

此組建無法搭配舊版`.nupkg`檔案。 如果您收到 null 參考例外狀況時，您使用舊`.nupkg`檔案，並需要重新更新[NuGet 命令列工具](http://nuget.codeplex.com/releases/52017/download/165468)。

以下是一份功能和 NuGet CTP 2 （不含次要的程式碼清除等的 bug）。 已修正的 bug。

* [錯誤進行解壓縮封裝組件時指定組件的 TargetFramework。](http://nuget.codeplex.com/workitem/10)
* [讓使用者更容易找到 NuPack 主控台視窗](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的錯誤/例外狀況處理](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager 應妥善處理摘要相關的錯誤](http://nuget.codeplex.com/workitem/28)
* [主控台需要新的圖示](http://nuget.codeplex.com/workitem/29)
* [在對話方塊中的字串當地語系化](http://nuget.codeplex.com/workitem/38)
* [NuPack 快取下載.nupack 在記憶體中的檔案](http://nuget.codeplex.com/workitem/40)
* [NuPack 主控台： 變更顯示主控台的預設快速鍵](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 應該支援的通用屬性的預設值](http://nuget.codeplex.com/workitem/49)
* [在資料夾中執行 nupack.exe，其中只包含一個 nuspec 檔案應該使用該 nuspec](http://nuget.codeplex.com/workitem/52)
* [即使在載入任何專案/方案時才會顯示專案 功能表](http://nuget.codeplex.com/workitem/54)
* [在程式碼基底的全新複本上失敗 build.cmd](http://nuget.codeplex.com/workitem/56)
* [更新可用的功能](http://nuget.codeplex.com/workitem/57)
* [ 對話方塊中： 新增套件，以透過對話方塊移除在主控台中的提示](http://nuget.codeplex.com/workitem/73)
* [依序按一下 [安裝] 新增套件通常是沒有視覺回應緩慢](http://nuget.codeplex.com/workitem/80)
* [沒有任何方法來探索其中一個我已安裝的套件已更新。](http://nuget.codeplex.com/workitem/82)
* [沒有任何方法來更新已安裝的封裝，在對話方塊中。](http://nuget.codeplex.com/workitem/83)
* [不沒有解除安裝已安裝的封裝，在對話方塊中的任何方法](http://nuget.codeplex.com/workitem/84)
* [&ldquo;新增套件參考&hellip;&rdquo;會出現在已安裝的參考的操作功能表](http://nuget.codeplex.com/workitem/85)
* [更新之後從主控台的封裝，它會顯示舊的版本以及新的版本為已安裝](http://nuget.codeplex.com/workitem/86)
* [在主控台中，當使用對話方塊中，活動就會消失，在使用後](http://nuget.codeplex.com/workitem/87)
* [清除命令列剖析 nupack.exe 中](http://nuget.codeplex.com/workitem/89)
* [新增套件來源的易記名稱](http://nuget.codeplex.com/workitem/98)
* [若要支援包括封裝圖示更新.nuspec](http://nuget.codeplex.com/workitem/103)
* [摘要的 UI 不允許複製 URL](http://nuget.codeplex.com/workitem/105)
* [更好的移除封裝的錯誤處理。](http://nuget.codeplex.com/workitem/107)
* [在主控台視窗中鍵入取決於將游標焦點](http://nuget.codeplex.com/workitem/112)
* [錯誤訊息看起來的樣子](http://nuget.codeplex.com/workitem/116)
* [移除封裝的效能，未安裝的封裝不正確](http://nuget.codeplex.com/workitem/117)
* [移除封裝失敗時沒有套件來源](http://nuget.codeplex.com/workitem/119)
* [套件來源無法使用時，就會失敗移除封裝](http://nuget.codeplex.com/workitem/120)
* [加入套件中繼資料，並且摘要的標題。](http://nuget.codeplex.com/workitem/125)
* [新增-回到 新增套件的來源參數](http://nuget.codeplex.com/workitem/127)
* [列出封裝應該有-來源參數](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack.Server 要求 NuPack 使用者代理程式來下載套件](http://nuget.codeplex.com/workitem/142)
* [接受授權 對話方塊必須列出所有相依性的必須接受授權](http://nuget.codeplex.com/workitem/145)
* [記錄錯誤時封裝就會擲回之摘要中](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 不應該允許空&lt;licenseurl&gt;項目](http://nuget.codeplex.com/workitem/152)
* [重新列出封裝命名為 Get-封裝時，新增-封裝安裝套件，並移除套件解除安裝套件](http://nuget.codeplex.com/workitem/155)
* [使用 新增套件參考功能表項目，從 「 方案導覽損毀 Visual Studio](http://nuget.codeplex.com/workitem/158)
* [遺漏冒號 [可用的封裝來源] 標籤。](http://nuget.codeplex.com/workitem/160)
* [請.nuspec xml 項目大小寫一致地駝峰式命名法大小寫](http://nuget.codeplex.com/workitem/161)
* [必須開啟 'admin' NuPack VSIX 資訊清單](http://nuget.codeplex.com/workitem/162)
* [如果您不執行任何摘要列出封裝，您會收到 null 參考錯誤](http://nuget.codeplex.com/workitem/164)
* [nuget.exe： 指定目的地路徑](http://nuget.codeplex.com/workitem/171)
* [開啟 [套件管理] 主控台上 WinXP 的 Powershell 錯誤](http://nuget.codeplex.com/workitem/175)
* [嘗試載入套件清單時的 VS 當機](http://nuget.codeplex.com/workitem/176)
* [允許中繼套件 （沒有檔案，只是相依性）](http://nuget.codeplex.com/workitem/180)
* [將 Powershell 指令碼轉換成 Powershell 2.0 模組](http://nuget.codeplex.com/workitem/181)
* [指定目標時，PathResolver 應該捨棄的路徑部分先前萬用字元](http://nuget.codeplex.com/workitem/183)
* [沒有相依性](http://nuget.codeplex.com/workitem/186)
* [安裝 Elmah 時發生錯誤](http://nuget.codeplex.com/workitem/192)
* [組態轉換無法正常運作，與&lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [變數 ' $global: projectCache' 無法擷取，因為尚未設定](http://nuget.codeplex.com/workitem/203)
* [新增 MSBuild 工作，以建立 NuPack 套件](http://nuget.codeplex.com/workitem/205)
* [列出封裝需要支援搜尋/篩選](http://nuget.codeplex.com/workitem/206)
* [一律授權如果封裝作者提供授權 URL](http://nuget.codeplex.com/workitem/208)
* [偶爾的 「 拒絕存取 」 例外狀況，並移除封裝](http://nuget.codeplex.com/workitem/213)
* [單元測試失敗： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [提供一組後援/預設檔案，如果找不到以特定 framework 版本](http://nuget.codeplex.com/workitem/223)
* [新增套件參考...UI 無法移除封裝](http://nuget.codeplex.com/workitem/225)
* [新增套件參考損毀 studio 當一或多個專案會卸載](http://nuget.codeplex.com/workitem/228)
* [設定轉換似乎未作用於 web.debug.config 檔案](http://nuget.codeplex.com/workitem/229)
* [init.ps1 未引發自訂的套件](http://nuget.codeplex.com/workitem/237)
* [將路徑加入至 feedlist 的預設按鈕設為 [確定]，因此如果按 ENTER 它會自動關閉](http://nuget.codeplex.com/workitem/240)
* [嘗試解除安裝相依性將會損毀 VS，如果嘗試在一個資料列中的 2 倍](http://nuget.codeplex.com/workitem/241)
* [顯示在 [新增套件] 對話方塊的 專案 URL](http://nuget.codeplex.com/workitem/253)
* [預設安裝套件的 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/254)
* [將變更新增套件 對話方塊的功能表項目。](http://nuget.codeplex.com/workitem/261)
* [重新命名的命名空間和組件](http://nuget.codeplex.com/workitem/274)
* [重新命名 NuPack 專案至 NuGet](http://nuget.codeplex.com/workitem/282)
* [加入下列文字底下的 相依性清單](http://nuget.codeplex.com/workitem/288)
* [變更授權接受文字中接受授權 對話方塊](http://nuget.codeplex.com/workitem/291)
* [變更中接受授權 對話方塊的套件清單上方的文字](http://nuget.codeplex.com/workitem/292)
* [OData 不適用於 fwlink URL](http://nuget.codeplex.com/workitem/304)
* [套件管理員 UI： 透過主動快取用於分頁的套件數目](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet-&gt;套件管理員主控台錯誤](http://nuget.codeplex.com/workitem/335)
* [新增套件 對話方塊會顯示授權接受如已安裝封裝](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

以下是一份功能和 NuGet CTP 1 已修正的 bug。

* [套件延伸模組應該重新命名為.nupack](http://nuget.codeplex.com/workitem/1)
* [將封裝檔案移至資料夾](http://nuget.codeplex.com/workitem/2)
* [合併安裝&amp;新增 PS 命令](http://nuget.codeplex.com/workitem/3)
* [為動詞-名詞 」 cmdlet 建立別名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切換方案時，取得混淆 NuPack](http://nuget.codeplex.com/workitem/6)
* [我們應該預設成隱藏 [套件] 方案資料夾](http://nuget.codeplex.com/workitem/11)
* [內容項目中新增語彙基元取代的支援。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI 應該使用 PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager 將套件標示為已安裝它們之前，安裝](http://nuget.codeplex.com/workitem/27)
* [從解決方案刪除預設專案仍會顯示已刪除的專案為預設值](http://nuget.codeplex.com/workitem/30)
* [新封裝失敗，發生 「 無法新增組件為指定的 URI 因為它已經在封裝中。 」](http://nuget.codeplex.com/workitem/32)
* [從 Visual Studio GUI 中移除"NuPack 」 字串](http://nuget.codeplex.com/workitem/35)
* [加入 COPYRIGHT.txt 至 Apache 標頭檔](http://nuget.codeplex.com/workitem/36)
* [移除更新 PackageSource 命令](http://nuget.codeplex.com/workitem/37)
* [正在載入設定檔就會擲回的例外狀況時，將無法使用的套件管理員](http://nuget.codeplex.com/workitem/39)
* [init.ps1、 install.ps1 和 uninstall.ps1 需要接收其他狀態](http://nuget.codeplex.com/workitem/41)
* [將主控台及 GUI 套件組合成一個套件](http://nuget.codeplex.com/workitem/42)
* [如果套用至不在根目錄的 XML，Xml 轉換邏輯無法運作](http://nuget.codeplex.com/workitem/43)
* [管理套件來源設定對話方塊，而不會更新 NuPack 主控台](http://nuget.codeplex.com/workitem/44)
* [NuPack 主控台 UI： 重新命名以 [封裝來源] 摘要的封裝 下拉式清單](http://nuget.codeplex.com/workitem/45)
* [NuPack 主控台選項： 重新命名 ' 存放庫 UI'，以便符合 NuPack 主控台](http://nuget.codeplex.com/workitem/46)
* [新增封裝也會針對 IIS 的 URL，或是從已開啟的網站](http://nuget.codeplex.com/workitem/53)
* [封裝管理員的來源不使用 FwLink](http://nuget.codeplex.com/workitem/55)
* [設定預設套件來源](http://nuget.codeplex.com/workitem/59)
* [當只有一個來源提供時，請在選項中，新增套件來源，假設它是預設值。](http://nuget.codeplex.com/workitem/60)
* [對話方塊 UI 顯示假的 「 新 」 套件](http://nuget.codeplex.com/workitem/62)
* [選項： 按一下 取消並不會取消變更](http://nuget.codeplex.com/workitem/63)
* [新增套件參考對話方塊搜尋應該區分大小寫](http://nuget.codeplex.com/workitem/65)
* [修正在 AssemblyInfo.cs 檔中的公司的中繼資料](http://nuget.codeplex.com/workitem/67)
* [VSIX 的版本號碼](http://nuget.codeplex.com/workitem/71)
* [移除封裝： 使用-？兩次顯示說明](http://nuget.codeplex.com/workitem/72)
* [執行專案層級套件安裝/解除安裝套件](http://nuget.codeplex.com/workitem/74)
* [伺服器無法建立一個 nupack 驗證失敗時的摘要](http://nuget.codeplex.com/workitem/90)
* [需要取代 NuPack 圖示](http://nuget.codeplex.com/workitem/94)
* [NTLM http proxy 不會驗證套件摘要。](http://nuget.codeplex.com/workitem/96)
* [對話方塊不一定置中與在視窗中啟動](http://nuget.codeplex.com/workitem/100)
* [許多套件詳細資料中的欄位不會填入對話方塊中](http://nuget.codeplex.com/workitem/102)
* [UI 對話方塊不會顯示作者姓名](http://nuget.codeplex.com/workitem/108)
* [為什麼-移除封裝的版本](http://nuget.codeplex.com/workitem/113)
* [移除對話方塊 UI 上的 [最近] 索引標籤](http://nuget.codeplex.com/workitem/115)
* [VS 會損毀時正確開啟至少一個對話方塊 UI 之後按一下方案資料夾。](http://nuget.codeplex.com/workitem/126)
* [變更清單套件的-本機參數-安裝](http://nuget.codeplex.com/workitem/129)
* [重新命名 NuPack.config packages.xml](http://nuget.codeplex.com/workitem/132)
* [主控台會在行尾中強制資料指標](http://nuget.codeplex.com/workitem/135)
* [移除套件 intellisense 便會中斷](http://nuget.codeplex.com/workitem/136)
* [將 RequireLicenseAcceptance 旗標新增至.nuspec 和摘要](http://nuget.codeplex.com/workitem/137)
* [新增至.nuspec 格式和封裝的 LicenseUrl 摘要](http://nuget.codeplex.com/workitem/138)
* [按一下 安裝套件需要接受，應該會顯示接受對話方塊](http://nuget.codeplex.com/workitem/139)
* [免責聲明文字加入 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/140)
* [加入免責聲明當封裝執行主控台的第一次](http://nuget.codeplex.com/workitem/143)
* [在主控台中安裝套件之後顯示免責聲明](http://nuget.codeplex.com/workitem/144)
* [重新命名為.nupkg 的.nupack 延伸模組](http://nuget.codeplex.com/workitem/146)