---
title: "識別碼前置詞保留項目參考 |Microsoft 文件"
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "封裝識別碼的前置詞保留項目功能的描述及撰寫指南。"
keywords: "NuGet 封裝識別碼、 前置詞、 保留項目"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: f74ea3c772a129f4b9cd286a77cf3e88eba2d33b
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="5067a-104">封裝識別碼前置詞保留項目</span><span class="sxs-lookup"><span data-stu-id="5067a-104">Package ID prefix reservation</span></span>

<span data-ttu-id="5067a-105">封裝擁有者可以保留，而保留識別碼前置詞來保護他們的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5067a-105">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="5067a-106">封裝取用者會提供其他資訊時使用之封裝的他們使用的封裝將不會詐騙識別屬性中。</span><span class="sxs-lookup"><span data-stu-id="5067a-106">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="5067a-107">[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 或更新版本的套件，只要封裝符合保留的識別碼送出的擁有者，以保留的封裝識別碼的前置詞，前置詞的命名模式，顯示一種視覺指標。</span><span class="sxs-lookup"><span data-stu-id="5067a-107">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="5067a-108">參考下列說明識別碼的前置詞保留區的需要，以及如何套用的擁有者識別碼前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-108">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="5067a-109">識別碼前置詞保留項目詳細資料</span><span class="sxs-lookup"><span data-stu-id="5067a-109">ID prefix reservation details</span></span>

<span data-ttu-id="5067a-110">上的封裝識別碼前置詞為保留字，當發生數種事項[nuget.org](https://www.nuget.org/)組件庫，以及與 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5067a-110">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="5067a-111">此外，屬於進階識別碼前置詞保留項目，例如，設定的前置詞為 'public'，而前置詞子集委派給多個擁有者所支援的案例。</span><span class="sxs-lookup"><span data-stu-id="5067a-111">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="5067a-112">識別碼前置詞在 nuget.org 的保留項目</span><span class="sxs-lookup"><span data-stu-id="5067a-112">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="5067a-113">前置詞都會保留在[nuget.org](https://www.nuget.org/)，將會發生下列：</span><span class="sxs-lookup"><span data-stu-id="5067a-113">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="5067a-114">前置詞保留項目關聯的擁有者或擁有者的集合上[nuget.org](https://www.nuget.org/)。</span><span class="sxs-lookup"><span data-stu-id="5067a-114">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="5067a-115">封裝每次提交給[nuget.org](https://www.nuget.org/)識別碼符合保留的識別碼前置詞，除非它來自保留識別碼首碼而後，會拒絕封裝。</span><span class="sxs-lookup"><span data-stu-id="5067a-115">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="5067a-116">符合保留的識別碼前置詞並源自保留識別碼首碼而後任何套件將具有視覺指標，在 Visual Studio 2017 15.4 以後版本，和[nuget.org](https://www.nuget.org/)指出封裝正在保留的識別碼前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-116">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="5067a-117">這是新的封裝提交以及下者的現有封裝，則為 true。</span><span class="sxs-lookup"><span data-stu-id="5067a-117">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="5067a-118">**注意：**單一摘要當做封裝來源時，才會出現在 Visual Studio 中的指標。</span><span class="sxs-lookup"><span data-stu-id="5067a-118">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="5067a-119">所有先前已存在封裝符合保留的識別碼前置詞，但這是*不*保留的擁有者所擁有的前置詞將維持不變 （而不要使用未列出，但也不會提供視覺指標）。</span><span class="sxs-lookup"><span data-stu-id="5067a-119">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="5067a-120">此外，這些封裝的擁有者仍會送出至封裝的新版本。</span><span class="sxs-lookup"><span data-stu-id="5067a-120">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="5067a-121">這些變更會根據下列條件，並強制執行數個其他的限制：</span><span class="sxs-lookup"><span data-stu-id="5067a-121">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="5067a-122">只有一個擁有者的封裝必須有保留的前置詞的視覺指標，以顯示 （適用於與多個擁有者的封裝）。</span><span class="sxs-lookup"><span data-stu-id="5067a-122">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="5067a-123">如果有一個以上的擁有者的其中一個或多個擁有者有保留的前置詞，而一或多個擁有者沒有保留的前置詞的封裝，以保留的前置詞者可以移除其他而後與保留的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-123">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="5067a-124">擁有者不需要保留的前置詞不能移除以保留的前置詞的擁有者。</span><span class="sxs-lookup"><span data-stu-id="5067a-124">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="5067a-125">他們仍然可以移除其他擁有者，也不需要保留的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-125">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="5067a-126">一旦封裝具有視覺指標，它應該*一律*將視覺化指標 （具有保留的前置詞，至少一個擁有者，以及確保一定會維持一位擁有者）</span><span class="sxs-lookup"><span data-stu-id="5067a-126">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="5067a-127">進階的前置詞保留項目案例</span><span class="sxs-lookup"><span data-stu-id="5067a-127">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="5067a-128">有數個更進階的前置詞保留案例如下所述，包括 subprefix 委派，並標示為公用的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-128">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="5067a-129">以下是更進階的前置詞保留項目，才能進行。</span><span class="sxs-lookup"><span data-stu-id="5067a-129">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="5067a-130">前置詞保留期間之擁有者可以要求的前置詞子集委派 （或前置詞） 其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="5067a-130">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="5067a-131">例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.\*'，但'[aspnet](https://www.nuget.org/profiles/aspnet)'想要保留' Microsoft.AspNet。\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇將委派 ' Microsoft.AspNet。\*' 至[aspnet](https://www.nuget.org/profiles/aspnet)帳戶。</span><span class="sxs-lookup"><span data-stu-id="5067a-131">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="5067a-132">前置詞保留期間的擁有者可以選擇將前置詞設為公用。</span><span class="sxs-lookup"><span data-stu-id="5067a-132">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="5067a-133">這仍然會提供這些封裝來自保留的前置詞，但不是會顯示的視覺指示器**不**封鎖前置詞的未來封裝提交任何擁有者。</span><span class="sxs-lookup"><span data-stu-id="5067a-133">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="5067a-134">這適用於具有許多參與者的開放原始碼專案： top 或核心參與者可以有前置詞保留，但它仍然是開放給所有參與者。</span><span class="sxs-lookup"><span data-stu-id="5067a-134">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="5067a-135">前置詞保留視覺指標</span><span class="sxs-lookup"><span data-stu-id="5067a-135">Prefix reservation visual indicator</span></span>

<span data-ttu-id="5067a-136">當封裝來自於保留的前置詞時，您會看到下面上的視覺指標[nuget.org](https://www.nuget.org/)組件庫和 Visual Studio 2017 15.4 或更新版本中：</span><span class="sxs-lookup"><span data-stu-id="5067a-136">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="5067a-137">**nuget.org 圖庫**
![nuget.org 組件庫](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="5067a-137">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="5067a-138">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="5067a-138">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="5067a-139">識別碼前置詞保留應用程式處理序</span><span class="sxs-lookup"><span data-stu-id="5067a-139">ID prefix reservation application process</span></span>

1. <span data-ttu-id="5067a-140">檢閱接受[前置詞識別碼保留項目的準則](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="5067a-140">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

1. <span data-ttu-id="5067a-141">判斷您想要保留時，除了任何命名的空間[進階前置詞保留案例](#advanced-prefix-reservation-scenarios)，您可能需要。</span><span class="sxs-lookup"><span data-stu-id="5067a-141">Determine the namespaces you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

1. <span data-ttu-id="5067a-142">傳送郵件給[ account@nuget.org ](mailto:account@nuget.org)與擁有者顯示名稱上[nuget.org](https://www.nuget.org/)，以及任何您要求保留的前置詞。</span><span class="sxs-lookup"><span data-stu-id="5067a-142">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="5067a-143">如果您正在委派前置詞的子集，多個擁有者，請確定您提到所有擁有者的顯示名稱和前置詞的子集。</span><span class="sxs-lookup"><span data-stu-id="5067a-143">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="5067a-144">在提交應用程式之後，就會通知的接受或拒絕 （使用準則造成拒絕）。</span><span class="sxs-lookup"><span data-stu-id="5067a-144">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="5067a-145">我們可能需要詢問確認擁有者身分識別的其他識別問題。</span><span class="sxs-lookup"><span data-stu-id="5067a-145">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="5067a-146">識別碼前置詞保留項目條件</span><span class="sxs-lookup"><span data-stu-id="5067a-146">ID prefix reservation criteria</span></span>

<span data-ttu-id="5067a-147">檢閱任何應用程式的識別碼前置詞保留項目時[nuget.org](https://www.nuget.org/)小組將會評估針對應用程式準則如下。</span><span class="sxs-lookup"><span data-stu-id="5067a-147">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="5067a-148">並非所有的條件必須符合的前置詞，而保留，但如果不是大量的辨識項的準則 （並提供說明） 符合應用程式可能會被拒絕：</span><span class="sxs-lookup"><span data-stu-id="5067a-148">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="5067a-149">就封裝識別碼首碼正確且清楚地識別封裝擁有者嗎？</span><span class="sxs-lookup"><span data-stu-id="5067a-149">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="5067a-150">已提交的封裝大量所下的封裝識別碼前置詞的擁有者嗎？</span><span class="sxs-lookup"><span data-stu-id="5067a-150">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="5067a-151">是封裝識別碼首碼一般應該不屬於任何個別擁有者或組織嗎？</span><span class="sxs-lookup"><span data-stu-id="5067a-151">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="5067a-152">會*不*保留封裝識別碼前置詞會造成模稜兩可和混淆社群？</span><span class="sxs-lookup"><span data-stu-id="5067a-152">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="5067a-153">會識別符合的封裝識別碼首碼清楚且一致 （尤其是封裝作者） 的封裝的內容嗎？</span><span class="sxs-lookup"><span data-stu-id="5067a-153">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="5067a-154">第三方摘要提供者案例</span><span class="sxs-lookup"><span data-stu-id="5067a-154">Third party feed provider scenarios</span></span>

<span data-ttu-id="5067a-155">如果想要實作自己的服務提供前置詞保留項目摘要提供者的第三方，您可以執行藉由修改搜尋服務 NuGet v3 摘要提供者。</span><span class="sxs-lookup"><span data-stu-id="5067a-155">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="5067a-156">摘要的搜尋服務中會新增*驗證*屬性，請使用下列的 V3 摘要的範例。</span><span class="sxs-lookup"><span data-stu-id="5067a-156">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="5067a-157">NuGet 用戶端將不會支援摘要 V2 中加入的屬性。</span><span class="sxs-lookup"><span data-stu-id="5067a-157">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="5067a-158">如需詳細資訊，請參閱[API 的搜尋服務的相關文件](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="5067a-158">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>
