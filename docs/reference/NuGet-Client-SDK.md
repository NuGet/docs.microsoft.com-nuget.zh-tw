---
title: NuGet 用戶端 SDK
description: API 不斷演進，尚未記載，但範例可在 Dave Glick 的 blog 中取得。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231236"
---
# <a name="nuget-client-sdk"></a>NuGet 用戶端 SDK

*Nuget 用戶端 SDK*是指 nuget 套件的群組：

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -用來與 HTTP 和以檔案為基礎的 NuGet 摘要互動
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -用來與 NuGet 套件互動。 `NuGet.Protocol` 相依于此套件

您可以在[nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub 存放庫中找到這些套件的原始程式碼。

> [!Note]
> 如需 NuGet 伺服器通訊協定的相關檔，請參閱[Nuget 伺服器 API](~/api/overview.md)。

## <a name="getting-started"></a>開始使用

### <a name="install-the-package"></a>安裝套件

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>範例

您可以在 GitHub 上的[範例](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)專案中找到這些範例。

### <a name="list-package-versions"></a>列出套件版本

使用[NuGet V3 套件內容 API](../api/package-base-address-resource.md#enumerate-package-versions)來尋找 Newtonsoft 的所有版本：

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>下載套件

使用[NuGet V3 套件內容 API](../api/package-base-address-resource.md)下載 Newtonsoft 12.0.1：

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>取得套件中繼資料

使用[NuGet V3 套件中繼資料 API](../api/registration-base-url-resource.md)取得 "Newtonsoft" 套件的中繼資料：

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>搜尋套件

使用[NuGet V3 搜尋 API](../api/search-query-service-resource.md)搜尋 "json" 套件：

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>協力廠商檔

您可以在下列 blog 系列中找到一些 API 的範例和檔： Dave Glick，發佈的2016：

- [探索 NuGet v3 程式庫，第1部分：簡介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [探索 NuGet v3 程式庫，第2部分：搜尋封裝](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [探索 NuGet v3 程式庫，第3部分：安裝套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 這些 blog 文章是在 NuGet 用戶端 SDK 套件的**3.4.3**版本發行後不久撰寫。
> 較新版本的套件可能與 blog 文章中的資訊不相容。

聖馬丁 Björkström 在 Dave Glick 的 blog 系列文章中，介紹了使用 NuGet 用戶端 SDK 來安裝 NuGet 套件的不同方法：

- [重新訪 NuGet v3 程式庫](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
