---
title: 刪除 nuget.org 中的 NuGet 套件
description: 取消列出 nuget.org 中套件的原則。除非套件違反其他原則，否則不支援永久刪除。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581271"
---
# <a name="deleting-packages"></a><span data-ttu-id="12397-103">刪除套件</span><span class="sxs-lookup"><span data-stu-id="12397-103">Deleting packages</span></span>

<span data-ttu-id="12397-104">nuget.org 不支援永久刪除套件。</span><span class="sxs-lookup"><span data-stu-id="12397-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="12397-105">這樣會中斷依賴套件可用性的每個專案，尤其是使用包含套件還原的建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="12397-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="12397-106">nuget.org支援[取消列出包](#unlisting-a-package),可以在網站上的包管理頁中完成。</span><span class="sxs-lookup"><span data-stu-id="12397-106">nuget.org does supports [unlisting a package](#unlisting-a-package), which can be done in the package management page on the web site.</span></span> <span data-ttu-id="12397-107">未列出的套件不會出現在 nuget.org 或 Visual Studio UI 中，也不會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="12397-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="12397-108">不過，使用支援套件還原的確切版本號碼仍可以下載及安裝未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="12397-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="12397-109">此外，下列特定案例仍會探索到未列出的套件：</span><span class="sxs-lookup"><span data-stu-id="12397-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="12397-110">使用浮點版本的套件還原 (例如，`1.0.0-*`)，如果最新的可用套件符合版本或相依性條件約束是未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="12397-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="12397-111">透過目錄複寫套件 (因為目錄也包含未列出的套件)。</span><span class="sxs-lookup"><span data-stu-id="12397-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="12397-112">例外狀況</span><span class="sxs-lookup"><span data-stu-id="12397-112">Exceptions</span></span>

<span data-ttu-id="12397-113">在發生著作權侵權和有潛在危險內容等例外情況下，NuGet 小組可以手動刪除套件。</span><span class="sxs-lookup"><span data-stu-id="12397-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="12397-114">您可使用 NuGet.org 套件詳細資料頁面上的 [檢舉不當使用] 按鈕來回報套件。</span><span class="sxs-lookup"><span data-stu-id="12397-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="12397-115">若您為套件擁有者，請登入 NuGet.org 帳戶，使用 NuGet.org 套件詳細資料頁面上的 [連絡支援人員] 按鈕來尋求 NuGet 的支援。</span><span class="sxs-lookup"><span data-stu-id="12397-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="12397-116">禁止使用</span><span class="sxs-lookup"><span data-stu-id="12397-116">Prohibited use</span></span>

<span data-ttu-id="12397-117">所有符合下列準則的套件概不允許出現在公用 NuGet 資源庫中，且沒有商量餘地立即移除。</span><span class="sxs-lookup"><span data-stu-id="12397-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="12397-118">但會通知套件擁有者移除相關事項。</span><span class="sxs-lookup"><span data-stu-id="12397-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="12397-119">包含惡意程式碼、廣告軟體或任何種類的間諜軟體。</span><span class="sxs-lookup"><span data-stu-id="12397-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="12397-120">旨在傷害開發人員工作站或其組織。</span><span class="sxs-lookup"><span data-stu-id="12397-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="12397-121">侵害著作權或違反授權。</span><span class="sxs-lookup"><span data-stu-id="12397-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="12397-122">包含不法內容。</span><span class="sxs-lookup"><span data-stu-id="12397-122">Contains illegal content.</span></span>
- <span data-ttu-id="12397-123">旨在佔用套件識別碼，包括具有零生產力內容的套件。</span><span class="sxs-lookup"><span data-stu-id="12397-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="12397-124">套件必須包含程式碼，否則擁有者必須將識別碼讓實際上有產品要出貨的人。</span><span class="sxs-lookup"><span data-stu-id="12397-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="12397-125">嘗試讓資源庫進行未明確設計其執行的作業。</span><span class="sxs-lookup"><span data-stu-id="12397-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="12397-126">如果您發現有套件違反其中任一項目，請按一下套件詳細資料頁面上的 [檢舉不當使用]\*\*\*\* 連結並提交報告。</span><span class="sxs-lookup"><span data-stu-id="12397-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="12397-127">請注意，NuGet 小組和 .NET Foundation 保留隨時變更這些準則的權利。</span><span class="sxs-lookup"><span data-stu-id="12397-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>

## <a name="unlisting-a-package"></a><span data-ttu-id="12397-128">取消列出套件</span><span class="sxs-lookup"><span data-stu-id="12397-128">Unlisting a package</span></span>
<span data-ttu-id="12397-129">取消列出包版本會將其隱藏在搜索和nuget.org包詳細資訊頁中。</span><span class="sxs-lookup"><span data-stu-id="12397-129">Unlisting a package version hides it from search and from nuget.org package details page.</span></span> <span data-ttu-id="12397-130">這允許包的現有使用者繼續使用它,但減少了新的採用,因為包在搜索中不可見。</span><span class="sxs-lookup"><span data-stu-id="12397-130">This allows existing users of the package to continue using it but reduces new adoption since the package is not visible in search.</span></span>

<span data-ttu-id="12397-131">取消列出套件清單的步驟:</span><span class="sxs-lookup"><span data-stu-id="12397-131">Steps to unlist a package:</span></span>

1. <span data-ttu-id="12397-132">選擇`Your account name`(右上角)>`Manage packages` > `Published packages`</span><span class="sxs-lookup"><span data-stu-id="12397-132">Select `Your account name` (at the top right corner) >`Manage packages` > `Published packages`</span></span>
1. <span data-ttu-id="12397-133">選擇「管理包」圖示</span><span class="sxs-lookup"><span data-stu-id="12397-133">Select the "Manage package" icon</span></span>
1. <span data-ttu-id="12397-134">展開「清單」部分並選擇套件版本</span><span class="sxs-lookup"><span data-stu-id="12397-134">Expand the "Listing" section and select the package version</span></span>
1. <span data-ttu-id="12397-135">取消選取中的"搜尋結果中的清單"並選擇"保存"</span><span class="sxs-lookup"><span data-stu-id="12397-135">Uncheck “List in search results” and select "Save"</span></span>

<span data-ttu-id="12397-136">特定包版本現已未列出。</span><span class="sxs-lookup"><span data-stu-id="12397-136">The specific package version has now been unlisted.</span></span> <span data-ttu-id="12397-137">為了驗證這一點,登出您的帳號並瀏覽到套件頁(沒有版本元件),例如: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/。</span><span class="sxs-lookup"><span data-stu-id="12397-137">In order to verify this, logout of your account and navigate to the package page (without the version part) e.g.: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/.</span></span> <span data-ttu-id="12397-138">您將看到該包的所有版本**尚未**列出。</span><span class="sxs-lookup"><span data-stu-id="12397-138">You will see all versions of that package that have **not** been unlisted.</span></span> <span data-ttu-id="12397-139">但是,包擁有者在登錄時可以看到所有版本及其列表狀態。</span><span class="sxs-lookup"><span data-stu-id="12397-139">However, the package owner, when logged in, can see all versions and their listing status.</span></span>

<span data-ttu-id="12397-140">也可以棄用套件版本(如果無法刪除包版本)。</span><span class="sxs-lookup"><span data-stu-id="12397-140">It's also possible to deprecate a package version (in case you can't delete a package version).</span></span> <span data-ttu-id="12397-141">有關棄用套件版本的詳細資訊,請參閱[棄用包](../deprecate-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="12397-141">For more information about deprecating package versions, see [Deprecating packages](../deprecate-packages.md).</span></span>
