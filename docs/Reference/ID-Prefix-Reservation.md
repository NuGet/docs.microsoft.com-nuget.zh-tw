---
title: 識別碼前置詞保留項目參考 |Microsoft 文件
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 封裝識別碼的前置詞保留項目功能的描述及撰寫指南。
keywords: NuGet 封裝識別碼、 前置詞、 保留項目
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7b1956612bd48a1c59503418f1a4d7d9dee900f5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="package-id-prefix-reservation"></a>封裝識別碼前置詞保留項目

封裝擁有者可以保留，而保留識別碼前置詞來保護他們的身分識別。 封裝取用者會提供其他資訊時使用之封裝的他們使用的封裝將不會詐騙識別屬性中。 

[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 或更新版本的套件，只要封裝符合保留的識別碼送出的擁有者，以保留的封裝識別碼的前置詞，前置詞的命名模式，顯示一種視覺指標。 參考下列說明識別碼的前置詞保留區的需要，以及如何套用的擁有者識別碼前置詞。

## <a name="id-prefix-reservation-details"></a>識別碼前置詞保留項目詳細資料

上的封裝識別碼前置詞為保留字，當發生數種事項[nuget.org](https://www.nuget.org/)組件庫，以及與 Visual Studio。 此外，屬於進階識別碼前置詞保留項目，例如，設定的前置詞為 'public'，而前置詞子集委派給多個擁有者所支援的案例。

### <a name="id-prefix-reservation-on-nugetorg"></a>識別碼前置詞在 nuget.org 的保留項目

前置詞都會保留在[nuget.org](https://www.nuget.org/)，將會發生下列：

1. 前置詞保留項目關聯的擁有者或擁有者的集合上[nuget.org](https://www.nuget.org/)。

1. 封裝每次提交給[nuget.org](https://www.nuget.org/)識別碼符合保留的識別碼前置詞，除非它來自保留識別碼首碼而後，會拒絕封裝。

1. 符合保留的識別碼前置詞並源自保留識別碼首碼而後任何套件將具有視覺指標，在 Visual Studio 2017 15.4 以後版本，和[nuget.org](https://www.nuget.org/)指出封裝正在保留的識別碼前置詞。 這是新的封裝提交以及下者的現有封裝，則為 true。 **注意：**單一摘要當做封裝來源時，才會出現在 Visual Studio 中的指標。

1. 所有先前已存在封裝符合保留的識別碼前置詞，但這是*不*保留的擁有者所擁有的前置詞將維持不變 （而不要使用未列出，但也不會提供視覺指標）。 此外，這些封裝的擁有者仍會送出至封裝的新版本。

這些變更會根據下列條件，並強制執行數個其他的限制：

- 只有一個擁有者的封裝必須有保留的前置詞的視覺指標，以顯示 （適用於與多個擁有者的封裝）。

- 如果有一個以上的擁有者的其中一個或多個擁有者有保留的前置詞，而一或多個擁有者沒有保留的前置詞的封裝，以保留的前置詞者可以移除其他而後與保留的前置詞。 擁有者不需要保留的前置詞不能移除以保留的前置詞的擁有者。 他們仍然可以移除其他擁有者，也不需要保留的前置詞。

- 一旦封裝具有視覺指標，它應該*一律*將視覺化指標 （具有保留的前置詞，至少一個擁有者，以及確保一定會維持一位擁有者）

### <a name="advanced-prefix-reservation-scenarios"></a>進階的前置詞保留項目案例

有數個更進階的前置詞保留案例如下所述，包括 subprefix 委派，並標示為公用的前置詞。 以下是更進階的前置詞保留項目，才能進行。 

- 前置詞保留期間之擁有者可以要求的前置詞子集委派 （或前置詞） 其他擁有者。 例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.\*'，但'[aspnet](https://www.nuget.org/profiles/aspnet)'想要保留' Microsoft.AspNet。\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇將委派 ' Microsoft.AspNet。\*' 至[aspnet](https://www.nuget.org/profiles/aspnet)帳戶。

- 前置詞保留期間的擁有者可以選擇將前置詞設為公用。 這仍然會提供這些封裝來自保留的前置詞，但不是會顯示的視覺指示器**不**封鎖前置詞的未來封裝提交任何擁有者。 這適用於具有許多參與者的開放原始碼專案： top 或核心參與者可以有前置詞保留，但它仍然是開放給所有參與者。 

### <a name="prefix-reservation-visual-indicator"></a>前置詞保留視覺指標

當封裝來自於保留的前置詞時，您會看到下面上的視覺指標[nuget.org](https://www.nuget.org/)組件庫和 Visual Studio 2017 15.4 或更新版本中：

**nuget.org 圖庫**
![nuget.org 組件庫](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>識別碼前置詞保留應用程式處理序

1. 檢閱接受[前置詞識別碼保留項目的準則](#id-prefix-reservation-criteria)。

1. 判斷您想要保留時，除了任何命名的空間[進階前置詞保留案例](#advanced-prefix-reservation-scenarios)，您可能需要。

1. 傳送郵件給[ account@nuget.org ](mailto:account@nuget.org)與擁有者顯示名稱上[nuget.org](https://www.nuget.org/)，以及任何您要求保留的前置詞。 如果您正在委派前置詞的子集，多個擁有者，請確定您提到所有擁有者的顯示名稱和前置詞的子集。

在提交應用程式之後，就會通知的接受或拒絕 （使用準則造成拒絕）。 我們可能需要詢問確認擁有者身分識別的其他識別問題。

### <a name="id-prefix-reservation-criteria"></a>識別碼前置詞保留項目條件

檢閱任何應用程式的識別碼前置詞保留項目時[nuget.org](https://www.nuget.org/)小組將會評估針對應用程式準則如下。 並非所有的條件必須符合的前置詞，而保留，但如果不是大量的辨識項的準則 （並提供說明） 符合應用程式可能會被拒絕：

1. 就封裝識別碼首碼正確且清楚地識別封裝擁有者嗎？

1. 已提交的封裝大量所下的封裝識別碼前置詞的擁有者嗎？

1. 是封裝識別碼首碼一般應該不屬於任何個別擁有者或組織嗎？

1. 會*不*保留封裝識別碼前置詞會造成模稜兩可和混淆社群？

1. 會識別符合的封裝識別碼首碼清楚且一致 （尤其是封裝作者） 的封裝的內容嗎？

## <a name="third-party-feed-provider-scenarios"></a>第三方摘要提供者案例

如果想要實作自己的服務提供前置詞保留項目摘要提供者的第三方，您可以執行藉由修改搜尋服務 NuGet v3 摘要提供者。 摘要的搜尋服務中會新增*驗證*屬性，請使用下列的 V3 摘要的範例。 NuGet 用戶端將不會支援摘要 V2 中加入的屬性。

如需詳細資訊，請參閱[API 的搜尋服務的相關文件](../api/search-query-service-resource.md)。
