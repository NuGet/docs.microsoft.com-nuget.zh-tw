---
title: "NuGet 專案治理 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 94c088ce-ec96-4876-a210-fbdae743942c
description: "NuGet 的治理模型，包含認可者、參與者和使用者的角色和責任。"
keywords: "NuGet 治理、NuGet 仁慈獨裁者、認可者責任、參與者責任、使用者責任"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db2ed774b35d5698a88f9afba43fd30692001f6a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-governance"></a>NuGet 治理

> 本文件是以牛津大學的 [Benevolent Dictator Governance Model](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) (仁慈獨裁者治理模型) 為基礎。 它是透過 [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/) 所授權。

NuGet 專案是由仁慈獨裁者所帶領，並且由社群進行管理。 也就是說，社群主動參與專案的日常維護，但是由仁慈獨裁者策畫一般策略線。 如果不一致，則由仁慈獨裁者決定。

仁慈獨裁者負責解決社群內的爭議，以及確保可以透過協作方式執行專案。 接著，社群負責透過主動參與和貢獻引導仁慈獨裁者進行決策。

## <a name="roles-and-responsibilities"></a>角色和責任

這裡描述四種角色：仁慈獨裁者、認可者、參與者和使用者。

### <a name="benevolent-dictator"></a>仁慈獨裁者

NuGet 核心小組會自行指派為仁慈獨裁者或專案負責人。 不過，因為社群一律可以進行分叉，所以小組可以對社群完全負責。 專案負責人必須了解整體社群，並致力於盡可能滿足許多衝突需求，同時確保專案長期存活。

在許多方面，仁慈獨裁者角色的獨裁性較少，圓滑性較高。 主要是確保專案擴充時，正確人員可對其造成影響，而且社群是依專案負責人的觀點重整。 負責人接著負責確保認可者 (請參閱下面) 代表專案做出正確決策。 一般而言，只要認可者遵循專案策略，專案負責人就允許他們依需要進行。

此外，基於商務作業用途，.NET Foundation 人員也會將專案負責人視為 NuGet 的主要或第一個連絡點，包含網域註冊和技術服務 (例如程式碼簽署)。

### <a name="committers"></a>認可者

認可者是對 NuGet 有持續重要貢獻且由仁慈獨裁者指派的參與者。 認可者在指派之後會依賴將程式碼直接寫入存放庫，並篩選其他人的貢獻。 認可者通常是開發人員，但可以透過其他方式參與。

一般而言，認可者著重於專案的特定層面，並具有某程度的專業和了解，讓他們贏得社群和專案負責人的尊重。 認可者角色不是正式角色，而只是具影響力的社群成員所擔任的身分，因為專案負責人會向其尋求指引和支援。

認可者沒有關注整體 NuGet 方向的授權。 不過，專案負責人會聽取他們的意見。 認可者負責確保負責人了解社群的需求和共同目標，並協助開發或引出對專案的適當貢獻。 通常，認可者可非正式控制他們負責的特定領域，並且獲指派直接修改原始程式碼特定領域的權限。 也就是說，雖然認可者沒有明確決策授權，但是他們通常會發現其動作與負責人的決策類似。

### <a name="contributors"></a>Contributors

參與者是將修補程式提交給 NuGet 的社群成員。 這些修補檔案可能只發生一次或一段時間。 參與者、認可者和專案負責人確信參與者的修補程式品質時，參與者預期會提交一開始很小但逐漸變大的修補程式。 在相關聯的產品版本資訊文件中可以辨識參與者。

參與者必須簽署[參與者授權合約](http://en.wikipedia.org/wiki/Contributor_License_Agreement)或 .NET Foundation 的指派合約，才會將他們的第一個修補程式放入存放庫中。 修補程式可以進行提交和討論，但它實際上需要有適當的書面文件才能認可到存放庫。 若要取得參與者授權合約，請透過電子郵件將要求傳送至 [contributions@nuget.org](mailto:contributions@nuget.org)。

若要成為參與者，請將提取要求提交至下列其中一個存放庫：

- [NuGet 用戶端](https://github.com/NuGet/NuGet.Client)
- [NuGet 資源庫](https://github.com/nuget/nugetgallery)
- [NuGet 文件](https://github.com/nuget/nugetdocs)

用於提交提取要求的詳細程序會因存放庫而不同：

- [NuGet 用戶端和 NuGet 資源庫的參與指示](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet 文件的參與指示](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>使用者

使用者是需要並使用 NuGet 作為套件取用者和 (或) 作者的社群成員。 使用者是最重要的社群成員：沒有他們，專案就沒有任何用途。 任何人都可以是使用者；沒有特定需求。

應該鼓勵使用者盡可能參與 NuGet 和社群的生命週期。 使用者參與可讓專案小組確保它們滿足這些使用者的需求。 常見使用者活動包含 (但不限於) 下列活動：

- 支援使用專案
- 通知開發人員從新使用者觀點的專案優點和缺點
- 提供士氣支援 (感謝您一路陪伴)
- 撰寫文件和教學課程
- 提出 Bug 報表和功能要求
- 參與社群事件 (例如群眾挑錯)
- 參與討論板或論壇

持續參與專案和其社群的使用者通常會發現自己涉入地越來越多。 這類使用者接著可能會變成參與者，如上所述。

## <a name="package-succession-under-special-circumstances"></a>特殊情況下的套件接續
在 NuGet 帳戶持有者無行為能力或死亡的不幸情況下，我們會與社群合作，以將適當的擁有者新增至所指出帳戶具有唯一擁有權的套件，並透過 [OSI 核准的授權](https://opensource.org/licenses/alphabetical)發行套件。 若要要求擁有權，您必須將下列文件傳送給我們：

1.  您政府核發的相片識別碼影本。
2.  下列其中一份文件證明先前帳戶持有者的狀態： 
    - 政府在先前帳戶持有人死亡時發出的正式死亡憑證，或者
    - 認證的文件，例如負責照護無行為能力之帳戶持有者的醫療專業人員所簽署的憑證。
3.  證明您擁有權權限的下列其中一份文件： 
    - 顯示您是帳戶持有者之存活配偶的結婚證書、
    - 簽署的委託書、
    - 將您命名為遺囑執行人或受益人的意向或信任文件複本、
    - 帳戶持有者的出生證明 (如果您是其父母)，或者
    - 監護權書面作業 (如果您是帳戶持有者的合法監護人)。
    
如果您發現自己確實需要叫用此原則，請使用套件的識別碼和版本，傳送電子郵件至下列地址：[support@nuget.org](mailto:support@nuget.org)。
    
## <a name="transparency"></a>透明度

建置透過開放原始碼專案治理的社群信任對於成功而言十分重要。 為了這個目的，必須以透明且開放的方式進行決策。 專案方向的討論必須公開進行。 社群絕對不應該提防仁慈獨裁者做出的決策。 此外，必須封存專案決策的討論，讓社群成員可以了解決策和其內容的整個歷程記錄。
