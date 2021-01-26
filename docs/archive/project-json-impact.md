---
title: project.json 對 NuGet 套件作者的影響
description: NuGet 3.x 中的 project.json 實作如何影響套件作者的詳細資料，例如不支援的功能、內容以及套件格式。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 82b7ce7962ecccc9559ae25a8fe35a3820238049
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775395"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="0ebbb-103">建立套件時 project.json 的影響</span><span class="sxs-lookup"><span data-stu-id="0ebbb-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="0ebbb-104">此內容已過時。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-104">This content is deprecated.</span></span> <span data-ttu-id="0ebbb-105">專案應使用 `packages.config` 或 PackageReference 格式。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="0ebbb-106">NuGet 3+ 中使用的 `project.json` 系統在很多方面會影響套件作者，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="0ebbb-107">影響現有套件使用方式的變更</span><span class="sxs-lookup"><span data-stu-id="0ebbb-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="0ebbb-108">傳統的 NuGet 套件支援一組不會保留到過渡環境的功能。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="0ebbb-109">安裝和解除安裝指令碼都予以忽略</span><span class="sxs-lookup"><span data-stu-id="0ebbb-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="0ebbb-110">過渡的還原模型，如[相依性解析](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)中所述，沒有「套件安裝時間」的概念。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="0ebbb-111">無論套件是否存在，安裝套件時，都不會出現任何一致的程序。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="0ebbb-112">此外，僅 Visual Studio 支援安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="0ebbb-113">其他 IDE 必須模擬 Visual Studio 擴充性 API 嘗試支援這類指令碼，一般編輯器和命令列工具中不提供支援。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="0ebbb-114">不支援內容轉換</span><span class="sxs-lookup"><span data-stu-id="0ebbb-114">Content transforms are not supported</span></span>

<span data-ttu-id="0ebbb-115">與安裝指令碼相類似，在套件安裝上執行的轉換通常不是等冪。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="0ebbb-116">因為不再有安裝時間，所以如果過渡案例使用這類套件，就不支援並會忽略 XDT 轉換和類似的功能。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="0ebbb-117">Content</span><span class="sxs-lookup"><span data-stu-id="0ebbb-117">Content</span></span>

<span data-ttu-id="0ebbb-118">傳統的 NuGet 套件傳送內容檔案，例如原始程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="0ebbb-119">通常用在兩個案例中：</span><span class="sxs-lookup"><span data-stu-id="0ebbb-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="0ebbb-120">放入專案的初始檔案，讓使用者可稍後編輯它們。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="0ebbb-121">常見範例為預設的組態檔。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="0ebbb-122">內容檔案用為安裝在專案中的組件隨附產品。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="0ebbb-123">此處的範例是組件使用的標誌影像。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="0ebbb-124">因類似原因，指令碼和轉換目前已停用內容支援，但我們正在努力設計內容支援。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="0ebbb-125">內容檔案仍然可以載入套件中，且目前仍予忽略，不過使用者仍可以將其複製到正確的位置。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="0ebbb-126">您可以看到其中一個用來導回內容檔案的提案，並遵循其進度，如下所示： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627) 。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="0ebbb-127">對套件作者的影響</span><span class="sxs-lookup"><span data-stu-id="0ebbb-127">Impact for package authors</span></span>

<span data-ttu-id="0ebbb-128">使用上述功能的套件必須使用不同的機制。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="0ebbb-129">最常用的機制是持續獲得完整支援的 MSBuild 目標/props。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="0ebbb-130">組建系統可以選擇挑選套件中的其他慣例。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="0ebbb-131">這是 MSBuild 目標以及 Roslyn 分析器的支援方式。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="0ebbb-132">您可以建置套件，支援 `packages.config` 和 `project.json` 案例的目標和分析器。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="0ebbb-133">嘗試修改專案以簡化啟動的套件，能夠作用的情況一般非常有限，應該改為提供有關如何使用套件的讀我檔案或指引。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="0ebbb-134">現有的套件大部分應該不需要使用下文描述的套件格式。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="0ebbb-135">格式會讓原生內容成為第一級案例。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="0ebbb-136">這表示受控組件相當仰賴硬體實作，以根據目標平台來送出受控組件及二進位實作。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="0ebbb-137">例如，System.IO.Compression 套件就是使用這項技術。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="0ebbb-138">在摘要中，如果上述功能不是絕對必要，建議您繼續使用現有的套件格式，因為這裡描述的格式只有 NuGet 3.x+ 支援。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="0ebbb-139">您可以透過填充建置套件以用於 `packages.config` 和 `project.json` 案例，不過以傳統方法建構套件通常比較簡單，不需要使用上述的過時功能。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="0ebbb-140">3.x 套件格式</span><span class="sxs-lookup"><span data-stu-id="0ebbb-140">3.x package format</span></span>

<span data-ttu-id="0ebbb-141">3.x 套件格式允許數個超越 NuGet 2.x 的其他功能：</span><span class="sxs-lookup"><span data-stu-id="0ebbb-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="0ebbb-142">定義用於編譯的參考組件，和一組用於不同平台/裝置執行階段的實作組件。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="0ebbb-143">可讓您充分利用平台特定的 API，同時為您的取用者提供常見的介面區。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="0ebbb-144">具體而言，這讓撰寫中繼可攜式程式庫變得更容易。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="0ebbb-145">讓套件對平台進行樞紐分析，例如作業系統或 CPU 架構。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="0ebbb-146">讓您分隔附屬套件的平台特定實作。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="0ebbb-147">支援原生相依性成為第一級成員。</span><span class="sxs-lookup"><span data-stu-id="0ebbb-147">Support Native dependencies as a first class citizen.</span></span>
