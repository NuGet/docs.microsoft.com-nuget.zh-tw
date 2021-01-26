---
title: NuGet 3.2 版本資訊
description: NuGet 3.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780306"
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 版本資訊

[NuGet 3.2-RC 版本](../release-notes/nuget-3.2-RC.md)  |  資訊[NuGet 3.2.1 版本](../release-notes/nuget-3.2.1.md)資訊

NuGet 3.2 于2015年9月16日發行為3.1.1 版本的改進和修正集合，可從 [dist.nuget.org](http://dist.nuget.org/index.html) 和 [Visual Studio 資源庫](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)取得。

## <a name="new-features"></a>新功能

* 存在於相同資料夾中的專案現在可以 `project.json` 在每個專案特有的該資料夾中有不同的檔案。  針對每個專案，為檔案命名， `project.json` `{ProjectName}.project.json` 且 NuGet 會適當地為每個專案提供該設定的喜好設定。  只有安裝 Windows 10 Tools v1.1 才支援此功能-  [1102](https://github.com/NuGet/Home/issues/1102)
* NuGet 用戶端支援指定全域 NUGET_PACKAGES 環境變數，以指定 `project.json` managed 專案中使用 Windows 10 tools v1.1 的共用全域套件資料夾的位置。

## <a name="command-line-updates"></a>命令列更新

這是第一個支援 NuGet v3 伺服器的 nuget.exe 用戶端版本，以及針對以檔案管理的專案還原套件的第一版 `project.json` 。

此版本中已解決一些已驗證的摘要問題，以改善與用戶端的互動。

* 安裝/還原互動只會將初始要求的認證提交給已驗證的摘要- [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)
* Push 命令無法解析來自設定的認證- [1248](https://github.com/NuGet/Home/issues/1248)
* 使用者代理程式和標頭現在已提交至 NuGet 存放庫，以協助進行統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)

我們進行了一些改善，以在嘗試使用遠端 NuGet 存放庫時更妥善處理網路失敗：

* 改進無法連接到遠端摘要時的錯誤訊息- [1238](https://github.com/NuGet/Home/issues/1238)
* 修正了 NuGet 還原命令，以在發生錯誤狀況時正確傳回 1- [1186](https://github.com/NuGet/Home/issues/1186)
* 現在，在 HTTP 5xx [1120](https://github.com/NuGet/Home/issues/1120)失敗的情況下，每個200毫秒重試網路連接最多5次
* 改進在推送命令期間處理伺服器重新導向回應的功能- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` 現在支援 Nuget.Config 的 URL 或存放庫名稱做為引數- [1046](https://github.com/NuGet/Home/issues/1046)
* 在還原期間缺少存放庫的套件，現在會回報為錯誤，而不是警告 [1038](https://github.com/NuGet/Home/issues/1038)
* 修正了 \r\n for Unix/Linux 案例的 multipartwebrequest 處理- [776](https://github.com/NuGet/Home/issues/776)

各種命令的問題有一些修正：

* 推播命令不再針對套件來源進行 PUT 之前的 GET- [1237](https://github.com/NuGet/Home/issues/1237)
* List 命令不再重複版本號碼- [1185](https://github.com/NuGet/Home/issues/1185)
* 具有-build 引數的套件現已正確支援 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107)
* 修正了嘗試封裝以 Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)所建立的 F # 專案時所發生的問題
* 當套件已存在時立即還原- [1040](https://github.com/NuGet/Home/issues/1040)
* 改進檔案 `packages.config` 格式不正確的錯誤訊息 [-1034](https://github.com/NuGet/Home/issues/1034)
* 使用-SolutionDirectory 參數更正了還原命令以使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)
* 改進的更新命令以支援解決方案範圍的更新- [924](https://github.com/NuGet/Home/issues/924)

您可以在 NuGet GitHub [命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)中找到此版本所解決之問題的完整清單。

## <a name="visual-studio-extension-updates"></a>Visual Studio 擴充功能更新

### <a name="new-features-in-visual-studio"></a>Visual Studio 的新功能

* 方案節點上的方案總管中加入了新的內容功能表項目，可讓封裝還原，而不需要 ([1274](https://github.com/NuGet/Home/issues/1274)) 建立解決方案。

![新增 [還原套件] 內容功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Visual Studio 中的更新和修正

驗證摘要的修正程式也會在擴充功能中匯總和定址。  下列驗證專案也會在擴充功能中解決：

* 現在正確地正確地將 NuGet v3 驗證的摘要正確地妥善處理，而不是 v2 驗證的摘要- [1216](https://github.com/NuGet/Home/issues/1216)
* 使用和與 v2 摘要進行通訊，以更正專案中驗證認證的要求 `project.json` - [1082](https://github.com/NuGet/Home/issues/1082)

網路連線已影響 Visual Studio 中的使用者介面，我們使用下列修正程式解決此問題：

* 改進套件版本的本機快取維護- [1096](https://github.com/NuGet/Home/issues/1096)
* 變更連接到 v3 摘要時失敗的行為，不會再嘗試將它視為 v2 摘要- [1253](https://github.com/NuGet/Home/issues/1253)
* 現在防止安裝具有多個套件來源的套件時安裝失敗- [1183](https://github.com/NuGet/Home/issues/1183)

我們已改善與組建作業的互動處理：

* 如果還原單一專案的封裝失敗，現在繼續建立專案- [1169](https://github.com/NuGet/Home/issues/1169)
* 將套件安裝至相依于方案中另一個專案的專案時，會強制方案重建- [981](https://github.com/NuGet/Home/issues/981)
* 已更正失敗的套件安裝以正確地復原專案的變更- [1265](https://github.com/NuGet/Home/issues/1265)
* 修正 `developmentDependency` 在 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)中意外移除封裝的屬性
* 呼叫 `install.ps1` 現在已傳遞適當的 `$package.AssemblyReferences` 物件- [1245](https://github.com/NuGet/Home/issues/1245)
* 當專案處於不正常的狀態時，不會再防止卸載 UWP 專案中的套件- [1128](https://github.com/NuGet/Home/issues/1128)
* `packages.config`現在已正確建立包含混合和專案的方案， `project.json` 而不需要第二個組建作業- [1122](https://github.com/NuGet/Home/issues/1122)
* 如果連結或位於不同的資料夾（ [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894) ），適當地找出 app.config 檔案
* UWP 專案現在可以安裝未列出的套件- [1109](https://github.com/NuGet/Home/issues/1109)
* 當解決方案未處於儲存狀態時，現在允許套件還原- [1081](https://github.com/NuGet/Home/issues/1081)

處理設定檔的更新已修正：

* 不再從 managed 專案的後續組建中移除套件所傳遞的目標檔案 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)
* 在 ASP.NET 5 解決方案組建期間，不再修改 Nuget.Config 檔案- [1201](https://github.com/NuGet/Home/issues/1201)
* 封裝更新期間不再變更允許的版本條件約束- [1130](https://github.com/NuGet/Home/issues/1130)
* 鎖定檔案現在在組建期間維持鎖定狀態- [1127](https://github.com/NuGet/Home/issues/1127)
* 現在修改 `packages.config` 並不會在更新期間重寫- [585](https://github.com/NuGet/Home/issues/585)

與 TFS 原始檔控制的互動已獲得改良：

* 針對系結至 TFS- [1164](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)的封裝，不會再安裝失敗
* 已更正 NuGet 使用者介面以允許 TFS 2013 整合- [1071](https://github.com/NuGet/Home/issues/1071)
* 已更正還原的套件參考，可正確地來自套件資料夾- [1004](https://github.com/NuGet/Home/issues/1004)

最後，我們也改善了這些專案：

* 針對 managed 專案減少記錄檔訊息的詳細資訊 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)
* 現在會正確地在使用者介面中顯示已安裝的套件版本- [1061](https://github.com/NuGet/Home/issues/1061)
* 具有 nuspec 中所指定相依性範圍的套件，現在已針對穩定套件版本安裝這些相依性的發行前版本- [1304](https://github.com/NuGet/Home/issues/1304)

您可以在 NuGet GitHub [3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)中找到針對 Visual Studio 擴充功能所解決之問題的完整清單

## <a name="known-issues"></a>已知問題

我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)