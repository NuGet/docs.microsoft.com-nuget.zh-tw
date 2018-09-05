---
title: Visual Studio 的 NuGet 認證提供者
description: NuGet 認證提供者會向藉由實作 IVsCredentialProvider 介面，在 Visual Studio 擴充功能的摘要。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547950"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>驗證 Visual Studio 中的摘要使用 NuGet 認證提供者

NuGet Visual Studio 延伸模組 3.6 + 支援認證提供者，可以讓 NuGet 將使用已驗證的摘要。
安裝 Visual Studio 的 NuGet 認證提供者之後，NuGet Visual Studio 延伸模組會自動取得，並重新整理已驗證的摘要，視需要的認證。

範例實作可在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

開始 4.8 + 在 Visual Studio 中的 NuGet 支援新跨平台驗證外掛程式，但它們不是建議的方法，基於效能考量。

> [!Note]
> Visual Studio 的 NuGet 認證提供者必須安裝為一般的 Visual Studio 擴充功能，而且需要[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)或更新版本。
>
> Visual Studio 的 NuGet 認證提供者僅適用於 Visual Studio （不在 dotnet restore 或 nuget.exe）。 Nuget.exe 認證提供者，請參閱 < [nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。
> Dotnet 和 msbuild 中的提供者如認證[NuGet 跨平台的外掛程式](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>使用 Visual Studio 的 NuGet 認證提供者

沒有認證提供者內建於 Visual Studio 的 NuGet 擴充功能以支援 Visual Studio Team Services。

NuGet Visual Studio 擴充功能會使用內部`VsCredentialProviderImporter`這也會掃描外掛程式認證提供者。 這些外掛程式認證提供者必須是 MEF 匯出的型別作為探索`IVsCredentialProvider`。

可用的外掛程式認證提供者包括：

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>建立 Visual Studio 的 NuGet 認證提供者

NuGet Visual Studio 延伸模組 3.6 + 會實作內部 CredentialService 用來取得認證。 CredentialService 具有內建和外掛程式認證提供者的清單。 每個提供者會依序嘗試，直到取得認證。

認證擷取、 憑證服務會嘗試依下列順序，停止只要取得認證的認證提供者：

1. 從 NuGet 組態檔，將擷取的認證 (使用內建`SettingsCredentialProvider`)。
1. 如果套件來源是在 Visual Studio Team Services，`VisualStudioAccountProvider`將使用。
1. 所有其他外掛程式 Visual Studio 認證提供者會嘗試依序。
1. 嘗試依序使用跨平台的認證提供者的所有 NuGet。
1. 如果已取得不使用認證，則會提示使用者，使用標準的基本驗證 對話方塊的認證。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>實作 IVsCredentialProvider.GetCredentialsAsync

若要建立 Visual Studio 的 NuGet 認證提供者，建立 Visual Studio 擴充功能會公開公用 MEF 匯出實作`IVsCredentialProvider`輸入，並且會遵守以下所述的準則。

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

範例實作可在[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

適用於 Visual Studio 的每個 NuGet 認證提供者必須：

1. 判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。 如果提供者無法提供認證做為目標的來源，則它應該傳回`null`。
1. 如果提供者無法處理要求的目標 URI，但無法提供認證，應該會擲回例外狀況。

Visual Studio 的自訂 NuGet 認證提供者必須實作`IVsCredentialProvider`介面中可用[NuGet.VisualStudio 封裝](https://www.nuget.org/packages/NuGet.VisualStudio/)。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 輸入的參數 |描述|
| ----------------|-----------|
| Uri 的 uri | 套件來源 Uri 所要求的認證。|
| IWebProxy proxy | 若要在網路上通訊時使用的 web proxy。 如果不沒有設定任何 proxy 驗證，則為 null。 |
| bool isProxyRequest | 如果這個要求取得 proxy 驗證認證，則為 true。 如果實作取得 proxy 認證無效，應該會傳回 null。 |
| bool isRetry | 如果這個 uri，先前要求的認證，但提供的認證不允許已獲授權的存取，則為 true。 |
| 非互動式的 bool | 如果為 true，認證提供者必須抑制所有使用者提示，並改為使用預設值。 |
| CancellationToken cancellationToken | 應該檢查這個取消語彙基元，以判斷是否已取消的作業要求的認證。 |

**傳回值**： 認證物件，實作[`System.Net.ICredentials`介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。
