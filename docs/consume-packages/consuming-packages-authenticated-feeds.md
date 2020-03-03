---
title: 使用已驗證摘要中的套件
description: 在所有 NuGet 用戶端案例中使用來自已驗證摘要的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231788"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="20cc9-103">使用已驗證摘要中的套件</span><span class="sxs-lookup"><span data-stu-id="20cc9-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="20cc9-104">除了 nuget.org[公用](https://api.nuget.org/v3/index.json)摘要以外，nuget 用戶端也能夠與檔案摘要和私人 HTTP 摘要互動。</span><span class="sxs-lookup"><span data-stu-id="20cc9-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="20cc9-105">若要使用私用 HTTP 摘要進行驗證，這2種方法是：</span><span class="sxs-lookup"><span data-stu-id="20cc9-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="20cc9-106">在[nuget.exe](../reference/nuget-config-file.md#packagesourcecredentials)中新增認證</span><span class="sxs-lookup"><span data-stu-id="20cc9-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="20cc9-107">根據使用的用戶端，使用許多擴充性模型其中之一進行驗證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="20cc9-108">NuGet 用戶端的驗證擴充性</span><span class="sxs-lookup"><span data-stu-id="20cc9-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="20cc9-109">針對各種 NuGet 用戶端，私用摘要提供者本身會負責驗證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="20cc9-110">所有 NuGet 用戶端都具有可支援此功能的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="20cc9-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="20cc9-111">這些是可以與 NuGet 通訊以取得認證的 Visual Studio 擴充功能或外掛程式。</span><span class="sxs-lookup"><span data-stu-id="20cc9-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="20cc9-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="20cc9-112">Visual Studio</span></span>

<span data-ttu-id="20cc9-113">在 Visual Studio 中，NuGet 會公開摘要提供者可以執行並提供給其客戶的介面。</span><span class="sxs-lookup"><span data-stu-id="20cc9-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="20cc9-114">如需詳細資訊，請參閱[如何建立 Visual Studio 認證提供者](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的檔。</span><span class="sxs-lookup"><span data-stu-id="20cc9-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="20cc9-115">Visual Studio 可用的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="20cc9-116">支援 Azure DevOps 的 Visual Studio 內建認證提供者。</span><span class="sxs-lookup"><span data-stu-id="20cc9-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="20cc9-117">可用的外掛程式認證提供者包括：</span><span class="sxs-lookup"><span data-stu-id="20cc9-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="20cc9-118">Visual Studio 的 MyGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="20cc9-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="20cc9-119">nuget.exe</span></span>

<span data-ttu-id="20cc9-120">當 `nuget.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="20cc9-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="20cc9-121">尋找 `NuGet.config` 檔案中的認證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="20cc9-122">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="20cc9-123">使用 V1 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="20cc9-124">然後，NuGet 會在命令列上提示使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="20cc9-125">nuget.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="20cc9-126">在版本中，`4.8` NuGet 定義了新的驗證外掛程式機制，而這裡則稱為 V2 認證提供者。</span><span class="sxs-lookup"><span data-stu-id="20cc9-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="20cc9-127">如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="20cc9-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="20cc9-128">nuget.exe 和 V1 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="20cc9-129">在版本中 `3.3` NuGet 引進了第一版的驗證外掛程式。</span><span class="sxs-lookup"><span data-stu-id="20cc9-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="20cc9-130">如需瞭解這些提供者的安裝和探索，請參閱[nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="20cc9-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="20cc9-131">適用于 nuget.exe 的認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="20cc9-132">[Azure DevOps V2 認證提供](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later)者或[Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="20cc9-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="20cc9-133">在 Visual Studio 2017 15.9 版和更新版本中，Azure DevOps 認證提供者已配套 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="20cc9-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="20cc9-134">如果 `nuget.exe` 使用該特定 Visual Studio 工具組中的 MSBuild，則會自動探索外掛程式。</span><span class="sxs-lookup"><span data-stu-id="20cc9-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="20cc9-135">dotnet .exe</span><span class="sxs-lookup"><span data-stu-id="20cc9-135">dotnet.exe</span></span>

<span data-ttu-id="20cc9-136">當 `dotnet.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="20cc9-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="20cc9-137">尋找 `NuGet.config` 檔案中的認證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="20cc9-138">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="20cc9-139">根據預設 `dotnet.exe` 不是互動式的，因此您可能需要傳遞 `--interactive` 旗標，才能讓工具封鎖以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="20cc9-140">dotnet .exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="20cc9-141">在 SDK 的版本 `2.2.100` 中，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="20cc9-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="20cc9-142">如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="20cc9-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="20cc9-143">Dotnet 可用的認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="20cc9-144">Azure Artifacts 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="20cc9-145">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="20cc9-145">MSBuild.exe</span></span>

<span data-ttu-id="20cc9-146">當 `MSBuild.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：</span><span class="sxs-lookup"><span data-stu-id="20cc9-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="20cc9-147">在 `NuGet.config` 檔案中尋找認證</span><span class="sxs-lookup"><span data-stu-id="20cc9-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="20cc9-148">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="20cc9-149">根據預設 `MSBuild.exe` 不是互動式的，因此您可能需要設定 `/p:NuGetInteractive=true` 屬性，才能讓工具封鎖以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="20cc9-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="20cc9-150">Msbuild.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="20cc9-151">在 Visual Studio 2019 Update 9 中，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="20cc9-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="20cc9-152">如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="20cc9-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="20cc9-153">Msbuild.exe 可用的認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="20cc9-154">Azure Artifacts 認證提供者</span><span class="sxs-lookup"><span data-stu-id="20cc9-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="20cc9-155">在 Visual Studio 2017 Update 9 和更新版本中，Azure DevOps 認證提供者會與 Visual Studio 配套。</span><span class="sxs-lookup"><span data-stu-id="20cc9-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="20cc9-156">不需要其他步驟。</span><span class="sxs-lookup"><span data-stu-id="20cc9-156">No additional steps are required.</span></span>
