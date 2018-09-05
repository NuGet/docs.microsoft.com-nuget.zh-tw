---
title: NuGet 2.6.1 for WebMatrix 版本資訊
description: Webmatrix 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.6.1 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550313"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 for WebMatrix 版本資訊

[NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md) | [NuGet 2.7 版本資訊](../release-notes/nuget-2.7.md)

NuGet 小組發行於 2014 年 3 月 26 日 WebMatrix 更新的 NuGet 套件管理員延伸模組。  可以從安裝此更新[WebMatrix 延伸模組庫](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用下列步驟：

1. 開啟 WebMatrix 3
1. 按一下 [首頁] 功能區中的延伸模組圖示
1. 選取 [更新] 索引標籤
1. 按一下以更新 2.6.1 NuGet 套件管理員
1. 關閉並重新啟動 WebMatrix 3

## <a name="notable-changes"></a>值得注意的變更

此延伸模組更新可解決兩個的最大的問題使用者面臨在 WebMatrix 內取用 NuGet 套件。  第一個是 NuGet 結構描述版本錯誤，且第二個前置零位元組 dll 的 bug`bin`資料夾。

### <a name="nuget-schema-version-error"></a>NuGet 的結構描述版本錯誤

WebMatrix 3 已發行，因為新的結構描述版本所需的 NuGet 套件的 nuget 已推出新功能。  管理網站中的 NuGet 封裝時，這些新的封裝可能會導致您在 WebMatrix 中看到的錯誤。

![發生錯誤。 結構描述版本不相容。 請升級至最新版本的 NuGet。](./media/NuGet-2.8/webmatrix-schema-version.png)

這個最新版本提供與最新的 NuGet 套件，防止發生此錯誤的相容性。 現在可以在 WebMatrix 中安裝套件包括 Microsoft.AspNet.WebPages 的新版本。  部分這些封裝所使用的 NuGet 功能，例如[XDT 組態轉換](../release-notes/nuget-2.6.md#xdt)，但不支援在 WebMatrix 中到目前為止。

### <a name="zero-byte-dlls-in-bin-folder"></a>在 bin 資料夾中的零位元組 Dll

安裝 NuGet 封裝在 WebMatrix 中包含 Dll 複製到分類收納，Dll 顯示中之後，某些使用者有報告的`bin`0 位元組檔案的資料夾。  這會中斷應用程式在執行階段。

[此問題](https://nuget.codeplex.com/workitem/4060)現在已修正。

## <a name="other-recent-improvements"></a>其他最近的改進功能

當 NuGet 封裝管理員 2.8 已發行適用於 Visual Studio 中時，我們也會發行 NuGet 套件管理員 2.5.0 for WebMatrix。  雖然這在提到[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我們忘了提特定的新功能導入該更新。

### <a name="update-all"></a>全部更新

您現在可以更新所有網站的套件，在一個步驟中 ！  當您在 WebMatrix 中開啟 NuGet 延伸模組時，您會看到資源庫、 安裝，以及可用的更新以外的所有封裝的清單。  之前，每個套件必須個別更新，但現在已經是有用的 [全部更新] 按鈕，就會出現在 [更新] 索引標籤。

![按一下 [全部更新]，以使用可用的更新來更新所有封裝](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆寫現有檔案

安裝套件，其中包含存在於您的網站的檔案時，NuGet 就是一律只以無訊息方式略過這些檔案 （保留現有的檔案）。  這可能會導致封裝已安裝，或當事實上它未正確更新的印象。  NuGet 現在會提示輸入覆寫檔案中。

![解決檔案衝突](./media/NuGet-2.8/webmatrix-overwrite-file.png)
