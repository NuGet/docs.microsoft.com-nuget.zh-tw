---
title: 識別碼首碼保留項目
description: 套件識別碼首碼保留項目功能的描述和作者指南。
author: JonDouglas
ms.author: jodou
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 428fd3d7b324f6eb825b17e4a87a662fbd84a2f0
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990096"
---
# <a name="package-id-prefix-reservation"></a>套件識別碼首碼保留項目

套件擁有者可以藉由保留識別碼首碼，保留並保護他們的身分識別。 當取用的套件在其識別屬性中沒有詐騙時，會提供其他資訊給套件取用者。 

[nuget.org](https://www.nuget.org/) 和 Visual Studio 2017 15.4 版或更新版本，對於由擁有者所提交、具有保留套件識別碼首碼的套件，只要套件符合保留識別碼首碼命名模式，便會顯示一個視覺指標。 以下參考說明識別碼首碼保留項目需要什麼，以及擁有者如何申請識別碼首碼。

## <a name="id-prefix-reservation-details"></a>識別碼首碼保留項目詳細資料

保留套件識別碼首碼時，在 [nuget.org](https://www.nuget.org/) 資源庫以及 Visual Studio 裡發生幾件事。 此外，有一些識別碼首碼保留項目支援的進階案例，例如設定首碼為 'public'，將首碼子集委派給多位擁有者。

### <a name="id-prefix-reservation-on-nugetorg"></a>nuget.org 上的識別碼首碼保留項目

在 [nuget.org](https://www.nuget.org/) 上保留首碼時，會發生下列各項：

1. 首碼保留項目與 [nuget.org](https://www.nuget.org/) 上的擁有者或擁有者集合建立關聯。

1. 每次提交套件給 [nuget.org](https://www.nuget.org/) 而其識別碼符合保留識別碼首碼時，除非它來自保留該識別碼首碼的擁有者，否則會拒絕該套件。

1. 任何符合保留識別碼首碼的套件，且套件是源自保留該識別碼首碼的擁有者時，在 Visual Studio 2017 15.4 版或更新版本以及 [nuget.org](https://www.nuget.org/) 上會有一個視覺指標，指出套件位於保留識別碼首碼底下。 對於新套件提交和擁有者底下的現有套件而言，都是如此。 **注意：** 只有在選取單一摘要作為套件來源時，才會顯示 Visual Studio 中的指標。

1. 符合保留識別碼首碼，但「不」是由保留首碼擁有者所擁有的任何先前現有套件將維持不變 (它們不會被列出，但也不會有視覺指標)。 此外，這些套件的擁有者將仍然可以將新版本提交至套件。

這些變更是根據下列條件，且加上幾個額外的限制：

- 只需要有一位套件擁有者具有保留首碼，便會顯示視覺指標 (對於有多位擁有者的套件而言)。

- 如果有多位套件擁有者，其中一或多位擁有者具有保留首碼，而一或多位擁有者沒有保留首碼，則只有具有保留首碼的擁有者可以移除具有保留首碼的其他擁有者。 沒有保留首碼之擁有者不能移除具有保留首碼的擁有者。 他們仍然可以移除也沒有保留首碼的其他擁有者。

- 套件有了視覺指標之後，它應該「一律」有視覺指標 (保證一律會有至少一位具有保留首碼的擁有者保持為擁有者)

### <a name="advanced-prefix-reservation-scenarios"></a>進階首碼保留案例

以下描述數個更進階的首碼保留案例，包括子首碼委派以及將首碼標記為公用。 以下是可以進行的較進階首碼保留項目。 

- 在首碼保留期間，擁有者可以要求委派首碼子集 (或首碼) 給其他擁有者。 例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.\*'，但 '[aspnet](https://www.nuget.org/profiles/aspnet)' 想要保留 'Microsoft.AspNet.\*'，則 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇將 'Microsoft.AspNet.\*' 委派給 [aspnet](https://www.nuget.org/profiles/aspnet) 帳戶。

- 在首碼保留期間，擁有者可以選擇將首碼設為公用。 這樣做仍然會提供他們視覺指標，其顯示套件來自保留首碼，但 **不會** 封鎖任何擁有者未來對於首碼的套件提交。 這適合具有許多參與者的開放原始碼專案 - 頂尖或核心參與者都可以保留首碼，但仍然開放給所有參與者。 

### <a name="prefix-reservation-visual-indicator"></a>首碼保留項目視覺指標

當套件來自保留首碼時，您會在 [nuget.org](https://www.nuget.org/) 資源庫上和 Visual Studio 2017 15.4 版或更新版本中，看到以下視覺指標：

**nuget.org 資源庫** 
 ![nuget.org 資源庫](media/nuget-gallery-reserved-prefix.png)

 
 Visual Studio ![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>識別碼首碼保留項目申請程序

1. 檢閱[首碼識別碼保留項目的驗收準則](#id-prefix-reservation-criteria)。

2. 決定您想要保留的首碼，以及您可能需要的任何[進階首碼保留案例](#advanced-prefix-reservation-scenarios)。

3. [account@nuget.org](mailto:account@nuget.org)使用[nuget.org](https://www.nuget.org/)上的擁有者顯示名稱和您所要求的任何保留首碼來傳送郵件給。 如果您委派首碼子集給多位擁有者，請務必提及所有擁有者顯示名稱和首碼子集。

在提交申請之後，您會收到接受或拒絕的通知 (以及導致拒絕的準則)。 我們可能需要詢問額外的識別問題以確認擁有者身分識別。

### <a name="id-prefix-reservation-criteria"></a>識別碼首碼保留項目準則

查看任何識別碼首碼保留專案的應用程式時， [NuGet.org](https://www.nuget.org) 團隊會根據下列準則來評估應用程式。 請注意，並非所有準則都必須符合，才能保留前置詞，但如果沒有符合準則的重大辨識項，應用程式可能會遭到拒絕， (有提供) 的說明：

1. 封裝識別碼首碼是否正確，並清楚地識別保留擁有者？

1. 擁有者已 [為其 NuGet.org 帳戶啟用 2FA](individual-accounts.md#enable-two-factor-authentication-2fa)嗎？

1. 套件識別碼首碼是否和不應該屬於任何個別擁有者或組織有某些雷同嗎？

1. *不* 會保留套件識別碼前置詞會導致對社區造成不明確、混淆或其他損害？

將套件發佈至識別碼首碼保留範圍內的 NuGet.org 時，必須考慮下列最佳做法：

1. 符合套件識別碼首碼的套件識別屬性是否清楚且一致 (尤其是套件作者)？

1. 套件是否有授權 (使用 [license](../reference/nuspec.md#license) 中繼資料元素，而非即將淘汰的 licenseUrl)？

1. 如果封裝有 (使用 iconUrl metadata 元素) 的圖示，是否也會使用 [icon](../reference/nuspec.md#icon) metadata 元素？ 不需要移除 iconUrl，但必須使用內嵌的圖示。
 
除了上述幾點，請考慮查看完整 [套件撰寫的最佳作法指南](../create-packages/package-authoring-best-practices.md) 。

## <a name="third-party-feed-provider-scenarios"></a>第三方摘要提供者案例

如果協力廠商摘要提供者想要執行自己的服務來提供前置詞保留，則可以藉由修改 NuGet V3 摘要提供者中的搜尋服務來執行此作業。 摘要搜尋服務中的變更是加入 `verified` 屬性。 NuGet 用戶端將不支援在 V2 摘要中新增的屬性。

如需詳細資訊，請參閱 [API 搜尋服務的相關文件](../api/search-query-service-resource.md)。

## <a name="package-id-prefix-reservation-dispute-policy"></a>套件識別碼首碼保留項目爭議原則
如果您認為 [NuGet.org](https://www.nuget.org) 上的擁有者已獲得指派套件識別碼首碼保留項目，而該項目違背了上述所列的準則，或侵害任何商標或著作權，請傳送電子郵件到 [support@nuget.org](mailto:support@nuget.org)，並附上討論中的識別碼首碼、識別碼首碼的擁有者，以及所指派首碼保留項目的爭議理由。

