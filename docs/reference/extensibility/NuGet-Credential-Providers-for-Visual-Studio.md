---
title: 適用於 Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會在 Visual Studio 擴充功能中執行 IVsCredentialProvider 介面，以透過摘要進行驗證。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859092"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="b8a27-103">使用 NuGet 認證提供者驗證 Visual Studio 中的摘要</span><span class="sxs-lookup"><span data-stu-id="b8a27-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="b8a27-104">NuGet Visual Studio Extension 3.6 + 支援認證提供者，可讓 NuGet 使用已驗證的摘要。</span><span class="sxs-lookup"><span data-stu-id="b8a27-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="b8a27-105">當您安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 擴充功能就會在必要時自動取得並重新整理已驗證摘要的認證。</span><span class="sxs-lookup"><span data-stu-id="b8a27-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="b8a27-106">您可以在 [VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)中找到範例執行。</span><span class="sxs-lookup"><span data-stu-id="b8a27-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="b8a27-107">在 Visual Studio 中，NuGet 會使用 `VsCredentialProviderImporter` 同時掃描外掛程式認證提供者的內部。</span><span class="sxs-lookup"><span data-stu-id="b8a27-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="b8a27-108">這些外掛程式認證提供者必須可探索為型別的 MEF 匯出 `IVsCredentialProvider` 。</span><span class="sxs-lookup"><span data-stu-id="b8a27-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="b8a27-109">從 4.8 + NuGet 開始，Visual Studio 也支援新的跨平臺驗證外掛程式，但基於效能考慮，不建議採用這種方法。</span><span class="sxs-lookup"><span data-stu-id="b8a27-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="b8a27-110">Visual Studio 的 NuGet 認證提供者必須安裝為一般 Visual Studio 延伸模組，而且需要 [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b8a27-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="b8a27-111">Visual Studio 的 NuGet 認證提供者僅適用于 Visual Studio (不在 dotnet restore 或 nuget.exe) 中。</span><span class="sxs-lookup"><span data-stu-id="b8a27-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="b8a27-112">如 nuget.exe 的認證提供者，請參閱 [nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a27-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="b8a27-113">針對 dotnet 和 msbuild 中的認證提供者，請參閱 [NuGet 跨平臺外掛程式](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="b8a27-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="b8a27-114">建立 Visual Studio 的 NuGet 認證提供者</span><span class="sxs-lookup"><span data-stu-id="b8a27-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="b8a27-115">NuGet Visual Studio Extension 3.6 + 會執行用來取得認證的內部 CredentialService。</span><span class="sxs-lookup"><span data-stu-id="b8a27-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="b8a27-116">CredentialService 具有內建和外掛程式認證提供者的清單。</span><span class="sxs-lookup"><span data-stu-id="b8a27-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="b8a27-117">每個提供者會依序嘗試，直到取得認證為止。</span><span class="sxs-lookup"><span data-stu-id="b8a27-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="b8a27-118">認證取得期間，認證服務會依下列順序嘗試認證提供者，並在取得認證時立即停止：</span><span class="sxs-lookup"><span data-stu-id="b8a27-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="b8a27-119">您將使用內建) ，從 NuGet 設定檔提取認證 (`SettingsCredentialProvider` 。</span><span class="sxs-lookup"><span data-stu-id="b8a27-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="b8a27-120">如果封裝來源在 Visual Studio Team Services 上，將會 `VisualStudioAccountProvider` 使用。</span><span class="sxs-lookup"><span data-stu-id="b8a27-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="b8a27-121">所有其他外掛程式 Visual Studio 認證提供者將依序嘗試。</span><span class="sxs-lookup"><span data-stu-id="b8a27-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="b8a27-122">請嘗試依序使用所有 NuGet 跨平臺認證提供者。</span><span class="sxs-lookup"><span data-stu-id="b8a27-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="b8a27-123">如果尚未取得認證，系統會使用標準的基本驗證對話方塊，提示使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="b8a27-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="b8a27-124">執行 IVsCredentialProvider. >getcredentialsasync</span><span class="sxs-lookup"><span data-stu-id="b8a27-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="b8a27-125">若要建立 Visual Studio 的 NuGet 認證提供者，請建立一個 Visual Studio 擴充功能，此擴充功能會公開實作為型別的公用 MEF 匯出 `IVsCredentialProvider` ，並遵守以下所述的原則。</span><span class="sxs-lookup"><span data-stu-id="b8a27-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="b8a27-126">您可以在 [VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)中找到範例執行。</span><span class="sxs-lookup"><span data-stu-id="b8a27-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="b8a27-127">Visual Studio 的每個 NuGet 認證提供者都必須：</span><span class="sxs-lookup"><span data-stu-id="b8a27-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="b8a27-128">判斷是否可以在起始認證取得之前，提供目標 URI 的認證。</span><span class="sxs-lookup"><span data-stu-id="b8a27-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b8a27-129">如果提供者無法提供目標來源的認證，則應該會傳回 `null` 。</span><span class="sxs-lookup"><span data-stu-id="b8a27-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="b8a27-130">如果提供者處理的是目標 URI 的要求，但無法提供認證，則應該擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b8a27-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="b8a27-131">Visual Studio 的自訂 NuGet 認證提供者必須執行 `IVsCredentialProvider` [VisualStudio 套件](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的介面。</span><span class="sxs-lookup"><span data-stu-id="b8a27-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="b8a27-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="b8a27-132">GetCredentialAsync</span></span>

| <span data-ttu-id="b8a27-133">輸入參數</span><span class="sxs-lookup"><span data-stu-id="b8a27-133">Input Parameter</span></span> |<span data-ttu-id="b8a27-134">描述</span><span class="sxs-lookup"><span data-stu-id="b8a27-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="b8a27-135">Uri uri</span><span class="sxs-lookup"><span data-stu-id="b8a27-135">Uri uri</span></span> | <span data-ttu-id="b8a27-136">要求認證的套件來源 Uri。</span><span class="sxs-lookup"><span data-stu-id="b8a27-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="b8a27-137">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="b8a27-137">IWebProxy proxy</span></span> | <span data-ttu-id="b8a27-138">網路上通訊時要使用的 Web proxy。</span><span class="sxs-lookup"><span data-stu-id="b8a27-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="b8a27-139">如果未設定 proxy 驗證，則為 Null。</span><span class="sxs-lookup"><span data-stu-id="b8a27-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="b8a27-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="b8a27-140">bool isProxyRequest</span></span> | <span data-ttu-id="b8a27-141">如果此要求是取得 proxy 驗證認證，則為 True。</span><span class="sxs-lookup"><span data-stu-id="b8a27-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="b8a27-142">如果實值對於取得 proxy 認證無效，則應該傳回 null。</span><span class="sxs-lookup"><span data-stu-id="b8a27-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="b8a27-143">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="b8a27-143">bool isRetry</span></span> | <span data-ttu-id="b8a27-144">如果先前已要求此 Uri 的認證，但提供的認證不允許授權存取，則為 True。</span><span class="sxs-lookup"><span data-stu-id="b8a27-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="b8a27-145">bool 非互動式</span><span class="sxs-lookup"><span data-stu-id="b8a27-145">bool nonInteractive</span></span> | <span data-ttu-id="b8a27-146">若為 true，認證提供者必須隱藏所有使用者提示，並改用預設值。</span><span class="sxs-lookup"><span data-stu-id="b8a27-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="b8a27-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="b8a27-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="b8a27-148">應檢查此解除標記，以判斷要求認證的作業是否已取消。</span><span class="sxs-lookup"><span data-stu-id="b8a27-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="b8a27-149">傳回 **值**：執行 [ `System.Net.ICredentials` 介面](/dotnet/api/system.net.icredentials)的認證物件。</span><span class="sxs-lookup"><span data-stu-id="b8a27-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials).</span></span>
