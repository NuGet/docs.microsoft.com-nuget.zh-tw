---
title: NuGet 用戶端 SDK
description: API 不斷演進且尚未記載，但範例可在 Dave Glick 的 blog 上取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235733"
---
# <a name="nuget-client-sdk"></a>NuGet 用戶端 SDK

*Nuget 用戶端 SDK* 指的是一組 nuget 套件：

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用來與 HTTP 和以檔案為基礎的 NuGet 摘要互動
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用來與 NuGet 套件互動。 `NuGet.Protocol` 相依于此套件

您可以在 [NuGet/nuget. 用戶端](https://github.com/NuGet/NuGet.Client) GitHub 存放庫中找到這些套件的原始程式碼。
您可以在 GitHub 上的 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 範例專案中找到這些範例的原始程式碼。

> [!Note]
> 如需 NuGet 伺服器通訊協定的相關檔，請參閱 [Nuget 伺服器 API](~/api/overview.md)。

## <a name="nugetprotocol"></a>Nuget.exe

安裝 `NuGet.Protocol` 套件以與 HTTP 和以資料夾為基礎的 NuGet 套件摘要進行互動：

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a>列出套件版本

使用 [NuGet V3 套件內容 API](../api/package-base-address-resource.md#enumerate-package-versions)尋找 Newtonsoft.Js的所有版本：

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>下載套件

使用 [NuGet V3 套件內容 API](../api/package-base-address-resource.md)下載 Newtonsoft.Json v 12.0.1：

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>取得套件中繼資料

使用 [NuGet V3 套件中繼資料 API](../api/registration-base-url-resource.md)來取得 "Newtonsoft.Json" 套件的中繼資料：

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>搜尋套件

使用 [NuGet V3 搜尋 API](../api/search-query-service-resource.md)來搜尋 "json" 套件：

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>推送套件

使用 [NuGet V3 推送和刪除 API](../api/package-publish-resource.md)來推送套件：

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>刪除套件

使用 [NuGet V3 推送和刪除 API](../api/package-publish-resource.md)來刪除套件：

> [!Note]
> NuGet 伺服器可任意將套件刪除要求解讀為「實刪除」、「虛刪除」或「取消列出」。
> 例如，nuget.org 會將套件刪除要求解讀為 "取消列出"。 如需這種作法的詳細資訊，請參閱 [刪除封裝](../nuget-org/policies/deleting-packages.md) 原則。

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>使用已驗證的摘要

使用 [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) 來處理已驗證的摘要。

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. 封裝

安裝 `NuGet.Packaging` 套件以與資料流程互動 `.nupkg` 和檔案 `.nuspec` ：

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>建立套件

使用建立封裝、設定中繼資料，以及新增相依性 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。

> [!IMPORTANT]
> 強烈建議您使用官方 NuGet 工具來建立 NuGet 套件，而 **不要** 使用此低層級 API。 格式正確的封裝有許多重要的特性，而最新版本的工具可協助您併入這些最佳做法。
> 
> 如需有關建立 NuGet 套件的詳細資訊，請參閱 [套件建立工作流程](../create-packages/overview-and-workflow.md) 的總覽，以及官方套件工具的檔 (例如， [使用 dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)) 。

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>讀取套件

使用從檔案資料流程讀取封裝 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 。

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>協力廠商檔

您可以在下列 Dave Glick 的 blog 系列中找到某些 API 的範例和檔，發佈2016：

- [探索 NuGet v3 程式庫，第1部分：簡介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [探索 NuGet v3 程式庫，第2部分：搜尋套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [探索 NuGet v3 程式庫，第3部分：安裝套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 這些 blog 文章是在 **3.4.3** 版本的 NuGet 用戶端 SDK 套件發行之後不久撰寫的。
> 較新版本的套件可能與 blog 文章中的資訊不相容。

Björkström 在 Dave Glick 的 blog 文章中，有一篇的 blog 文章，其中引進了使用 NuGet 用戶端 SDK 安裝 NuGet 套件的不同方法：

- [重新訪 NuGet v3 程式庫](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
