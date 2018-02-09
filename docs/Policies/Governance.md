---
title: "NuGet 專案治理 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 的治理模型，包含認可者、參與者和使用者的角色和責任。"
keywords: "NuGet 治理、NuGet 仁慈獨裁者、認可者責任、參與者責任、使用者責任"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ea1ddcc3e145afe3b905b23db37e1e61500200bb
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-governance"></a><span data-ttu-id="26b5b-104">NuGet 治理</span><span class="sxs-lookup"><span data-stu-id="26b5b-104">NuGet governance</span></span>

> <span data-ttu-id="26b5b-105">本文件是以牛津大學的 [Benevolent Dictator Governance Model](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) (仁慈獨裁者治理模型) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="26b5b-105">This document is based upon the [Benevolent Dictator Governance Model](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) by the University of Oxford.</span></span> <span data-ttu-id="26b5b-106">它是透過 [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/) 所授權。</span><span class="sxs-lookup"><span data-stu-id="26b5b-106">It is licensed under a [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).</span></span>

<span data-ttu-id="26b5b-107">NuGet 專案是由仁慈獨裁者所帶領，並且由社群進行管理。</span><span class="sxs-lookup"><span data-stu-id="26b5b-107">The NuGet project is led by a Benevolent Dictator and managed by the community.</span></span> <span data-ttu-id="26b5b-108">也就是說，社群主動參與專案的日常維護，但是由仁慈獨裁者策畫一般策略線。</span><span class="sxs-lookup"><span data-stu-id="26b5b-108">That is, the community actively contributes to the day-to-day maintenance of the project, but the general strategic line is drawn by the benevolent dictator.</span></span> <span data-ttu-id="26b5b-109">如果不一致，則由仁慈獨裁者決定。</span><span class="sxs-lookup"><span data-stu-id="26b5b-109">In case of disagreement, the benevolent dictator has the last word.</span></span>

<span data-ttu-id="26b5b-110">仁慈獨裁者負責解決社群內的爭議，以及確保可以透過協作方式執行專案。</span><span class="sxs-lookup"><span data-stu-id="26b5b-110">It is the benevolent dictator’s job to resolve disputes within the community and to ensure that the project is able to progress in a coordinated way.</span></span> <span data-ttu-id="26b5b-111">而社群則負責透過主動參與和貢獻引導仁慈獨裁者進行決策。</span><span class="sxs-lookup"><span data-stu-id="26b5b-111">In turn, it's the community’s job to guide the decisions of the benevolent dictator through active engagement and contribution.</span></span>

## <a name="roles-and-responsibilities"></a><span data-ttu-id="26b5b-112">角色和責任</span><span class="sxs-lookup"><span data-stu-id="26b5b-112">Roles and responsibilities</span></span>

<span data-ttu-id="26b5b-113">這裡描述四種角色：仁慈獨裁者、認可者、參與者和使用者。</span><span class="sxs-lookup"><span data-stu-id="26b5b-113">There are four roles described here: Benevolent Dictator, Committers, Contributors, and Users.</span></span>

### <a name="benevolent-dictator"></a><span data-ttu-id="26b5b-114">仁慈獨裁者</span><span class="sxs-lookup"><span data-stu-id="26b5b-114">Benevolent dictator</span></span>

<span data-ttu-id="26b5b-115">NuGet 核心小組會自行指派為仁慈獨裁者或專案負責人。</span><span class="sxs-lookup"><span data-stu-id="26b5b-115">The NuGet core team is self-appointed as Benevolent Dictator or project lead.</span></span> <span data-ttu-id="26b5b-116">不過，因為社群一律可以進行分叉，所以小組可以對社群完全負責。</span><span class="sxs-lookup"><span data-stu-id="26b5b-116">However, because the community always has the ability to fork, the team is fully answerable to the community.</span></span> <span data-ttu-id="26b5b-117">專案負責人必須了解整體社群，並致力於盡可能滿足許多衝突需求，同時確保專案長期存活。</span><span class="sxs-lookup"><span data-stu-id="26b5b-117">The project lead is expected to understand the community as a whole and strive to satisfy as many conflicting needs as possible, while ensuring that the project survives in the long term.</span></span>

<span data-ttu-id="26b5b-118">在許多方面，仁慈獨裁者角色的獨裁性較少，圓滑性較高。</span><span class="sxs-lookup"><span data-stu-id="26b5b-118">In many ways, the role of the benevolent dictator is less about dictatorship and more about diplomacy.</span></span> <span data-ttu-id="26b5b-119">主要是確保專案擴充時，正確人員可對其造成影響，而且社群是依專案負責人的觀點重整。</span><span class="sxs-lookup"><span data-stu-id="26b5b-119">The key is to ensure that, as the project expands, the right people are given influence over it and the community rallies behind the vision of the project lead.</span></span> <span data-ttu-id="26b5b-120">負責人接著負責確保認可者 (請參閱下面) 代表專案做出正確決策。</span><span class="sxs-lookup"><span data-stu-id="26b5b-120">The lead’s job is then to ensure that the committers (see below) make the right decisions on behalf of the project.</span></span> <span data-ttu-id="26b5b-121">一般而言，只要認可者遵循專案策略，專案負責人就允許他們依需要進行。</span><span class="sxs-lookup"><span data-stu-id="26b5b-121">Generally speaking, as long as the committers are aligned with the project’s strategy, the project lead will allow them to proceed as they desire.</span></span>

<span data-ttu-id="26b5b-122">此外，基於商務作業用途，.NET Foundation 人員也會將專案負責人視為 NuGet 的主要或第一個連絡點，包含網域註冊和技術服務 (例如程式碼簽署)。</span><span class="sxs-lookup"><span data-stu-id="26b5b-122">Additionally, .NET Foundation staff consider the project lead the primary or first point of contact for NuGet for purposes of business operations including domain registrations, and technical services (e.g. code-signing).</span></span>

### <a name="committers"></a><span data-ttu-id="26b5b-123">認可者</span><span class="sxs-lookup"><span data-stu-id="26b5b-123">Committers</span></span>

<span data-ttu-id="26b5b-124">認可者是對 NuGet 有持續重要貢獻且由仁慈獨裁者指派的參與者。</span><span class="sxs-lookup"><span data-stu-id="26b5b-124">Committers are contributors who have made sustained valuable contributions to NuGet and are appointed by the Benevolent Dictator.</span></span> <span data-ttu-id="26b5b-125">認可者在指派之後會依賴將程式碼直接寫入存放庫，並篩選其他人的貢獻。</span><span class="sxs-lookup"><span data-stu-id="26b5b-125">One appointed, committers are relied upon to both write code directly to the repository and screen the contributions of others.</span></span> <span data-ttu-id="26b5b-126">認可者通常是開發人員，但可以透過其他方式參與。</span><span class="sxs-lookup"><span data-stu-id="26b5b-126">Committers are often developers but can contribute in other ways.</span></span>

<span data-ttu-id="26b5b-127">一般而言，認可者著重於專案的特定層面，並具有某程度的專業和了解，讓他們贏得社群和專案負責人的尊重。</span><span class="sxs-lookup"><span data-stu-id="26b5b-127">Typically, a committer focuses on a specific aspect of the project, and brings a level of expertise and understanding that earns them the respect of the community and the project lead.</span></span> <span data-ttu-id="26b5b-128">認可者角色不是正式角色，而只是具影響力的社群成員所擔任的身分，因為專案負責人會向其尋求指引和支援。</span><span class="sxs-lookup"><span data-stu-id="26b5b-128">The role of committer is not an official one, it's simply a position that influential members of the community assume as the project lead looks to them for guidance and support.</span></span>

<span data-ttu-id="26b5b-129">認可者沒有關注整體 NuGet 方向的授權。</span><span class="sxs-lookup"><span data-stu-id="26b5b-129">Committers have no authority where the overall direction of NuGet is concerned.</span></span> <span data-ttu-id="26b5b-130">不過，專案負責人會聽取他們的意見。</span><span class="sxs-lookup"><span data-stu-id="26b5b-130">However, they do have the ear of the project lead.</span></span> <span data-ttu-id="26b5b-131">認可者負責確保負責人了解社群的需求和共同目標，並協助開發或引出對專案的適當貢獻。</span><span class="sxs-lookup"><span data-stu-id="26b5b-131">It is a committer’s job to ensure that the lead is aware of the community’s needs and collective objectives, and to help develop or elicit appropriate contributions to the project.</span></span> <span data-ttu-id="26b5b-132">通常，認可者可非正式控制他們負責的特定領域，並且獲指派直接修改原始程式碼特定領域的權限。</span><span class="sxs-lookup"><span data-stu-id="26b5b-132">Often, committers are given informal control over their specific areas of responsibility, and are assigned rights to directly modify certain areas of the source code.</span></span> <span data-ttu-id="26b5b-133">也就是說，雖然認可者沒有明確決策授權，但是他們通常會發現其動作與負責人的決策類似。</span><span class="sxs-lookup"><span data-stu-id="26b5b-133">That is, although committers do not have explicit decision-making authority, they will often find that their actions are synonymous with the decisions made by the lead.</span></span>

### <a name="contributors"></a><span data-ttu-id="26b5b-134">Contributors</span><span class="sxs-lookup"><span data-stu-id="26b5b-134">Contributors</span></span>

<span data-ttu-id="26b5b-135">參與者是將修補程式提交給 NuGet 的社群成員。</span><span class="sxs-lookup"><span data-stu-id="26b5b-135">Contributors are community members who submit patches to NuGet.</span></span> <span data-ttu-id="26b5b-136">這些修補檔案可能只發生一次或一段時間。</span><span class="sxs-lookup"><span data-stu-id="26b5b-136">These patches may be a one-time occurrence or occur over time.</span></span> <span data-ttu-id="26b5b-137">參與者、認可者和專案負責人確信參與者的修補程式品質時，參與者預期會提交一開始很小但逐漸變大的修補程式。</span><span class="sxs-lookup"><span data-stu-id="26b5b-137">Expectations are that contributors submit patches that are small at first and grow larger when the contributor, committers, and the project lead have built confidence in the quality of a contributor's patches.</span></span> <span data-ttu-id="26b5b-138">在相關聯的產品版本資訊文件中可以辨識參與者。</span><span class="sxs-lookup"><span data-stu-id="26b5b-138">Contributors are recognized in the associated product release notes document.</span></span>

<span data-ttu-id="26b5b-139">參與者必須簽署[參與者授權合約](http://en.wikipedia.org/wiki/Contributor_License_Agreement)或 .NET Foundation 的指派合約，才會將他們的第一個修補程式放入存放庫中。</span><span class="sxs-lookup"><span data-stu-id="26b5b-139">Before a contributor’s first patch is put into the repository, they must sign a [Contributor License Agreement](http://en.wikipedia.org/wiki/Contributor_License_Agreement) or an assignment agreement to the .NET Foundation.</span></span> <span data-ttu-id="26b5b-140">修補程式可以進行提交和討論，但它實際上需要有適當的書面文件才能認可到存放庫。</span><span class="sxs-lookup"><span data-stu-id="26b5b-140">The patch can be submitted and discussed but it can’t actually be committed to the repository without the appropriate paperwork in place.</span></span> <span data-ttu-id="26b5b-141">若要取得參與者授權合約，請透過電子郵件將要求傳送至 [contributions@nuget.org](mailto:contributions@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="26b5b-141">To obtain a contributor license agreement, please send a request in email to [contributions@nuget.org](mailto:contributions@nuget.org).</span></span>

<span data-ttu-id="26b5b-142">若要成為參與者，請將提取要求提交至下列其中一個存放庫：</span><span class="sxs-lookup"><span data-stu-id="26b5b-142">To become a contributor, submit a pull request to one of the following repositories:</span></span>

- [<span data-ttu-id="26b5b-143">NuGet 用戶端</span><span class="sxs-lookup"><span data-stu-id="26b5b-143">NuGet Client</span></span>](https://github.com/NuGet/NuGet.Client)
- [<span data-ttu-id="26b5b-144">NuGet 資源庫</span><span class="sxs-lookup"><span data-stu-id="26b5b-144">NuGet Gallery</span></span>](https://github.com/nuget/nugetgallery)
- [<span data-ttu-id="26b5b-145">NuGet 文件</span><span class="sxs-lookup"><span data-stu-id="26b5b-145">NuGet Docs</span></span>](https://github.com/nuget/nugetdocs)

<span data-ttu-id="26b5b-146">用於提交提取要求的詳細程序會因存放庫而不同：</span><span class="sxs-lookup"><span data-stu-id="26b5b-146">The detailed process for submitting a pull request varies by repository:</span></span>

- [<span data-ttu-id="26b5b-147">NuGet 用戶端和 NuGet 資源庫的參與指示</span><span class="sxs-lookup"><span data-stu-id="26b5b-147">Contribution instructions for NuGet Client and NuGet Gallery</span></span>](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [<span data-ttu-id="26b5b-148">NuGet 文件的參與指示</span><span class="sxs-lookup"><span data-stu-id="26b5b-148">Contribution instructions for NuGet Docs</span></span>](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a><span data-ttu-id="26b5b-149">使用者</span><span class="sxs-lookup"><span data-stu-id="26b5b-149">Users</span></span>

<span data-ttu-id="26b5b-150">使用者是需要並使用 NuGet 作為套件取用者和 (或) 作者的社群成員。</span><span class="sxs-lookup"><span data-stu-id="26b5b-150">Users are community members who have a need for and use NuGet, as package consumers and/or authors.</span></span> <span data-ttu-id="26b5b-151">使用者是最重要的社群成員：沒有他們，專案就沒有任何用途。</span><span class="sxs-lookup"><span data-stu-id="26b5b-151">Users are the most important members of the community: without them, the project would have no purpose.</span></span> <span data-ttu-id="26b5b-152">任何人都可以是使用者；沒有特定需求。</span><span class="sxs-lookup"><span data-stu-id="26b5b-152">Anyone can be a user; there are no specific requirements.</span></span>

<span data-ttu-id="26b5b-153">應該鼓勵使用者盡可能參與 NuGet 和社群的生命週期。</span><span class="sxs-lookup"><span data-stu-id="26b5b-153">Users should be encouraged to participate in the life of NuGet and the community as much as possible.</span></span> <span data-ttu-id="26b5b-154">使用者參與可讓專案小組確保它們滿足這些使用者的需求。</span><span class="sxs-lookup"><span data-stu-id="26b5b-154">User contributions enable the project team to ensure that they are satisfying the needs of those users.</span></span> <span data-ttu-id="26b5b-155">常見使用者活動包含 (但不限於) 下列活動：</span><span class="sxs-lookup"><span data-stu-id="26b5b-155">Common user activities include but are not limited to the following:</span></span>

- <span data-ttu-id="26b5b-156">支援使用專案</span><span class="sxs-lookup"><span data-stu-id="26b5b-156">Advocating for use of the project</span></span>
- <span data-ttu-id="26b5b-157">通知開發人員從新使用者觀點的專案優點和缺點</span><span class="sxs-lookup"><span data-stu-id="26b5b-157">Informing developers of project strengths and weaknesses from a new user’s perspective</span></span>
- <span data-ttu-id="26b5b-158">提供士氣支援 (感謝您一路陪伴)</span><span class="sxs-lookup"><span data-stu-id="26b5b-158">Providing moral support (a thank you goes a long way)</span></span>
- <span data-ttu-id="26b5b-159">撰寫文件和教學課程</span><span class="sxs-lookup"><span data-stu-id="26b5b-159">Writing documentation and tutorials</span></span>
- <span data-ttu-id="26b5b-160">提出 Bug 報表和功能要求</span><span class="sxs-lookup"><span data-stu-id="26b5b-160">Filing bug reports and feature requests</span></span>
- <span data-ttu-id="26b5b-161">參與社群事件 (例如群眾挑錯)</span><span class="sxs-lookup"><span data-stu-id="26b5b-161">Participating in community events, such as bug bashes</span></span>
- <span data-ttu-id="26b5b-162">參與討論板或論壇</span><span class="sxs-lookup"><span data-stu-id="26b5b-162">Participating on discussion boards or forums</span></span>

<span data-ttu-id="26b5b-163">持續參與專案和其社群的使用者通常會發現自己涉入地越來越多。</span><span class="sxs-lookup"><span data-stu-id="26b5b-163">Users who continue to engage with the project and its community will often find themselves becoming more and more involved.</span></span> <span data-ttu-id="26b5b-164">這類使用者接著可能會變成參與者，如上所述。</span><span class="sxs-lookup"><span data-stu-id="26b5b-164">Such users may then go on to become contributors, as described above.</span></span>

## <a name="package-succession-under-special-circumstances"></a><span data-ttu-id="26b5b-165">特殊情況下的套件接續</span><span class="sxs-lookup"><span data-stu-id="26b5b-165">Package succession under special circumstances</span></span>

<span data-ttu-id="26b5b-166">在 NuGet 帳戶持有者無行為能力或死亡的不幸情況下，我們會與社群合作，以將適當的擁有者新增至所指出帳戶具有唯一擁有權的套件，並透過 [OSI 核准的授權](https://opensource.org/licenses/alphabetical)發行套件。</span><span class="sxs-lookup"><span data-stu-id="26b5b-166">In the unfortunate situation where a NuGet account holder is incapacitated or deceased, we’ll work with the community to add appropriate owner/s to the package where the said account has sole ownership and the package is published under an [OSI approved license](https://opensource.org/licenses/alphabetical).</span></span> <span data-ttu-id="26b5b-167">若要要求擁有權，您必須將下列文件傳送給我們：</span><span class="sxs-lookup"><span data-stu-id="26b5b-167">To request ownership you must send us the following documents:</span></span>

1. <span data-ttu-id="26b5b-168">您政府核發的相片識別碼影本。</span><span class="sxs-lookup"><span data-stu-id="26b5b-168">A photocopy of your government-issued photo ID.</span></span>
1. <span data-ttu-id="26b5b-169">下列其中一份文件證明先前帳戶持有者的狀態：</span><span class="sxs-lookup"><span data-stu-id="26b5b-169">One of the following documents proving the previous account holder’s status:</span></span> 
    - <span data-ttu-id="26b5b-170">政府在先前帳戶持有人死亡時發出的正式死亡憑證，或者</span><span class="sxs-lookup"><span data-stu-id="26b5b-170">An official, government-issued death certificate if the previous account holder is deceased, or,</span></span>
    - <span data-ttu-id="26b5b-171">認證的文件，例如負責照護無行為能力之帳戶持有者的醫療專業人員所簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="26b5b-171">A certified document such as a certificate signed by a medical professional in charge of the care of an incapacitated account holder.</span></span>
1. <span data-ttu-id="26b5b-172">證明您擁有權權限的下列其中一份文件：</span><span class="sxs-lookup"><span data-stu-id="26b5b-172">One of the following documents proving your right to ownership:</span></span> 
    - <span data-ttu-id="26b5b-173">顯示您是帳戶持有者之存活配偶的結婚證書、</span><span class="sxs-lookup"><span data-stu-id="26b5b-173">Marriage certificate showing that you are the surviving spouse of the account holder,</span></span>
    - <span data-ttu-id="26b5b-174">簽署的委託書、</span><span class="sxs-lookup"><span data-stu-id="26b5b-174">Signed power of attorney,</span></span>
    - <span data-ttu-id="26b5b-175">將您命名為遺囑執行人或受益人的意向或信任文件複本、</span><span class="sxs-lookup"><span data-stu-id="26b5b-175">Copy of a will or trust document naming you as executor or beneficiary,</span></span>
    - <span data-ttu-id="26b5b-176">帳戶持有者的出生證明 (如果您是其父母)，或者</span><span class="sxs-lookup"><span data-stu-id="26b5b-176">Birth certificate for the account holder, if you are their parent, or,</span></span>
    - <span data-ttu-id="26b5b-177">監護權書面作業 (如果您是帳戶持有者的合法監護人)。</span><span class="sxs-lookup"><span data-stu-id="26b5b-177">Guardianship paperwork if you are a legal guardian of the account holder.</span></span>

<span data-ttu-id="26b5b-178">如果您發現自己確實需要叫用此原則，請使用套件的識別碼和版本，傳送電子郵件至下列地址：[support@nuget.org](mailto:support@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="26b5b-178">If you find yourself in need of invoking this policy, please send us an email at [support@nuget.org](mailto:support@nuget.org) with the ID and version of the package.</span></span>

## <a name="transparency"></a><span data-ttu-id="26b5b-179">透明度</span><span class="sxs-lookup"><span data-stu-id="26b5b-179">Transparency</span></span>

<span data-ttu-id="26b5b-180">建置透過開放原始碼專案治理的社群信任對於成功而言十分重要。</span><span class="sxs-lookup"><span data-stu-id="26b5b-180">Building community trust in the governance of an open-source project is vital to its success.</span></span> <span data-ttu-id="26b5b-181">為了這個目的，必須以透明且開放的方式進行決策。</span><span class="sxs-lookup"><span data-stu-id="26b5b-181">To that end, decision making must be done in a transparent, open fashion.</span></span> <span data-ttu-id="26b5b-182">專案方向的討論必須公開進行。</span><span class="sxs-lookup"><span data-stu-id="26b5b-182">Discussion about the project’s direction must be done publicly.</span></span> <span data-ttu-id="26b5b-183">社群絕對不應該提防仁慈獨裁者做出的決策。</span><span class="sxs-lookup"><span data-stu-id="26b5b-183">The community should never be caught off-guard by a decision by the Benevolent Dictator.</span></span> <span data-ttu-id="26b5b-184">此外，必須封存專案決策的討論，讓社群成員可以了解決策和其內容的整個歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="26b5b-184">Additionally, discussion about project decisions must be archived so that community members can understand the entire history of a decision and its context.</span></span>
