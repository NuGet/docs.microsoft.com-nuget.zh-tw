---
title: NuGet 5.4 版本資訊
description: NuGet 5.4 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776179"
---
# <a name="nuget-54-release-notes"></a>NuGet 5.4 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.4 版](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-54"></a>摘要：5.4 中的新功能

* 更快速的解決方案載入時間-第一個解決方案載入期間執行 NuGet 程式碼的額外負荷已透過部分 ngen 減少，以降低 JIT 成本 [#6007](https://github.com/NuGet/Home/issues/6007)

* 新的 helper 函式-提供套件識別碼和版本的清單，取得可能的最上層套件。 - [#8316](https://github.com/NuGet/Home/issues/8316)

* [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)在[GitHub Actions](https://github.com/features/actions)上安裝和設定 NuGet.exe 的新動作。 - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 外掛程式： linux/Mac 上的記錄時間精確度已關閉- [#8747](https://github.com/NuGet/Home/issues/8747)

* 處置外掛程式有時可能會擲回並讓整個作業失敗。 - [#8732](https://github.com/NuGet/Home/issues/8732)

* 停止在 PMUI 中于允許和封鎖的版本清單中顯示版本重複專案- [#8679](https://github.com/NuGet/Home/issues/8679)

* 鎖定檔案未正確產生-架構排序不應該影響 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* 針對 SDK 3.0.100 中設定的專案，LockFile 驗證失敗 <RuntimeIdentifiers> - [#8639](https://github.com/NuGet/Home/issues/8639)

* 簽署驗證現在會正確地拒絕具有時間戳記的簽章，這在相同的 OID 下有2個值 [#8629](https://github.com/NuGet/Home/issues/8629)

* 更新授權清單- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* 將診斷檔案上架到 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[此版本修正的所有問題清單-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
