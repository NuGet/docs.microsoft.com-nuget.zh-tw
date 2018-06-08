---
title: 刪除 nuget.org 中的 NuGet 套件
description: 取消列出 nuget.org 中套件的原則。除非套件違反其他原則，否則不支援永久刪除。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 84a27c16968fa55ff1929db1adf98b8242a64fcf
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816976"
---
# <a name="deleting-packages"></a><span data-ttu-id="94cba-103">刪除套件</span><span class="sxs-lookup"><span data-stu-id="94cba-103">Deleting packages</span></span>

<span data-ttu-id="94cba-104">nuget.org 不支援永久刪除套件。</span><span class="sxs-lookup"><span data-stu-id="94cba-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="94cba-105">這樣會中斷依賴套件可用性的每個專案，尤其是使用包含套件還原的建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="94cba-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="94cba-106">nuget.org 不支援「取消列出」套件，此作業可在網站的套件管理頁面中完成。</span><span class="sxs-lookup"><span data-stu-id="94cba-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="94cba-107">未列出的套件不會出現在 nuget.org 或 Visual Studio UI 中，也不會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="94cba-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="94cba-108">不過，使用支援套件還原的確切版本號碼仍可以下載及安裝未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="94cba-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="94cba-109">此外，下列特定案例仍會探索到未列出的套件：</span><span class="sxs-lookup"><span data-stu-id="94cba-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="94cba-110">使用浮點版本的套件還原 (例如，`1.0.0-*`)，如果最新的可用套件符合版本或相依性條件約束是未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="94cba-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="94cba-111">透過目錄複寫套件 (因為目錄也包含未列出的套件)。</span><span class="sxs-lookup"><span data-stu-id="94cba-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="94cba-112">例外狀況</span><span class="sxs-lookup"><span data-stu-id="94cba-112">Exceptions</span></span>

<span data-ttu-id="94cba-113">在發生著作權侵權和有潛在危險內容等例外情況下，NuGet 小組可以手動刪除套件。</span><span class="sxs-lookup"><span data-stu-id="94cba-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="94cba-114">透過 [NuGet 資源庫](http://www.nuget.org)提交支援要求以啟動程序。</span><span class="sxs-lookup"><span data-stu-id="94cba-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="94cba-115">禁止使用</span><span class="sxs-lookup"><span data-stu-id="94cba-115">Prohibited use</span></span>

<span data-ttu-id="94cba-116">所有符合下列準則的套件概不允許出現在公用 NuGet 資源庫中，且沒有商量餘地立即移除。</span><span class="sxs-lookup"><span data-stu-id="94cba-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="94cba-117">但會通知套件擁有者移除相關事項。</span><span class="sxs-lookup"><span data-stu-id="94cba-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="94cba-118">包含惡意程式碼、廣告軟體或任何種類的間諜軟體。</span><span class="sxs-lookup"><span data-stu-id="94cba-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="94cba-119">旨在傷害開發人員工作站或其組織。</span><span class="sxs-lookup"><span data-stu-id="94cba-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="94cba-120">侵害著作權或違反授權。</span><span class="sxs-lookup"><span data-stu-id="94cba-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="94cba-121">包含不法內容。</span><span class="sxs-lookup"><span data-stu-id="94cba-121">Contains illegal content.</span></span>
- <span data-ttu-id="94cba-122">旨在佔用套件識別碼，包括具有零生產力內容的套件。</span><span class="sxs-lookup"><span data-stu-id="94cba-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="94cba-123">套件必須包含程式碼，否則擁有者必須將識別碼讓實際上有產品要出貨的人。</span><span class="sxs-lookup"><span data-stu-id="94cba-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="94cba-124">嘗試讓資源庫進行未明確設計其執行的作業。</span><span class="sxs-lookup"><span data-stu-id="94cba-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="94cba-125">如果您發現違反上述任一項目的套件，請按一下套件詳細資料頁面上的 [檢舉不當使用] 連結，並提交報告。</span><span class="sxs-lookup"><span data-stu-id="94cba-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="94cba-126">請注意，NuGet 小組和 .NET Foundation 保留隨時變更這些準則的權利。</span><span class="sxs-lookup"><span data-stu-id="94cba-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
