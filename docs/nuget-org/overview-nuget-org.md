---
title: NuGet.org 概觀
description: NuGet.org 概觀
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427013"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="c084b-103">NuGet.org 概觀</span><span class="sxs-lookup"><span data-stu-id="c084b-103">Overview of NuGet.org</span></span>

<span data-ttu-id="c084b-104">NuGet.org 是 NuGet 套件的公用主機，每天都有數百萬的 .NET 和 .NET Core 開發人員採用 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c084b-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="c084b-105">NuGet.org 在 NuGet 生態系統中的角色</span><span class="sxs-lookup"><span data-stu-id="c084b-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="c084b-106">作為公共主機,NuGet.org本身在[nuget.org](https://www.nuget.org)維護超過 100,000 個唯一包的中央存儲庫。NuGet.org不是包的唯一可能的主機。</span><span class="sxs-lookup"><span data-stu-id="c084b-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="c084b-107">NuGet 技術也讓您能夠在雲端 (例如在 Azure DevOps 上)、私人網路或甚至只是在本機檔案系統中，私下裝載套件。</span><span class="sxs-lookup"><span data-stu-id="c084b-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="c084b-108">如果您對於不同的主機或裝載選項有興趣，請參閱[裝載您自己的 NuGet 摘要](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c084b-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="c084b-109">NuGet.org 如同 NuGet 套件的任何主機，都是作為套件「建立者」\*\* 與套件「取用者」\*\* 之間的聯繫點。</span><span class="sxs-lookup"><span data-stu-id="c084b-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="c084b-110">建立者會建置有用的 NuGet 套件，並加以發佈。</span><span class="sxs-lookup"><span data-stu-id="c084b-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="c084b-111">取用者接著會搜尋可存取主機上的實用和相容套件，並下載這些套件且將其包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="c084b-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="c084b-112">一旦安裝於專案，套件的 API 就可供專案程式碼的其餘部分使用。</span><span class="sxs-lookup"><span data-stu-id="c084b-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![套件建立者、套件主機與套件取用者之間的關聯性](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="c084b-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="c084b-114">Accounts</span></span>

<span data-ttu-id="c084b-115">若要在 NuGet.org 上發佈套件，請先建立[個人 (使用者) 帳戶](individual-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="c084b-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="c084b-116">這會成為您在 NuGet.org 上的身分識別。</span><span class="sxs-lookup"><span data-stu-id="c084b-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="c084b-117">NuGet.org 也可讓您建立[組織帳戶](organizations-on-nuget-org.md)。</span><span class="sxs-lookup"><span data-stu-id="c084b-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="c084b-118">組織帳戶有一或多個作為其成員的個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="c084b-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="c084b-119">成員可以管理一組套件，同時維持擁有權的單一身分識別。</span><span class="sxs-lookup"><span data-stu-id="c084b-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="c084b-120">透過您的個人帳戶，您可以是任意數目組織的成員。</span><span class="sxs-lookup"><span data-stu-id="c084b-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="c084b-121">套件可以屬於組織帳戶，就像可以屬於個人帳戶一樣。</span><span class="sxs-lookup"><span data-stu-id="c084b-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="c084b-122">套件取用者看不到個別帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。</span><span class="sxs-lookup"><span data-stu-id="c084b-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="c084b-123">API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c084b-123">API keys</span></span>

<span data-ttu-id="c084b-124">一旦擁有要發佈的 NuGet 套件 (*.nupkg*) 時，您會使用 nuget.exe CLI 或 donet.exe CLI 以及從 NuGet.org 取得的 [API 金鑰](scoped-api-keys.md)，將它發佈到 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="c084b-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="c084b-125">當您[發佈套件](../create-packages/creating-a-package.md)時，請在 CLI 命令中包含 API 金鑰值。</span><span class="sxs-lookup"><span data-stu-id="c084b-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="c084b-126">識別碼首碼</span><span class="sxs-lookup"><span data-stu-id="c084b-126">ID prefixes</span></span>

<span data-ttu-id="c084b-127">當您發佈套件時，可以[保留識別碼首碼](id-prefix-reservation.md) 以保留並保護您的身分識別。</span><span class="sxs-lookup"><span data-stu-id="c084b-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="c084b-128">套件取用者安裝套件時會提供其額外的資訊，指出他們取用的套件在其識別屬性中沒有欺騙成分。</span><span class="sxs-lookup"><span data-stu-id="c084b-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="c084b-129">NuGet.org 的 API 端點</span><span class="sxs-lookup"><span data-stu-id="c084b-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="c084b-130">若要以 NuGet 用戶端來將 NuGet.org 作為套件存放庫使用，您應使用下列 V3 API 端點：</span><span class="sxs-lookup"><span data-stu-id="c084b-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="c084b-131">較舊的用戶端仍可以使用 V2 協定來達到 NuGet.org。但是,請注意,NuGet 用戶端 3.0 或更高版本將使用 V2 協定提供較慢且不太可靠的服務:</span><span class="sxs-lookup"><span data-stu-id="c084b-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="c084b-132">`https://www.nuget.org/api/v2` (**V2 通訊協定已淘汰！**)</span><span class="sxs-lookup"><span data-stu-id="c084b-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
