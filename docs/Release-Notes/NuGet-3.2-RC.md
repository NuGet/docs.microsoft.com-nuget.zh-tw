---
title: "NuGet 3.2 RC 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 330577fa-7965-4433-98ad-b4b4575e1452
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.2 RC 版本資訊。"
keywords: "NuGet 3.2 RC 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4b5f83f521cb326f5b3a5e6c202cdcb77acde5e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC 版本資訊

[NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md)

發行 NuGet 3.2 發行候選版本 2015 年 9 月 2 日的改良功能和修正程式 3.1.1 集合。  此外，這些是第一次發行至新的 dist.nuget.org 儲存機制的第一個發行版本。

## <a name="new-features"></a>新功能

* 在相同的資料夾中的專案現在可以有不同`project.json`特有的每個專案的資料夾中的檔案。  針對每個專案，名稱`project.json`檔案`{ProjectName}.project.json`NuGet 會正確參考，並且針對每個專案可以適當地利用該內容。  這種情況支援新功能[1102年](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config`現在支援為相對路徑-globalPackagesFolder [1062年](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>命令列的更新

這是支援 NuGet v3 伺服器 nuget.exe 用戶端的第一個版本，而且還原專案封裝管理與`project.json`檔案。

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>沒有已驗證摘要的問題已解決在此版本中以改善用戶端之間的互動數目。

* 安裝 / 還原互動只能提交認證已驗證的摘要-初始要求[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)
* 推播命令無法解決從設定-認證[1248年](https://github.com/NuGet/Home/issues/1248)
* 使用者代理程式和標頭會立即提交到 NuGet 儲存機制，以協助統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>我們進行改善可更妥善處理網路失敗嘗試與遠端的 NuGet 儲存機制搭配時數：

* 改善錯誤訊息時無法連線到遠端摘要- [1238年](https://github.com/NuGet/Home/issues/1238)
* 已更正 NuGet 還原命令時，會發生錯誤狀況的正確傳回 1 [1186年](https://github.com/NuGet/Home/issues/1186)
* 現在網路連線重試一次最多 5 次故障 HTTP 5xx-每個 200 毫秒[1120年](https://github.com/NuGet/Home/issues/1120)
* 改善伺服器重新導向回應的處理期間的推播命令- [1051年](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`現在支援 URL 或儲存機制名稱做為引數-Nuget.Config [1046年](https://github.com/NuGet/Home/issues/1046)
* 遺漏已在還原期間不位於儲存機制的套件現在會報告為錯誤，而非警告[1038年](https://github.com/NuGet/Home/issues/1038)
* 已更正的 Unix/Linux 案例-\r\n multipartwebrequest 處理[776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>有許多使用各種命令的問題的修正：

* 推播命令不會再對套件來源-PUT 之前 GET [1237年](https://github.com/NuGet/Home/issues/1237)
* List 命令不會再重複一次的版本號碼為[1185年](https://github.com/NuGet/Home/issues/1185)
* 組件使用-建置引數現在正確支援 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)
* 已修正的問題嘗試將組件 F # 專案建置 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)
* 封裝已存在時，還原現在沒有 ops [1040年](https://github.com/NuGet/Home/issues/1040)
* 改良的錯誤訊息`packages.config`檔案格式不正確- [1034年](https://github.com/NuGet/Home/issues/1034)
* 修正與 restore 命令`-SolutionDirectory`切換到使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)
* 改善更新命令，以支援整個方案的更新- [924](https://github.com/NuGet/Home/issues/924)

在此版本中解決問題的完整清單位於 NuGet GitHub[命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。

## <a name="visual-studio-extension-updates"></a>Visual Studio 擴充功能更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 中的新功能

* 新的操作功能表項目已加入可讓封裝以建置方案，才能還原 [解決方案] 節點上的 [方案總管] ([1274年](https://github.com/NuGet/Home/issues/1274))。

![新 '還原封裝' 操作功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新和修正程式，Visual Studio 中

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>修正已驗證的摘要已彙總，並且處理中的延伸模組。  下列的驗證項目也是延伸模組中定址：

* 現在正確視為 NuGet v3 驗證摘要正常運作，而不是 v2 通過驗證後摘要- [1216年](https://github.com/NuGet/Home/issues/1216)
* 修正過的要求，在專案中使用的驗證認證`project.json`和溝通 v2 摘要- [1082年](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>網路連線有影響的使用者介面，在 Visual Studio 中，我們解決這有下列的修正程式：

* 改善的封裝版本的本機快取維護[1096年](https://github.com/NuGet/Home/issues/1096)
* 當連接至 v3，摘要不會再將它視為 v2 摘要-嘗試變更失敗行為[1253年](https://github.com/NuGet/Home/issues/1253)
* 使用多個封裝來源的安裝封裝時，現在防止安裝失敗[1183年](https://github.com/NuGet/Home/issues/1183)

我們改進處理的建置作業之間的互動：

* 現在繼續建立專案，如果還原封裝的單一專案失敗- [1169年](https://github.com/NuGet/Home/issues/1169)
* 安裝到方案中的另一個專案相依於專案的封裝會強制方案重建- [981](https://github.com/NuGet/Home/issues/981)
* 修正失敗的封裝會安裝至專案的正確復原變更[1265年](https://github.com/NuGet/Home/issues/1265)
* 已更正不小心移除`developmentDependency`屬性中的封裝`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)
* 呼叫`install.ps1`現在有適當的`$package.AssemblyReferences`物件傳遞為[1245年](https://github.com/NuGet/Home/issues/1245)
* 不會再妨礙解除安裝 UWP 專案中的封裝專案處於不正常的狀態時[1128年](https://github.com/NuGet/Home/issues/1128)
* 包含混合方案`packages.config`和`project.json`專案現在正確建置而不需要第二個建置作業- [1122年](https://github.com/NuGet/Home/issues/1122)
* 適當地尋找 app.config 檔案，如果連結或位於不同的資料夾- [1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)
* UWP 專案現在可以安裝未列出的套件- [1109年](https://github.com/NuGet/Home/issues/1109)
* 封裝還原現在允許時方案不是處於已儲存的狀態- [1081年](https://github.com/NuGet/Home/issues/1081)


處理的組態檔已更正的更新：

* 從封裝的後續組建不會再移除目標檔案傳遞`project.json`受管理的專案- [1288年](https://github.com/NuGet/Home/issues/1288)
* 無法再修改 Nuget.Config 檔案在 ASP.NET 5 方案建置- [1201年](https://github.com/NuGet/Home/issues/1201)
* 不會再變更期間套件更新為允許版本條件約束[1130年](https://github.com/NuGet/Home/issues/1130)
* 鎖定檔案現在保持鎖定期間組建- [1127年](https://github.com/NuGet/Home/issues/1127)
* 現在修改`packages.config`和不重寫期間更新- [585](https://github.com/NuGet/Home/issues/585)


已改進 TFS 原始檔控制的互動：

* 不會再失敗的封裝繫結至 TFS 的安裝[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)
* 修正過的 NuGet 使用者介面，讓 TFS 2013 整合- [1071年](https://github.com/NuGet/Home/issues/1071)
* 已更正封裝還原正確來自封裝資料夾的參考[1004年](https://github.com/NuGet/Home/issues/1004)

最後，我們也有所改善，這些項目：

* 針對記錄檔訊息的詳細等級縮小`project.json`managed 專案的[1163年](https://github.com/NuGet/Home/issues/1163)
* 現在正確安裝的封裝版本使用者介面中顯示為[1061年](https://github.com/NuGet/Home/issues/1061)


Visual Studio 擴充功能可以找到 NuGet GitHub 中解決問題的完整清單[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>已知問題

我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)