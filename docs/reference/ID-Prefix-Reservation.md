---
title: 識別碼首碼保留項目參考
description: 套件識別碼首碼保留項目功能的描述和作者指南。
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 10d017d67cf2bd49812c5d54f9fca063f32cc052
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2018
ms.locfileid: "37948391"
---
# <a name="package-id-prefix-reservation"></a>套件識別碼首碼保留項目

套件擁有者可保留並保護他們的身分識別，藉由保留識別碼前置詞。 套件取用者會提供其他資訊時使用之封裝的他們耗用的封裝將不會詐騙其識別的屬性中。 

[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 版或更新版本的套件，只要封裝符合保留的 ID，由擁有者具有保留的套件識別碼前置詞，會提交前置詞的命名模式，顯示的視覺指標。 下列參考說明識別碼首碼保留項目需要什麼，以及如何擁有者可以申請識別碼前置詞。

## <a name="id-prefix-reservation-details"></a>識別碼首碼保留項目詳細資料

當保留的套件識別碼前置詞時，在 發生幾件事[nuget.org](https://www.nuget.org/)資源庫，以及與 Visual Studio。 此外，那里一些進階的識別碼首碼保留項目，例如設定的前置詞為 'public'，將前置詞子集委派給多個擁有者所支援的案例。

### <a name="id-prefix-reservation-on-nugetorg"></a>在 nuget.org 上的識別碼首碼保留項目

當保留上的前置詞[nuget.org](https://www.nuget.org/)，會發生下列：

1. 首碼保留項目相關聯的擁有者或擁有者的集合上[nuget.org](https://www.nuget.org/)。

1. 封裝每次提交給[nuget.org](https://www.nuget.org/)識別碼符合的保留的識別碼前置詞，除非它來自擁有者保留識別碼前置詞，會拒絕封裝。

1. 在 Visual Studio 2017 15.4 版或更新版本，和任何符合保留的識別碼前置詞，以及所有源自保留識別碼前置詞的擁有者的套件會有視覺指示器[nuget.org](https://www.nuget.org/)指出封裝正在進行保留的識別碼前置詞。 這是新的封裝提交以及現有的封裝，在擁有者，則為 true。 **注意：** 單一摘要選取作為封裝來源時，才會出現在 Visual Studio 中的指標。

1. 所有先前已經有套件符合保留的識別碼前置詞，但會*不*保留的擁有者所擁有的前置詞將維持不變 （它們不會列出，但它們也不會具有視覺指標）。 此外，這些套件的擁有者將仍然可以提交給封裝的新版本。

這些變更根據下列條件，並且加上幾個額外的限制：

- 封裝只能有一個擁有者必須具有保留的前置詞，如 （適用於與多個擁有者的套件） 所顯示的視覺指示器。

- 如果有一個以上的擁有者的其中一個或多個擁有者具有保留的前置詞，而一或多個擁有者並沒有保留的前置詞的套件，只保留的前置詞與擁有者可以移除其他擁有者與保留的前置詞。 擁有者並沒有保留的前置詞不能移除以保留的前置詞的擁有者。 它們仍可以移除其他擁有者，也不需要保留的前置詞。

- 當封裝具有視覺指標之後，它應該*一律*有視覺指示器 （保證具有保留的前置詞，至少一個擁有者將會一直保持 「 擁有者）

### <a name="advanced-prefix-reservation-scenarios"></a>進階的前置詞保留案例

有數個更進階的前置詞保留案例如下所述，包括 subprefix 委派和標記前置詞為公用。 以下是更進階的前置詞保留項目可進行。 

- 首碼保留項目，在擁有者可以要求委派的前置詞的子集 （或前置詞） 給其他擁有者。 例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.著作權\*'，但'[aspnet](https://www.nuget.org/profiles/aspnet)'想要保留' Microsoft.AspNet。\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇委派 ' Microsoft.AspNet。\*' 來[aspnet](https://www.nuget.org/profiles/aspnet)帳戶。

- 在 首碼保留項目，擁有者可以選擇，設為前置詞為公用。 這樣做仍然會提供這些封裝來自保留的前置詞，但不是會顯示的視覺指示器**不**封鎖這個前置詞的未來封裝提交，任何擁有者。 這是適用於具有許多的參與者的開放原始碼專案-top 或核心參與者都可以有前置詞保留，但它仍然是開放給所有的參與者。 

### <a name="prefix-reservation-visual-indicator"></a>前置詞保留區視覺指示器。

當封裝來自保留的前置詞時，您會看到下面上的視覺指示器[nuget.org](https://www.nuget.org/)資源庫和 Visual Studio 2017 15.4 版或更新版本中：

**nuget.org 資源庫**
![nuget.org 資源庫](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>識別碼首碼保留項目應用程式處理序

1. 檢閱接受[首碼識別碼保留項目準則](#id-prefix-reservation-criteria)。

2. 決定您想要保留時，除了任何命名的空間[進階的前置詞保留案例](#advanced-prefix-reservation-scenarios)您可能需要。

3. 傳送郵件給[ account@nuget.org ](mailto:account@nuget.org)擁有者顯示名稱上[nuget.org](https://www.nuget.org/)，以及您所要求的任何保留前置詞。 如果您多個擁有者委派前置詞的子集，請確定您提到所有擁有者顯示名稱和前置詞子集。

在提交應用程式之後，您會收到通知的接受或拒絕 （並導致拒絕的準則）。 我們可能需要詢問以確認擁有者身分識別的其他識別問題。

### <a name="id-prefix-reservation-criteria"></a>識別碼首碼保留項目條件

檢閱識別碼首碼保留項目，任何應用程式時[nuget.org](https://www.nuget.org/)小組會評估應用程式對於下列準則。 並非所有的準則必須符合的前置詞保留，但如果不是大量的辨識項 （與指定的說明） 符合準則的應用程式可能會被拒絕：

1. 沒有套件識別碼前置詞正確且清楚地識別套件擁有者？

1. 有大量已提交的封裝所下的套件識別碼前置詞的擁有者嗎？

1. 是的套件識別碼前置詞一般指應該不屬於任何個別擁有者或組織嗎？

1. 想*不*保留的套件識別碼前置詞會造成模稜兩可和社群的混淆嗎？

1. 會識別符合的套件識別碼前置詞清楚且一致 （尤其是封裝作者） 的封裝的內容嗎？

## <a name="third-party-feed-provider-scenarios"></a>摘要提供者案例的第三方

如果想要實作自己的服務，以提供前置詞保留項目摘要提供者的第三方，您可以執行修改 NuGet V3 中的搜尋服務摘要提供者。 摘要的搜尋服務中會新增*驗證*屬性，使用下列的 V3 摘要的範例。 在 V2 中摘要，NuGet 用戶端將不支援加入的屬性。

如需詳細資訊，請參閱 < [API 的搜尋服務相關的文件](../api/search-query-service-resource.md)。

## <a name="package-id-prefix-reservation-dispute-policy"></a>套件識別碼首碼保留項目爭議原則
如果您認為上的擁有者[NuGet.org](https://www.nuget.org)已指派的套件識別碼首碼保留項目違背了上述所列的準則，或侵害任何商標或著作權，請電子郵件[ support@nuget.org ](mailto:support@nuget.org)問題識別碼首碼、 的擁有者識別碼前置詞，以及基於 disputing 指派的首碼保留項目。

