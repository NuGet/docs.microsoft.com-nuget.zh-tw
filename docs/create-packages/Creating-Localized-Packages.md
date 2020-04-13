---
title: 如何建立當地語系化 NuGet 套件
description: 兩種當地語系化 NuGet 套件建立方式的詳細資料：包含單一套件中的所有組件，或發行不同的組件。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610945"
---
# <a name="creating-localized-nuget-packages"></a>建立當地語系化 NuGet 套件

有兩種方式可以建立文件庫的當地語系化版本：

1. 在單一套件中包含所有當地語系化資源組件。
1. 遵循一組嚴格的慣例，以建立不同的當地語系化附屬套件。

兩種方法都有其優缺點，如下列各節中所述。

## <a name="localized-resource-assemblies-in-a-single-package"></a>單一套件中的當地語系化資源組件

在單一套件中包含當地語系化資源組件，一般就是最簡單的方法。 若要這樣做，請在 `lib` 內建立套件預設值 (假設為 en-us) 以外之支援語言的資料夾。 您可以在這些資料夾中放置資源組件和當地語系化 IntelliSense XML 檔案。

例如，下列資料夾結構支援德文 (de)、義大利文 (it)、日文 (ja)、俄文 (ru)、繁體中文 (zh-Hans) 和繁體中文 (zh-Hant)：

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

您可以看到語言全部列在 `net40` 目標架構資料夾下方。 如果您[支援多個架構](../create-packages/supporting-multiple-target-frameworks.md)，則在每個變異的 `lib` 下方會有一個資料夾。

有了這些資料夾之後，您接著參考 `.nuspec` 中的所有檔案：

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

使用此方法的其中一個範例套件是 [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0)。

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>優點和缺點 (當地語系化的資源組件)

將所有語言組合在單一套件中有幾個缺點：

1. **共用中繼資料**：因為 NuGet 套件只能包含單一 `.nuspec` 檔案，所以您只能為單一語言提供中繼資料。 也就是說，NuGet 不會支援當地語系化中繼資料。
1. **套件大小**：根據您所支援的語言數目，程式庫可能會變得相當大，這會減慢安裝和還原套件的速度。
1. **同時發行**：將當地語系化檔案組合成單一套件，需要您同時發行該套件中的所有資產，而不是可以個別發行每個當地語系化。 此外，任何一個當地語系化的任何更新都需要整個套件的新版本。

不過，它也有幾個優點：

1. **簡單**：套件的取用者會取得單一安裝中所有支援的語言，而不需要個別安裝每種語言。 在 nuget.org 上也較容易找到單一套件。
1. **結合版本**：因為所有資源組件都位在與主要組件相同的套件中，所以它們全都會共用相同的版本號碼，而且沒有錯誤分離的風險。

## <a name="localized-satellite-packages"></a>當地語系化附屬套件

與 .NET Framework 如何支援附屬組件類似，此方法會將當地語系化資源和 IntelliSense XML 檔案區隔到附屬套件。

至此，您的主要套件會使用命名慣例 `{identifier}.{version}.nupkg`，並包含預設語言 (例如 en-US) 的組件。 例如，`ContosoUtilities.1.0.0.nupkg` 會包含下列結構：

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

附屬組件接著會使用命名慣例 `{identifier}.{language}.{version}.nupkg` (例如 `ContosoUtilities.de.1.0.0.nupkg`)。 識別碼**必須**完全符合主要套件的識別碼。

因為這是不同的套件，所以它的專屬 `.nuspec` 檔案會包含當地語系化中繼資料。 請注意， 中的語言`.nuspec` **必須**符合檔案名稱中所使用的語言。

附屬組件也**必須**使用 [] 版本標記法將主要套件的確切版本宣告為相依性 (請參閱[套件版本控制](../concepts/package-versioning.md))。 例如，`ContosoUtilities.de.1.0.0.nupkg` 必須使用 `[1.0.0]` 標記法來宣告與 `ContosoUtilities.1.0.0.nupkg` 的相依性。 附屬套件的版本號碼當然可以與主要套件的版本號碼不同。

附屬套件的結構接著必須包含套件檔案名稱中符合 `{language}` 之子資料夾中的資源組件和 XML IntelliSense 檔案：

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**注意**：除非需要 `ja-JP` 這類特定子文化特性，否則一律會使用較高層的語言識別碼 (例如 `ja`)。

在附屬組件中，NuGet **只**會辨識檔案名稱中符合 `{language}` 之資料夾中的這些檔案。 其他所有項目都會被忽略。

符合所有這些慣例時，NuGet 會將套件辨識為附屬套件，並將當地語系化檔案安裝到主要套件的 `lib` 資料夾，就像它們一開始就已組合一樣。 解除安裝附屬套件將會從該相同資料夾中移除其檔案。

您可以使用相同的方式，針對每個支援的語言建立其他附屬組件。 如需範例，請檢查 ASP.NET MVC 套件集：

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (英文主要)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (德文)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (日文)
- [Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (簡體中文)
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (繁體中文)

### <a name="summary-of-required-conventions"></a>必要慣例的摘要

- 主要套件必須命名為 `{identifier}.{version}.nupkg`
- 附屬套件必須命名為 `{identifier}.{language}.{version}.nupkg`
- 附屬套件的 `.nuspec` 必須指定其語言符合檔案名稱。
- 附屬套件必須在其 `.nuspec` 檔案中使用 [] 標記法宣告與主要套件之確切版本的相依性。 不支援範圍。
- 附屬套件必須將檔案放在完全符合檔案名稱中 `{language}` 的 `lib\[{framework}\]{language}` 資料夾中。

### <a name="advantages-and-disadvantages-satellite-packages"></a>優點和缺點 (附屬套件)

使用附屬套件有幾個優點：

1. **套件大小**：主要套件的整體使用量會降到最低，而且取用者只會造成他們想要使用之每種語言的成本。
1. **區隔中繼資料**：每個附屬套件都有它的專屬 `.nuspec` 檔案，因此包含它的專屬當地語系化中繼資料。 這可讓部分取用者使用當地語系化詞彙來搜尋 nuget.org，更輕鬆地找到套件。
1. **低耦合版本**：可在一段時間內 (而非同時) 發行附屬組件，以讓您散發當地語系化工作。

不過，附屬套件有自己的一組缺點：

1. **雜亂**：您有許多套件可能導致 nuget.org 的搜尋結果雜亂，以及 Visual Studio 專案中的參考清單較長，而不是單一套件。
1. **嚴格慣例**. 附屬套件必須完全遵循慣例，否則無法正確反映當地語系化版本。
1. **版本控制**：每個附屬套件都必須具有與主要套件的確切版本相依性。 這表示，即使資源未變更，更新主要套件時也可能需要更新所有附屬套件。
