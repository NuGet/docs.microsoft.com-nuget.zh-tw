---
title: NuGet 錯誤和警告參考
description: 警告和錯誤各種 NuGet 作業期間發出 NuGet 從的完整參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="aefcd-103">錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-103">Errors and warnings</span></span>

<span data-ttu-id="aefcd-104">在 NuGet 4.3.0+ 錯誤和警告本主題中所述的編號，並提供可協助您解決相關的問題的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="aefcd-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="aefcd-105">錯誤和警告此處所列都僅能使用[PackageReference 基礎](../consume-packages/package-references-in-project-files.md)專案和 NuGet 4.3.0+。</span><span class="sxs-lookup"><span data-stu-id="aefcd-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="aefcd-106">NuGet 會隱藏警告或提高這些錯誤的 MSBuild 屬性也為準。</span><span class="sxs-lookup"><span data-stu-id="aefcd-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="aefcd-107">如需詳細資訊，請參閱[如何： 隱藏編譯器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文件中。</span><span class="sxs-lookup"><span data-stu-id="aefcd-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="aefcd-108">**錯誤**</span><span class="sxs-lookup"><span data-stu-id="aefcd-108">**Errors**</span></span>

| <span data-ttu-id="aefcd-109">群組</span><span class="sxs-lookup"><span data-stu-id="aefcd-109">Group</span></span> | <span data-ttu-id="aefcd-110">錯誤號碼</span><span class="sxs-lookup"><span data-stu-id="aefcd-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="aefcd-111">無效的輸入的錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="aefcd-112">[NU1001](#nu1001)， [NU1002](#nu1002)， [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="aefcd-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="aefcd-113">遺失封裝和專案的錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="aefcd-114">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (先前 NU1607) [NU1108](#nu1108) (先前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="aefcd-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="aefcd-115">相容性錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="aefcd-116">[NU1201](#nu1201)， [NU1202](#nu1202)， [NU1203](#nu1203)， [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="aefcd-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="aefcd-117">**警告**</span><span class="sxs-lookup"><span data-stu-id="aefcd-117">**Warnings**</span></span>

| <span data-ttu-id="aefcd-118">群組</span><span class="sxs-lookup"><span data-stu-id="aefcd-118">Group</span></span> | <span data-ttu-id="aefcd-119">警告編號</span><span class="sxs-lookup"><span data-stu-id="aefcd-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="aefcd-120">無效的輸入的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="aefcd-121">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="aefcd-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="aefcd-122">未預期的封裝版本警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="aefcd-123">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="aefcd-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="aefcd-124">解決衝突的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="aefcd-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="aefcd-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="aefcd-126">封裝後援警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="aefcd-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="aefcd-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="aefcd-128">摘要的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="aefcd-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="aefcd-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="aefcd-130">NuGet 的內部錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="aefcd-131">[NU1000](#nu1000)， [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="aefcd-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="aefcd-132">簽署的封裝 （建立及驗證）</span><span class="sxs-lookup"><span data-stu-id="aefcd-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="aefcd-133">[NU3000](#nu3000)， [NU3001](#nu3001)， [NU3002](#nu3002)， [NU3004](#nu3004)， [NU3008](#nu3008)， [NU3018](#nu3018)， [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="aefcd-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="aefcd-134">無效的輸入的錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-134">Invalid input errors</span></span>

<span data-ttu-id="aefcd-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="aefcd-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="aefcd-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="aefcd-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-137">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-137">**Issue**</span></span> | <span data-ttu-id="aefcd-138">專案未包含一或多個架構。</span><span class="sxs-lookup"><span data-stu-id="aefcd-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="aefcd-139">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-139">**Example message**</span></span> | <span data-ttu-id="aefcd-140">*專案找到了 c:\tmp\projA.csproj 中未指定任何目標架構*</span><span class="sxs-lookup"><span data-stu-id="aefcd-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="aefcd-141">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-141">**Solution**</span></span> | <span data-ttu-id="aefcd-142">新增`TargetFramework`或`TargetFrameworks`屬性，以指定的專案檔。</span><span class="sxs-lookup"><span data-stu-id="aefcd-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="aefcd-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="aefcd-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-144">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-144">**Issue**</span></span> | <span data-ttu-id="aefcd-145">輸入與清除關鍵字的組合無效。</span><span class="sxs-lookup"><span data-stu-id="aefcd-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="aefcd-146">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-146">**Example message**</span></span> | <span data-ttu-id="aefcd-147">*搭配其他的值不能使用 'CLEAR'*</span><span class="sxs-lookup"><span data-stu-id="aefcd-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="aefcd-148">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-148">**Solution**</span></span> | <span data-ttu-id="aefcd-149">清除單獨使用，並省略其他所有的輸入。</span><span class="sxs-lookup"><span data-stu-id="aefcd-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="aefcd-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="aefcd-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-151">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-151">**Issue**</span></span> | <span data-ttu-id="aefcd-152">`PackageTargetFallback` 和`AssetTargetFallback`選取資產時，提供不同的行為，而且無法一起使用。</span><span class="sxs-lookup"><span data-stu-id="aefcd-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="aefcd-153">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-153">**Example message**</span></span> | <span data-ttu-id="aefcd-154">*PackageTargetFallback 和 AssetTargetFallback 無法一起使用。從專案環境移除 PackageTargetFallback(deprecated) 參考。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="aefcd-155">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-155">**Solution**</span></span> | <span data-ttu-id="aefcd-156">移除已被取代`PackageTargetFallback`從專案的項目。</span><span class="sxs-lookup"><span data-stu-id="aefcd-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="aefcd-157">遺失封裝和專案的錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-157">Missing package and project errors</span></span>

<span data-ttu-id="aefcd-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="aefcd-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="aefcd-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="aefcd-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-160">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-160">**Issue**</span></span> | <span data-ttu-id="aefcd-161">相依性群組無法解析。</span><span class="sxs-lookup"><span data-stu-id="aefcd-161">A dependency group not be resolved.</span></span> <span data-ttu-id="aefcd-162">這是泛型類型不是封裝或專案的問題。</span><span class="sxs-lookup"><span data-stu-id="aefcd-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="aefcd-163">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-163">**Example message**</span></span> | <span data-ttu-id="aefcd-164">*無法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="aefcd-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="aefcd-165">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-165">**Solution**</span></span> | <span data-ttu-id="aefcd-166">開啟專案檔，並檢查其相依性的清單。</span><span class="sxs-lookup"><span data-stu-id="aefcd-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="aefcd-167">請檢查每個相依性存在套件來源使用，以及封裝支援此專案的目標架構。</span><span class="sxs-lookup"><span data-stu-id="aefcd-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="aefcd-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="aefcd-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-169">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-169">**Issue**</span></span> | <span data-ttu-id="aefcd-170">任何來源上找不到封裝。</span><span class="sxs-lookup"><span data-stu-id="aefcd-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="aefcd-171">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-171">**Example message**</span></span> | <span data-ttu-id="aefcd-172">*找不到封裝 System.Missing。無封裝存在具有此 id 來源中： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="aefcd-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="aefcd-173">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-173">**Solution**</span></span> | <span data-ttu-id="aefcd-174">檢查以確定您使用正確的封裝識別碼和版本號碼的 Visual Studio 中的專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="aefcd-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="aefcd-175">也請檢查[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)識別封裝來源您預期會使用。</span><span class="sxs-lookup"><span data-stu-id="aefcd-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="aefcd-176">如果您使用具有封裝[語意版本設定 2.0.0](../reference/package-versioning.md#semantic-versioning-200)，請確定您使用換行字元、 V3 `https://api.nuget.org/v3/index.json`，請在[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="aefcd-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="aefcd-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-178">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-178">**Issue**</span></span> | <span data-ttu-id="aefcd-179">找到的封裝識別碼，但任何來源上找不到指定的相依性範圍內的版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="aefcd-180">封裝並不是使用者，可能指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="aefcd-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="aefcd-181">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-181">**Example message**</span></span> | <span data-ttu-id="aefcd-182">*找不到版本套件 NuGet.Versioning (> = 9.0.1)<br/> -找到 30 位在 nuget.org 的版本 [最近的版本： 4.0.0]<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -找到 9版本 NuGetVolatile 中的 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="aefcd-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="aefcd-183">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-183">**Solution**</span></span> | <span data-ttu-id="aefcd-184">編輯專案檔以便可以正確封裝版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="aefcd-185">也請檢查[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)識別封裝來源您預期會使用。</span><span class="sxs-lookup"><span data-stu-id="aefcd-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="aefcd-186">您可能需要變更 requeted 版本，如果此封裝直接專案參考。</span><span class="sxs-lookup"><span data-stu-id="aefcd-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="aefcd-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="aefcd-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-188">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-188">**Issue**</span></span> | <span data-ttu-id="aefcd-189">指定的專案相依性範圍的穩定版本，但該範圍中找不到任何穩定版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="aefcd-190">找不到發行前版本，但不是允許。</span><span class="sxs-lookup"><span data-stu-id="aefcd-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="aefcd-191">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-191">**Example message**</span></span> | <span data-ttu-id="aefcd-192">*找不到版本為穩定套件 NuGet.Versioning (> = 3.0.0)<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="aefcd-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="aefcd-193">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-193">**Solution**</span></span> |  <span data-ttu-id="aefcd-194">編輯專案檔，以包含發行前版本中的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="aefcd-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="aefcd-195">請參閱[封裝版本控制](../reference/Package-Versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="aefcd-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="aefcd-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-197">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-197">**Issue**</span></span> | <span data-ttu-id="aefcd-198">ProjectReference 指向不存在的檔案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="aefcd-199">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-199">**Example message**</span></span> | <span data-ttu-id="aefcd-200">*專案參考不存在 'c:\a.csproj'。請檢查該專案的參考有效，且專案檔已存在。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="aefcd-201">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-201">**Solution**</span></span> | <span data-ttu-id="aefcd-202">編輯專案檔，請更正路徑參考的專案，或移除的參考完全不再需要。</span><span class="sxs-lookup"><span data-stu-id="aefcd-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="aefcd-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="aefcd-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-204">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-204">**Issue**</span></span> | <span data-ttu-id="aefcd-205">專案檔存在，但沒有還原資訊並未提供它。</span><span class="sxs-lookup"><span data-stu-id="aefcd-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="aefcd-206">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-206">**Example message**</span></span> | <span data-ttu-id="aefcd-207">*無法讀取 'c:\a.csproj' 的專案資訊。專案檔可能無效或遺漏目標所需的還原。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="aefcd-208">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-208">**Solution**</span></span> | <span data-ttu-id="aefcd-209">在 Visual Studio 中，錯誤可能表示專案已卸載，在這種情況下重新載入專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="aefcd-210">從命令列，這可能表示檔案已損毀或不包含自訂 「 呼叫後匯入 「 還原若要讀取專案所需的目標。</span><span class="sxs-lookup"><span data-stu-id="aefcd-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="aefcd-211">專案檔無效，而且包含 「 呼叫後匯入 」 目標核取。</span><span class="sxs-lookup"><span data-stu-id="aefcd-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="aefcd-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="aefcd-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-213">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-213">**Issue**</span></span> | <span data-ttu-id="aefcd-214">無法解析相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="aefcd-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="aefcd-215">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-215">**Example message**</span></span> | <span data-ttu-id="aefcd-216">*無法滿足 {id} 的衝突要求: {衝突 path} Framework: {目標圖表}*</span><span class="sxs-lookup"><span data-stu-id="aefcd-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="aefcd-217">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-217">**Solution**</span></span> | <span data-ttu-id="aefcd-218">編輯專案檔來指定相依性，而不是正確的版本更開放式的範圍。</span><span class="sxs-lookup"><span data-stu-id="aefcd-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="aefcd-219">NU1107 (先前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="aefcd-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-220">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-220">**Issue**</span></span> | <span data-ttu-id="aefcd-221">無法解析封裝之間的相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="aefcd-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="aefcd-222">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-222">**Example message**</span></span> | <span data-ttu-id="aefcd-223">*偵測到 NuGet.Versioning 版本衝突。參照套件，直接從專案以解決此問題。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning （= 3.5.0）]-> [<br/> NuGet.Configuration 4.0.0]-> [的 NuGet.Versioning （等於 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="aefcd-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="aefcd-224">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-224">**Solution**</span></span> | <span data-ttu-id="aefcd-225">封裝名稱中有相依性條件約束，確切的版本上不允許其他封裝，以提高版本，如有需要。</span><span class="sxs-lookup"><span data-stu-id="aefcd-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="aefcd-226">加入直接 （專案檔） 中的專案參考所需的正確版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="aefcd-227">NU1108 (先前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="aefcd-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-228">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-228">**Issue**</span></span> | <span data-ttu-id="aefcd-229">偵測到循環相依性。</span><span class="sxs-lookup"><span data-stu-id="aefcd-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="aefcd-230">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-230">**Example message**</span></span> | <span data-ttu-id="aefcd-231">*偵測到循環： a-> B-A >*</span><span class="sxs-lookup"><span data-stu-id="aefcd-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="aefcd-232">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-232">**Solution**</span></span> | <span data-ttu-id="aefcd-233">封裝被撰寫不正確;請連絡封裝擁有者，以修正 bug。</span><span class="sxs-lookup"><span data-stu-id="aefcd-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="aefcd-234">相容性錯誤</span><span class="sxs-lookup"><span data-stu-id="aefcd-234">Compatibility errors</span></span>

<span data-ttu-id="aefcd-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="aefcd-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="aefcd-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="aefcd-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-237">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-237">**Issue**</span></span> | <span data-ttu-id="aefcd-238">相依性專案未包含與目前的專案相容的架構。</span><span class="sxs-lookup"><span data-stu-id="aefcd-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="aefcd-239">一般而言，此專案的目標架構是版本高於使用的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="aefcd-240">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-240">**Example message**</span></span> | <span data-ttu-id="aefcd-241">*專案 ServerWeb 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。專案 ServerWeb 支援：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="aefcd-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="aefcd-242">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-242">**Solution**</span></span> | <span data-ttu-id="aefcd-243">將專案的目標 framework 變更為相同或較低的版本比使用的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="aefcd-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="aefcd-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-245">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-245">**Issue**</span></span> | <span data-ttu-id="aefcd-246">相依性封裝未包含任何與專案相容的資產。</span><span class="sxs-lookup"><span data-stu-id="aefcd-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="aefcd-247">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-247">**Example message**</span></span> | <span data-ttu-id="aefcd-248">*封裝 System.ComponentModel.EventBasedAsync 4.0.11 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。封裝 System.ComponentModel.EventBasedAsync 4.0.11 支援：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = 4.5 版)<br/> -netcore50 (。NETCore，Version = v5.0)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可攜式 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，設定檔 = Profile259)<br/> -win8 (Windows，Version = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="aefcd-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="aefcd-249">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-249">**Solution**</span></span> | <span data-ttu-id="aefcd-250">將專案的目標 framework 變更為套件支援。</span><span class="sxs-lookup"><span data-stu-id="aefcd-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="aefcd-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="aefcd-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-252">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-252">**Issue**</span></span> | <span data-ttu-id="aefcd-253">封裝不支援專案的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="aefcd-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="aefcd-254">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-254">**Example message**</span></span> | <span data-ttu-id="aefcd-255">*System.Example 1.0.0 提供 net461，a.dll 的編譯階段的參考組件，但沒有相容的執行階段組件。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="aefcd-256">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-256">**Solution**</span></span> | <span data-ttu-id="aefcd-257">變更`RuntimeIdentifier`視專案中使用的值。</span><span class="sxs-lookup"><span data-stu-id="aefcd-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="aefcd-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="aefcd-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-259">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-259">**Issue**</span></span> | <span data-ttu-id="aefcd-260">此封裝需要的功能或安裝的 NuGet 版本目前不支援的架構。</span><span class="sxs-lookup"><span data-stu-id="aefcd-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="aefcd-261">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-261">**Example message**</span></span> | <span data-ttu-id="aefcd-262">*'NuGet.Versioning' 封裝需要 NuGet 用戶端版本 '5.0.0' 或以上版本，但是目前 NuGet 版本是 '4.3.0'。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="aefcd-263">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-263">**Solution**</span></span> | <span data-ttu-id="aefcd-264">安裝 NuGet 較新的版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="aefcd-265">請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="aefcd-266">無效的輸入的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-266">Invalid input warnings</span></span>

<span data-ttu-id="aefcd-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="aefcd-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="aefcd-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="aefcd-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-269">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-269">**Issue**</span></span> | <span data-ttu-id="aefcd-270">專案還原操作嘗試在找不到。</span><span class="sxs-lookup"><span data-stu-id="aefcd-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="aefcd-271">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-271">**Example message**</span></span> | <span data-ttu-id="aefcd-272">*資料夾 'c:\projects\a' 沒有可還原的專案。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="aefcd-273">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-273">**Solution**</span></span> | <span data-ttu-id="aefcd-274">包含專案的資料夾中執行 nuget 還原。</span><span class="sxs-lookup"><span data-stu-id="aefcd-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="aefcd-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="aefcd-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-276">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-276">**Issue**</span></span> | <span data-ttu-id="aefcd-277">`RuntimeSupports` 包含無效的設定檔。</span><span class="sxs-lookup"><span data-stu-id="aefcd-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="aefcd-278">一般而言，支援的設定檔中未找到`runtime.json`從目前的相依性套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="aefcd-279">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-279">**Example message**</span></span> | <span data-ttu-id="aefcd-280">*未知的相容性設定檔： aaa*</span><span class="sxs-lookup"><span data-stu-id="aefcd-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="aefcd-281">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-281">**Solution**</span></span> | <span data-ttu-id="aefcd-282">請檢查`RuntimeSupports`專案中的值。</span><span class="sxs-lookup"><span data-stu-id="aefcd-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="aefcd-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="aefcd-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-284">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-284">**Issue**</span></span> | <span data-ttu-id="aefcd-285">相依性專案不會匯入 NuGet 的還原目標。</span><span class="sxs-lookup"><span data-stu-id="aefcd-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="aefcd-286">這類似於 NU1105 但此處已略過專案，而不會引發還原失敗的所有忽略。</span><span class="sxs-lookup"><span data-stu-id="aefcd-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="aefcd-287">在複雜的解決方案通常會其他類型可能不支援還原的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="aefcd-288">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-288">**Example message**</span></span> | <span data-ttu-id="aefcd-289">*正在略過專案 'c:\a.csproj' 的還原。專案檔可能無效或遺漏目標所需的還原。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="aefcd-290">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-290">**Solution**</span></span> | <span data-ttu-id="aefcd-291">這種情形，不會匯入一般 props/目標自動匯入還原的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="aefcd-292">如果專案不需要還原可以忽略此參數。</span><span class="sxs-lookup"><span data-stu-id="aefcd-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="aefcd-293">否則，請編輯受影響的專案，以便將還原的目標。</span><span class="sxs-lookup"><span data-stu-id="aefcd-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="aefcd-294">未預期的封裝版本警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-294">Unexpected package version warnings</span></span>

<span data-ttu-id="aefcd-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="aefcd-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="aefcd-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="aefcd-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-297">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-297">**Issue**</span></span> | <span data-ttu-id="aefcd-298">直接專案相依性是只有當更新的版本比指定的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="aefcd-299">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-299">**Example message**</span></span> | <span data-ttu-id="aefcd-300">*指定的相依性為 NuGet.Versioning (> = 3.5.0) 但 NuGet.Versioning 4.0.0 結果。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="aefcd-301">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-301">**Solution**</span></span> | <span data-ttu-id="aefcd-302">適當版本來更新專案中的相依性。</span><span class="sxs-lookup"><span data-stu-id="aefcd-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="aefcd-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="aefcd-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-304">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-304">**Issue**</span></span> | <span data-ttu-id="aefcd-305">封裝的相依性遺漏下限。</span><span class="sxs-lookup"><span data-stu-id="aefcd-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="aefcd-306">這不允許還原，若要尋找*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="aefcd-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="aefcd-307">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="aefcd-308">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="aefcd-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="aefcd-309">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-309">**Example message**</span></span> | <span data-ttu-id="aefcd-310">*NuGet.Packaging 4.0.0 不提供相依性 NuGet.Versioning (> 3.5.0) 下限 （內含）。3.6.0 的近似最符合項目已解決。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="aefcd-311">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-311">**Solution**</span></span> | <span data-ttu-id="aefcd-312">這通常是撰寫錯誤的封裝。</span><span class="sxs-lookup"><span data-stu-id="aefcd-312">This is usually a package authoring error.</span></span> <span data-ttu-id="aefcd-313">請連絡封裝作者以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="aefcd-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="aefcd-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="aefcd-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-315">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-315">**Issue**</span></span> | <span data-ttu-id="aefcd-316">封裝的相依性指定找不到的版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="aefcd-317">通常，封裝來源不包含預期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="aefcd-318">較高的版本來取代，這不同於封裝所撰寫針對。</span><span class="sxs-lookup"><span data-stu-id="aefcd-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="aefcd-319">這表示找不到該還原*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="aefcd-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="aefcd-320">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="aefcd-321">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="aefcd-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="aefcd-322">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-322">**Example message**</span></span> | <span data-ttu-id="aefcd-323">NuGet.Packaging 4.0.0 取決於 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="aefcd-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="aefcd-324">5.0.0 的近似最符合項目已解決。</span><span class="sxs-lookup"><span data-stu-id="aefcd-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="aefcd-325">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-325">**Solution**</span></span> | <span data-ttu-id="aefcd-326">如果封裝應該沒有釋出，這可能是封裝撰寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="aefcd-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="aefcd-327">請連絡封裝作者以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="aefcd-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="aefcd-328">如果已發行的封裝，然後檢查它是否可用上您所使用的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="aefcd-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="aefcd-329">如果使用的私用的來源，您可能需要更新該摘要上的封裝。</span><span class="sxs-lookup"><span data-stu-id="aefcd-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="aefcd-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="aefcd-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-331">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-331">**Issue**</span></span> | <span data-ttu-id="aefcd-332">專案相依性不會定義繫結至較低。</span><span class="sxs-lookup"><span data-stu-id="aefcd-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="aefcd-333">這表示找不到該還原*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="aefcd-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="aefcd-334">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="aefcd-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="aefcd-335">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="aefcd-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="aefcd-336">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-336">**Example message**</span></span> | <span data-ttu-id="aefcd-337">*專案相依性 NuGet.Versioning (< = 9.0.0) doe 包含下限 （內含）。相依性版本，以確保結果一致還原包含下限。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="aefcd-338">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-338">**Solution**</span></span> | <span data-ttu-id="aefcd-339">更新專案的`PackageReference``Version`包含繫結至較低的屬性。</span><span class="sxs-lookup"><span data-stu-id="aefcd-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="aefcd-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="aefcd-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-341">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-341">**Issue**</span></span> | <span data-ttu-id="aefcd-342">相依性套件指定版本上的條件約束的封裝版本高於還原最後都會解析。</span><span class="sxs-lookup"><span data-stu-id="aefcd-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="aefcd-343">也就是 「 最接近獲勝 」 規則解析封裝時，因為圖形中的最接近的封裝可能已覆寫遠方的封裝。</span><span class="sxs-lookup"><span data-stu-id="aefcd-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="aefcd-344">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-344">**Example message**</span></span> | <span data-ttu-id="aefcd-345">*偵測到套件降級： 3.5.0 來從 4.0.0 NuGet.Versioning。直接從要選取不同版本的專案參考封裝。<br/>NuGet.Packaging 3.5.0]-> [NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0]-> [NuGet.Configuration 4.0.0]-> [NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="aefcd-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="aefcd-346">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-346">**Solution**</span></span> | <span data-ttu-id="aefcd-347">直接將參考加入至您想要使用的封裝更高版本的專案。</span><span class="sxs-lookup"><span data-stu-id="aefcd-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="aefcd-348">解決衝突的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="aefcd-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="aefcd-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-350">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-350">**Issue**</span></span> | <span data-ttu-id="aefcd-351">解析的封裝高於允許的相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="aefcd-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="aefcd-352">這表示，直接在專案所參考的封裝會覆寫從其他套件相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="aefcd-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="aefcd-353">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-353">**Example message**</span></span> | <span data-ttu-id="aefcd-354">*外部相依性條件約束的偵測到的套件版本： x 1.0.0 需要的 y （= 1.0.0），但 y 2.0.0 的版本是已解決。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="aefcd-355">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-355">**Solution**</span></span> | <span data-ttu-id="aefcd-356">在某些情況下，這是有意如此，可以隱藏的警告。</span><span class="sxs-lookup"><span data-stu-id="aefcd-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="aefcd-357">否則，變更以擴大其版本條件約束的封裝專案的參考。</span><span class="sxs-lookup"><span data-stu-id="aefcd-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="aefcd-358">封裝後援警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="aefcd-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="aefcd-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-360">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-360">**Issue**</span></span> | <span data-ttu-id="aefcd-361">`PackageTargetFallback` / `AssetTargetFallback` 用來從封裝中選取的資產。</span><span class="sxs-lookup"><span data-stu-id="aefcd-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="aefcd-362">警告會讓使用者知道資產可能不相容的 100%。</span><span class="sxs-lookup"><span data-stu-id="aefcd-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="aefcd-363">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-363">**Example message**</span></span> | <span data-ttu-id="aefcd-364">*已還原封裝 'NuGet.Versioning'，'可攜式 net45 + win8' 改為使用專案目標 framework 'netstandard1.5'。此封裝可能無法完全相容，您的專案。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="aefcd-365">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-365">**Solution**</span></span> | <span data-ttu-id="aefcd-366">將專案的目標 framework 變更為套件支援。</span><span class="sxs-lookup"><span data-stu-id="aefcd-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="aefcd-367">摘要的警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="aefcd-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="aefcd-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-369">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-369">**Issue**</span></span> | <span data-ttu-id="aefcd-370">讀取摘要時，發生錯誤時`IgnoreFailedSources`設為 true，將它轉換成非嚴重警告。</span><span class="sxs-lookup"><span data-stu-id="aefcd-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="aefcd-371">這可能會包含任何訊息，而且是泛型。</span><span class="sxs-lookup"><span data-stu-id="aefcd-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="aefcd-372">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-372">**Example message**</span></span> | <span data-ttu-id="aefcd-373">N/A</span><span class="sxs-lookup"><span data-stu-id="aefcd-373">n/a</span></span> |
| <span data-ttu-id="aefcd-374">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-374">**Solution**</span></span> | <span data-ttu-id="aefcd-375">編輯您的設定以指定有效的來源。</span><span class="sxs-lookup"><span data-stu-id="aefcd-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="aefcd-376">NuGet 的內部錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="aefcd-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="aefcd-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="aefcd-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="aefcd-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="aefcd-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-379">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-379">**Issue**</span></span> | <span data-ttu-id="aefcd-380">從 NuGet 非特定的內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="aefcd-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="aefcd-381">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-381">**Solution**</span></span> | <span data-ttu-id="aefcd-382">檢查記錄檔，如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="aefcd-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="aefcd-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="aefcd-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-384">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-384">**Issue**</span></span> | <span data-ttu-id="aefcd-385">從 NuGet 非特定內部警告。</span><span class="sxs-lookup"><span data-stu-id="aefcd-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="aefcd-386">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-386">**Solution**</span></span> | <span data-ttu-id="aefcd-387">檢查記錄檔，如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="aefcd-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="aefcd-388">簽署的封裝 （建立及驗證）</span><span class="sxs-lookup"><span data-stu-id="aefcd-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="aefcd-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="aefcd-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="aefcd-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="aefcd-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="aefcd-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="aefcd-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-392">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-392">**Issue**</span></span> | <span data-ttu-id="aefcd-393">簽署封裝驗證和非特定錯誤相關封裝簽章。</span><span class="sxs-lookup"><span data-stu-id="aefcd-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="aefcd-394">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-394">**Solution**</span></span> | <span data-ttu-id="aefcd-395">請檢查記錄以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="aefcd-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="aefcd-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="aefcd-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-397">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-397">**Issue**</span></span> | <span data-ttu-id="aefcd-398">無效的引數設為 [簽署命令](../tools/cli-ref-sign.md)或[確認命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="aefcd-399">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-399">**Solution**</span></span> | <span data-ttu-id="aefcd-400">檢查並更正提供的引數。</span><span class="sxs-lookup"><span data-stu-id="aefcd-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="aefcd-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="aefcd-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-402">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-402">**Issue**</span></span> | <span data-ttu-id="aefcd-403">`-Timestamper`未指定選項與[nuget 登命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="aefcd-404">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-404">**Example message**</span></span> | <span data-ttu-id="aefcd-405">*'-Timestamper' 無法提供選項。已簽署的套件不會加。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="aefcd-406">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-406">**Solution**</span></span> | <span data-ttu-id="aefcd-407">指定`-Timestamper`選項與`nuget sign`。</span><span class="sxs-lookup"><span data-stu-id="aefcd-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="aefcd-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="aefcd-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-409">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-409">**Issue**</span></span> | <span data-ttu-id="aefcd-410">不帶正負號的封裝提供給[nuget 確認命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="aefcd-411">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-411">**Solution**</span></span> | <span data-ttu-id="aefcd-412">執行`nuget verify`與已簽署封裝。</span><span class="sxs-lookup"><span data-stu-id="aefcd-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="aefcd-413">請參閱[簽署封裝](../create-packages/Sign-a-Package.md)。</span><span class="sxs-lookup"><span data-stu-id="aefcd-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="aefcd-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="aefcd-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-415">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-415">**Issue**</span></span> | <span data-ttu-id="aefcd-416">套件完整性檢查失敗，這表示已簽署的封裝要簽署後已遭竄改。</span><span class="sxs-lookup"><span data-stu-id="aefcd-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="aefcd-417">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-417">**Solution**</span></span> | <span data-ttu-id="aefcd-418">掃描您的防毒軟體的電腦。</span><span class="sxs-lookup"><span data-stu-id="aefcd-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="aefcd-419">然後從電腦移除封裝、 重新安裝它，然後再次嘗試操作。</span><span class="sxs-lookup"><span data-stu-id="aefcd-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="aefcd-420">如果此問題持續發生，請連絡封裝來源的擁有者及封裝擁有者。</span><span class="sxs-lookup"><span data-stu-id="aefcd-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="aefcd-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="aefcd-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-422">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-422">**Issue**</span></span> | <span data-ttu-id="aefcd-423">主要簽章的憑證鏈結建立失敗。</span><span class="sxs-lookup"><span data-stu-id="aefcd-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="aefcd-424">主要簽署憑證不受信任，撤銷，或憑證的撤銷資訊無法使用。</span><span class="sxs-lookup"><span data-stu-id="aefcd-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="aefcd-425">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-425">**Example message**</span></span> | <span data-ttu-id="aefcd-426">*警告： NU3018： 撤銷功能無法檢查撤銷憑證。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="aefcd-427">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-427">**Solution**</span></span> | <span data-ttu-id="aefcd-428">使用受信任且有效的憑證。</span><span class="sxs-lookup"><span data-stu-id="aefcd-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="aefcd-429">請檢查網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="aefcd-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="aefcd-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="aefcd-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="aefcd-431">**問題**</span><span class="sxs-lookup"><span data-stu-id="aefcd-431">**Issue**</span></span> | <span data-ttu-id="aefcd-432">時間戳記簽章的憑證鏈結建立失敗。</span><span class="sxs-lookup"><span data-stu-id="aefcd-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="aefcd-433">時間戳記簽章憑證不受信任，撤銷，或憑證的撤銷資訊無法使用。</span><span class="sxs-lookup"><span data-stu-id="aefcd-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="aefcd-434">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="aefcd-434">**Example message**</span></span> | <span data-ttu-id="aefcd-435">*警告： NU3028： 撤銷功能無法檢查撤銷憑證。*</span><span class="sxs-lookup"><span data-stu-id="aefcd-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="aefcd-436">**方案**</span><span class="sxs-lookup"><span data-stu-id="aefcd-436">**Solution**</span></span> | <span data-ttu-id="aefcd-437">使用受信任且有效的憑證。</span><span class="sxs-lookup"><span data-stu-id="aefcd-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="aefcd-438">請檢查網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="aefcd-438">Check internet connectivity.</span></span> |
