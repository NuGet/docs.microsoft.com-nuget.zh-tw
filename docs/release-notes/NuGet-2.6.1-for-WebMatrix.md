---
title: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊
description: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780417"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>適用于 WebMatrix 的 NuGet 2.6.1 版本資訊

[NuGet 2.6 版本](../release-notes/nuget-2.6.md)  |  資訊[NuGet 2.7 版本](../release-notes/nuget-2.7.md)資訊

NuGet 小組在2014年3月26日發行了 WebMatrix 的更新 NuGet 封裝管理員延伸模組。  您可以使用下列步驟，從 [WebMatrix 擴充功能庫](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 安裝此更新：

1. 開啟 WebMatrix 3
1. 按一下 [首頁] 功能區中的延伸模組圖示
1. 選取 [更新] 索引標籤
1. 按一下以將 NuGet 封裝管理員更新為2.6。1
1. 關閉並重新啟動 WebMatrix 3

## <a name="notable-changes"></a>值得注意的變更

此延伸模組更新解決了使用者在 WebMatrix 中使用 NuGet 套件的兩個最大問題。  第一個是 NuGet 架構版本錯誤，第二個是在資料夾中導致零位元組 Dll 的錯誤（bug） `bin` 。

### <a name="nuget-schema-version-error"></a>NuGet 架構版本錯誤

由於 WebMatrix 3 已發行，因此已將新功能引進 NuGet 套件，需要新的架構版本。  當您嘗試在網站中管理 NuGet 套件時，這些新的封裝可能會導致您在 WebMatrix 中看到的錯誤。

![發生錯誤。 架構版本不相容。 請將 NuGet 升級至最新版本。](./media/NuGet-2.8/webmatrix-schema-version.png)

此最新版本提供與最新 NuGet 套件的相容性，以防止發生此錯誤。 新版本的套件（包括 Microsoft）現在可以安裝在 WebMatrix 中。  其中有些套件使用 NuGet 功能，例如 XDT 設定 [轉換](../release-notes/nuget-2.6.md#xdt)，在 WebMatrix 中不受支援。

### <a name="zero-byte-dlls-in-bin-folder"></a>在 bin 資料夾中 Zero-Byte Dll

有些使用者在安裝包含複製到 bin 之 Dll 的 WebMatrix 中安裝 NuGet 套件之後，會發現 Dll 會以0位元組檔案的 `bin` 形式顯示在資料夾中。  這會在執行時間中斷應用程式。

現在已修正[此問題](https://nuget.codeplex.com/workitem/4060)。

## <a name="other-recent-improvements"></a>其他最近的改進

針對 Visual Studio 發行 NuGet 封裝管理員2.8 時，我們也發行了適用于 WebMatrix 的 NuGet 封裝管理員2.5.0。  雖然 [NuGet 2.8 版本](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)資訊中提及這一點，但我們並未提及更新所引進的特定新功能。

### <a name="update-all"></a>全部更新

您現在可以在一個步驟中更新所有網站套件！  當您在 WebMatrix 中開啟 NuGet 擴充功能時，您會看到資源庫上的所有套件清單、已安裝的套件，以及有可用更新的套件。  先前，每個套件都必須個別更新，但現在會在 [更新] 索引標籤上顯示有用的 [全部更新] 按鈕。

![按一下 [全部更新] 以更新具有可用更新的所有套件](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆寫現有的檔案

當您安裝的套件中包含已存在於您的網站中的檔案時，NuGet 一律只會以無訊息方式略過這些檔案， (保留現有的檔案) 。  這可能會導致您認為封裝已正確安裝或更新，但事實上並不是。  NuGet 現在會提示您輸入要覆寫的檔案。

![檔案衝突解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
