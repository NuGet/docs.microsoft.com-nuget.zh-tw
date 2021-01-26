---
title: 適用於 Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會在 Visual Studio 擴充功能中執行 IVsCredentialProvider 介面，以透過摘要進行驗證。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777761"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>使用 NuGet 認證提供者驗證 Visual Studio 中的摘要

NuGet Visual Studio Extension 3.6 + 支援認證提供者，可讓 NuGet 使用已驗證的摘要。
當您安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 擴充功能就會在必要時自動取得並重新整理已驗證摘要的認證。

您可以在 [VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到範例執行。

在 Visual Studio 中，NuGet 會使用 `VsCredentialProviderImporter` 同時掃描外掛程式認證提供者的內部。 這些外掛程式認證提供者必須可探索為型別的 MEF 匯出 `IVsCredentialProvider` 。

從 4.8 + NuGet 開始，Visual Studio 也支援新的跨平臺驗證外掛程式，但基於效能考慮，不建議採用這種方法。

> [!Note]
> Visual Studio 的 NuGet 認證提供者必須安裝為一般 Visual Studio 延伸模組，而且需要 [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 或更新版本。
>
> Visual Studio 的 NuGet 認證提供者僅適用于 Visual Studio (不在 dotnet restore 或 nuget.exe) 中。 如 nuget.exe 的認證提供者，請參閱 [nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。
> 針對 dotnet 和 msbuild 中的認證提供者，請參閱 [NuGet 跨平臺外掛程式](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>建立 Visual Studio 的 NuGet 認證提供者

NuGet Visual Studio Extension 3.6 + 會執行用來取得認證的內部 CredentialService。 CredentialService 具有內建和外掛程式認證提供者的清單。 每個提供者會依序嘗試，直到取得認證為止。

認證取得期間，認證服務會依下列順序嘗試認證提供者，並在取得認證時立即停止：

1. 您將使用內建) ，從 NuGet 設定檔提取認證 (`SettingsCredentialProvider` 。
1. 如果封裝來源在 Visual Studio Team Services 上，將會 `VisualStudioAccountProvider` 使用。
1. 所有其他外掛程式 Visual Studio 認證提供者將依序嘗試。
1. 請嘗試依序使用所有 NuGet 跨平臺認證提供者。
1. 如果尚未取得認證，系統會使用標準的基本驗證對話方塊，提示使用者輸入認證。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>執行 IVsCredentialProvider. >getcredentialsasync

若要建立 Visual Studio 的 NuGet 認證提供者，請建立一個 Visual Studio 擴充功能，此擴充功能會公開實作為型別的公用 MEF 匯出 `IVsCredentialProvider` ，並遵守以下所述的原則。

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

您可以在 [VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到範例執行。

Visual Studio 的每個 NuGet 認證提供者都必須：

1. 判斷是否可以在起始認證取得之前，提供目標 URI 的認證。 如果提供者無法提供目標來源的認證，則應該會傳回 `null` 。
1. 如果提供者處理的是目標 URI 的要求，但無法提供認證，則應該擲回例外狀況。

Visual Studio 的自訂 NuGet 認證提供者必須執行 `IVsCredentialProvider` [VisualStudio 套件](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的介面。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 輸入參數 |描述|
| ----------------|-----------|
| Uri uri | 要求認證的套件來源 Uri。|
| IWebProxy proxy | 網路上通訊時要使用的 Web proxy。 如果未設定 proxy 驗證，則為 Null。 |
| bool isProxyRequest | 如果此要求是取得 proxy 驗證認證，則為 True。 如果實值對於取得 proxy 認證無效，則應該傳回 null。 |
| bool isRetry | 如果先前已要求此 Uri 的認證，但提供的認證不允許授權存取，則為 True。 |
| bool 非互動式 | 若為 true，認證提供者必須隱藏所有使用者提示，並改用預設值。 |
| CancellationToken cancellationToken | 應檢查此解除標記，以判斷要求認證的作業是否已取消。 |

傳回 **值**：執行 [ `System.Net.ICredentials` 介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的認證物件。
