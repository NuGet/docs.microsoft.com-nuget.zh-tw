---
title: "NuGet 1.0 和 1.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.1 版本資訊。"
keywords: "NuGet 1.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a596e61f144e7269f703f2dba3dddb4fd338e6a
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 和 1.1 版版本資訊

[NuGet 1.2 的版本資訊](../release-notes/nuget-1.2.md)

NuGet 1.0 已於 2011 年 1 月 13 日發行。  NuGet 1.1 已於 2011 年 2 月 12 日發行。

## <a name="overview"></a>總覽

本文件包含 NuGet 1.0 主要的預覽版本進行分組的各種版本的版本資訊。

NuGet 會包含下列元件：

* *NuGet.Tools.vsix* * 所組成：
  * **新增程式庫封裝對話方塊*** Visual Studio 用來瀏覽及安裝套件 對話方塊。
  * **Package Manager Console** * Powershell 型的 Visual Studio 中的主控台。
* *NuGet 命令列工具** 工具用來建立 （及最終發佈） 封裝。

NuGet 工具 Visual Studio 擴充功能 (*NuGet.Tools.vsix*) 需要：

* Visual Studio 2010 或 Visual Web Developer 2010 Express。

需要 NuGet 命令列工具：

* .NET framework 4 版

## <a name="installation"></a>安裝

若要使用這個[最新版本](http://nuget.codeplex.com/releases/view/52018):

* 先解除安裝較舊組建。 您要與執行以系統管理員身分執行此動作。
* 移除您所擁有的所有現有摘要。
* 加入新的摘要指向[http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669)。

## <a name="nuget-11"></a>NuGet 1.1

在此版本中修正的問題清單[可以在這裡找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

一個問題已修正自 RC RTM。

* [問題 474： 移除封裝會影響方案中的所有專案](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>發行候選版本

以下是自 CTP 2 本發行候選版本中所做的變更。 請瀏覽問題追蹤程式，以查看完整的 bug 清單。

* [更新套件的主控台不會更新相依性。](http://nuget.codeplex.com/workitem/443)
* [Bin 加入封裝拾取不套件參考 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [更新封裝離開中斷的參考](http://nuget.codeplex.com/workitem/440)
* [取得封裝的更新失敗，在對話方塊中，或在主控台中選取 所有' 彙總來源](http://nuget.codeplex.com/workitem/439)
* [取得封裝驗證錯誤](http://nuget.codeplex.com/workitem/426)
* [無法安裝封裝，從 [新增套件] 對話方塊時警告使用者](http://nuget.codeplex.com/workitem/425)
* [取得封裝的更新封裝的大數目時，更新會擲回](http://nuget.codeplex.com/workitem/424)
* [改善錯誤處理時 nuspec 檔案撰寫不正確](http://nuget.codeplex.com/workitem/423)
* [Nuget 套件會忽略指定的檔案](http://nuget.codeplex.com/workitem/422)
* [移除第二個到最後一個封裝來源，然後按一下 [下移] 損毀 VS](http://nuget.codeplex.com/workitem/418)
* [安裝封裝時移除組件參考](http://nuget.codeplex.com/workitem/413)
* [開啟 [設定] 對話方塊時 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [Package Manager Console 中的封裝來源的存取金鑰無法運作](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 設定對話方塊存取的索引鍵將焦點提供給錯誤的欄位](http://nuget.codeplex.com/workitem/409)
* [封裝識別碼 intellisense 不應該查詢項目太多](http://nuget.codeplex.com/workitem/404)
* [將封裝加入至專案，以點字元專案名稱中的失敗](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中指定的檔案的問題](http://nuget.codeplex.com/workitem/400)
* [使用較新組建時，應該取得註冊正確官方摘要](http://nuget.codeplex.com/workitem/399)
* [標記應該使用空格而不是 #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少某些有用的資訊](http://nuget.codeplex.com/workitem/388)
* [將報表濫用連結加入至對話方塊](http://nuget.codeplex.com/workitem/386)
* [若要解壓縮封裝符號，Visual Studio 中的使用 App_Data](http://nuget.codeplex.com/workitem/380)
* [實作標記](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 可讓不含相依性建立的空白封裝](http://nuget.codeplex.com/workitem/373)
* [加入封裝的擁有者欄位](http://nuget.codeplex.com/workitem/365)
* [更新說出 NuGet 封裝管理員，而不是 VSIX 工具的 VSIX 資訊清單](http://nuget.codeplex.com/workitem/364)
* [取得封裝的命令在選取所有的來源時，會擲回錯誤](http://nuget.codeplex.com/workitem/359)
* [允許的選項 對話方塊中的封裝來源順序](http://nuget.codeplex.com/workitem/356)
* [更新套件不會移除舊的版本](http://nuget.codeplex.com/workitem/352)
* [相依性的實作版本範圍規格](http://nuget.codeplex.com/workitem/347)
* [按一下 [加入新的封裝] 時，visual Studio 損毀](http://nuget.codeplex.com/workitem/346)
* [在 [新增套件] 對話方塊中顯示的下載與分級](http://nuget.codeplex.com/workitem/345)
* [在對話方塊中的封裝來源之間的變更不會更新使用中的來源](http://nuget.codeplex.com/workitem/344)
* [移除封裝管理員主控台 視窗的索引鍵繫結](http://nuget.codeplex.com/workitem/339)
* [安裝套件無法辨識為指令程式名稱...](http://nuget.codeplex.com/workitem/338)
* [無法解析安裝封裝，從本機摘要的相依性規則的摘要](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 應該略過仍在使用的相依性](http://nuget.codeplex.com/workitem/331)
* [如果取消頁面巡覽，使用者無法瀏覽至其他頁面而原始頁面要求會傳回](http://nuget.codeplex.com/workitem/325)
* [請調查 NuPack.Server 的效能摘要提供使用大量的封裝。](http://nuget.codeplex.com/workitem/324)
* [封裝的第二次我篩選它會使用 「 新增 」 封裝來源，而不是先前選取的來源。](http://nuget.codeplex.com/workitem/321)
* [選取對話方塊上的 「 上線 」 索引標籤時，就應該選取預設的封裝來源。](http://nuget.codeplex.com/workitem/320)
* [列出封裝應顯示預設的已安裝的封裝](http://nuget.codeplex.com/workitem/309)
* [組件參考 HintPaths](http://nuget.codeplex.com/workitem/294)
* [開啟 Package Manager Console 時發生例外狀況](http://nuget.codeplex.com/workitem/268)
* [主控台 intellisense 下載整個摘要](http://nuget.codeplex.com/workitem/259)
* ['Default' 封裝來源應該重新命名為 'Active'](http://nuget.codeplex.com/workitem/258)
* [封裝來源 UI： 按下 [確定] 應該加入新的來源，如果名稱/來源欄位不可空白](http://nuget.codeplex.com/workitem/257)
* [已安裝的封裝數目很大時，對話方塊變成 super 緩慢](http://nuget.codeplex.com/workitem/243)
* [支援強式名稱組件繫結重新導向](http://nuget.codeplex.com/workitem/238)
* [新增封裝參考...UI 以向下包含封裝來源拖放](http://nuget.codeplex.com/workitem/226)
* [NuPack 需要支援的組態檔名稱 agnostically config 轉換](http://nuget.codeplex.com/workitem/224)
* [允許將它覆寫 NuPack.exe 中的基本路徑](http://nuget.codeplex.com/workitem/222)
* [封裝來源後援行為](http://nuget.codeplex.com/workitem/204)
* [GUI 損毀](http://nuget.codeplex.com/workitem/201)
* [加入排序新增套件 對話方塊的選項](http://nuget.codeplex.com/workitem/179)
* [若要清除在 Package Manager Console 攠摝坫](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 會導致失敗的 NuPack 主控台](http://nuget.codeplex.com/workitem/166)
* [主控台和新增套件 對話方塊應該在要求中設定使用者代理程式](http://nuget.codeplex.com/workitem/141)
* [在組建中，設定 VSIX 和 NuPack.exe 版本號碼。](http://nuget.codeplex.com/workitem/134)
* [隱藏一般 PowerShell 參數？](http://nuget.codeplex.com/workitem/118)
* [新增主控台命令詳細的的說明](http://nuget.codeplex.com/workitem/110)
* [新增套件 對話方塊應該允許選擇目前的封裝來源](http://nuget.codeplex.com/workitem/88)
* [將 NuPack.Core 類別移至不同的命名空間](http://nuget.codeplex.com/workitem/50)
* [新增至 cmdlet 的說明](http://nuget.codeplex.com/workitem/23)
* [在套件下載後確認從摘要的雜湊](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

以下是最重要 CTP 2 中所做的變更：

* 切換至 OData 服務端點從 ATOM 摘要的封裝： 如果您升級到 CTP2 版本的 NuGet，請務必新增為套件來源的下列 URL: https://feed.nuget.org/ctp2/odata/v1/。
* 重新命名以 [新增套件] 命令*Install-package*。
* 更新`.nuspec`格式。 `.nuspec`格式現在包含*iconUrl*欄位來指定將會顯示在 [新增套件] 對話方塊 32 x 32 png 圖示。 因此請務必設定，以區別您的封裝。 `.nuspec`格式亦包含新*projectUrl*欄位可用來指向提供封裝的詳細資訊的網頁。

此組建將無法運作，與舊`.nupkg`檔案。 如果您收到 null 參考例外狀況，您要使用舊`.nupkg`檔案，並需要重建與更新[NuGet 命令列工具](http://nuget.codeplex.com/releases/52017/download/165468)。

以下是功能清單 （不包括錯誤的次要的程式碼清除等）。 NuGet CTP 2 已獲得修正的 bug。

* [解壓縮封裝組件的錯誤時與指定之組件 TargetFramework。](http://nuget.codeplex.com/workitem/10)
* [請更容易找到 NuPack 主控台視窗](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的錯誤/例外狀況處理](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager 應妥善處理摘要相關的錯誤](http://nuget.codeplex.com/workitem/28)
* [主控台需要新的圖示](http://nuget.codeplex.com/workitem/29)
* [在對話方塊中的字串當地語系化](http://nuget.codeplex.com/workitem/38)
* [NuPack 快取下載的.nupack 檔案中的記憶體](http://nuget.codeplex.com/workitem/40)
* [NuPack 主控台： 變更預設快速鍵顯示主控台](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 應該支援的通用屬性的預設值](http://nuget.codeplex.com/workitem/49)
* [執行 nupack.exe 資料夾中只有一個 nuspec 檔案，則應該使用該 nuspec](http://nuget.codeplex.com/workitem/52)
* [即使載入任何專案/方案時顯示的專案 功能表](http://nuget.codeplex.com/workitem/54)
* [在程式碼基底的全新複本上的 build.cmd 失敗](http://nuget.codeplex.com/workitem/56)
* [更新可用的功能](http://nuget.codeplex.com/workitem/57)
* [對話方塊： 加入封裝，以透過對話方塊在主控台中移除提示](http://nuget.codeplex.com/workitem/73)
* [新增套件，依序按一下 [安裝] 通常是沒有視覺回應緩慢](http://nuget.codeplex.com/workitem/80)
* [沒有任何方法來探索我已安裝的套件必須有更新。](http://nuget.codeplex.com/workitem/82)
* [沒有任何方法以更新對話方塊中已安裝的封裝。](http://nuget.codeplex.com/workitem/83)
* [沒有任何方法來解除安裝 對話方塊中已安裝的封裝](http://nuget.codeplex.com/workitem/84)
* [&ldquo;新增封裝參考&hellip;&rdquo;會出現在已安裝參照的內容功能表](http://nuget.codeplex.com/workitem/85)
* [在更新之後從主控台的封裝，它會顯示舊的版本與新的版本已安裝](http://nuget.codeplex.com/workitem/86)
* [使用之後，在主控台中，當使用對話方塊中，活動會消失](http://nuget.codeplex.com/workitem/87)
* [清除命令列剖析 nupack.exe 中](http://nuget.codeplex.com/workitem/89)
* [加入封裝來源中的易記名稱](http://nuget.codeplex.com/workitem/98)
* [更新.nuspec 支援包括套件圖示](http://nuget.codeplex.com/workitem/103)
* [摘要的 UI 不允許複製 URL](http://nuget.codeplex.com/workitem/105)
* [更好的移除封裝的錯誤處理。](http://nuget.codeplex.com/workitem/107)
* [在主控台視窗中輸入取決於將游標焦點](http://nuget.codeplex.com/workitem/112)
* [錯誤訊息看起來的樣子](http://nuget.codeplex.com/workitem/116)
* [移除封裝的效能，也未安裝的套件已損毀](http://nuget.codeplex.com/workitem/117)
* [移除封裝失敗時沒有套件來源](http://nuget.codeplex.com/workitem/119)
* [封裝來源無法使用時，移除封裝會失敗](http://nuget.codeplex.com/workitem/120)
* [加入封裝中繼資料和摘要的標題。](http://nuget.codeplex.com/workitem/125)
* [新增-來源參數傳回給加入封裝](http://nuget.codeplex.com/workitem/127)
* [清單套件都應該有-來源參數](http://nuget.codeplex.com/workitem/128)
* [若要要求 NuPack 使用者代理程式來下載套件的更新 NuPack.Server](http://nuget.codeplex.com/workitem/142)
* [授權接受對話方塊必須列出授權要求接受的所有相依性](http://nuget.codeplex.com/workitem/145)
* [記錄錯誤時封裝就會擲回之摘要中](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 應該不允許空&lt;licenseurl&gt;項目](http://nuget.codeplex.com/workitem/152)
* [將列出封裝重新命名為 Get 封裝，加入-封裝安裝套件，並移除套件解除安裝套件](http://nuget.codeplex.com/workitem/155)
* [使用新增封裝參考功能表項目，從方案導覽損毀 Visual Studio](http://nuget.codeplex.com/workitem/158)
* [遺漏冒號 [可用的封裝來源] 標籤。](http://nuget.codeplex.com/workitem/160)
* [請.nuspec xml 項目大小寫一致地 camel 命名法的大小寫](http://nuget.codeplex.com/workitem/161)
* [若要開啟 「 管理員 」 位元必須 NuPack VSIX 資訊清單](http://nuget.codeplex.com/workitem/162)
* [如果您列出封裝執行了任何摘要時，會產生 null 參考錯誤](http://nuget.codeplex.com/workitem/164)
* [nuget.exe： 指定目的地路徑](http://nuget.codeplex.com/workitem/171)
* [開啟 套件管理主控台上 WinXP Powershell 錯誤](http://nuget.codeplex.com/workitem/175)
* [VS 損毀時嘗試載入的封裝清單](http://nuget.codeplex.com/workitem/176)
* [允許中繼封裝 （沒有檔案、 相依性）](http://nuget.codeplex.com/workitem/180)
* [將 Powershell 指令碼轉換成 Powershell 2.0 模組](http://nuget.codeplex.com/workitem/181)
* [指定目標時，PathResolver 應該捨棄路徑部分都與先前萬用字元](http://nuget.codeplex.com/workitem/183)
* [沒有任何相依性](http://nuget.codeplex.com/workitem/186)
* [安裝 Elmah 時發生錯誤](http://nuget.codeplex.com/workitem/192)
* [設定轉換不正確地使用&lt;c&gt;](http://nuget.codeplex.com/workitem/194)
* [變數 ' $全域： projectCache' 無法擷取，因為尚未設定](http://nuget.codeplex.com/workitem/203)
* [將加入 MSBuild 工作，以建立 NuPack 封裝](http://nuget.codeplex.com/workitem/205)
* [列出封裝需要支援搜尋/篩選](http://nuget.codeplex.com/workitem/206)
* [一律授權如果封裝作者提供授權 URL](http://nuget.codeplex.com/workitem/208)
* [偶發的 「 拒絕存取 」 例外狀況，並移除封裝](http://nuget.codeplex.com/workitem/213)
* [單元測試失敗： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [允許後援/預設的檔案集，如果找不到以特定的 framework 版本](http://nuget.codeplex.com/workitem/223)
* [新增封裝參考...UI 無法移除封裝](http://nuget.codeplex.com/workitem/225)
* [新增封裝參考發生當機 studio 當一個或多個專案是卸載](http://nuget.codeplex.com/workitem/228)
* [Config 轉換，似乎不處理 web.debug.config 檔案](http://nuget.codeplex.com/workitem/229)
* [init.ps1 不引發自訂封裝](http://nuget.codeplex.com/workitem/237)
* [將路徑加入至 feedlist 的預設按鈕設為 [確定]，因此如果按 ENTER 它會自動關閉](http://nuget.codeplex.com/workitem/240)
* [嘗試解除安裝相依性將會損毀 VS，如果嘗試在資料列中的 2 倍](http://nuget.codeplex.com/workitem/241)
* [在 [新增套件] 對話方塊中顯示專案 URL](http://nuget.codeplex.com/workitem/253)
* [預設已安裝的套件 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/254)
* [將變更新增套件 對話方塊的功能表項目。](http://nuget.codeplex.com/workitem/261)
* [重新命名的命名空間和組件](http://nuget.codeplex.com/workitem/274)
* [重新命名 NuPack 專案至 NuGet](http://nuget.codeplex.com/workitem/282)
* [加入下列文字底下的相依性清單](http://nuget.codeplex.com/workitem/288)
* [變更授權接受對話方塊中的授權接受文字](http://nuget.codeplex.com/workitem/291)
* [變更在 授權接受對話方塊中的封裝清單上方的文字](http://nuget.codeplex.com/workitem/292)
* [OData 無法搭配 fwlink URL](http://nuget.codeplex.com/workitem/304)
* [封裝管理員 UI： 透過主動快取封裝用於分頁的計數](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet-&gt; Package Manager Console 錯誤](http://nuget.codeplex.com/workitem/335)
* [新增套件 對話方塊會顯示授權接受的已安裝封裝](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

以下是功能 NuGet CTP 1 已獲得修正的 bug 清單。

* [組件延伸應該會重新命名為.nupack](http://nuget.codeplex.com/workitem/1)
* [將封裝檔案移到資料夾](http://nuget.codeplex.com/workitem/2)
* [合併安裝&amp;新增 PS 命令](http://nuget.codeplex.com/workitem/3)
* [為動詞-名詞 」 cmdlet 建立別名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切換方案時，取得混淆 NuPack](http://nuget.codeplex.com/workitem/6)
* [依預設，我們應該隱藏 'packages' 方案資料夾](http://nuget.codeplex.com/workitem/11)
* [內容項目中新增語彙基元替換的支援。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI 應該使用 PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager 將標示封裝為安裝它們之前，安裝](http://nuget.codeplex.com/workitem/27)
* [刪除預設專案從方案仍會顯示已刪除的專案做為預設值](http://nuget.codeplex.com/workitem/30)
* [新封裝會失敗，並 無法新增部分為指定的 URI 因為它已經在封裝中。](http://nuget.codeplex.com/workitem/32)
* [從 Visual Studio GUI 移除"NuPack 」 字串](http://nuget.codeplex.com/workitem/35)
* [加入 COPYRIGHT.txt 至 Apache 標頭檔](http://nuget.codeplex.com/workitem/36)
* [移除更新 PackageSource 命令](http://nuget.codeplex.com/workitem/37)
* [封裝管理員無法使用載入設定檔時擲回例外狀況](http://nuget.codeplex.com/workitem/39)
* [init.ps1 install.ps1，uninstall.ps1 需要接收其他狀態](http://nuget.codeplex.com/workitem/41)
* [將主控台和 GUI 封裝結合成單一套件](http://nuget.codeplex.com/workitem/42)
* [如果套用至不在根目錄的 XML，Xml 轉換邏輯無法運作](http://nuget.codeplex.com/workitem/43)
* [管理未更新 NuPack 主控台的封裝來源設定對話方塊](http://nuget.codeplex.com/workitem/44)
* [NuPack 主控台 UI： 重新命名 '封裝來源' 摘要的 「 封裝 」 下拉式清單](http://nuget.codeplex.com/workitem/45)
* [NuPack 主控台選項： 重新命名 ' 儲存機制 UI' NuPack 主控台與一致](http://nuget.codeplex.com/workitem/46)
* [加入封裝失敗時針對開啟從 IIS 或 URL 的網站](http://nuget.codeplex.com/workitem/53)
* [封裝管理員的來源不能使用 FwLink](http://nuget.codeplex.com/workitem/55)
* [設定預設的封裝來源](http://nuget.codeplex.com/workitem/59)
* [當加入封裝來源 選項，提供唯一的來源時，會假設它是預設值。](http://nuget.codeplex.com/workitem/60)
* [對話方塊 UI 顯示假的 「 最新 」 封裝](http://nuget.codeplex.com/workitem/62)
* [選項： 按一下 [取消] 5d; 並不會取消變更](http://nuget.codeplex.com/workitem/63)
* [新增套件參考對話方塊搜尋應該不區分大小寫](http://nuget.codeplex.com/workitem/65)
* [在 AssemblyInfo.cs 檔案中修正公司中繼資料](http://nuget.codeplex.com/workitem/67)
* [Vsix 的版本號碼](http://nuget.codeplex.com/workitem/71)
* [移除封裝： 使用-？顯示說明兩次](http://nuget.codeplex.com/workitem/72)
* [執行安裝/解除安裝封裝的專案層級的封裝](http://nuget.codeplex.com/workitem/74)
* [伺服器無法建立一個 nupack 驗證失敗時的摘要](http://nuget.codeplex.com/workitem/90)
* [需要取代 NuPack 圖示](http://nuget.codeplex.com/workitem/94)
* [NTLM http proxy 不會驗證摘要的封裝。](http://nuget.codeplex.com/workitem/96)
* [對話方塊不一定置中與在視窗中啟動](http://nuget.codeplex.com/workitem/100)
* [許多封裝詳細資料中的欄位未被填入對話方塊](http://nuget.codeplex.com/workitem/102)
* [UI 對話方塊不會顯示作者姓名](http://nuget.codeplex.com/workitem/108)
* [為什麼-移除封裝版本](http://nuget.codeplex.com/workitem/113)
* [移除對話方塊 UI 上的 [最近] 索引標籤](http://nuget.codeplex.com/workitem/115)
* [VS 損毀時右邊按一下方案資料夾開啟對話方塊 UI 至少一個之後。](http://nuget.codeplex.com/workitem/126)
* [變更清單封裝-本機參數-安裝](http://nuget.codeplex.com/workitem/129)
* [重新命名 NuPack.config packages.xml](http://nuget.codeplex.com/workitem/132)
* [主控台會在行尾中強制資料指標](http://nuget.codeplex.com/workitem/135)
* [移除封裝 intellisense 已中斷](http://nuget.codeplex.com/workitem/136)
* [將 RequireLicenseAcceptance 旗標加入.nuspec 和摘要](http://nuget.codeplex.com/workitem/137)
* [新增.nuspec 格式和套件的 LicenseUrl 摘要](http://nuget.codeplex.com/workitem/138)
* [按一下 安裝套件需要接受，應該會顯示接受對話方塊](http://nuget.codeplex.com/workitem/139)
* [免責聲明文字加入 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/140)
* [新增免責聲明當封裝執行主控台的第一次](http://nuget.codeplex.com/workitem/143)
* [在主控台安裝封裝之後顯示免責聲明](http://nuget.codeplex.com/workitem/144)
* [重新命名.nupkg.nupack 延伸模組](http://nuget.codeplex.com/workitem/146)