---
title: 識別碼首碼保留項目
description: 套件識別碼首碼保留項目功能的描述和作者指南。
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 94036e3ca7c65e6878f24a5a8514cbb0d8816d9c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427223"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="efd61-103">套件識別碼首碼保留項目</span><span class="sxs-lookup"><span data-stu-id="efd61-103">Package ID prefix reservation</span></span>

<span data-ttu-id="efd61-104">套件擁有者可以藉由保留識別碼首碼，保留並保護他們的身分識別。</span><span class="sxs-lookup"><span data-stu-id="efd61-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="efd61-105">套件取用者在取用套件時會得到額外的資訊，指出他們取用的套件在其識別屬性中沒有欺騙成分。</span><span class="sxs-lookup"><span data-stu-id="efd61-105">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="efd61-106">[nuget.org](https://www.nuget.org/) 和 Visual Studio 2017 15.4 版或更新版本，對於由擁有者所提交、具有保留套件識別碼首碼的套件，只要套件符合保留識別碼首碼命名模式，便會顯示一個視覺指標。</span><span class="sxs-lookup"><span data-stu-id="efd61-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="efd61-107">以下參考說明識別碼首碼保留項目需要什麼，以及擁有者如何申請識別碼首碼。</span><span class="sxs-lookup"><span data-stu-id="efd61-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="efd61-108">識別碼首碼保留項目詳細資料</span><span class="sxs-lookup"><span data-stu-id="efd61-108">ID prefix reservation details</span></span>

<span data-ttu-id="efd61-109">保留套件識別碼首碼時，在 [nuget.org](https://www.nuget.org/) 資源庫以及 Visual Studio 裡發生幾件事。</span><span class="sxs-lookup"><span data-stu-id="efd61-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="efd61-110">此外，有一些識別碼首碼保留項目支援的進階案例，例如設定首碼為 'public'，將首碼子集委派給多位擁有者。</span><span class="sxs-lookup"><span data-stu-id="efd61-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="efd61-111">nuget.org 上的識別碼首碼保留項目</span><span class="sxs-lookup"><span data-stu-id="efd61-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="efd61-112">在 [nuget.org](https://www.nuget.org/) 上保留首碼時，會發生下列各項：</span><span class="sxs-lookup"><span data-stu-id="efd61-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="efd61-113">首碼保留項目與 [nuget.org](https://www.nuget.org/) 上的擁有者或擁有者集合建立關聯。</span><span class="sxs-lookup"><span data-stu-id="efd61-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="efd61-114">每次提交套件給 [nuget.org](https://www.nuget.org/) 而其識別碼符合保留識別碼首碼時，除非它來自保留該識別碼首碼的擁有者，否則會拒絕該套件。</span><span class="sxs-lookup"><span data-stu-id="efd61-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="efd61-115">任何符合保留識別碼首碼的套件，且套件是源自保留該識別碼首碼的擁有者時，在 Visual Studio 2017 15.4 版或更新版本以及 [nuget.org](https://www.nuget.org/) 上會有一個視覺指標，指出套件位於保留識別碼首碼底下。</span><span class="sxs-lookup"><span data-stu-id="efd61-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="efd61-116">對於新套件提交和擁有者底下的現有套件而言，都是如此。</span><span class="sxs-lookup"><span data-stu-id="efd61-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="efd61-117">**注意：** Visual Studio 中的指標僅會在單一摘要選取為套件來源時出現。</span><span class="sxs-lookup"><span data-stu-id="efd61-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="efd61-118">符合保留識別碼首碼，但「不」  是由保留首碼擁有者所擁有的任何先前現有套件將維持不變 (它們不會被列出，但也不會有視覺指標)。</span><span class="sxs-lookup"><span data-stu-id="efd61-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="efd61-119">此外，這些套件的擁有者將仍然可以將新版本提交至套件。</span><span class="sxs-lookup"><span data-stu-id="efd61-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="efd61-120">這些變更是根據下列條件，且加上幾個額外的限制：</span><span class="sxs-lookup"><span data-stu-id="efd61-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="efd61-121">只需要有一位套件擁有者具有保留首碼，便會顯示視覺指標 (對於有多位擁有者的套件而言)。</span><span class="sxs-lookup"><span data-stu-id="efd61-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="efd61-122">如果有多位套件擁有者，其中一或多位擁有者具有保留首碼，而一或多位擁有者沒有保留首碼，則只有具有保留首碼的擁有者可以移除具有保留首碼的其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="efd61-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="efd61-123">沒有保留首碼之擁有者不能移除具有保留首碼的擁有者。</span><span class="sxs-lookup"><span data-stu-id="efd61-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="efd61-124">他們仍然可以移除也沒有保留首碼的其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="efd61-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="efd61-125">套件有了視覺指標之後，它應該「一律」  有視覺指標 (保證一律會有至少一位具有保留首碼的擁有者保持為擁有者)</span><span class="sxs-lookup"><span data-stu-id="efd61-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="efd61-126">進階首碼保留案例</span><span class="sxs-lookup"><span data-stu-id="efd61-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="efd61-127">以下描述數個更進階的首碼保留案例，包括子首碼委派以及將首碼標記為公用。</span><span class="sxs-lookup"><span data-stu-id="efd61-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="efd61-128">以下是可以進行的較進階首碼保留項目。</span><span class="sxs-lookup"><span data-stu-id="efd61-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="efd61-129">在首碼保留期間，擁有者可以要求委派首碼子集 (或首碼) 給其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="efd61-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="efd61-130">例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 擁有 'Microsoft.\*'，但 '[aspnet](https://www.nuget.org/profiles/aspnet)' 想要保留 'Microsoft.AspNet.\*'，則 '[Microsoft](https://www.nuget.org/profiles/microsoft)' 可以選擇將 'Microsoft.AspNet.\*' 委派給 [aspnet](https://www.nuget.org/profiles/aspnet) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="efd61-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="efd61-131">在首碼保留期間，擁有者可以選擇將首碼設為公用。</span><span class="sxs-lookup"><span data-stu-id="efd61-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="efd61-132">這樣做仍然會提供他們視覺指標，其顯示套件來自保留首碼，但**不會**封鎖任何擁有者未來對於首碼的套件提交。</span><span class="sxs-lookup"><span data-stu-id="efd61-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="efd61-133">這適合具有許多參與者的開放原始碼專案 - 頂尖或核心參與者都可以保留首碼，但仍然開放給所有參與者。</span><span class="sxs-lookup"><span data-stu-id="efd61-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="efd61-134">首碼保留項目視覺指標</span><span class="sxs-lookup"><span data-stu-id="efd61-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="efd61-135">當套件來自保留首碼時，您會在 [nuget.org](https://www.nuget.org/) 資源庫上和 Visual Studio 2017 15.4 版或更新版本中，看到以下視覺指標：</span><span class="sxs-lookup"><span data-stu-id="efd61-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="efd61-136">**nuget.org 資源庫**
![nuget.org 資源庫](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="efd61-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="efd61-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="efd61-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="efd61-138">識別碼首碼保留項目申請程序</span><span class="sxs-lookup"><span data-stu-id="efd61-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="efd61-139">檢閱[首碼識別碼保留項目的驗收準則](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="efd61-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="efd61-140">決定您想要保留的首碼，以及您可能需要的任何[進階首碼保留案例](#advanced-prefix-reservation-scenarios)。</span><span class="sxs-lookup"><span data-stu-id="efd61-140">Determine the prefixes you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="efd61-141">傳送郵件到 [account@nuget.org](mailto:account@nuget.org)，附上 [nuget.org](https://www.nuget.org/) 上的擁有者顯示名稱，以及您所要求的任何保留首碼。</span><span class="sxs-lookup"><span data-stu-id="efd61-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="efd61-142">如果您委派首碼子集給多位擁有者，請務必提及所有擁有者顯示名稱和首碼子集。</span><span class="sxs-lookup"><span data-stu-id="efd61-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="efd61-143">在提交申請之後，您會收到接受或拒絕的通知 (以及導致拒絕的準則)。</span><span class="sxs-lookup"><span data-stu-id="efd61-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="efd61-144">我們可能需要詢問額外的識別問題以確認擁有者身分識別。</span><span class="sxs-lookup"><span data-stu-id="efd61-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="efd61-145">識別碼首碼保留項目準則</span><span class="sxs-lookup"><span data-stu-id="efd61-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="efd61-146">檢閱識別碼首碼保留項目的任何申請時，[nuget.org](https://www.nuget.org/) 小組會針對以下準則評估申請。</span><span class="sxs-lookup"><span data-stu-id="efd61-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="efd61-147">不必滿足所有準則即可保留首碼，但如果沒有實質證明滿足準則 (提供說明)，申請可能遭拒：</span><span class="sxs-lookup"><span data-stu-id="efd61-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="efd61-148">套件識別碼首碼是否能正確且清楚地識別套件擁有者？</span><span class="sxs-lookup"><span data-stu-id="efd61-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="efd61-149">有由擁有者已經在套件識別碼首碼下提交的大量套件嗎？</span><span class="sxs-lookup"><span data-stu-id="efd61-149">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="efd61-150">套件識別碼首碼是否和不應該屬於任何個別擁有者或組織有某些雷同嗎？</span><span class="sxs-lookup"><span data-stu-id="efd61-150">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="efd61-151">保留套件識別碼首碼「不會」  造成模稜兩可和社群的混淆嗎？</span><span class="sxs-lookup"><span data-stu-id="efd61-151">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="efd61-152">符合套件識別碼首碼的套件識別屬性是否清楚且一致 (尤其是套件作者)？</span><span class="sxs-lookup"><span data-stu-id="efd61-152">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

1. <span data-ttu-id="efd61-153">套件是否有授權 (使用 [license](../reference/nuspec.md#license) 中繼資料元素，而非即將淘汰的 licenseUrl)？</span><span class="sxs-lookup"><span data-stu-id="efd61-153">Do the packages have a license (using the [license](../reference/nuspec.md#license) metadata element and NOT licenseUrl which is being deprecated)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="efd61-154">第三方摘要提供者案例</span><span class="sxs-lookup"><span data-stu-id="efd61-154">Third party feed provider scenarios</span></span>

<span data-ttu-id="efd61-155">如果第三方摘要提供者想要實作自己的服務以提供首碼保留項目，您可以修改 NuGet V3 摘要提供者中的搜尋服務來辦到。</span><span class="sxs-lookup"><span data-stu-id="efd61-155">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="efd61-156">摘要搜尋服務中的新增是要新增 *verified* 屬性，V3 摘要的範例如下。</span><span class="sxs-lookup"><span data-stu-id="efd61-156">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="efd61-157">NuGet 用戶端將不支援在 V2 摘要中新增的屬性。</span><span class="sxs-lookup"><span data-stu-id="efd61-157">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="efd61-158">如需詳細資訊，請參閱 [API 搜尋服務的相關文件](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="efd61-158">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="efd61-159">套件識別碼首碼保留項目爭議原則</span><span class="sxs-lookup"><span data-stu-id="efd61-159">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="efd61-160">如果您認為 [NuGet.org](https://www.nuget.org) 上的擁有者已獲得指派套件識別碼首碼保留項目，而該項目違背了上述所列的準則，或侵害任何商標或著作權，請傳送電子郵件到 [support@nuget.org](mailto:support@nuget.org)，並附上討論中的識別碼首碼、識別碼首碼的擁有者，以及所指派首碼保留項目的爭議理由。</span><span class="sxs-lookup"><span data-stu-id="efd61-160">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>
