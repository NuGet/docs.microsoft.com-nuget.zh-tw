---
title: NuGet 的 project.json 檔案參考
description: 在某些專案類型中，project.json 會維護專案中所使用的 NuGet 套件清單。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e558bdb969d4c70f85a3c89a426f1c7b11525402
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817121"
---
# <a name="projectjson-reference"></a><span data-ttu-id="7eb78-103">project.json 參考</span><span class="sxs-lookup"><span data-stu-id="7eb78-103">project.json reference</span></span>

<span data-ttu-id="7eb78-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="7eb78-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="7eb78-105">`project.json` 檔案維護一份專案中使用的套件之清單，稱為套件管理格式。</span><span class="sxs-lookup"><span data-stu-id="7eb78-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="7eb78-106">它會取代 `packages.config`，但又被 NuGet 4.0+ 的 [PackageReference](../consume-packages/package-references-in-project-files.md) 所取代。</span><span class="sxs-lookup"><span data-stu-id="7eb78-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="7eb78-107">[`project.lock.json`](#projectlockjson) 檔案 (如下所述) 也用於採用 `project.json` 的專案。</span><span class="sxs-lookup"><span data-stu-id="7eb78-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="7eb78-108">`project.json` 有下列的基本結構，其中四個最上層物件每個都可以有任意數目的子物件：</span><span class="sxs-lookup"><span data-stu-id="7eb78-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="7eb78-109">相依性</span><span class="sxs-lookup"><span data-stu-id="7eb78-109">Dependencies</span></span>

<span data-ttu-id="7eb78-110">以下列形式，列出您專案的 NuGet 套件相依性：</span><span class="sxs-lookup"><span data-stu-id="7eb78-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="7eb78-111">例如: </span><span class="sxs-lookup"><span data-stu-id="7eb78-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="7eb78-112">`dependencies` 區段是 [NuGet 套件管理員] 對話方塊將套件相依性新增到專案的位置。</span><span class="sxs-lookup"><span data-stu-id="7eb78-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="7eb78-113">套件識別碼對應至 nuget.org 上的套件識別碼，與套件管理員主控台中使用的識別碼相同：`Install-Package Microsoft.NETCore`。</span><span class="sxs-lookup"><span data-stu-id="7eb78-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="7eb78-114">還原套件時，`"5.0.0"` 的版本條件約束意味著 `>= 5.0.0`。</span><span class="sxs-lookup"><span data-stu-id="7eb78-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="7eb78-115">也就是說，如果伺服器上未提供 5.0.0，但有提供 5.0.1，則 NuGet 會安裝 5.0.1，而且會警告您有關此升級。</span><span class="sxs-lookup"><span data-stu-id="7eb78-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="7eb78-116">否則 NuGet 會在符合條件約束的伺服器上挑選最低的可能版本。</span><span class="sxs-lookup"><span data-stu-id="7eb78-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="7eb78-117">如需解析規則的詳細資料，請參閱[相依性解析](../consume-packages/dependency-resolution.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb78-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="7eb78-118">管理相依性資產</span><span class="sxs-lookup"><span data-stu-id="7eb78-118">Managing dependency assets</span></span>

<span data-ttu-id="7eb78-119">相依性的哪些資產流入最上層專案，是藉由在相依性參考的 `include` 和 `exclude` 屬性指定以逗號分隔的標記集合來控制。</span><span class="sxs-lookup"><span data-stu-id="7eb78-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="7eb78-120">標記會列在下列資料表中：</span><span class="sxs-lookup"><span data-stu-id="7eb78-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="7eb78-121">包含/排除標記</span><span class="sxs-lookup"><span data-stu-id="7eb78-121">Include/Exclude tag</span></span> | <span data-ttu-id="7eb78-122">目標的受影響資料夾</span><span class="sxs-lookup"><span data-stu-id="7eb78-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="7eb78-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7eb78-123">contentFiles</span></span> | <span data-ttu-id="7eb78-124">內容</span><span class="sxs-lookup"><span data-stu-id="7eb78-124">Content</span></span>  |
| <span data-ttu-id="7eb78-125">執行階段</span><span class="sxs-lookup"><span data-stu-id="7eb78-125">runtime</span></span> | <span data-ttu-id="7eb78-126">執行階段、資源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7eb78-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="7eb78-127">compile</span><span class="sxs-lookup"><span data-stu-id="7eb78-127">compile</span></span> | <span data-ttu-id="7eb78-128">lib</span><span class="sxs-lookup"><span data-stu-id="7eb78-128">lib</span></span> |
| <span data-ttu-id="7eb78-129">build</span><span class="sxs-lookup"><span data-stu-id="7eb78-129">build</span></span> | <span data-ttu-id="7eb78-130">組建 (MSBuild props 和目標)</span><span class="sxs-lookup"><span data-stu-id="7eb78-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="7eb78-131">native</span><span class="sxs-lookup"><span data-stu-id="7eb78-131">native</span></span> | <span data-ttu-id="7eb78-132">native</span><span class="sxs-lookup"><span data-stu-id="7eb78-132">native</span></span> |
| <span data-ttu-id="7eb78-133">無</span><span class="sxs-lookup"><span data-stu-id="7eb78-133">none</span></span> | <span data-ttu-id="7eb78-134">無資料夾</span><span class="sxs-lookup"><span data-stu-id="7eb78-134">No folders</span></span> |
| <span data-ttu-id="7eb78-135">全部</span><span class="sxs-lookup"><span data-stu-id="7eb78-135">all</span></span> | <span data-ttu-id="7eb78-136">全部資料夾</span><span class="sxs-lookup"><span data-stu-id="7eb78-136">All folders</span></span> |

<span data-ttu-id="7eb78-137">以 `exclude` 指定的標記優先於以 `include` 指定的標記。</span><span class="sxs-lookup"><span data-stu-id="7eb78-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="7eb78-138">例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="7eb78-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="7eb78-139">例如，若要包含相依性的 `build` 和 `native` 資料夾，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="7eb78-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="7eb78-140">若要排除相依性的 `content` 和 `build` 資料夾，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="7eb78-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="7eb78-141">架構</span><span class="sxs-lookup"><span data-stu-id="7eb78-141">Frameworks</span></span>

<span data-ttu-id="7eb78-142">列出專案執行所在的架構，例如 `net45`、`netcoreapp`、`netstandard`。</span><span class="sxs-lookup"><span data-stu-id="7eb78-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="7eb78-143">在 `frameworks` 區段中只允許單一項目。</span><span class="sxs-lookup"><span data-stu-id="7eb78-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="7eb78-144">(有一項例外就是使用已淘汰的 DNX 工具鏈建置之 ASP.NET 專案的 `project.json` 檔，它允許多個目標。)</span><span class="sxs-lookup"><span data-stu-id="7eb78-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="7eb78-145">執行階段</span><span class="sxs-lookup"><span data-stu-id="7eb78-145">Runtimes</span></span>

<span data-ttu-id="7eb78-146">列出您的應用程式執行所在的作業系統和架構，例如 `win10-arm`、`win8-x64`、`win8-x86`。</span><span class="sxs-lookup"><span data-stu-id="7eb78-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="7eb78-147">包含可在任何執行階段上執行之 PCL 的套件不需要指定執行階段。</span><span class="sxs-lookup"><span data-stu-id="7eb78-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="7eb78-148">任何相依性也必須都是如此，否則您必須指定執行階段。</span><span class="sxs-lookup"><span data-stu-id="7eb78-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="7eb78-149">Supports</span><span class="sxs-lookup"><span data-stu-id="7eb78-149">Supports</span></span>

<span data-ttu-id="7eb78-150">定義一組套件相依性檢查。</span><span class="sxs-lookup"><span data-stu-id="7eb78-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="7eb78-151">您可以定義您預期 PCL 或應用程式執行的位置。</span><span class="sxs-lookup"><span data-stu-id="7eb78-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="7eb78-152">定義沒有限制，因為您的程式碼可能能夠在其他位置執行。</span><span class="sxs-lookup"><span data-stu-id="7eb78-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="7eb78-153">但是，指定這些檢查可以讓 NuGet 確認在列出的 TxM 上符合所有相依性。</span><span class="sxs-lookup"><span data-stu-id="7eb78-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="7eb78-154">此值的範例有 `net46.app`、`uwp.10.0.app` 等等。</span><span class="sxs-lookup"><span data-stu-id="7eb78-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="7eb78-155">當您在可攜式類別庫目標對話方塊中選取一個項目時，應該會自動填入此區段。</span><span class="sxs-lookup"><span data-stu-id="7eb78-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="7eb78-156">Imports</span><span class="sxs-lookup"><span data-stu-id="7eb78-156">Imports</span></span>

<span data-ttu-id="7eb78-157">Imports 設計目的是為了讓使用 `dotnet` TxM 的套件能和未宣告 dotnet TxM 的套件一起運作。</span><span class="sxs-lookup"><span data-stu-id="7eb78-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="7eb78-158">如果您的專案使用 `dotnet` TxM，除非您將下列內容新增至 `project.json`，以讓非 `dotnet` 平台變成能與 `dotnet` 相容，否則您相依的所有套件也必須要有 `dotnet` TxM：</span><span class="sxs-lookup"><span data-stu-id="7eb78-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="7eb78-159">如果您使用 `dotnet` TxM，則 PCL 專案系統會根據支援的目標，新增適當的 `imports` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7eb78-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="7eb78-160">與可攜式應用程式和 Web 專案的差異</span><span class="sxs-lookup"><span data-stu-id="7eb78-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="7eb78-161">NuGet 所使用的 `project.json` 檔案，是在 ASP.NET Core 專案中找到的檔案子集。</span><span class="sxs-lookup"><span data-stu-id="7eb78-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="7eb78-162">在 ASP.NET Core 中，`project.json` 用於專案中繼資料、編譯資訊，以及相依性。</span><span class="sxs-lookup"><span data-stu-id="7eb78-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="7eb78-163">用於其他專案系統時，這三項會分成不同的檔案，且 `project.json` 會包含較少資訊。</span><span class="sxs-lookup"><span data-stu-id="7eb78-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="7eb78-164">值得注意的差異包括：</span><span class="sxs-lookup"><span data-stu-id="7eb78-164">Notable differences include:</span></span>

- <span data-ttu-id="7eb78-165">在 `frameworks` 區段只能有一個架構。</span><span class="sxs-lookup"><span data-stu-id="7eb78-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="7eb78-166">檔案不能包含您在 DNX `project.json` 檔案看到的相依性、編譯選項等等。</span><span class="sxs-lookup"><span data-stu-id="7eb78-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="7eb78-167">假設只能有單一架構，輸入特定架構的相依性便沒有意義。</span><span class="sxs-lookup"><span data-stu-id="7eb78-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="7eb78-168">編譯由 MSBuild 處理，所以編譯選項、前置處理器定義等都是屬於 MSBuild 專案檔，而非 `project.json`。</span><span class="sxs-lookup"><span data-stu-id="7eb78-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="7eb78-169">在 NuGet 3+ 中，開發人員不應該手動編輯 `project.json`，因為 Visual Studio 中的套件管理員 UI 會操作其內容。</span><span class="sxs-lookup"><span data-stu-id="7eb78-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="7eb78-170">話雖如此，您確實可以編輯檔案，但您必須建置專案以啟動套件還原，或以另一種方式叫用還原。</span><span class="sxs-lookup"><span data-stu-id="7eb78-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="7eb78-171">請參閱[套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb78-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="7eb78-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="7eb78-172">project.lock.json</span></span>

<span data-ttu-id="7eb78-173">在使用 `project.json` 的專案中還原 NuGet 套件的過程，會產生 `project.lock.json` 檔。</span><span class="sxs-lookup"><span data-stu-id="7eb78-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="7eb78-174">它保留當 NuGet 逐步檢查套件的圖形時所產生的所有資訊快照集，並且包含您專案中所有套件的版本、內容和相依性。</span><span class="sxs-lookup"><span data-stu-id="7eb78-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="7eb78-175">在建置專案時，組建系統用這來從相關全域位置選擇套件，而不依賴專案本身的本機 packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7eb78-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="7eb78-176">這會導致更快的組建效能，因為只需要讀取 `project.lock.json`，而不是許多個不同的 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7eb78-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="7eb78-177">`project.lock.json` 會在套件還原時自動產生，所以可以從原始檔控制中省略，方法是將它新增至 `.gitignore` 和 `.tfignore` 檔案 (請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb78-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="7eb78-178">不過，如果您將它包含在原始檔控制中，變更歷程記錄會顯示在一段時間解析的相依性變化。</span><span class="sxs-lookup"><span data-stu-id="7eb78-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
