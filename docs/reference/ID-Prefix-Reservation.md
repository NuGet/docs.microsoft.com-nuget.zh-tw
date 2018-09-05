---
title: 識別碼首碼保留項目參考
description: 套件識別碼首碼保留項目功能的描述和作者指南。
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 0711f3ee00b4a387d676ca43c98a9467effed90a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546586"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="20747-103">套件識別碼首碼保留項目</span><span class="sxs-lookup"><span data-stu-id="20747-103">Package ID prefix reservation</span></span>

<span data-ttu-id="20747-104">套件擁有者可保留並保護他們的身分識別，藉由保留識別碼前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="20747-105">套件取用者會提供其他資訊時使用之封裝的他們耗用的封裝將不會詐騙其識別的屬性中。</span><span class="sxs-lookup"><span data-stu-id="20747-105">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="20747-106">[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 版或更新版本的套件，只要封裝符合保留的 ID，由擁有者具有保留的套件識別碼前置詞，會提交前置詞的命名模式，顯示的視覺指標。</span><span class="sxs-lookup"><span data-stu-id="20747-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="20747-107">下列參考說明識別碼首碼保留項目需要什麼，以及如何擁有者可以申請識別碼前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="20747-108">識別碼首碼保留項目詳細資料</span><span class="sxs-lookup"><span data-stu-id="20747-108">ID prefix reservation details</span></span>

<span data-ttu-id="20747-109">當保留的套件識別碼前置詞時，在 發生幾件事[nuget.org](https://www.nuget.org/)資源庫，以及與 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="20747-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="20747-110">此外，那里一些進階的識別碼首碼保留項目，例如設定的前置詞為 'public'，將前置詞子集委派給多個擁有者所支援的案例。</span><span class="sxs-lookup"><span data-stu-id="20747-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="20747-111">在 nuget.org 上的識別碼首碼保留項目</span><span class="sxs-lookup"><span data-stu-id="20747-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="20747-112">當保留上的前置詞[nuget.org](https://www.nuget.org/)，會發生下列：</span><span class="sxs-lookup"><span data-stu-id="20747-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="20747-113">首碼保留項目相關聯的擁有者或擁有者的集合上[nuget.org](https://www.nuget.org/)。</span><span class="sxs-lookup"><span data-stu-id="20747-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="20747-114">封裝每次提交給[nuget.org](https://www.nuget.org/)識別碼符合的保留的識別碼前置詞，除非它來自擁有者保留識別碼前置詞，會拒絕封裝。</span><span class="sxs-lookup"><span data-stu-id="20747-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="20747-115">在 Visual Studio 2017 15.4 版或更新版本，和任何符合保留的識別碼前置詞，以及所有源自保留識別碼前置詞的擁有者的套件會有視覺指示器[nuget.org](https://www.nuget.org/)指出封裝正在進行保留的識別碼前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="20747-116">這是新的封裝提交以及現有的封裝，在擁有者，則為 true。</span><span class="sxs-lookup"><span data-stu-id="20747-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="20747-117">**注意：** 單一摘要選取作為封裝來源時，才會出現在 Visual Studio 中的指標。</span><span class="sxs-lookup"><span data-stu-id="20747-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="20747-118">所有先前已經有套件符合保留的識別碼前置詞，但會*不*保留的擁有者所擁有的前置詞將維持不變 （它們不會列出，但它們也不會具有視覺指標）。</span><span class="sxs-lookup"><span data-stu-id="20747-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="20747-119">此外，這些套件的擁有者將仍然可以提交給封裝的新版本。</span><span class="sxs-lookup"><span data-stu-id="20747-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="20747-120">這些變更根據下列條件，並且加上幾個額外的限制：</span><span class="sxs-lookup"><span data-stu-id="20747-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="20747-121">封裝只能有一個擁有者必須具有保留的前置詞，如 （適用於與多個擁有者的套件） 所顯示的視覺指示器。</span><span class="sxs-lookup"><span data-stu-id="20747-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="20747-122">如果有一個以上的擁有者的其中一個或多個擁有者具有保留的前置詞，而一或多個擁有者並沒有保留的前置詞的套件，只保留的前置詞與擁有者可以移除其他擁有者與保留的前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="20747-123">擁有者並沒有保留的前置詞不能移除以保留的前置詞的擁有者。</span><span class="sxs-lookup"><span data-stu-id="20747-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="20747-124">它們仍可以移除其他擁有者，也不需要保留的前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="20747-125">當封裝具有視覺指標之後，它應該*一律*有視覺指示器 （保證具有保留的前置詞，至少一個擁有者將會一直保持 「 擁有者）</span><span class="sxs-lookup"><span data-stu-id="20747-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="20747-126">進階的前置詞保留案例</span><span class="sxs-lookup"><span data-stu-id="20747-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="20747-127">有數個更進階的前置詞保留案例如下所述，包括 subprefix 委派和標記前置詞為公用。</span><span class="sxs-lookup"><span data-stu-id="20747-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="20747-128">以下是更進階的前置詞保留項目可進行。</span><span class="sxs-lookup"><span data-stu-id="20747-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="20747-129">首碼保留項目，在擁有者可以要求委派的前置詞的子集 （或前置詞） 給其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="20747-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="20747-130">例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.著作權\*'，但'[aspnet](https://www.nuget.org/profiles/aspnet)'想要保留' Microsoft.AspNet。\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇委派 ' Microsoft.AspNet。\*' 來[aspnet](https://www.nuget.org/profiles/aspnet)帳戶。</span><span class="sxs-lookup"><span data-stu-id="20747-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="20747-131">在 首碼保留項目，擁有者可以選擇，設為前置詞為公用。</span><span class="sxs-lookup"><span data-stu-id="20747-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="20747-132">這樣做仍然會提供這些封裝來自保留的前置詞，但不是會顯示的視覺指示器**不**封鎖這個前置詞的未來封裝提交，任何擁有者。</span><span class="sxs-lookup"><span data-stu-id="20747-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="20747-133">這是適用於具有許多的參與者的開放原始碼專案-top 或核心參與者都可以有前置詞保留，但它仍然是開放給所有的參與者。</span><span class="sxs-lookup"><span data-stu-id="20747-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="20747-134">前置詞保留區視覺指示器。</span><span class="sxs-lookup"><span data-stu-id="20747-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="20747-135">當封裝來自保留的前置詞時，您會看到下面上的視覺指示器[nuget.org](https://www.nuget.org/)資源庫和 Visual Studio 2017 15.4 版或更新版本中：</span><span class="sxs-lookup"><span data-stu-id="20747-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="20747-136">**nuget.org 資源庫**
![nuget.org 資源庫](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="20747-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="20747-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="20747-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="20747-138">識別碼首碼保留項目應用程式處理序</span><span class="sxs-lookup"><span data-stu-id="20747-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="20747-139">檢閱接受[首碼識別碼保留項目準則](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="20747-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="20747-140">決定您想要保留時，除了任何命名的空間[進階的前置詞保留案例](#advanced-prefix-reservation-scenarios)您可能需要。</span><span class="sxs-lookup"><span data-stu-id="20747-140">Determine the namespaces you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="20747-141">傳送郵件給[ account@nuget.org ](mailto:account@nuget.org)擁有者顯示名稱上[nuget.org](https://www.nuget.org/)，以及您所要求的任何保留前置詞。</span><span class="sxs-lookup"><span data-stu-id="20747-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="20747-142">如果您多個擁有者委派前置詞的子集，請確定您提到所有擁有者顯示名稱和前置詞子集。</span><span class="sxs-lookup"><span data-stu-id="20747-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="20747-143">在提交應用程式之後，您會收到通知的接受或拒絕 （並導致拒絕的準則）。</span><span class="sxs-lookup"><span data-stu-id="20747-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="20747-144">我們可能需要詢問以確認擁有者身分識別的其他識別問題。</span><span class="sxs-lookup"><span data-stu-id="20747-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="20747-145">識別碼首碼保留項目條件</span><span class="sxs-lookup"><span data-stu-id="20747-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="20747-146">檢閱識別碼首碼保留項目，任何應用程式時[nuget.org](https://www.nuget.org/)小組會評估應用程式對於下列準則。</span><span class="sxs-lookup"><span data-stu-id="20747-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="20747-147">並非所有的準則必須符合的前置詞保留，但如果不是大量的辨識項 （與指定的說明） 符合準則的應用程式可能會被拒絕：</span><span class="sxs-lookup"><span data-stu-id="20747-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="20747-148">沒有套件識別碼前置詞正確且清楚地識別套件擁有者？</span><span class="sxs-lookup"><span data-stu-id="20747-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="20747-149">有大量已提交的封裝所下的套件識別碼前置詞的擁有者嗎？</span><span class="sxs-lookup"><span data-stu-id="20747-149">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="20747-150">是的套件識別碼前置詞一般指應該不屬於任何個別擁有者或組織嗎？</span><span class="sxs-lookup"><span data-stu-id="20747-150">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="20747-151">想*不*保留的套件識別碼前置詞會造成模稜兩可和社群的混淆嗎？</span><span class="sxs-lookup"><span data-stu-id="20747-151">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="20747-152">會識別符合的套件識別碼前置詞清楚且一致 （尤其是封裝作者） 的封裝的內容嗎？</span><span class="sxs-lookup"><span data-stu-id="20747-152">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="20747-153">摘要提供者案例的第三方</span><span class="sxs-lookup"><span data-stu-id="20747-153">Third party feed provider scenarios</span></span>

<span data-ttu-id="20747-154">如果想要實作自己的服務，以提供前置詞保留項目摘要提供者的第三方，您可以執行修改 NuGet V3 中的搜尋服務摘要提供者。</span><span class="sxs-lookup"><span data-stu-id="20747-154">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="20747-155">摘要的搜尋服務中會新增*驗證*屬性，使用下列的 V3 摘要的範例。</span><span class="sxs-lookup"><span data-stu-id="20747-155">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="20747-156">在 V2 中摘要，NuGet 用戶端將不支援加入的屬性。</span><span class="sxs-lookup"><span data-stu-id="20747-156">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="20747-157">如需詳細資訊，請參閱 < [API 的搜尋服務相關的文件](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="20747-157">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="20747-158">套件識別碼首碼保留項目爭議原則</span><span class="sxs-lookup"><span data-stu-id="20747-158">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="20747-159">如果您認為上的擁有者[NuGet.org](https://www.nuget.org)已指派的套件識別碼首碼保留項目違背了上述所列的準則，或侵害任何商標或著作權，請電子郵件[ support@nuget.org ](mailto:support@nuget.org)問題識別碼首碼、 的擁有者識別碼前置詞，以及基於 disputing 指派的首碼保留項目。</span><span class="sxs-lookup"><span data-stu-id="20747-159">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

