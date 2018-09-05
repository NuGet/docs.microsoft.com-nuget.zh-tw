---
title: NuGet 3.2 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.2 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551494"
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC 版本資訊

[NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md)

發行候選版 NuGet 3.2 2015 年 9 月 2 日的改進和修正 3.1.1 集合版本。  此外，這些是第一次發行至新的 dist.nuget.org 存放庫的第一個版本。

## <a name="new-features"></a>新功能

* 存在於相同的資料夾中的專案現在可以有不同`project.json`特有的每個專案的資料夾中的檔案。  針對每個專案，命名`project.json`檔案`{ProjectName}.project.json`NuGet 會正確地參考，並且適當地為每個專案使用該內容。  這可支援的新功能[1102年](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` 現在支援為相對路徑-globalPackagesFolder [1062年](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>命令列的更新

這是支援 NuGet v3 伺服器的 nuget.exe 用戶端的第一個版本，並使用正在還原專案的封裝管理`project.json`檔案。

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>沒有已驗證摘要處理問題，都在此版本中提升用戶端之間的互動數。

* 安裝 / 還原互動只會提交已驗證的摘要-的初始要求的認證[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)
* 推送命令無法解決從組態集的認證[1248年](https://github.com/NuGet/Home/issues/1248)
* 使用者代理程式 」 和 「 標頭現在會提交至 NuGet 存放庫，來協助進行統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>我們進行了多項改良，可更妥善處理網路失敗，嘗試使用遠端的 NuGet 存放庫：

* 改進錯誤訊息時無法連線到遠端的摘要- [1238年](https://github.com/NuGet/Home/issues/1238)
* 已更正 NuGet 還原命令，以正確地傳回 1，當錯誤狀況，就會發生- [1186年](https://github.com/NuGet/Home/issues/1186)
* 現在重試網路連線的 HTTP 5xx 故障-5 的嘗試次數最多每隔 200 毫秒[1120年](https://github.com/NuGet/Home/issues/1120)
* 改進的伺服器重新導向回應的處理期間的 push 命令- [1051年](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 現在支援 URL 或儲存機制名稱做為引數-Nuget.Config [1046年](https://github.com/NuGet/Home/issues/1046)
* 遺漏的套件在還原期間不位於存放庫現在會回報為錯誤而非警告[1038年](https://github.com/NuGet/Home/issues/1038)
* 已更正的 Unix/Linux 案例-\r\n multipartwebrequest 處理[776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>有數個與各種命令的問題的修正：

* 推送命令不會再發生之前對套件來源-PUT GET [1237年](https://github.com/NuGet/Home/issues/1237)
* 列出命令不會再重複的版本號碼- [1185年](https://github.com/NuGet/Home/issues/1185)
* 組件使用-建置引數現在正確支援 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)
* 已修正的問題，嘗試將組件的 F # 專案建置與 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)
* 還原現在不會生效，當封裝已經存在- [1040年](https://github.com/NuGet/Home/issues/1040)
* 改良的錯誤訊息的時機`packages.config`檔案格式不正確- [1034年](https://github.com/NuGet/Home/issues/1034)
* 已更正與 restore 命令`-SolutionDirectory`切換到使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)
* 改善更新命令，以支援整個方案的更新- [924](https://github.com/NuGet/Home/issues/924)

在此版本中已解決問題的完整清單可在 NuGet GitHub[命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。

## <a name="visual-studio-extension-updates"></a>Visual Studio 擴充功能更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 中的新功能

* 新的操作功能表項目已加入至方案總管中，於 [方案] 節點，可讓封裝以建置方案，才能還原 ([1274年](https://github.com/NuGet/Home/issues/1274))。

![新 '還原套件' 操作功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新和修正在 Visual Studio 中

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>已驗證的摘要的修正彙總中的延伸模組已解決。  延伸模組已也將討論下列驗證項目：

* 現在正確將 NuGet v3 已驗證的摘要正確，而不是如 v2 驗證摘要- [1216年](https://github.com/NuGet/Home/issues/1216)
* 已更正的要求，在專案中使用的驗證認證`project.json`，而且與 v2 摘要-通訊[1082年](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>網路連線有影響的使用者介面，在 Visual Studio 中，和我們解決這與下列修正：

* 改善的套件版本的本機快取維護[1096年](https://github.com/NuGet/Home/issues/1096)
* 連接至 v3，不會再嘗試將它視為 v2 摘要-摘要時，變更失敗行為[1253年](https://github.com/NuGet/Home/issues/1253)
* 現在會導致安裝失敗，使用多個套件來源-安裝套件時[1183年](https://github.com/NuGet/Home/issues/1183)

我們已改善建置作業之間的互動的處理：

* 現在繼續建立專案，如果還原套件，針對單一專案失敗- [1169年](https://github.com/NuGet/Home/issues/1169)
* 套件安裝至專案的方案中的另一個專案相依於強制方案重建- [981](https://github.com/NuGet/Home/issues/981)
* 已更正失敗的封裝會安裝正確的回復變更的專案- [1265年](https://github.com/NuGet/Home/issues/1265)
* 已更正不小心移除`developmentDependency`中的封裝屬性`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)
* 呼叫`install.ps1`現在有適當`$package.AssemblyReferences`物件傳遞為[1245年](https://github.com/NuGet/Home/issues/1245)
* 不會再導致解除安裝的 UWP 專案中的封裝專案時處於不正常的狀態- [1128年](https://github.com/NuGet/Home/issues/1128)
* 解決方案包含各種`packages.config`並`project.json`而不需要第二個現在正確建置的專案建立作業- [1122年](https://github.com/NuGet/Home/issues/1122)
* 適當地尋找 app.config 檔案，如果其為連結，或位於不同的資料夾- [1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)
* UWP 專案現在可以安裝未列出的套件- [1109年](https://github.com/NuGet/Home/issues/1109)
* 套件還原不允許使用時的方案不是處於儲存狀態- [1081年](https://github.com/NuGet/Home/issues/1081)


處理已更正檔案的組態更新：

* 從後續建置的套件不會再移除目標檔案傳遞`project.json`受管理的專案- [1288年](https://github.com/NuGet/Home/issues/1288)
* 無法再修改 ASP.NET 5 方案建置-期間的 Nuget.Config 檔案[1201年](https://github.com/NuGet/Home/issues/1201)
* 不會再變更套件的更新-期間允許版本條件約束[1130年](https://github.com/NuGet/Home/issues/1130)
* 鎖定檔案現在保持鎖定狀態期間組建- [1127年](https://github.com/NuGet/Home/issues/1127)
* 現在修改`packages.config`並不重寫期間更新- [585](https://github.com/NuGet/Home/issues/585)


TFS 原始檔控制與互動都已獲得改善：

* 不會再失敗的繫結至 TFS-的套件會安裝[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)
* 已更正的 NuGet 使用者介面，以允許 TFS 2013 整合- [1071年](https://github.com/NuGet/Home/issues/1071)
* 已更正正確來自的 packages 資料夾-還原的套件參考[1004年](https://github.com/NuGet/Home/issues/1004)

最後，我們也改進了這些項目：

* 記錄檔訊息詳細程度降低`project.json`managed 專案- [1163年](https://github.com/NuGet/Home/issues/1163)
* 現在正確顯示使用者介面-中的 安裝的封裝的版本[1061年](https://github.com/NuGet/Home/issues/1061)


Visual Studio 擴充功能可以找到 NuGet GitHub 中的已解決問題的完整清單[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>已知問題

我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)