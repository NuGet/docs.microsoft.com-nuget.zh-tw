---
title: NuGet 用戶端 SDK
description: API 不斷演進且尚未記載，但範例可在 Dave Glick 的 blog 上取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622924"
---
# <a name="nuget-client-sdk"></a>NuGet 用戶端 SDK

*Nuget 用戶端 SDK*指的是一組 nuget 套件：

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用來與 HTTP 和以檔案為基礎的 NuGet 摘要互動
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用來與 NuGet 套件互動。 `NuGet.Protocol` 相依于此套件

您可以在 [NuGet/nuget. 用戶端](https://github.com/NuGet/NuGet.Client) GitHub 存放庫中找到這些套件的原始程式碼。

> [!Note]
> 如需 NuGet 伺服器通訊協定的相關檔，請參閱 [Nuget 伺服器 API](~/api/overview.md)。

## <a name="getting-started"></a>開始使用

### <a name="install-the-packages"></a>安裝套件

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>範例

您可以在 GitHub 上的 [nuget.exe. 範例](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 專案中找到這些範例。

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
