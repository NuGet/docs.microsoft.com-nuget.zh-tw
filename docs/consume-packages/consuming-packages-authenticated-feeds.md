---
title: 從經過驗證的摘要使用套件
description: 在所有 NuGet 用戶端案例中使用來自已驗證摘要的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901508"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="59dc1-103">從經過驗證的摘要使用套件</span><span class="sxs-lookup"><span data-stu-id="59dc1-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="59dc1-104">除了 nuget.org [公用](https://api.nuget.org/v3/index.json)摘要，nuget 用戶端還能夠與檔案摘要和私用 HTTP 摘要互動。</span><span class="sxs-lookup"><span data-stu-id="59dc1-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="59dc1-105">若要使用私用 HTTP 摘要進行驗證，2種方法如下：</span><span class="sxs-lookup"><span data-stu-id="59dc1-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="59dc1-106">在[NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)中新增認證</span><span class="sxs-lookup"><span data-stu-id="59dc1-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="59dc1-107">視使用的用戶端而定，使用許多擴充性模型的其中一種進行驗證。</span><span class="sxs-lookup"><span data-stu-id="59dc1-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="59dc1-108">NuGet 用戶端的驗證擴充性</span><span class="sxs-lookup"><span data-stu-id="59dc1-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="59dc1-109">針對不同的 NuGet 用戶端，私用摘要提供者本身會負責驗證。</span><span class="sxs-lookup"><span data-stu-id="59dc1-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="59dc1-110">所有 NuGet 用戶端都具有可支援此功能的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="59dc1-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="59dc1-111">這些是 Visual Studio 擴充功能或可與 NuGet 通訊以取得認證的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="59dc1-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="59dc1-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59dc1-112">Visual Studio</span></span>

<span data-ttu-id="59dc1-113">在 Visual Studio 中，NuGet 會公開一個介面，讓摘要提供者可以執行並提供給客戶。</span><span class="sxs-lookup"><span data-stu-id="59dc1-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="59dc1-114">如需詳細資訊，請參閱有關 [如何建立 Visual Studio 認證提供者](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的檔。</span><span class="sxs-lookup"><span data-stu-id="59dc1-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="59dc1-115">Visual Studio 的可用 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="59dc1-116">Visual Studio 內建的認證提供者可支援 Azure DevOps。</span><span class="sxs-lookup"><span data-stu-id="59dc1-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="59dc1-117">可用的外掛程式認證提供者包括：</span><span class="sxs-lookup"><span data-stu-id="59dc1-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="59dc1-118">適用于 Visual Studio 的 MyGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="59dc1-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="59dc1-119">nuget.exe</span></span>

<span data-ttu-id="59dc1-120">`nuget.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="59dc1-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="59dc1-121">尋找檔案中的認證 `NuGet.config` 。</span><span class="sxs-lookup"><span data-stu-id="59dc1-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="59dc1-122">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="59dc1-123">使用 V1 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="59dc1-124">接著，NuGet 會在命令列提示使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="59dc1-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="59dc1-125">nuget.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="59dc1-126">在 NuGet 版中 `4.8` ，定義了新的驗證外掛程式機制，此處稱為 V2 認證提供者。</span><span class="sxs-lookup"><span data-stu-id="59dc1-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="59dc1-127">若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="59dc1-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="59dc1-128">nuget.exe 和 V1 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="59dc1-129">在 NuGet 版中 `3.3` 引進了第一版的驗證外掛程式。</span><span class="sxs-lookup"><span data-stu-id="59dc1-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="59dc1-130">若要安裝和探索這些提供者，請參閱 [nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="59dc1-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="59dc1-131">nuget.exe 可用的認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="59dc1-132">[Azure DevOps V2 認證提供者](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) 或 [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="59dc1-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="59dc1-133">在 Visual Studio 2017 15.9 版和更新版本中，Azure DevOps 認證提供者會隨附于 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="59dc1-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="59dc1-134">如果 `nuget.exe` 從該特定的 Visual Studio 工具組使用 MSBuild，則會自動探索該外掛程式。</span><span class="sxs-lookup"><span data-stu-id="59dc1-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="59dc1-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="59dc1-135">dotnet.exe</span></span>

<span data-ttu-id="59dc1-136">`dotnet.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="59dc1-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="59dc1-137">尋找檔案中的認證 `NuGet.config` 。</span><span class="sxs-lookup"><span data-stu-id="59dc1-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="59dc1-138">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="59dc1-139">根據預設 `dotnet.exe` ，您可能需要傳遞旗標， `--interactive` 才能讓工具封鎖以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="59dc1-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="59dc1-140">dotnet.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="59dc1-141">在 SDK 版本中 `2.2.100` ，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="59dc1-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="59dc1-142">若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="59dc1-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="59dc1-143">dotnet.exe 可用的認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="59dc1-144">Azure Artifacts 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="59dc1-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="59dc1-145">MSBuild.exe</span></span>

<span data-ttu-id="59dc1-146">`MSBuild.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="59dc1-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="59dc1-147">在檔案中尋找認證 `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="59dc1-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="59dc1-148">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="59dc1-149">依預設 `MSBuild.exe` 不是互動式的，因此您可能需要設定 `/p:NuGetInteractive=true` 屬性，以取得封鎖驗證的工具。</span><span class="sxs-lookup"><span data-stu-id="59dc1-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="59dc1-150">MSBuild.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="59dc1-151">在 Visual Studio 2019 Update 9 中，NuGet 定義了可在所有用戶端中運作的驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="59dc1-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="59dc1-152">若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="59dc1-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="59dc1-153">MSBuild.exe 可用的認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="59dc1-154">Azure Artifacts 認證提供者</span><span class="sxs-lookup"><span data-stu-id="59dc1-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="59dc1-155">在 Visual Studio 2017 Update 9 和更新版本中，Azure DevOps 認證提供者會隨附于 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="59dc1-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="59dc1-156">不需要任何額外步驟。</span><span class="sxs-lookup"><span data-stu-id="59dc1-156">No additional steps are required.</span></span>
