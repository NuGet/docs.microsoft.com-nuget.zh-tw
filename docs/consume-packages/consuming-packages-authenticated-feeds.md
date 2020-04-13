---
title: 使用來自經過身份驗證的來源的套件
description: 在所有 NuGet 用戶端機制中使用來自經過身份驗證的來源的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231788"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="49498-103">使用來自經過身份驗證的來源的套件</span><span class="sxs-lookup"><span data-stu-id="49498-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="49498-104">除了nuget.org[公共來源](https://api.nuget.org/v3/index.json),NuGet 用戶端還能夠與檔案源和專用 HTTP 源進行互動。</span><span class="sxs-lookup"><span data-stu-id="49498-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="49498-105">要使用私有 HTTP 源進行身份驗證,這兩種方法是:</span><span class="sxs-lookup"><span data-stu-id="49498-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="49498-106">在[NuGet.config 中加入](../reference/nuget-config-file.md#packagesourcecredentials)認證</span><span class="sxs-lookup"><span data-stu-id="49498-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="49498-107">根據所使用的用戶端,使用眾多擴充性模型之一進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="49498-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="49498-108">NuGet 客戶端的驗證擴充性</span><span class="sxs-lookup"><span data-stu-id="49498-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="49498-109">對於各種 NuGet 用戶端,專用源提供程式本身負責身份驗證。</span><span class="sxs-lookup"><span data-stu-id="49498-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="49498-110">所有 NuGet 用戶端都有擴充性方法來支援此功能。</span><span class="sxs-lookup"><span data-stu-id="49498-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="49498-111">這些擴展可以是 Visual Studio 擴充,也可以是一個外掛程式,可以與 NuGet 通信以檢索認證。</span><span class="sxs-lookup"><span data-stu-id="49498-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="49498-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49498-112">Visual Studio</span></span>

<span data-ttu-id="49498-113">在 Visual Studio 中,NuGet 公開了一個介面,供應商可以實現該介面並將其提供給其客戶。</span><span class="sxs-lookup"><span data-stu-id="49498-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="49498-114">有關詳細資訊,請參閱有關如何創建 Visual Studio[認證提供程式](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的文件。</span><span class="sxs-lookup"><span data-stu-id="49498-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="49498-115">適用於視覺化工作室的可用 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="49498-116">可視化工作室中內置了一個憑據提供程式來支援 Azure DevOps。</span><span class="sxs-lookup"><span data-stu-id="49498-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="49498-117">可用的外掛程式認證提供者包括:</span><span class="sxs-lookup"><span data-stu-id="49498-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="49498-118">MyGet 視覺化工作室的認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="49498-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="49498-119">nuget.exe</span></span>

<span data-ttu-id="49498-120">當`nuget.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:</span><span class="sxs-lookup"><span data-stu-id="49498-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="49498-121">在`NuGet.config`檔中查找憑據。</span><span class="sxs-lookup"><span data-stu-id="49498-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="49498-122">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="49498-123">使用 V1 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="49498-124">然後,NuGet 會提示使用者在命令列上獲取憑據。</span><span class="sxs-lookup"><span data-stu-id="49498-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="49498-125">nuget.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="49498-126">在版本`4.8`NuGet 中定義了一種新的身份驗證外掛程式機制,以下簡稱 V2 認證提供提供者。</span><span class="sxs-lookup"><span data-stu-id="49498-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="49498-127">有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="49498-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="49498-128">nuget.exe 和 V1 認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="49498-129">在版本`3.3`NuGet 中引入了身份驗證外掛程式的第一個版本。</span><span class="sxs-lookup"><span data-stu-id="49498-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="49498-130">有關這些提供程式的安裝和發現,請參閱[nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="49498-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="49498-131">nuget.exe 可用認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="49498-132">[Azure DevOps V2 認證提供者](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later)或[Azure 專案認證提供者](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="49498-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="49498-133">使用 Visual Studio 2017 版本 15.9 及更高版本,Azure DevOps 認證提供程式捆綁在可視化工作室中。</span><span class="sxs-lookup"><span data-stu-id="49498-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="49498-134">如果`nuget.exe`使用來自該特定可視化工作室工具集的 MSBuild,則外掛程式將自動發現。</span><span class="sxs-lookup"><span data-stu-id="49498-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="49498-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="49498-135">dotnet.exe</span></span>

<span data-ttu-id="49498-136">當`dotnet.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:</span><span class="sxs-lookup"><span data-stu-id="49498-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="49498-137">在`NuGet.config`檔中查找憑據。</span><span class="sxs-lookup"><span data-stu-id="49498-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="49498-138">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="49498-139">預設情況下`dotnet.exe`,它不是互動式的,因此您可能需要傳遞標誌`--interactive`才能阻止該工具進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="49498-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="49498-140">dotnet.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="49498-141">在`2.2.100`SDK 版本中,NuGet 定義了適用於所有用戶端的身份驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="49498-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="49498-142">有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="49498-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="49498-143">dotnet.exe 的可用認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="49498-144">Azure 專案認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="49498-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="49498-145">MSBuild.exe</span></span>

<span data-ttu-id="49498-146">當`MSBuild.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:</span><span class="sxs-lookup"><span data-stu-id="49498-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="49498-147">在`NuGet.config`檔案中尋找認證</span><span class="sxs-lookup"><span data-stu-id="49498-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="49498-148">使用 V2 外掛程式認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="49498-149">預設情況下`MSBuild.exe`不是互動`/p:NuGetInteractive=true`式的 ,因此您可能需要設置屬性以使工具阻止進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="49498-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="49498-150">MSBuild.exe 和 V2 認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="49498-151">在 Visual Studio 2019 更新 9 中,NuGet 定義了適用於所有用戶端的身份驗證外掛程式機制。</span><span class="sxs-lookup"><span data-stu-id="49498-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="49498-152">有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="49498-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="49498-153">可用於 MSBuild.exe 可用認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="49498-154">Azure 專案認證提供者</span><span class="sxs-lookup"><span data-stu-id="49498-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="49498-155">使用 Visual Studio 2017 更新 9 及更高版本,Azure DevOps 認證提供提供程式捆綁在可視化工作室中。</span><span class="sxs-lookup"><span data-stu-id="49498-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="49498-156">無需執行其他步驟。</span><span class="sxs-lookup"><span data-stu-id="49498-156">No additional steps are required.</span></span>
