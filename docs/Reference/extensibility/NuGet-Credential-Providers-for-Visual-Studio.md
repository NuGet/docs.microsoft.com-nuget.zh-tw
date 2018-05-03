---
title: Visual Studio 的 NuGet 認證提供者
description: NuGet 的認證提供者會向 IVsCredentialProvider 介面實作中的 Visual Studio 擴充功能的摘要。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>驗證 Visual Studio 中搭配 NuGet 認證提供者使用的摘要

NuGet Visual Studio 擴充功能 3.6 + 支援認證提供者，可讓已驗證的摘要所使用的 NuGet。
安裝 Visual Studio 的 NuGet 認證提供者之後，Visual Studio 擴充功能會自動取得，並重新整理的已驗證的摘要，視需要的認證。

中可以找到範例實作[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

> [!Note]
> Visual Studio 的 NuGet 認證提供者必須安裝成一般的 Visual Studio 擴充功能，而且需要[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) （目前處於預覽階段） 或更新版本。
>
> Visual Studio 的 NuGet 認證提供者僅適用於 Visual Studio （不在 dotnet 還原或 nuget.exe）。 對於與 nuget.exe 的認證提供者，請參閱[nuget.exe 認證提供者](nuget-exe-Credential-providers.md)。

## <a name="available-nuget-credential-providers-for-visual-studio"></a>使用 Visual Studio 的 NuGet 認證提供者

沒有認證提供者內建於 Visual Studio 的 NuGet 延伸模組來支援 Visual Studio Team Services。

NuGet Visual Studio 擴充功能會使用內部`VsCredentialProviderImporter`這也會掃描外掛程式的認證提供者。 這些外掛程式的認證提供者必須是做為 MEF 匯出類型的可探索`IVsCredentialProvider`。

可用的外掛程式認證提供者包括：

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>建立 Visual Studio 的 NuGet 認證提供者

NuGet Visual Studio 擴充功能 3.6 + 會實作內部 CredentialService 用來取得認證。 CredentialService 具有內建和外掛程式的認證提供者的清單。 每個提供者會嘗試依序直到取得認證。

認證擷取期間認證服務會嘗試依下列順序，停止只要取得認證的認證提供者：

1. 認證將會提取從 NuGet 組態檔 (使用內建`SettingsCredentialProvider`)。
1. 如果套件來源位於 Visual Studio Team Services，`VisualStudioAccountProvider`將使用。
1. 所有其他外掛程式的認證提供者會嘗試依序。
1. 如果已取得不含認證的資訊，將會提示使用者輸入認證，使用標準的基本驗證 對話方塊。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>實作 IVsCredentialProvider.GetCredentialsAsync

若要建立 Visual Studio 的 NuGet 認證提供者，建立 Visual Studio 擴充功能會公開公用 MEF 匯出實作`IVsCredentialProvider`輸入，並遵守如下所述的原則。

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

中可以找到範例實作[VsCredentialProvider 範例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

Visual Studio 的每個 NuGet 認證提供者必須：

1. 判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。 如果提供者無法提供認證做為目標的來源，則應該傳回`null`。
1. 如果提供者無法處理要求的目標 URI，但無法提供認證，就應該擲回例外狀況。

Visual Studio 的自訂 NuGet 認證提供者必須實作`IVsCredentialProvider`中提供的介面[NuGet.VisualStudio 封裝](https://www.nuget.org/packages/NuGet.VisualStudio/)。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 輸入的參數 |描述|
| ----------------|-----------|
| Uri 的 uri | 封裝來源 Uri 要求認證。|
| IWebProxy proxy | 若要在網路上通訊時使用的 web proxy。 如果不沒有設定任何 proxy 驗證，則為 null。 |
| bool isProxyRequest | 如果這個要求是以取得 proxy 驗證認證，則為 true。 如果實作取得 proxy 認證無效，應該會傳回 null。 |
| bool isRetry | 如果這個 uri，先前要求的認證，但提供的認證不允許存取的權限，則為 true。 |
| 非互動式 bool | 如果為 true，則認證提供者必須抑制所有使用者提示，並改為使用預設值。 |
| CancellationToken cancellationToken | 這個取消語彙基元應該檢查以判斷作業要求認證已被取消。 |

**傳回值**： 認證物件實作[`System.Net.ICredentials`介面](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。
