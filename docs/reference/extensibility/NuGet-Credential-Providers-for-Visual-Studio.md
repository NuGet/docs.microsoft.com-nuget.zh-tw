---
title: 適用於 Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會藉由在 Visual Studio 延伸模組中執行 IVsCredentialProvider 介面，藉以向摘要進行驗證。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384435"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="383f8-103">使用 NuGet 認證提供者驗證 Visual Studio 中的摘要</span><span class="sxs-lookup"><span data-stu-id="383f8-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="383f8-104">NuGet Visual Studio 延伸模組 3.6 + 支援認證提供者，可讓 NuGet 使用已驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="383f8-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="383f8-105">在您安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 延伸模組將會自動取得並重新整理已驗證摘要的認證（如有需要）。</span><span class="sxs-lookup"><span data-stu-id="383f8-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="383f8-106">在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中可以找到範例執行。</span><span class="sxs-lookup"><span data-stu-id="383f8-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="383f8-107">從 4.8 + NuGet 開始，Visual Studio 也支援新的跨平臺驗證外掛程式，但基於效能考慮，它們不是建議的方法。</span><span class="sxs-lookup"><span data-stu-id="383f8-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="383f8-108">Visual Studio 的 NuGet 認證提供者必須安裝為一般 Visual Studio 延伸模組，而且將需要[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="383f8-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="383f8-109">Visual Studio 的 NuGet 認證提供者僅適用于 Visual Studio （不在 dotnet restore 或 nuget.exe 中）。</span><span class="sxs-lookup"><span data-stu-id="383f8-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="383f8-110">如需使用 nuget.exe 的認證提供者，請參閱[Nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="383f8-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="383f8-111">如需 dotnet 和 msbuild 中的認證提供者，請參閱[NuGet 跨平臺外掛程式](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="383f8-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="383f8-112">Visual Studio 可用的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="383f8-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="383f8-113">Visual Studio NuGet 延伸模組內建有認證提供者，可支援 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="383f8-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="383f8-114">NuGet Visual Studio 延伸模組會使用內部`VsCredentialProviderImporter` ，這也會掃描外掛程式認證提供者。</span><span class="sxs-lookup"><span data-stu-id="383f8-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="383f8-115">這些外掛程式認證提供者必須可視為類型`IVsCredentialProvider`的 MEF 匯出。</span><span class="sxs-lookup"><span data-stu-id="383f8-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="383f8-116">可用的外掛程式認證提供者包括：</span><span class="sxs-lookup"><span data-stu-id="383f8-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="383f8-117">Visual Studio 的 MyGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="383f8-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="383f8-118">建立 Visual Studio 的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="383f8-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="383f8-119">NuGet Visual Studio 延伸模組 3.6 + 會實行用來取得認證的內部 CredentialService。</span><span class="sxs-lookup"><span data-stu-id="383f8-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="383f8-120">CredentialService 具有內建和外掛程式認證提供者的清單。</span><span class="sxs-lookup"><span data-stu-id="383f8-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="383f8-121">系統會依序嘗試每個提供者，直到取得認證為止。</span><span class="sxs-lookup"><span data-stu-id="383f8-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="383f8-122">在認證取得期間，認證服務會依下列順序嘗試認證提供者，並在取得認證時立即停止：</span><span class="sxs-lookup"><span data-stu-id="383f8-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="383f8-123">將從 NuGet 設定檔提取認證（使用內`SettingsCredentialProvider`建）。</span><span class="sxs-lookup"><span data-stu-id="383f8-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="383f8-124">如果封裝來源在 Visual Studio Team Services 上， `VisualStudioAccountProvider`則會使用。</span><span class="sxs-lookup"><span data-stu-id="383f8-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="383f8-125">所有其他外掛程式 Visual Studio 認證提供者都會依序嘗試。</span><span class="sxs-lookup"><span data-stu-id="383f8-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="383f8-126">請嘗試順序使用所有的 NuGet 跨平臺認證提供者。</span><span class="sxs-lookup"><span data-stu-id="383f8-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="383f8-127">如果尚未取得認證，則會使用標準的基本驗證對話方塊來提示使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="383f8-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="383f8-128">執行 IVsCredentialProvider。 GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="383f8-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="383f8-129">若要建立 Visual Studio 的 NuGet 認證提供者，請建立 Visual Studio 延伸模組，該擴充功能會公開`IVsCredentialProvider`實作為類型的公用 MEF 匯出，並遵循下面所述的原則。</span><span class="sxs-lookup"><span data-stu-id="383f8-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="383f8-130">在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中可以找到範例執行。</span><span class="sxs-lookup"><span data-stu-id="383f8-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="383f8-131">Visual Studio 的每個 NuGet 認證提供者都必須：</span><span class="sxs-lookup"><span data-stu-id="383f8-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="383f8-132">判斷它是否可以在起始認證之前，提供目標 URI 的認證。</span><span class="sxs-lookup"><span data-stu-id="383f8-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="383f8-133">如果提供者無法提供目標來源的認證，則它應該`null`會傳回。</span><span class="sxs-lookup"><span data-stu-id="383f8-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="383f8-134">如果提供者確實處理目標 URI 的要求，但無法提供認證，則應該擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="383f8-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="383f8-135">Visual Studio 的自訂 NuGet 認證提供者必須執行`IVsCredentialProvider` [VisualStudio 套件](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的介面。</span><span class="sxs-lookup"><span data-stu-id="383f8-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="383f8-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="383f8-136">GetCredentialAsync</span></span>

| <span data-ttu-id="383f8-137">輸入參數</span><span class="sxs-lookup"><span data-stu-id="383f8-137">Input Parameter</span></span> |<span data-ttu-id="383f8-138">說明</span><span class="sxs-lookup"><span data-stu-id="383f8-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="383f8-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="383f8-139">Uri uri</span></span> | <span data-ttu-id="383f8-140">要求認證的套件來源 Uri。</span><span class="sxs-lookup"><span data-stu-id="383f8-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="383f8-141">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="383f8-141">IWebProxy proxy</span></span> | <span data-ttu-id="383f8-142">在網路上通訊時所要使用的 Web proxy。</span><span class="sxs-lookup"><span data-stu-id="383f8-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="383f8-143">如果未設定 proxy 驗證，則為 Null。</span><span class="sxs-lookup"><span data-stu-id="383f8-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="383f8-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="383f8-144">bool isProxyRequest</span></span> | <span data-ttu-id="383f8-145">如果此要求是取得 proxy 驗證認證，則為 True。</span><span class="sxs-lookup"><span data-stu-id="383f8-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="383f8-146">如果此實作為取得 proxy 認證的無效，則應該傳回 null。</span><span class="sxs-lookup"><span data-stu-id="383f8-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="383f8-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="383f8-147">bool isRetry</span></span> | <span data-ttu-id="383f8-148">如果先前已針對此 Uri 要求認證，但提供的認證不允許授權存取，則為 True。</span><span class="sxs-lookup"><span data-stu-id="383f8-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="383f8-149">bool 非互動式</span><span class="sxs-lookup"><span data-stu-id="383f8-149">bool nonInteractive</span></span> | <span data-ttu-id="383f8-150">若為 true，則認證提供者必須隱藏所有使用者提示，並改為使用預設值。</span><span class="sxs-lookup"><span data-stu-id="383f8-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="383f8-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="383f8-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="383f8-152">應檢查此解除標記，以判斷要求認證的作業是否已取消。</span><span class="sxs-lookup"><span data-stu-id="383f8-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="383f8-153">傳回**值**：用來執行[ `System.Net.ICredentials`介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的認證物件。</span><span class="sxs-lookup"><span data-stu-id="383f8-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
