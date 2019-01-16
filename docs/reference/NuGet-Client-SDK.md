---
title: NuGet 用戶端 SDK
description: API 是不斷演變以及不尚未記載，但 Dave Glick 部落格上的範例可用。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324678"
---
# <a name="nuget-client-sdk"></a>NuGet 用戶端 SDK

> [!Note]
> 不到與混淆[NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

*NuGet 用戶端 SDK*參考為主的.NET 程式庫的一組[NuGet.Client](https://www.nuget.org/packages/NuGet.Client)， [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)，和[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). 這些套件取代舊版[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)程式庫。

我們正努力有穩定的介面區，我們很快就可以文件。

## <a name="source-code"></a>原始程式碼

GitHub 上發行的原始碼專案中[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)。

## <a name="third-party-documentation"></a>協力廠商文件

下列部落格系列由 Dave Glick，發行 2016年中，您可以找到範例和某些 API 的文件：

- [瀏覽 NuGet v3 程式庫，第 1 部分：簡介和概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [瀏覽 NuGet v3 程式庫，第 2 部分：搜尋套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [瀏覽 NuGet v3 程式庫，第 3 部分：安裝套件](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 這些部落格文章所撰寫後不久**3.4.3**發行用戶端 SDK 套件的 NuGet 版本。
> 較新版本的封裝可能與部落格文章中的資訊不相容。

Martin Björkström 未 Dave Glick 部落格系列的待處理的部落格文章，其中介紹他如何使用安裝 NuGet 套件的 NuGet 用戶端 SDK 不同的方法：

- [重新認識 NuGet v3 程式庫](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
