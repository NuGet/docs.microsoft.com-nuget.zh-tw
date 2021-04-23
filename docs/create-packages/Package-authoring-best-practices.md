---
title: 封裝撰寫的最佳作法
description: 建立高品質 NuGet 套件的最佳作法一般指南。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 358e574339688514448b684aadc6911f9d83611f
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901443"
---
# <a name="package-authoring-best-practices"></a><span data-ttu-id="c6a1d-103">封裝撰寫的最佳作法</span><span class="sxs-lookup"><span data-stu-id="c6a1d-103">Package authoring best practices</span></span>

<span data-ttu-id="c6a1d-104">本指南的目的是要為 NuGet 套件作者提供建立和發佈高品質套件的輕量參考。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-104">This guidance is intended to give NuGet package authors a lightweight reference to create and publish high-quality packages.</span></span> <span data-ttu-id="c6a1d-105">它主要會著重于封裝特定的最佳作法，例如中繼資料和封裝。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-105">It will primarily focus on package-specific best practices such as metadata and packing.</span></span> <span data-ttu-id="c6a1d-106">如需建立高品質程式庫的更深入建議，請參閱 .NET [開放原始碼程式庫指引](/dotnet/standard/library-guidance/)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-106">For more in-depth suggestions for building high quality libraries, see the .NET [Open-source library guidance](/dotnet/standard/library-guidance/).</span></span>

## <a name="types-of-recommendations"></a><span data-ttu-id="c6a1d-107">建議類型</span><span class="sxs-lookup"><span data-stu-id="c6a1d-107">Types of recommendations</span></span>

<span data-ttu-id="c6a1d-108">每篇文章都呈現四種類型的建議：**優先**、**考慮**、**避免** 與 **禁止**。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-108">Each article presents four types of recommendations: **Do**, **Consider**, **Avoid**, and **Do not**.</span></span> <span data-ttu-id="c6a1d-109">建議的類型指出應遵循的程度。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-109">The type of recommendation indicates how closely it should be followed.</span></span>

<span data-ttu-id="c6a1d-110">您應該一律遵循 **優先** 類型的建議。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-110">You should almost always follow a **Do** recommendation.</span></span> <span data-ttu-id="c6a1d-111">例如：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-111">For example:</span></span>

<span data-ttu-id="c6a1d-112">✔️包含描述其用途之套件的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-112">✔️ DO include a short description for your package that describes what it's for.</span></span>

<span data-ttu-id="c6a1d-113">相反地，請 **考慮** 建議一般遵循建議，但規則有合法的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-113">On the other hand, **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule:</span></span>

<span data-ttu-id="c6a1d-114">✔️ 請考慮選擇具有符合 NuGet 的前置詞保留[準則](../nuget-org/id-prefix-reservation.md)之前置詞的 NuGet 套件名稱。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-114">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's prefix reservation [criteria](../nuget-org/id-prefix-reservation.md).</span></span>

<span data-ttu-id="c6a1d-115">**避免** 建議指的是通常不建議採行的建議，但有時違反規則尚屬合理情況：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-115">**Avoid** recommendations mention things that are generally not a good idea, but breaking the rule sometimes makes sense:</span></span>

<span data-ttu-id="c6a1d-116">❌ 避免需要精確版本的 NuGet 套件參考。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-116">❌ AVOID NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="c6a1d-117">最後，**禁止** 類型的建議表示在多數情況下都不應採取的動作：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-117">And finally, **Do not** recommendations indicate something you should almost never do:</span></span>

<span data-ttu-id="c6a1d-118">❌ 請勿使用 `LicenseUrl` 中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-118">❌ DO NOT use the `LicenseUrl` metadata property.</span></span>

## <a name="create-a-nuget-package"></a><span data-ttu-id="c6a1d-119">建立 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c6a1d-119">Create a NuGet package</span></span>

<span data-ttu-id="c6a1d-120">建立 NuGet 套件的最新建議方法是從 [SDK 樣式專案](../resources/check-project-format.md)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-120">The latest recommended way to to create a NuGet package is from an [SDK-style project](../resources/check-project-format.md).</span></span> <span data-ttu-id="c6a1d-121">SDK 樣式的專案屬性（包括 [目標 framework](/dotnet/standard/frameworks) 和 [套件中繼資料](#package-metadata)）是在 [專案](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)檔中定義。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-121">SDK-style project properties, including [target framework](/dotnet/standard/frameworks) and [package metadata](#package-metadata), are defined in the [project file](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).</span></span>

<span data-ttu-id="c6a1d-122">在 [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) 或 [dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)中定義必要的屬性和封裝，以從您的 SDK 樣式專案建立套件。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-122">Create a package from your SDK-style project by defining the required properties and packing in [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) or the [dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="c6a1d-123">✔️確實會建立 SDK 樣式的專案，並使用 Visual Studio 或 dotnet CLI) 套件建立 (套件。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-123">✔️ DO create an SDK-style project and create (pack) your package using Visual Studio or the dotnet CLI.</span></span>

<span data-ttu-id="c6a1d-124">如需有關套件建立的詳細指引，包括必要的用戶端工具、專案檔範例和命令，請參閱 [使用 DOTNET CLI 建立 NuGet 套件](./creating-a-package-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-124">For more detailed guidance regarding package creation including necessary client tools, project file example, and commands, see [Create a NuGet package using the dotnet CLI](./creating-a-package-dotnet-cli.md).</span></span>

<span data-ttu-id="c6a1d-125">若要協助決定要作為目標的 .NET framework，請參閱我們 [的跨平臺目標的最新指導](/dotnet/standard/library-guidance/cross-platform-targeting)方針。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-125">To help decide which .NET frameworks to target, see our [latest guidance for cross-platform targeting](/dotnet/standard/library-guidance/cross-platform-targeting).</span></span>

## <a name="package-metadata"></a><span data-ttu-id="c6a1d-126">套件中繼資料</span><span class="sxs-lookup"><span data-stu-id="c6a1d-126">Package metadata</span></span>

<span data-ttu-id="c6a1d-127">中繼資料是任何 NuGet 套件的基礎元件。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-127">Metadata is a foundational component of any NuGet package.</span></span> <span data-ttu-id="c6a1d-128">您的中繼資料品質可能會大幅影響套件的可探索性、可用性和可信度。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-128">The quality of your metadata can vastly influence the discoverability, usability, and trustworthiness of your package.</span></span>

<span data-ttu-id="c6a1d-129">在 Visual Studio 中，指定套件中繼資料的建議方式是將專案 > [專案名稱] 屬性 > 封裝中。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-129">In Visual Studio, the recommended way to specify package metadata is to go Project > [Project Name] Properties > Package.</span></span>

<span data-ttu-id="c6a1d-130">您也可以 [直接在專案檔中指定](./creating-a-package-msbuild.md#set-properties)封裝中繼資料元素。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-130">Package metadata elements can also be [specified directly in the project file](./creating-a-package-msbuild.md#set-properties).</span></span>

<span data-ttu-id="c6a1d-131">以下是資料表對應和描述可用的封裝中繼資料元素：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-131">Below is a table mapping and describing available package metadata elements:</span></span>

| <span data-ttu-id="c6a1d-132">Visual Studio 屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c6a1d-132">Visual Studio property name</span></span>                       | [<span data-ttu-id="c6a1d-133">專案檔/MSBuild 屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c6a1d-133">Project file/ MSBuild property name</span></span>](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                            | [<span data-ttu-id="c6a1d-134">Nuspec 屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c6a1d-134">Nuspec property name</span></span>](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema)     | <span data-ttu-id="c6a1d-135">Description</span><span class="sxs-lookup"><span data-stu-id="c6a1d-135">Description</span></span>                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                          | <span data-ttu-id="c6a1d-136">封裝名稱或識別碼。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-136">The package name or identifier.</span></span>                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                    | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                                | <span data-ttu-id="c6a1d-137">NuGet 套件版本。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-137">NuGet package version.</span></span>                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                                   | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                                | <span data-ttu-id="c6a1d-138">以逗號分隔的套件作者清單，通常使用個人或組織的「美觀名稱」。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-138">A comma-separated list of package authors, often using the individual's or an organization's "pretty name."</span></span>           |
| [`Description`](#description)                     | [`Description`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                        | <span data-ttu-id="c6a1d-139">套件的描述。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-139">A description of the package.</span></span>                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                            | <span data-ttu-id="c6a1d-140">套件的著作權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-140">Copyright details for the package.</span></span>                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)   | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)              | <span data-ttu-id="c6a1d-141">SPDX 授權運算式。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-141">An SPDX license expression.</span></span>                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)         | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                    | <span data-ttu-id="c6a1d-142">自訂授權檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-142">Path to a custom license file.</span></span>                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                          | <span data-ttu-id="c6a1d-143">專案首頁的 URL。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-143">A URL for the project homepage.</span></span>                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                    | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                      | <span data-ttu-id="c6a1d-144">封裝圖示影像檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-144">Path to the package icon image file.</span></span>                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                      | <span data-ttu-id="c6a1d-145">用來建立封裝之來源存放庫的 URL。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-145">URL to the repository from which the package was built.</span></span>                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                   | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                     | <span data-ttu-id="c6a1d-146">存放庫 URL 指向 (也就是 "git" ) 的存放庫類型。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-146">Type of repository the repository URL is pointing to (i.e. "git").</span></span>                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                      | <span data-ttu-id="c6a1d-147">以空格分隔的標記與關鍵字清單，能描述套件。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-147">A space-delimited list of tags and keywords that describe the package.</span></span> <span data-ttu-id="c6a1d-148">標記會在搜尋套件時使用。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-148">Tags are used when searching for packages.</span></span>     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                           | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                      | <span data-ttu-id="c6a1d-149">這一版封裝中所做變更的描述。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-149">A description of the changes made in this release of the package.</span></span>                                                     |
### <a name="package-id"></a><span data-ttu-id="c6a1d-150">封裝識別碼</span><span class="sxs-lookup"><span data-stu-id="c6a1d-150">Package ID</span></span>

<span data-ttu-id="c6a1d-151">如果您要發佈全新的封裝：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-151">If you're publishing a completely new package:</span></span>

<span data-ttu-id="c6a1d-152">✔️選擇的套件識別碼是唯一的，而且與 NuGet.org 上現有的套件清楚區別。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-152">✔️ DO choose a package ID that is unique and clearly differentiated from existing packages on NuGet.org.</span></span>
> <span data-ttu-id="c6a1d-153">您可以藉由在 NuGet.org 上搜尋識別碼，或檢查下列連結是否存在來檢查封裝識別碼是否唯一和 differentiable： https://www.nuget.org/packages/<package name \> 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-153">You can check if a package ID is unique and differentiable by searching for the ID on NuGet.org or checking if the following link exists: https://www.nuget.org/packages/<package name\>.</span></span>

<span data-ttu-id="c6a1d-154">✔️考慮選擇具有符合 NuGet [首碼保留準則](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)之前置詞的 nuget 套件名稱。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-154">✔️ CONSIDER choosing a NuGet package name with a prefix that meets NuGet's [prefix reservation criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).</span></span>
> <span data-ttu-id="c6a1d-155">保留套件的前置詞識別碼，可讓您取得已驗證的核取記號： ![ 影像](media/Verified-check-mark.png)</span><span class="sxs-lookup"><span data-stu-id="c6a1d-155">Reserving the prefix ID for your package will let you get the verified check mark: ![image](media/Verified-check-mark.png)</span></span>
> 
> <span data-ttu-id="c6a1d-156">若要深入瞭解，請參閱 [套件識別碼前置詞保留檔](../nuget-org/id-prefix-reservation.md) 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-156">Check out the [Package ID prefix reservation docs](../nuget-org/id-prefix-reservation.md) to learn more.</span></span>

### <a name="package-version"></a><span data-ttu-id="c6a1d-157">封裝版本</span><span class="sxs-lookup"><span data-stu-id="c6a1d-157">Package Version</span></span>

<span data-ttu-id="c6a1d-158">✔️考慮使用 [SemVer](https://semver.org/) 來為您的 NuGet 套件版本。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-158">✔️ CONSIDER using [SemVer](https://semver.org/) to version your NuGet package.</span></span>
> <span data-ttu-id="c6a1d-159">基本上，這表示使用主要的. Patch [-搶鮮版（發行前版本）格式。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-159">Essentially, this means using the Major.Minor.Patch[-prerelease] format.</span></span>

<span data-ttu-id="c6a1d-160">如果封裝不穩定或處於預覽狀態，✔️會將套件發佈為 [發行前版本的套件](./prerelease-packages.md) 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-160">✔️ DO publish a package as a [pre-release package](./prerelease-packages.md) if it is non-stable or a preview.</span></span>

<span data-ttu-id="c6a1d-161">如需更先進的指引，請參閱 [.net 程式庫版本設定指南](/dotnet/standard/library-guidance/versioning) 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-161">See the [.NET library versioning guide](/dotnet/standard/library-guidance/versioning) for more advanced guidance.</span></span>

### <a name="authors"></a><span data-ttu-id="c6a1d-162">Authors</span><span class="sxs-lookup"><span data-stu-id="c6a1d-162">Authors</span></span>

<span data-ttu-id="c6a1d-163">✔️請將 [作者] 欄位用於您或您組織的「美觀名稱」。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-163">✔️ DO use the author field for your or your organization's "pretty name."</span></span>
> <span data-ttu-id="c6a1d-164">例如，如果我的 NuGet.org 使用者名稱是 "jdoe"，則針對作者欄位使用 "Jane Doe" 可協助取用者將我辨識為作者。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-164">For example, if my NuGet.org username is "jdoe" then using "Jane Doe" for the author field may help consumers recognize me as an author.</span></span> <span data-ttu-id="c6a1d-165">如果我組織的 NuGet.org 使用者名稱是 "ContosoToolkit"，則使用 "Contoso Corporation" 可能更容易辨識，並可激發更多消費者信任。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-165">If my organization's NuGet.org username is "ContosoToolkit" then using "Contoso Corporation" may be more recognizable and inspire more consumer trust.</span></span>
### <a name="description"></a><span data-ttu-id="c6a1d-166">Description</span><span class="sxs-lookup"><span data-stu-id="c6a1d-166">Description</span></span>

<span data-ttu-id="c6a1d-167">✔️包含 (最多4000個字元) 描述套件的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-167">✔️ DO include a short description (up to 4000 characters) to describe your package.</span></span>
> <span data-ttu-id="c6a1d-168">套件描述是 NuGet 搜尋中最重要的其中一個欄位，可能是潛在客戶的第一件事，就是判斷套件是否適合它們。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-168">Package descriptions are one of the most prominent fields surfaced in NuGet search and will likely be the first thing potential consumers looks at to determine if a package is right for them.</span></span>

### <a name="copyright"></a><span data-ttu-id="c6a1d-169">著作權</span><span class="sxs-lookup"><span data-stu-id="c6a1d-169">Copyright</span></span>

<span data-ttu-id="c6a1d-170">✔️考慮使用 "著作權 (c) <姓名/公司 <年份）來 copyrighting 您的套件 \> \> 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-170">✔️ CONSIDER copyrighting your package with "Copyright (c) <name/company\> <year\>."</span></span>
><span data-ttu-id="c6a1d-171">著作權注意事項基本上表示無法在沒有您的許可權的情況下複製您的工作。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-171">A copyright notice essentially indicates that your work cannot be copied without your permission.</span></span> <span data-ttu-id="c6a1d-172">您可以輕鬆地在套件中包含著作權聲明，而不會造成任何損害！</span><span class="sxs-lookup"><span data-stu-id="c6a1d-172">Including a copyright notice in your package is easy and won't do any harm!</span></span>

<span data-ttu-id="c6a1d-173">範例：著作權 (c) Contoso 2020</span><span class="sxs-lookup"><span data-stu-id="c6a1d-173">Example: Copyright (c) Contoso 2020</span></span>

### <a name="licensing"></a><span data-ttu-id="c6a1d-174">授權</span><span class="sxs-lookup"><span data-stu-id="c6a1d-174">Licensing</span></span>

<span data-ttu-id="c6a1d-175">✔️ [在您的封裝中包含授權運算式或授權檔案](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-175">✔️ DO [include a license expression or license file in your package](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c6a1d-176">沒有授權的專案預設為 [專有著作權](https://choosealicense.com/no-permission/)，表示您尚未授與任何人使用您專案的許可權。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-176">A project without a license defaults to [exclusive copyright](https://choosealicense.com/no-permission/), meaning that you have not granted anyone permission to use your project.</span></span>

<span data-ttu-id="c6a1d-177">❌ 請勿使用已被取代的 `LicenseUrl` 中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-177">❌ DO NOT use the deprecated `LicenseUrl` metadata property.</span></span>
> <span data-ttu-id="c6a1d-178">如此一來，當 URL 的授權變更追溯變更先前套件版本的顯示授權時，就會發生法律上的混淆。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-178">This presents legal ambiguity as license changes at the URL will retroactively change the displayed license for previous package versions.</span></span>

#### <a name="if-your-package-is-open-source"></a><span data-ttu-id="c6a1d-179">如果您的套件是[開放原始](https://opensource.org/osd)碼</span><span class="sxs-lookup"><span data-stu-id="c6a1d-179">If your package is [open source](https://opensource.org/osd)</span></span>

<span data-ttu-id="c6a1d-180">✔️ [選擇開放原始碼授權](https://choosealicense.com/) 以使套件成為開放原始碼。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-180">✔️ DO [choose an open source license](https://choosealicense.com/) to make your package open source.</span></span>
> <span data-ttu-id="c6a1d-181">*「開放原始碼授權是符合開放原始碼定義的授權-簡單來說，這些授權可讓軟體自由使用、修改及共用。」*</span><span class="sxs-lookup"><span data-stu-id="c6a1d-181">*"Open source licenses are licenses that comply with the Open Source Definition — in brief, they allow software to be freely used, modified, and shared."*</span></span> <span data-ttu-id="c6a1d-182">-開放原始碼計畫。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-182">- Open Source Initiative.</span></span> <span data-ttu-id="c6a1d-183">若要深入瞭解開放原始碼軟體和開放原始碼的計畫，請參閱 https://opensource.org/ 。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-183">To learn more about open source software and the Open Source Initiative, check out https://opensource.org/.</span></span>

<span data-ttu-id="c6a1d-184">✔️考慮 [將授權運算式包含在您的封裝中](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-184">✔️ CONSIDER [including a license expression in your package](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="c6a1d-185">如果授權運算式可以使用您的套件，或如果授權已變更，則會以更清楚的方式呈現授權運算式，並讓取用者更清楚。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-185">License expressions are surfaced the most clearly and make it more obvious to consumers if they can use your package or if the license has changed.</span></span> 
> [!Note]
> <span data-ttu-id="c6a1d-186">NuGet.org 只接受開放原始碼計畫或免費 Software Foundation 核准之授權的授權運算式。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-186">NuGet.org only accepts license expressions for licenses that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

#### <a name="if-your-package-is-not-open-source"></a><span data-ttu-id="c6a1d-187">如果您的套件不是開放原始碼</span><span class="sxs-lookup"><span data-stu-id="c6a1d-187">If your package is not open source</span></span>

<span data-ttu-id="c6a1d-188">✔️ [包含套件中的授權檔案](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-188">✔️ DO [include a license file in your package](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>
> <span data-ttu-id="c6a1d-189">任何 ( .txt 或 md) 的授權檔都可以新增至您的封裝，包括非標準授權。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-189">Any license file (.txt or .md) can be added to your package, including non-standard licenses.</span></span> 

### <a name="project-url"></a><span data-ttu-id="c6a1d-190">專案 URL</span><span class="sxs-lookup"><span data-stu-id="c6a1d-190">Project URL</span></span>

<span data-ttu-id="c6a1d-191">✔️考慮包含關聯專案、存放庫或公司網站的連結。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-191">✔️ CONSIDER including a link to an associated project, repository, or company website.</span></span>
> <span data-ttu-id="c6a1d-192">您的專案網站應該有使用者需要知道的套件，而且可能是使用者尋找檔的位置。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-192">Your project site should have everything users need to know about your package and will likely be where users look for documentation.</span></span>

### <a name="icon"></a><span data-ttu-id="c6a1d-193">圖示</span><span class="sxs-lookup"><span data-stu-id="c6a1d-193">Icon</span></span>

<span data-ttu-id="c6a1d-194">✔️考慮 [包含套件的圖示](../reference/msbuild-targets.md#packing-an-icon-image-file) ，以協助以視覺化方式區分。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-194">✔️ CONSIDER [including an icon with your package](../reference/msbuild-targets.md#packing-an-icon-image-file) to help visually differentiate it.</span></span> <span data-ttu-id="c6a1d-195">它是相對較小的加法，可改善對封裝品質的認知。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-195">It's a relatively small addition that can improve perception of package quality.</span></span>
> <span data-ttu-id="c6a1d-196">圖示可以特定于個別套件，也可以是品牌標誌。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-196">Icons can be specific to individual packages or be a brand logo.</span></span>

<span data-ttu-id="c6a1d-197">✔️使用128x128 的影像，並具有透明背景 (PNG) ，以獲得最佳的觀看結果。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-197">✔️ DO use an image that is 128x128 and has a transparent background (PNG) for best viewing results.</span></span>
> <span data-ttu-id="c6a1d-198">NuGet 會自動將您的映射調整為顯示的用戶端。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-198">NuGet will automatically scale your image to the client it is being displayed on.</span></span>

<span data-ttu-id="c6a1d-199">❌ 請勿使用已被取代的 `IconUrl` 中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-199">❌ DO NOT use the deprecated `IconUrl` metadata property.</span></span>

### <a name="repository-type-and-url"></a><span data-ttu-id="c6a1d-200">存放庫類型和 URL</span><span class="sxs-lookup"><span data-stu-id="c6a1d-200">Repository Type and URL</span></span>

<span data-ttu-id="c6a1d-201">✔️考慮設定 [來源連結](/dotnet/standard/library-guidance/sourcelink) ，以自動將原始檔控制中繼資料新增至您的 NuGet 套件，並讓您的程式庫更容易進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-201">✔️ CONSIDER setting up [Source Link](/dotnet/standard/library-guidance/sourcelink) to automatically add source control metadata to your NuGet package and make your library easier to debug.</span></span>
> <span data-ttu-id="c6a1d-202">來源連結會自動將 `Repository URL` 和新增 `Repository Type` 至套件中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-202">Source Link automatically adds `Repository URL` and `Repository Type` to the package metadata.</span></span> <span data-ttu-id="c6a1d-203">它也會新增與套件版本相關聯的特定認可。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-203">It also adds the specific commit associated with your package version.</span></span>

### <a name="tags"></a><span data-ttu-id="c6a1d-204">標籤</span><span class="sxs-lookup"><span data-stu-id="c6a1d-204">Tags</span></span>

<span data-ttu-id="c6a1d-205">✔️包含多個標記，其中包含與您的套件相關的重要詞彙，以增強可探索性。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-205">✔️ DO include several tags with key terms related to your package to enhance discoverability.</span></span>
> <span data-ttu-id="c6a1d-206">標籤會以 Nuget.exe 的搜尋演算法來考慮，對於不在封裝識別碼中但相關的詞彙特別有用。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-206">Tags are taken into account in NuGet.org's search algorithm and are especially helpful for terms that are not in the Package ID but are relevant.</span></span>

<span data-ttu-id="c6a1d-207">例如，如果我發佈了封裝以將字串記錄到主控台，就會包含：「記錄、記錄、主控台、字串、輸出」</span><span class="sxs-lookup"><span data-stu-id="c6a1d-207">For example, if I published a package to log strings to the console, I would include: "logging, log, console, string, output"</span></span>

### <a name="release-notes"></a><span data-ttu-id="c6a1d-208">版本資訊</span><span class="sxs-lookup"><span data-stu-id="c6a1d-208">Release notes</span></span>

<span data-ttu-id="c6a1d-209">✔️考慮包含版本資訊，其中每個更新都會描述所做的變更。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-209">✔️ CONSIDER including release notes with each update describing what changes were made.</span></span>
> <span data-ttu-id="c6a1d-210">雖然版本資訊不需要特定格式，但建議您包括：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-210">While there is no specific format required for release notes, we recommend including:</span></span>
>
> 1. <span data-ttu-id="c6a1d-211">重大變更</span><span class="sxs-lookup"><span data-stu-id="c6a1d-211">Breaking changes</span></span>
> 2. <span data-ttu-id="c6a1d-212">新功能</span><span class="sxs-lookup"><span data-stu-id="c6a1d-212">New features</span></span>
> 3. <span data-ttu-id="c6a1d-213">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="c6a1d-213">Bug fixes</span></span>
> 
> <span data-ttu-id="c6a1d-214">如果您已經在存放庫中追蹤版本資訊或變更記錄，也可以包含相關檔案的連結。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-214">If you already track release notes or a changelog in your repo, you can also include a link to the relevant file.</span></span>

## <a name="related-topics"></a><span data-ttu-id="c6a1d-215">相關主題</span><span class="sxs-lookup"><span data-stu-id="c6a1d-215">Related topics</span></span>

- [<span data-ttu-id="c6a1d-216">建立及發行套件 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="c6a1d-216">Create and publish a package (dotnet CLI)</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="c6a1d-217">建立及發行套件 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c6a1d-217">Create and publish a package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
