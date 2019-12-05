---
title: NuGet 5.4 版本資訊
description: NuGet 5.4 的版本資訊，包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828405"
---
# <a name="nuget-54-release-notes"></a>NuGet 5.4 版本資訊

NuGet 配送車：

| NuGet 版本 | 隨附於 Visual Studio 版本| 隨附於 .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.4 版](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝

## <a name="summary-whats-new-in-54"></a>摘要：5.4 中的新功能

* 更快速的解決方案載入時間-第一次載入解決方案時，執行 NuGet 程式碼的額外負荷已透過部分-ngen 降低，以減少 JIT 成本- [#6007](https://github.com/NuGet/Home/issues/6007)

* 新 helper 函式-提供套件識別碼和版本清單，取得可能的最上層套件。 - [#8316](https://github.com/NuGet/Home/issues/8316)

### <a name="issues-fixed-in-this-release"></a>本版已修正的問題

**Bug**

* 外掛程式： linux/Mac 上的記錄時間準確度已關閉- [#8747](https://github.com/NuGet/Home/issues/8747)

* 處置外掛程式有時可能會擲回並使整個作業失敗。 - [#8732](https://github.com/NuGet/Home/issues/8732)

* 在 PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)中停止顯示 [允許] 和 [封鎖的版本] 清單中的版本重複

* 鎖定檔案未正確產生-架構順序應該不會影響 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* 在 SDK 3.0.100 中設定 <RuntimeIdentifiers> 的專案 LockFile 驗證失敗- [#8639](https://github.com/NuGet/Home/issues/8639)

* 簽署驗證現在會使用具有相同 OID 之2個值的時間戳記，正確地拒絕簽章[#8629](https://github.com/NuGet/Home/issues/8629)

* 更新授權清單- [#8544](https://github.com/NuGet/Home/issues/8544)

**Dcr**

* 將診斷檔案上架至 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[此版本中已修正的所有問題清單-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
