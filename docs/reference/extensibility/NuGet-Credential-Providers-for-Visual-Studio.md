---
title: 適用於 Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會藉由在 Visual Studio 延伸模組中執行 IVsCredentialProvider 介面，藉以向摘要進行驗證。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 13b6f5abe93a17c809564265990f86f6780aa67e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230807"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>使用 NuGet 認證提供者驗證 Visual Studio 中的摘要

NuGet Visual Studio 延伸模組 3.6 + 支援認證提供者，可讓 NuGet 使用已驗證的摘要。
在您安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 延伸模組將會自動取得並重新整理已驗證摘要的認證（如有需要）。

在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中可以找到範例執行。

在 Visual Studio 中，NuGet 會使用內部 `VsCredentialProviderImporter`，這也會掃描外掛程式認證提供者。 這些外掛程式認證提供者必須可視為 `IVsCredentialProvider`類型的 MEF 匯出。

從 4.8 + NuGet 開始，Visual Studio 也支援新的跨平臺驗證外掛程式，但基於效能考慮，它們不是建議的方法。

> [!Note]
> Visual Studio 的 NuGet 認證提供者必須安裝為一般 Visual Studio 延伸模組，而且將需要[Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe)或更新版本。
>
> Visual Studio 的 NuGet 認證提供者僅適用于 Visual Studio （不在 dotnet restore 或 nuget.exe 中）。 如需使用 nuget.exe 的認證提供者，請參閱[Nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。
> 如需 dotnet 和 msbuild 中的認證提供者，請參閱[NuGet 跨平臺外掛程式](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>建立 Visual Studio 的 NuGet 認證提供者

NuGet Visual Studio 延伸模組 3.6 + 會實行用來取得認證的內部 CredentialService。 CredentialService 具有內建和外掛程式認證提供者的清單。 系統會依序嘗試每個提供者，直到取得認證為止。

在認證取得期間，認證服務會依下列順序嘗試認證提供者，並在取得認證時立即停止：

1. 將從 NuGet 設定檔提取認證（使用內建的 `SettingsCredentialProvider`）。
1. 如果封裝來源在 Visual Studio Team Services 上，則會使用 `VisualStudioAccountProvider`。
1. 所有其他外掛程式 Visual Studio 認證提供者都會依序嘗試。
1. 請嘗試順序使用所有的 NuGet 跨平臺認證提供者。
1. 如果尚未取得認證，則會使用標準的基本驗證對話方塊來提示使用者提供認證。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>執行 IVsCredentialProvider。 GetCredentialsAsync

若要建立 Visual Studio 的 NuGet 認證提供者，請建立 Visual Studio 延伸模組，以公開執行 `IVsCredentialProvider` 類型的公用 MEF 匯出，並遵循下面所述的原則。

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

在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中可以找到範例執行。

Visual Studio 的每個 NuGet 認證提供者都必須：

1. 判斷它是否可以在起始認證之前，提供目標 URI 的認證。 如果提供者無法提供目標來源的認證，則應該會傳回 `null`。
1. 如果提供者確實處理目標 URI 的要求，但無法提供認證，則應該擲回例外狀況。

Visual Studio 的自訂 NuGet 認證提供者必須執行[VisualStudio 套件](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的 `IVsCredentialProvider` 介面。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 輸入參數 |描述|
| ----------------|-----------|
| Uri uri | 要求認證的套件來源 Uri。|
| IWebProxy proxy | 在網路上通訊時所要使用的 Web proxy。 如果未設定 proxy 驗證，則為 Null。 |
| bool isProxyRequest | 如果此要求是取得 proxy 驗證認證，則為 True。 如果此實作為取得 proxy 認證的無效，則應該傳回 null。 |
| bool isRetry | 如果先前已針對此 Uri 要求認證，但提供的認證不允許授權存取，則為 True。 |
| bool 非互動式 | 若為 true，則認證提供者必須隱藏所有使用者提示，並改為使用預設值。 |
| CancellationToken cancellationToken | 應檢查此解除標記，以判斷要求認證的作業是否已取消。 |

傳回**值**：用來執行[`System.Net.ICredentials` 介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的認證物件。
