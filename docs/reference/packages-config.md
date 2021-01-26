---
title: NuGet packages.config 檔案參考
description: 在某些專案類型中，packages.config 會維護專案中所使用的 NuGet 套件清單。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3e5db779f735cd42aa331f9f8a93496d32c8df54
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777628"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="1fb8e-103">packages.config 參考</span><span class="sxs-lookup"><span data-stu-id="1fb8e-103">packages.config reference</span></span>

<span data-ttu-id="1fb8e-104">`packages.config` 檔案用於某些專案類型，以維護專案所參考的套件清單。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="1fb8e-105">將專案傳輸至沒有所有這些套件的不同電腦 (例如組建伺服器) 時，這可讓 NuGet 輕鬆地還原專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="1fb8e-106">如果使用的話， `packages.config` 通常位於專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="1fb8e-107">當第一個 NuGet 作業執行時，它會自動建立，但也可以在執行任何命令（例如）之前手動建立 `nuget restore` 。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="1fb8e-108">使用 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 的專案不會使用 `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="1fb8e-109">結構描述</span><span class="sxs-lookup"><span data-stu-id="1fb8e-109">Schema</span></span>

<span data-ttu-id="1fb8e-110">結構描述十分簡單：標準 XML 標頭後面是包含一或多個 `<package>` 項目的單一 `<packages>` 節點，而每個參考都會有一個。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="1fb8e-111">每個 `<package>` 項目都可以有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="1fb8e-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="1fb8e-112">屬性</span><span class="sxs-lookup"><span data-stu-id="1fb8e-112">Attribute</span></span> | <span data-ttu-id="1fb8e-113">必要</span><span class="sxs-lookup"><span data-stu-id="1fb8e-113">Required</span></span> | <span data-ttu-id="1fb8e-114">描述</span><span class="sxs-lookup"><span data-stu-id="1fb8e-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fb8e-115">id</span><span class="sxs-lookup"><span data-stu-id="1fb8e-115">id</span></span> | <span data-ttu-id="1fb8e-116">是</span><span class="sxs-lookup"><span data-stu-id="1fb8e-116">Yes</span></span> | <span data-ttu-id="1fb8e-117">套件的識別碼，例如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="1fb8e-118">version</span><span class="sxs-lookup"><span data-stu-id="1fb8e-118">version</span></span> | <span data-ttu-id="1fb8e-119">是</span><span class="sxs-lookup"><span data-stu-id="1fb8e-119">Yes</span></span> | <span data-ttu-id="1fb8e-120">要安裝之套件的確切版本，例如 3.1.1 或 4.2.5.11-beta。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="1fb8e-121">版本字串必須包含至少三個數字；第四個數字是選擇性的，即發行前版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="1fb8e-122">不允許使用範圍。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="1fb8e-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="1fb8e-123">targetFramework</span></span> | <span data-ttu-id="1fb8e-124">否</span><span class="sxs-lookup"><span data-stu-id="1fb8e-124">No</span></span> | <span data-ttu-id="1fb8e-125">要在安裝套件時套用的[目標架構 Moniker (TFM)](target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="1fb8e-126">安裝套件時，這一開始設定為專案的目標。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="1fb8e-127">因此，不同 `<package>` 項目可以有不同 TFM。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="1fb8e-128">例如，如果您所建立專案的目標設為 .NET 4.5.2，則當時所安裝的套件將會使用 net452 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="1fb8e-129">如果您稍後將專案的目標重設為 .NET 4.6，並新增更多套件，則它們會使用 net46 的 TFM。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="1fb8e-130">專案目標與 `targetFramework` 屬性之間的不相容將會產生警告，在此情況下，您可以重新安裝受影響的套件。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="1fb8e-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="1fb8e-131">allowedVersions</span></span> | <span data-ttu-id="1fb8e-132">否</span><span class="sxs-lookup"><span data-stu-id="1fb8e-132">No</span></span> | <span data-ttu-id="1fb8e-133">此套件在套件更新期間套用的允許版本範圍 (請參閱[限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="1fb8e-134">它「不」會影響在安裝或還原作業期間所安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="1fb8e-135">如需語法，請參閱[套件版本控制](../concepts/package-versioning.md#version-ranges)。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="1fb8e-136">PackageManager UI 也會停用允許範圍之外的所有版本。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="1fb8e-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="1fb8e-137">developmentDependency</span></span> | <span data-ttu-id="1fb8e-138">否</span><span class="sxs-lookup"><span data-stu-id="1fb8e-138">No</span></span> | <span data-ttu-id="1fb8e-139">如果取用專案本身會建立 NuGet 套件，則將相依性的這個項目設定為 `true` 可在建立取用套件時防止包含該套件。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="1fb8e-140">預設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="1fb8e-141">範例</span><span class="sxs-lookup"><span data-stu-id="1fb8e-141">Examples</span></span>

<span data-ttu-id="1fb8e-142">下列 `packages.config` 參照兩個相依性：</span><span class="sxs-lookup"><span data-stu-id="1fb8e-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="1fb8e-143">下列 `packages.config` 參照九個套件，但因 `developmentDependency` 屬性而建置取用套件時不會包含 `Microsoft.Net.Compilers`。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="1fb8e-144">Newtonsoft.Json 的參考也只會限制 8.x 和 9.x 版的更新。</span><span class="sxs-lookup"><span data-stu-id="1fb8e-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
