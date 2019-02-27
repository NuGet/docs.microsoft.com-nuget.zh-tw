---
title: tools.json 探索 nuget.exe 版本
description: 端點
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852529"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.json 探索 nuget.exe 版本

現在，有幾種可編寫指令碼的方式在電腦上取得最新版的 nuget.exe 的方式。 例如，您可以下載並解壓縮[ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/)從 nuget.org 的套件。這會有一些複雜性，因為它可能需要您已經有 nuget.exe (如`nuget.exe install`) 或您必須解壓縮.nupkg 使用基本的解壓縮工具，並尋找二進位的內部。

如果您已經有 nuget.exe，您也可以使用`nuget.exe update -self`，但也必須有現有的 nuget.exe 版本。 這個方法也會更新您的最新版本。 它不允許使用特定版本。

`tools.json`端點會提供給同時解決啟動問題並讓您下載 nuget.exe 的版本控制。 這可用在 CI/CD 環境中，或在自訂指令碼來探索並下載任何已發行的新版的 nuget.exe。

`tools.json`可以使用未經驗證的 HTTP 要求擷取端點 (例如`Invoke-WebRequest`在 PowerShell 中或`wget`)。 可以剖析使用 JSON 還原序列化程式，而且後續的 nuget.exe 下載 Url 可以也會擷取使用未經驗證的 HTTP 要求。

端點可以使用擷取`GET`方法：

    GET https://dist.nuget.org/tools.json

[JSON 結構描述](http://json-schema.org/)的端點，請參閱這裡：

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>回應

回應是 nuget.exe 的 JSON 文件包含所有可用版本。

根 JSON 物件具有下列屬性：

名稱      | 類型             | 必要
--------- | ---------------- | --------
nuget.exe | 物件的陣列 | 是

在每個物件`nuget.exe`陣列具有下列屬性：

名稱     | 類型   | 必要 | 注意
-------- | ------ | -------- | -----
版本  | 字串 | 是      | SemVer 2.0.0 字串
URL      | 字串 | 是      | 絕對 URL 下載這個新版的 nuget.exe
階段    | 字串 | 是      | 列舉字串
上傳 | 字串 | 是      | 版本時所提供之近似 ISO 8601 時間戳記

陣列中的項目會以遞減，SemVer 2.0.0 順序來排序。 這項保證是要降低最高的版本號碼有興趣的用戶端的負擔。 不過這表示不依時間順序排序清單。 例如，如果較舊的主要版本服務在日期晚於更高版本的主要版本中，此服務的版本不會出現在清單頂端。 如果您想要發行的最新版本*時間戳記*，只是排序的陣列`uploaded`字串。 這是因為`uploaded`時間戳記是以[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式也可以使用詞彙編篡排序 （也就是簡單的字串排序） 來依時間先後順序排序。

`stage`屬性表示是如何經審核的此版本的工具。 

階段              | 意義
------------------ | ------
EarlyAccessPreview | 尚未顯示在[下載網頁](https://www.nuget.org/downloads)和應該由協力廠商驗證
已發行           | 下載站台上的可用但尚未建議用於普遍耗用量
ReleasedAndBlessed | 下載站台上的可用建議在耗用量

有最新一個簡單的作法，建議的版本是要採取的第一個版本的清單中，具有`stage`的值`ReleasedAndBlessed`。 這是因為 SemVer 2.0.0 順序排序的版本。

`NuGet.CommandLine` Nuget.org 上的封裝通常只會更新與`ReleasedAndBlessed`版本。

### <a name="sample-request"></a>範例要求

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>範例回應

[!code-JSON [tools-json.json](./_data/tools-json.json)]
