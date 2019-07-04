---
title: 使用者資料要求
description: 要求使用者資料匯出和刪除的原則
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426983"
---
# <a name="user-data-requests"></a><span data-ttu-id="805ec-103">使用者資料要求</span><span class="sxs-lookup"><span data-stu-id="805ec-103">User Data Requests</span></span>

<span data-ttu-id="805ec-104">nuget.org 使用者可以透過 [nuget.org](https://www.nuget.org) 送出資訊刪除要求和資訊匯出要求。這兩種類型都會以支援要求形式送出，並由 nuget.org 系統管理員在 30 天內執行。</span><span class="sxs-lookup"><span data-stu-id="805ec-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="805ec-105">下列使用者資料可直接透過 nuget.org 存取：</span><span class="sxs-lookup"><span data-stu-id="805ec-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="805ec-106">帳戶相關資料，例如電子郵件地址、登入帳戶、個人資料圖片和電子郵件通知設定</span><span class="sxs-lookup"><span data-stu-id="805ec-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="805ec-107">擁有的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="805ec-107">Owned API Keys</span></span>
* <span data-ttu-id="805ec-108">擁有的套件清單</span><span class="sxs-lookup"><span data-stu-id="805ec-108">List of owned packages</span></span>

<span data-ttu-id="805ec-109">透過支援要求匯出的資料中不包含這項資料。</span><span class="sxs-lookup"><span data-stu-id="805ec-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="805ec-110">識別客戶資料</span><span class="sxs-lookup"><span data-stu-id="805ec-110">Identifying customer data</span></span>

<span data-ttu-id="805ec-111">客戶資料可識別為 nuget.org 使用者帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="805ec-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="805ec-112">刪除客戶資料</span><span class="sxs-lookup"><span data-stu-id="805ec-112">Deleting customer data</span></span>

<span data-ttu-id="805ec-113">若要要求從 nuget.org 刪除使用者資料：</span><span class="sxs-lookup"><span data-stu-id="805ec-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="805ec-114">使用者必須登入 [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="805ec-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="805ec-115">使用者必須送出要刪除其帳戶的要求 [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="805ec-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="805ec-116">建議唯一擁有套件的使用者先尋找新的擁有者，再要求刪除其帳戶。</span><span class="sxs-lookup"><span data-stu-id="805ec-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="805ec-117">如果未轉移套件擁有權，NuGet 套件不會列出，如此一來，就無法再用於 Visual Studio 中或 nuget.org 網站上的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="805ec-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="805ec-118">刪除帳戶之前，nuget.org 系統管理員會與使用者合作，尋找使用者所擁有之套件的新擁有者。</span><span class="sxs-lookup"><span data-stu-id="805ec-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="805ec-119">nuget.org 系統管理員會在要求日期起的 30 天內完成帳戶刪除動作。</span><span class="sxs-lookup"><span data-stu-id="805ec-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="805ec-120">刪除帳戶時，會從 nuget.org 系統移除使用者的所有資料，並執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="805ec-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="805ec-121">與 nuget.org 取消註冊已刪除的帳戶</span><span class="sxs-lookup"><span data-stu-id="805ec-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="805ec-122">刪除所有擁有的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="805ec-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="805ec-123">釋放所有保留的命名空間</span><span class="sxs-lookup"><span data-stu-id="805ec-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="805ec-124">移除任何套件擁有權</span><span class="sxs-lookup"><span data-stu-id="805ec-124">Any package ownership are removed</span></span>

<span data-ttu-id="805ec-125">「不會」  刪除擁有的套件。</span><span class="sxs-lookup"><span data-stu-id="805ec-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="805ec-126">雖然這些套件未列於搜尋結果中，但透過套件還原，還是可供相依於這些套件的專案使用。</span><span class="sxs-lookup"><span data-stu-id="805ec-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="805ec-127">匯出客戶資料</span><span class="sxs-lookup"><span data-stu-id="805ec-127">Exporting customer data</span></span>

<span data-ttu-id="805ec-128">登入 nuget.org 之後，使用者可以透過 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) 送出匯出要求</span><span class="sxs-lookup"><span data-stu-id="805ec-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="805ec-129">使用者可以在 48 小時內透過 Azure Blob 下載匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="805ec-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="805ec-130">48 小時後，存取會過期，而使用者必須視需求送出新的匯出要求。</span><span class="sxs-lookup"><span data-stu-id="805ec-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="805ec-131">匯出的資料包括：</span><span class="sxs-lookup"><span data-stu-id="805ec-131">The exported data includes:</span></span>

* <span data-ttu-id="805ec-132">使用者的支援要求</span><span class="sxs-lookup"><span data-stu-id="805ec-132">The user's support requests</span></span>
* <span data-ttu-id="805ec-133">保存在稽核記錄中的使用者動作 (發佈套件、建立帳戶)</span><span class="sxs-lookup"><span data-stu-id="805ec-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="805ec-134">保存在 IIS 記錄中的任何使用者資訊</span><span class="sxs-lookup"><span data-stu-id="805ec-134">Any user information as persisted in the IIS logs</span></span>
