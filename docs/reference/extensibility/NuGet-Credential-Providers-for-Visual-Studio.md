---
title: Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會向藉由實作 IVsCredentialProvider 介面，在 Visual Studio 擴充功能的摘要。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793899"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="41e00-103">驗證 Visual Studio 中的摘要使用 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="41e00-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="41e00-104">NuGet Visual Studio 延伸模組 3.6 + 支援認證提供者，可以讓 NuGet 將使用已驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="41e00-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="41e00-105">安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 延伸模組會自動取得，並重新整理已驗證的摘要，視需要的認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="41e00-106">範例實作可在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="41e00-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="41e00-107">開始 4.8 + 在 Visual Studio 中的 NuGet 支援新跨平台驗證外掛程式，但它們不是建議的方法，基於效能考量。</span><span class="sxs-lookup"><span data-stu-id="41e00-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="41e00-108">Visual Studio 的 NuGet 認證提供者必須安裝為一般的 Visual Studio 擴充功能，而且需要[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="41e00-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="41e00-109">Visual Studio 的 NuGet 認證提供者僅適用於 Visual Studio （不在 dotnet restore 或 nuget.exe）。</span><span class="sxs-lookup"><span data-stu-id="41e00-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="41e00-110">Nuget.exe 認證提供者，請參閱 < [nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="41e00-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="41e00-111">Dotnet 和 msbuild 中的提供者如認證[NuGet 跨平台的外掛程式](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="41e00-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="41e00-112">使用 Visual Studio 的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="41e00-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="41e00-113">沒有認證提供者內建於 Visual Studio 的 NuGet 擴充功能以支援 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="41e00-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="41e00-114">NuGet Visual Studio 擴充功能會使用內部`VsCredentialProviderImporter`這也會掃描外掛程式認證提供者。</span><span class="sxs-lookup"><span data-stu-id="41e00-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="41e00-115">這些外掛程式認證提供者必須是 MEF 匯出的型別作為探索`IVsCredentialProvider`。</span><span class="sxs-lookup"><span data-stu-id="41e00-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="41e00-116">可用的外掛程式認證提供者包括：</span><span class="sxs-lookup"><span data-stu-id="41e00-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="41e00-117">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="41e00-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="41e00-118">建立 Visual Studio 的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="41e00-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="41e00-119">NuGet Visual Studio 延伸模組 3.6 + 會實作內部 CredentialService 用來取得認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="41e00-120">CredentialService 具有內建和外掛程式認證提供者的清單。</span><span class="sxs-lookup"><span data-stu-id="41e00-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="41e00-121">每個提供者會依序嘗試，直到取得認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="41e00-122">認證擷取、 憑證服務會嘗試依下列順序，停止只要取得認證的認證提供者：</span><span class="sxs-lookup"><span data-stu-id="41e00-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="41e00-123">從 NuGet 組態檔，將擷取的認證 (使用內建`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="41e00-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="41e00-124">如果套件來源是在 Visual Studio Team Services，`VisualStudioAccountProvider`將使用。</span><span class="sxs-lookup"><span data-stu-id="41e00-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="41e00-125">所有其他外掛程式 Visual Studio 認證提供者會嘗試依序。</span><span class="sxs-lookup"><span data-stu-id="41e00-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="41e00-126">嘗試依序使用跨平台的認證提供者的所有 NuGet。</span><span class="sxs-lookup"><span data-stu-id="41e00-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="41e00-127">如果已取得不使用認證，則會提示使用者，使用標準的基本驗證 對話方塊的認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="41e00-128">實作 IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="41e00-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="41e00-129">若要建立 Visual Studio 的 NuGet 認證提供者，建立 Visual Studio 擴充功能會公開公用 MEF 匯出實作`IVsCredentialProvider`輸入，並且會遵守以下所述的準則。</span><span class="sxs-lookup"><span data-stu-id="41e00-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="41e00-130">範例實作可在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="41e00-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="41e00-131">適用於 Visual Studio 的每個 NuGet 認證提供者必須：</span><span class="sxs-lookup"><span data-stu-id="41e00-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="41e00-132">判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。</span><span class="sxs-lookup"><span data-stu-id="41e00-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="41e00-133">如果提供者無法提供認證做為目標的來源，則它應該傳回`null`。</span><span class="sxs-lookup"><span data-stu-id="41e00-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="41e00-134">如果提供者無法處理要求的目標 URI，但無法提供認證，應該會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="41e00-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="41e00-135">Visual Studio 的自訂 NuGet 認證提供者必須實作`IVsCredentialProvider`介面中可用[NuGet.VisualStudio 封裝](https://www.nuget.org/packages/NuGet.VisualStudio/)。</span><span class="sxs-lookup"><span data-stu-id="41e00-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="41e00-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="41e00-136">GetCredentialAsync</span></span>

| <span data-ttu-id="41e00-137">輸入的參數</span><span class="sxs-lookup"><span data-stu-id="41e00-137">Input Parameter</span></span> |<span data-ttu-id="41e00-138">描述</span><span class="sxs-lookup"><span data-stu-id="41e00-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="41e00-139">Uri 的 uri</span><span class="sxs-lookup"><span data-stu-id="41e00-139">Uri uri</span></span> | <span data-ttu-id="41e00-140">套件來源 Uri 所要求的認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="41e00-141">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="41e00-141">IWebProxy proxy</span></span> | <span data-ttu-id="41e00-142">若要在網路上通訊時使用的 web proxy。</span><span class="sxs-lookup"><span data-stu-id="41e00-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="41e00-143">如果不沒有設定任何 proxy 驗證，則為 null。</span><span class="sxs-lookup"><span data-stu-id="41e00-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="41e00-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="41e00-144">bool isProxyRequest</span></span> | <span data-ttu-id="41e00-145">如果這個要求取得 proxy 驗證認證，則為 true。</span><span class="sxs-lookup"><span data-stu-id="41e00-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="41e00-146">如果實作取得 proxy 認證無效，應該會傳回 null。</span><span class="sxs-lookup"><span data-stu-id="41e00-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="41e00-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="41e00-147">bool isRetry</span></span> | <span data-ttu-id="41e00-148">如果這個 uri，先前要求的認證，但提供的認證不允許已獲授權的存取，則為 true。</span><span class="sxs-lookup"><span data-stu-id="41e00-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="41e00-149">非互動式的 bool</span><span class="sxs-lookup"><span data-stu-id="41e00-149">bool nonInteractive</span></span> | <span data-ttu-id="41e00-150">如果為 true，認證提供者必須抑制所有使用者提示，並改為使用預設值。</span><span class="sxs-lookup"><span data-stu-id="41e00-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="41e00-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="41e00-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="41e00-152">應該檢查這個取消語彙基元，以判斷是否已取消的作業要求的認證。</span><span class="sxs-lookup"><span data-stu-id="41e00-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="41e00-153">**傳回值**： 認證物件，實作[`System.Net.ICredentials`介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。</span><span class="sxs-lookup"><span data-stu-id="41e00-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
