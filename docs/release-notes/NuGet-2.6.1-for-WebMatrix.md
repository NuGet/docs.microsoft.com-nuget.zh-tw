---
title: NuGet 2.6.1 WebMatrix 版本資訊
description: Webmatrix 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.6.1 的版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 WebMatrix 版本資訊

[NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md) | [NuGet 2.7 版本資訊](../release-notes/nuget-2.7.md)

NuGet 小組發行於 2014 年 3 月 26 日更新的 NuGet 套件管理員擴充 WebMatrix。  可以從安裝此更新[WebMatrix 擴充程式庫](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用下列步驟：

1. 開啟 WebMatrix 3
1. 按一下 [首頁] 功能區中的擴充功能圖示
1. 選取 [更新] 索引標籤
1. 按一下以更新 2.6.1 NuGet 封裝管理員
1. 關閉並重新啟動 WebMatrix 3

## <a name="notable-changes"></a>值得注意的變更

最大問題使用者此擴充功能更新解決兩個具有面臨取用 NuGet 封裝在 WebMatrix 內。  第一個是 NuGet 結構描述版本錯誤，且第二個前置零位元組 dll 的 bug`bin`資料夾。

### <a name="nuget-schema-version-error"></a>NuGet 的結構描述版本錯誤

自 WebMatrix 3 發行以來，已引進新的功能到新的結構描述版本所需的 NuGet 套件的 NuGet。  管理網站中的 NuGet 封裝時，這些新的封裝可能會導致您在 WebMatrix 中看到的錯誤。

![發生錯誤。 結構描述版本不相容。 請將 NuGet 升級為最新版本。](./media/NuGet-2.8/webmatrix-schema-version.png)

這個最新版本提供的最新的 NuGet 套件，防止發生這個錯誤與相容性。 現在可以在 WebMatrix 安裝包括 Microsoft.AspNet.WebPages 套件的新版本。  這些封裝的某些已使用 NuGet 功能，例如[XDT config 轉換](../release-notes/nuget-2.6.md#xdt)，這不支援在 WebMatrix 到目前為止。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin 資料夾中的零位元組 Dll

某些使用者回報，之後安裝 NuGet 套件中包含 Dll 複製到 bin，WebMatrix Dll 顯示`bin`0 個位元組的檔案與資料夾。  這會中斷應用程式在執行階段。

[此問題](https://nuget.codeplex.com/workitem/4060)現在已修正。

## <a name="other-recent-improvements"></a>其他最新的增強功能

NuGet 封裝管理員 2.8 已發行適用於 Visual Studio，我們也會發行 NuGet 套件管理員 2.5.0 for WebMatrix。  雖然這在提到[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我們沒有提到特定的新功能導入了該更新。

### <a name="update-all"></a>更新所有

您現在可以更新的所有網站的封裝，以一個步驟 ！  當您在 WebMatrix 中開啟 NuGet 延伸模組時，您會看到所有的封裝清單上的組件庫，安裝，以及具有可用的更新。  之前，必須個別更新每個套件，但現在是有用的 [更新全部] 按鈕，就會出現在 [更新] 索引標籤。

![按一下 全部更新使用可用的更新來更新所有的封裝](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆寫現有檔案

安裝封裝，其中包含存在於您的網站的檔案時，NuGet 就是一律只以無訊息方式略過這些檔案 （保留現有的檔案）。  這可能會導致印象封裝已安裝，或當實際上它未正確更新。  NuGet 現在會提示輸入覆寫檔案。

![解決檔案衝突](./media/NuGet-2.8/webmatrix-overwrite-file.png)
