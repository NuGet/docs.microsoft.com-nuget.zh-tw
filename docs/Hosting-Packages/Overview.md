---
title: "裝載您自己的 NuGet 摘要概觀 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "在本機或遠端開啟裝載您自己的 NuGet 套件摘要或資源庫的概觀。"
keywords: "NuGet 摘要, NuGet 資源庫, 自訂套件摘要, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="c2bf5-104">裝載您自己的 NuGet 摘要</span><span class="sxs-lookup"><span data-stu-id="c2bf5-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="c2bf5-105">而不是向公眾開放套件，您可能只想向有限的對象發行套件，例如您的組織或工作群組。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="c2bf5-106">此外，有些公司可能想要限制其開發人員可以使用的協力廠商程式庫，因此引導這些開發人員離開有限的套件來源，而不是離開 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="c2bf5-107">針對所有這類用途，NuGet 以下列方式支援設定私用的套件來源：</span><span class="sxs-lookup"><span data-stu-id="c2bf5-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="c2bf5-108">本機摘要：套件只位於適當的網路檔案共用，最好使用 `nuget init` 和 `nuget add`，以建立階層式資料夾結構 (NuGet 3.3+)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="c2bf5-109">如需詳細資料，請參閱[本機摘要](../hosting-packages/local-feeds.md)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="c2bf5-110">NuGet.Server：套件可以透過本機 HTTP 伺服器提供。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="c2bf5-111">如需詳細資料，請參閱 [NuGet.Server](../hosting-packages/nuget-server.md)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="c2bf5-112">NuGet 資源庫：套件裝載在使用 [NuGet 資源庫專案](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps)的網際網路伺服器上 (github.com)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="c2bf5-113">NuGet 資源庫讓使用者能夠管理及使用功能，例如大量 web UI，在瀏覽器中搜尋和瀏覽套件，類似 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="c2bf5-114">另外還有數個 NuGet 裝載產品支援遠端私用摘要，包括：</span><span class="sxs-lookup"><span data-stu-id="c2bf5-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="c2bf5-115">[Visual Studio Team Services 套件管理](https://www.visualstudio.com/docs/package/nuget/publish)，這也可在 Team Foundation Server 2017 及更新版本中取得。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="c2bf5-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="c2bf5-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="c2bf5-117">Inedo 的 [ProGet](http://inedo.com/proget)</span><span class="sxs-lookup"><span data-stu-id="c2bf5-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="c2bf5-118">[NuGet 伺服器](http://nugetserver.net/)，Inedo 社群專案</span><span class="sxs-lookup"><span data-stu-id="c2bf5-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="c2bf5-119">[NuGet 伺服器 (開放原始碼)](http://nuget-server.net)，類似於 Inedo NuGet 伺服器的開放原始碼實作</span><span class="sxs-lookup"><span data-stu-id="c2bf5-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="c2bf5-120">JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="c2bf5-121">Sonatype 的 [Nexus](http://www.sonatype.org/nexus/)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="c2bf5-122">JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="c2bf5-123">不論套件的裝載方式為何，您都要將它們新增至 `NuGet.Config` 的可用來源清單中，才能存取它們。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="c2bf5-124">如[套件來源](../tools/package-manager-ui.md#package-sources)中所述在 Visual Studio 中完成，或從命令列使用 [`nuget sources`](../tools/cli-ref-sources.md) 完成。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="c2bf5-125">來源的路徑可以是本機資料夾的路徑名稱、網路名稱或 URL。</span><span class="sxs-lookup"><span data-stu-id="c2bf5-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
