---
ms.openlocfilehash: 7ebe3c0f75b8de158879119bce4df26217849251
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488955"
---
套件識別碼與版本號碼是專案中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。

**套件識別碼的最佳做法：**

- **唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。 決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。 若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。
- **命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。 例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。 套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。
- **範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示 (範例套件當然會有與另一個套件的相依性)。建立範例套件時，請使用 `<IncludeAssets>` 中的 `contentFiles` 值。 在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。

**套件版本的最佳做法：**

- 一般而言，請設定套件版本，使其符合專案 (或組件)，但這不是絕對必要。 當您將套件限制為單一組件時，這很簡單。 整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。
- 使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../../concepts/package-versioning.md)中所述。 NuGet 大多[符合 semver 2 規範](../../concepts/package-versioning.md#semantic-versioning-200)。

> 如需相依性解析的相關資訊，請參閱[使用 PackageReference 的相依性解析](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)。 如需更深入了解版本控制的較舊資訊，請參閱這一系列的部落格文章。
>
> - [第 1 部分：接受 DLL 挑戰](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) \(英文\)
> - [第 2 部分：核心演算法](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) \(英文\)
> - [第 3 部分：透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) \(英文\)