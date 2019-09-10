---
title: 識別碼首碼保留項目
description: 套件識別碼首碼保留項目功能的描述和作者指南。
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 630c2b193500ec0b9aa5a7fe4af3ea95ae52aeec
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815275"
---
# <a name="package-id-prefix-reservation"></a>套件識別碼首碼保留項目

套件擁有者可以藉由保留識別碼首碼，保留並保護他們的身分識別。 套件取用者在取用套件時會得到額外的資訊，指出他們取用的套件在其識別屬性中沒有欺騙成分。 

[nuget.org](https://www.nuget.org/) 和 Visual Studio 2017 15.4 版或更新版本，對於由擁有者所提交、具有保留套件識別碼首碼的套件，只要套件符合保留識別碼首碼命名模式，便會顯示一個視覺指標。 以下參考說明識別碼首碼保留項目需要什麼，以及擁有者如何申請識別碼首碼。

## <a name="id-prefix-reservation-details"></a>識別碼首碼保留項目詳細資料

保留套件識別碼首碼時，在 [nuget.org](https://www.nuget.org/) 資源庫以及 Visual Studio 裡發生幾件事。 此外，有一些識別碼首碼保留項目支援的進階案例，例如設定首碼為 'public'，將首碼子集委派給多位擁有者。

### <a name="id-prefix-reservation-on-nugetorg"></a>nuget.org 上的識別碼首碼保留項目

在 [nuget.org](https://www.nuget.org/) 上保留首碼時，會發生下列各項：

1. 首碼保留項目與 [nuget.org](https://www.nuget.org/) 上的擁有者或擁有者集合建立關聯。

1. 每次提交套件給 [nuget.org](https://www.nuget.org/) 而其識別碼符合保留識別碼首碼時，除非它來自保留該識別碼首碼的擁有者，否則會拒絕該套件。

1. 任何符合保留識別碼首碼的套件，且套件是源自保留該識別碼首碼的擁有者時，在 Visual Studio 2017 15.4 版或更新版本以及 [nuget.org](https://www.nuget.org/) 上會有一個視覺指標，指出套件位於保留識別碼首碼底下。 對於新套件提交和擁有者底下的現有套件而言，都是如此。 **注意：** Visual Studio 中的指標僅會在單一摘要選取為套件來源時出現。

1. 符合保留識別碼首碼，但「不」是由保留首碼擁有者所擁有的任何先前現有套件將維持不變 (它們不會被列出，但也不會有視覺指標)。 此外，這些套件的擁有者將仍然可以將新版本提交至套件。

這些變更是根據下列條件，且加上幾個額外的限制：

- 只需要有一位套件擁有者具有保留首碼，便會顯示視覺指標 (對於有多位擁有者的套件而言)。

- 如果有多位套件擁有者，其中一或多位擁有者具有保留首碼，而一或多位擁有者沒有保留首碼，則只有具有保留首碼的擁有者可以移除具有保留首碼的其他擁有者。 沒有保留首碼之擁有者不能移除具有保留首碼的擁有者。 他們仍然可以移除也沒有保留首碼的其他擁有者。

- 套件有了視覺指標之後，它應該「一律」有視覺指標 (保證一律會有至少一位具有保留首碼的擁有者保持為擁有者)

### <a name="advanced-prefix-reservation-scenarios"></a>進階首碼保留案例

以下描述數個更進階的首碼保留案例，包括子首碼委派以及將首碼標記為公用。 以下是可以進行的較進階首碼保留項目。 

- 在首碼保留期間，擁有者可以要求委派首碼子集 (或首碼) 給其他擁有者。 例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.\*'，但 '[aspnet](https://www.nuget.org/profiles/aspnet)' 想要保留 'Microsoft.AspNet.\*'，則 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇將 'Microsoft.AspNet.\*' 委派給 [aspnet](https://www.nuget.org/profiles/aspnet) 帳戶。

- 在首碼保留期間，擁有者可以選擇將首碼設為公用。 這樣做仍然會提供他們視覺指標，其顯示套件來自保留首碼，但**不會**封鎖任何擁有者未來對於首碼的套件提交。 這適合具有許多參與者的開放原始碼專案 - 頂尖或核心參與者都可以保留首碼，但仍然開放給所有參與者。 

### <a name="prefix-reservation-visual-indicator"></a>首碼保留項目視覺指標

當套件來自保留首碼時，您會在 [nuget.org](https://www.nuget.org/) 資源庫上和 Visual Studio 2017 15.4 版或更新版本中，看到以下視覺指標：

**nuget.org 資源庫**
![nuget.org 資源庫](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>識別碼首碼保留項目申請程序

1. 檢閱[首碼識別碼保留項目的驗收準則](#id-prefix-reservation-criteria)。

2. 決定您想要保留的首碼，以及您可能需要的任何[進階首碼保留案例](#advanced-prefix-reservation-scenarios)。

3. 傳送郵件到 [account@nuget.org](mailto:account@nuget.org)，附上 [nuget.org](https://www.nuget.org/) 上的擁有者顯示名稱，以及您所要求的任何保留首碼。 如果您委派首碼子集給多位擁有者，請務必提及所有擁有者顯示名稱和首碼子集。

在提交申請之後，您會收到接受或拒絕的通知 (以及導致拒絕的準則)。 我們可能需要詢問額外的識別問題以確認擁有者身分識別。

### <a name="id-prefix-reservation-criteria"></a>識別碼首碼保留項目準則

檢閱識別碼首碼保留項目的任何申請時，[nuget.org](https://www.nuget.org/) 小組會針對以下準則評估申請。 不必滿足所有準則即可保留首碼，但如果沒有實質證明滿足準則 (提供說明)，申請可能遭拒：

1. 套件識別碼首碼是否能正確且清楚地識別套件擁有者？

1. 套件擁有者是否已[為自己的 NuGet.org 帳戶啟用2FA](individual-accounts.md#enable-two-factor-authentication-2fa)？

1. 有由擁有者已經在套件識別碼首碼下提交的大量套件嗎？

1. 套件識別碼首碼是否和不應該屬於任何個別擁有者或組織有某些雷同嗎？

1. 保留套件識別碼首碼「不會」造成模稜兩可和社群的混淆嗎？

1. 符合套件識別碼首碼的套件識別屬性是否清楚且一致 (尤其是套件作者)？

1. 套件是否有授權 (使用 [license](../reference/nuspec.md#license) 中繼資料元素，而非即將淘汰的 licenseUrl)？

1. 如果封裝有圖示（使用 iconUrl 中繼資料元素），它們是否也會使用[圖示](../reference/nuspec.md#icon)中繼資料元素（不需要移除 iconUrl）？

## <a name="third-party-feed-provider-scenarios"></a>第三方摘要提供者案例

如果第三方摘要提供者想要實作自己的服務以提供首碼保留項目，您可以修改 NuGet V3 摘要提供者中的搜尋服務來辦到。 摘要搜尋服務中的新增是要新增 *verified* 屬性，V3 摘要的範例如下。 NuGet 用戶端將不支援在 V2 摘要中新增的屬性。

如需詳細資訊，請參閱 [API 搜尋服務的相關文件](../api/search-query-service-resource.md)。

## <a name="package-id-prefix-reservation-dispute-policy"></a>套件識別碼首碼保留項目爭議原則
如果您認為 [NuGet.org](https://www.nuget.org) 上的擁有者已獲得指派套件識別碼首碼保留項目，而該項目違背了上述所列的準則，或侵害任何商標或著作權，請傳送電子郵件到 [support@nuget.org](mailto:support@nuget.org)，並附上討論中的識別碼首碼、識別碼首碼的擁有者，以及所指派首碼保留項目的爭議理由。

