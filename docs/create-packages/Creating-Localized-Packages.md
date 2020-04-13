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
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="9d24c-103">建立當地語系化 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="9d24c-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="9d24c-104">有兩種方式可以建立文件庫的當地語系化版本：</span><span class="sxs-lookup"><span data-stu-id="9d24c-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="9d24c-105">在單一套件中包含所有當地語系化資源組件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="9d24c-106">遵循一組嚴格的慣例，以建立不同的當地語系化附屬套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="9d24c-107">兩種方法都有其優缺點，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="9d24c-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="9d24c-108">單一套件中的當地語系化資源組件</span><span class="sxs-lookup"><span data-stu-id="9d24c-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="9d24c-109">在單一套件中包含當地語系化資源組件，一般就是最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="9d24c-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="9d24c-110">若要這樣做，請在 `lib` 內建立套件預設值 (假設為 en-us) 以外之支援語言的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9d24c-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="9d24c-111">您可以在這些資料夾中放置資源組件和當地語系化 IntelliSense XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9d24c-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="9d24c-112">例如，下列資料夾結構支援德文 (de)、義大利文 (it)、日文 (ja)、俄文 (ru)、繁體中文 (zh-Hans) 和繁體中文 (zh-Hant)：</span><span class="sxs-lookup"><span data-stu-id="9d24c-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="9d24c-113">您可以看到語言全部列在 `net40` 目標架構資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="9d24c-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="9d24c-114">如果您[支援多個架構](../create-packages/supporting-multiple-target-frameworks.md)，則在每個變異的 `lib` 下方會有一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="9d24c-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="9d24c-115">有了這些資料夾之後，您接著參考 `.nuspec` 中的所有檔案：</span><span class="sxs-lookup"><span data-stu-id="9d24c-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="9d24c-116">使用此方法的其中一個範例套件是 [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0)。</span><span class="sxs-lookup"><span data-stu-id="9d24c-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="9d24c-117">優點和缺點 (當地語系化的資源組件)</span><span class="sxs-lookup"><span data-stu-id="9d24c-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="9d24c-118">將所有語言組合在單一套件中有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="9d24c-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="9d24c-119">**共用中繼資料**：因為 NuGet 套件只能包含單一 `.nuspec` 檔案，所以您只能為單一語言提供中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d24c-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="9d24c-120">也就是說，NuGet 不會支援當地語系化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d24c-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="9d24c-121">**套件大小**：根據您所支援的語言數目，程式庫可能會變得相當大，這會減慢安裝和還原套件的速度。</span><span class="sxs-lookup"><span data-stu-id="9d24c-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="9d24c-122">**同時發行**：將當地語系化檔案組合成單一套件，需要您同時發行該套件中的所有資產，而不是可以個別發行每個當地語系化。</span><span class="sxs-lookup"><span data-stu-id="9d24c-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="9d24c-123">此外，任何一個當地語系化的任何更新都需要整個套件的新版本。</span><span class="sxs-lookup"><span data-stu-id="9d24c-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="9d24c-124">不過，它也有幾個優點：</span><span class="sxs-lookup"><span data-stu-id="9d24c-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="9d24c-125">**簡單**：套件的取用者會取得單一安裝中所有支援的語言，而不需要個別安裝每種語言。</span><span class="sxs-lookup"><span data-stu-id="9d24c-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="9d24c-126">在 nuget.org 上也較容易找到單一套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="9d24c-127">**結合版本**：因為所有資源組件都位在與主要組件相同的套件中，所以它們全都會共用相同的版本號碼，而且沒有錯誤分離的風險。</span><span class="sxs-lookup"><span data-stu-id="9d24c-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="9d24c-128">當地語系化附屬套件</span><span class="sxs-lookup"><span data-stu-id="9d24c-128">Localized satellite packages</span></span>

<span data-ttu-id="9d24c-129">與 .NET Framework 如何支援附屬組件類似，此方法會將當地語系化資源和 IntelliSense XML 檔案區隔到附屬套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="9d24c-130">至此，您的主要套件會使用命名慣例 `{identifier}.{version}.nupkg`，並包含預設語言 (例如 en-US) 的組件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="9d24c-131">例如，`ContosoUtilities.1.0.0.nupkg` 會包含下列結構：</span><span class="sxs-lookup"><span data-stu-id="9d24c-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="9d24c-132">附屬組件接著會使用命名慣例 `{identifier}.{language}.{version}.nupkg` (例如 `ContosoUtilities.de.1.0.0.nupkg`)。</span><span class="sxs-lookup"><span data-stu-id="9d24c-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="9d24c-133">識別碼**必須**完全符合主要套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d24c-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="9d24c-134">因為這是不同的套件，所以它的專屬 `.nuspec` 檔案會包含當地語系化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d24c-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="9d24c-135">請注意， 中的語言`.nuspec` **必須**符合檔案名稱中所使用的語言。</span><span class="sxs-lookup"><span data-stu-id="9d24c-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="9d24c-136">附屬組件也**必須**使用 [] 版本標記法將主要套件的確切版本宣告為相依性 (請參閱[套件版本控制](../concepts/package-versioning.md))。</span><span class="sxs-lookup"><span data-stu-id="9d24c-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="9d24c-137">例如，`ContosoUtilities.de.1.0.0.nupkg` 必須使用 `[1.0.0]` 標記法來宣告與 `ContosoUtilities.1.0.0.nupkg` 的相依性。</span><span class="sxs-lookup"><span data-stu-id="9d24c-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="9d24c-138">附屬套件的版本號碼當然可以與主要套件的版本號碼不同。</span><span class="sxs-lookup"><span data-stu-id="9d24c-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="9d24c-139">附屬套件的結構接著必須包含套件檔案名稱中符合 `{language}` 之子資料夾中的資源組件和 XML IntelliSense 檔案：</span><span class="sxs-lookup"><span data-stu-id="9d24c-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="9d24c-140">**注意**：除非需要 `ja-JP` 這類特定子文化特性，否則一律會使用較高層的語言識別碼 (例如 `ja`)。</span><span class="sxs-lookup"><span data-stu-id="9d24c-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="9d24c-141">在附屬組件中，NuGet **只**會辨識檔案名稱中符合 `{language}` 之資料夾中的這些檔案。</span><span class="sxs-lookup"><span data-stu-id="9d24c-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="9d24c-142">其他所有項目都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="9d24c-142">All others are ignored.</span></span>

<span data-ttu-id="9d24c-143">符合所有這些慣例時，NuGet 會將套件辨識為附屬套件，並將當地語系化檔案安裝到主要套件的 `lib` 資料夾，就像它們一開始就已組合一樣。</span><span class="sxs-lookup"><span data-stu-id="9d24c-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="9d24c-144">解除安裝附屬套件將會從該相同資料夾中移除其檔案。</span><span class="sxs-lookup"><span data-stu-id="9d24c-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="9d24c-145">您可以使用相同的方式，針對每個支援的語言建立其他附屬組件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="9d24c-146">如需範例，請檢查 ASP.NET MVC 套件集：</span><span class="sxs-lookup"><span data-stu-id="9d24c-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="9d24c-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (英文主要)</span><span class="sxs-lookup"><span data-stu-id="9d24c-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="9d24c-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (德文)</span><span class="sxs-lookup"><span data-stu-id="9d24c-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="9d24c-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (日文)</span><span class="sxs-lookup"><span data-stu-id="9d24c-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="9d24c-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (簡體中文)</span><span class="sxs-lookup"><span data-stu-id="9d24c-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="9d24c-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (繁體中文)</span><span class="sxs-lookup"><span data-stu-id="9d24c-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="9d24c-152">必要慣例的摘要</span><span class="sxs-lookup"><span data-stu-id="9d24c-152">Summary of required conventions</span></span>

- <span data-ttu-id="9d24c-153">主要套件必須命名為 `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9d24c-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="9d24c-154">附屬套件必須命名為 `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9d24c-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="9d24c-155">附屬套件的 `.nuspec` 必須指定其語言符合檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="9d24c-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="9d24c-156">附屬套件必須在其 `.nuspec` 檔案中使用 [] 標記法宣告與主要套件之確切版本的相依性。</span><span class="sxs-lookup"><span data-stu-id="9d24c-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="9d24c-157">不支援範圍。</span><span class="sxs-lookup"><span data-stu-id="9d24c-157">Ranges are not supported.</span></span>
- <span data-ttu-id="9d24c-158">附屬套件必須將檔案放在完全符合檔案名稱中 `{language}` 的 `lib\[{framework}\]{language}` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="9d24c-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="9d24c-159">優點和缺點 (附屬套件)</span><span class="sxs-lookup"><span data-stu-id="9d24c-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="9d24c-160">使用附屬套件有幾個優點：</span><span class="sxs-lookup"><span data-stu-id="9d24c-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="9d24c-161">**套件大小**：主要套件的整體使用量會降到最低，而且取用者只會造成他們想要使用之每種語言的成本。</span><span class="sxs-lookup"><span data-stu-id="9d24c-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="9d24c-162">**區隔中繼資料**：每個附屬套件都有它的專屬 `.nuspec` 檔案，因此包含它的專屬當地語系化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9d24c-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="9d24c-163">這可讓部分取用者使用當地語系化詞彙來搜尋 nuget.org，更輕鬆地找到套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="9d24c-164">**低耦合版本**：可在一段時間內 (而非同時) 發行附屬組件，以讓您散發當地語系化工作。</span><span class="sxs-lookup"><span data-stu-id="9d24c-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="9d24c-165">不過，附屬套件有自己的一組缺點：</span><span class="sxs-lookup"><span data-stu-id="9d24c-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="9d24c-166">**雜亂**：您有許多套件可能導致 nuget.org 的搜尋結果雜亂，以及 Visual Studio 專案中的參考清單較長，而不是單一套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="9d24c-167">**嚴格慣例**.</span><span class="sxs-lookup"><span data-stu-id="9d24c-167">**Strict conventions**.</span></span> <span data-ttu-id="9d24c-168">附屬套件必須完全遵循慣例，否則無法正確反映當地語系化版本。</span><span class="sxs-lookup"><span data-stu-id="9d24c-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="9d24c-169">**版本控制**：每個附屬套件都必須具有與主要套件的確切版本相依性。</span><span class="sxs-lookup"><span data-stu-id="9d24c-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="9d24c-170">這表示，即使資源未變更，更新主要套件時也可能需要更新所有附屬套件。</span><span class="sxs-lookup"><span data-stu-id="9d24c-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
