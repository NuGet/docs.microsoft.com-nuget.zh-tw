---
title: "NuGet 還原錯誤和警告參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "警告和錯誤發出從 NuGet 封裝還原期間的完整參考"
keywords: "NuGet 錯誤、 NuGet 警告診斷"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="6bf50-104">錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-104">Errors and warnings</span></span>

<span data-ttu-id="6bf50-105">在 NuGet 4.3.0、 錯誤和警告本主題中所述的編號，並提供可協助您解決相關的問題的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="6bf50-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="6bf50-106">錯誤和警告此處所列都僅能使用[PackageReference 基礎](../Consume-Packages/Package-References-in-Project-Files.md)專案和 NuGet 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="6bf50-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="6bf50-107">NuGet 會隱藏警告或提高這些錯誤的 MSBuild 屬性也為準。</span><span class="sxs-lookup"><span data-stu-id="6bf50-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="6bf50-108">如需詳細資訊，請參閱[如何： 隱藏編譯器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文件中。</span><span class="sxs-lookup"><span data-stu-id="6bf50-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="6bf50-109">**錯誤**</span><span class="sxs-lookup"><span data-stu-id="6bf50-109">**Errors**</span></span>

| <span data-ttu-id="6bf50-110">群組</span><span class="sxs-lookup"><span data-stu-id="6bf50-110">Group</span></span> | <span data-ttu-id="6bf50-111">錯誤號碼</span><span class="sxs-lookup"><span data-stu-id="6bf50-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="6bf50-112">無效的輸入的錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="6bf50-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="6bf50-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="6bf50-114">遺失封裝和專案的錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="6bf50-115">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (先前 NU1607) [NU1108](#nu1108) (先前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="6bf50-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="6bf50-116">相容性錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="6bf50-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="6bf50-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="6bf50-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="6bf50-118">**Warnings**</span></span>

| <span data-ttu-id="6bf50-119">群組</span><span class="sxs-lookup"><span data-stu-id="6bf50-119">Group</span></span> | <span data-ttu-id="6bf50-120">警告編號</span><span class="sxs-lookup"><span data-stu-id="6bf50-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="6bf50-121">無效的輸入的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="6bf50-122">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="6bf50-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="6bf50-123">未預期的封裝版本警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="6bf50-124">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="6bf50-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="6bf50-125">解決衝突的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="6bf50-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="6bf50-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="6bf50-127">封裝後援警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="6bf50-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="6bf50-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="6bf50-129">摘要的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="6bf50-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="6bf50-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="6bf50-131">NuGet 的內部錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="6bf50-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="6bf50-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="6bf50-133">無效的輸入的錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-133">Invalid input errors</span></span>

<span data-ttu-id="6bf50-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="6bf50-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="6bf50-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="6bf50-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-136">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-136">**Issue**</span></span> | <span data-ttu-id="6bf50-137">專案未包含一或多個架構。</span><span class="sxs-lookup"><span data-stu-id="6bf50-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="6bf50-138">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-138">**Common causes**</span></span> | <span data-ttu-id="6bf50-139">專案不包含`TargetFramework`或`TargetFrameworks`屬性。</span><span class="sxs-lookup"><span data-stu-id="6bf50-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="6bf50-140">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-140">**Example message**</span></span> | <span data-ttu-id="6bf50-141">*專案找到了 c:\tmp\projA.csproj 中未指定任何目標架構*</span><span class="sxs-lookup"><span data-stu-id="6bf50-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="6bf50-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="6bf50-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-143">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-143">**Issue**</span></span> | <span data-ttu-id="6bf50-144">輸入與清除關鍵字的組合無效。</span><span class="sxs-lookup"><span data-stu-id="6bf50-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="6bf50-145">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-145">**Common causes**</span></span> | <span data-ttu-id="6bf50-146">清除不結合其他輸入。</span><span class="sxs-lookup"><span data-stu-id="6bf50-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="6bf50-147">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-147">**Example message**</span></span> | <span data-ttu-id="6bf50-148">*搭配其他的值不能使用 'CLEAR'*</span><span class="sxs-lookup"><span data-stu-id="6bf50-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="6bf50-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="6bf50-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-150">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-150">**Issue**</span></span> | <span data-ttu-id="6bf50-151">`PackageTargetFallback`和`AssetTargetFallback`選取資產時，提供不同的行為，而且無法一起使用。</span><span class="sxs-lookup"><span data-stu-id="6bf50-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="6bf50-152">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-152">**Common causes**</span></span> | <span data-ttu-id="6bf50-153">同時`PackageTargetFallback`和`AssetTargetFallback`存在於專案中。</span><span class="sxs-lookup"><span data-stu-id="6bf50-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="6bf50-154">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-154">**Example message**</span></span> | <span data-ttu-id="6bf50-155">*PackageTargetFallback 和 AssetTargetFallback 無法一起使用。從專案環境移除 PackageTargetFallback(deprecated) 參考。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="6bf50-156">遺失封裝和專案的錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-156">Missing package and project errors</span></span>

<span data-ttu-id="6bf50-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="6bf50-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="6bf50-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="6bf50-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-159">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-159">**Issue**</span></span> | <span data-ttu-id="6bf50-160">相依性群組無法解析。</span><span class="sxs-lookup"><span data-stu-id="6bf50-160">A dependency group not be resolved.</span></span> <span data-ttu-id="6bf50-161">這是泛型類型不是封裝或專案的問題。</span><span class="sxs-lookup"><span data-stu-id="6bf50-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="6bf50-162">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-162">**Common causes**</span></span> | <span data-ttu-id="6bf50-163">專案包含不存在的項目上的相依性。</span><span class="sxs-lookup"><span data-stu-id="6bf50-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="6bf50-164">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-164">**Example message**</span></span> | <span data-ttu-id="6bf50-165">*無法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="6bf50-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="6bf50-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="6bf50-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-167">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-167">**Issue**</span></span> | <span data-ttu-id="6bf50-168">任何來源上找不到封裝。</span><span class="sxs-lookup"><span data-stu-id="6bf50-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="6bf50-169">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-169">**Common causes**</span></span> | <span data-ttu-id="6bf50-170">正確的套件來源遺漏或封裝識別碼不正確。</span><span class="sxs-lookup"><span data-stu-id="6bf50-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="6bf50-171">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-171">**Example message**</span></span> | <span data-ttu-id="6bf50-172">*找不到封裝 System.Missing。無封裝存在具有此 id 來源中： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="6bf50-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="6bf50-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="6bf50-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-174">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-174">**Issue**</span></span> | <span data-ttu-id="6bf50-175">找到的封裝識別碼，但任何來源上找不到指定的相依性範圍內的版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="6bf50-176">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-176">**Common causes**</span></span> | <span data-ttu-id="6bf50-177">正確的套件來源遺漏或相依性範圍不正確。</span><span class="sxs-lookup"><span data-stu-id="6bf50-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="6bf50-178">封裝並不是使用者，可能指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="6bf50-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="6bf50-179">使用者可能需要切換至 可用的版本，如果此封裝直接參考由專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="6bf50-180">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-180">**Example message**</span></span> | <span data-ttu-id="6bf50-181">*找不到版本套件 NuGet.Versioning (> = 9.0.1)<br/> -找到 30 位在 nuget.org 的版本 [最近的版本： 4.0.0]<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -找到 9版本 NuGetVolatile 中的 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="6bf50-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="6bf50-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="6bf50-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-183">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-183">**Issue**</span></span> | <span data-ttu-id="6bf50-184">相依性範圍中找不到任何穩定版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="6bf50-185">找不到發行前版本，但不是允許。</span><span class="sxs-lookup"><span data-stu-id="6bf50-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="6bf50-186">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-186">**Common causes**</span></span> | <span data-ttu-id="6bf50-187">指定相依性範圍的穩定版本的專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="6bf50-188">使用者必須變更要包含發行前版本的版本範圍。</span><span class="sxs-lookup"><span data-stu-id="6bf50-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="6bf50-189">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-189">**Example message**</span></span> | <span data-ttu-id="6bf50-190">*找不到版本為穩定套件 NuGet.Versioning (> = 3.0.0)<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="6bf50-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="6bf50-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="6bf50-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-192">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-192">**Issue**</span></span> | <span data-ttu-id="6bf50-193">ProjectReference 指向不存在的檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="6bf50-194">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-194">**Common causes**</span></span> | <span data-ttu-id="6bf50-195">磁碟中的專案檔遺漏或參考不正確。</span><span class="sxs-lookup"><span data-stu-id="6bf50-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="6bf50-196">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-196">**Example message**</span></span> | <span data-ttu-id="6bf50-197">*專案參考不存在 'c:\a.csproj'。請檢查該專案的參考有效，且專案檔已存在。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="6bf50-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="6bf50-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-199">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-199">**Issue**</span></span> | <span data-ttu-id="6bf50-200">專案檔存在，但沒有還原資訊並未提供它。</span><span class="sxs-lookup"><span data-stu-id="6bf50-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="6bf50-201">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-201">**Common causes**</span></span> | <span data-ttu-id="6bf50-202">在 Visual Studio 中，這可能表示專案已卸載。</span><span class="sxs-lookup"><span data-stu-id="6bf50-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="6bf50-203">從命令列中，這可能表示檔案已損毀或還原若要讀取專案所需的匯入目標之後，它不包含自訂。</span><span class="sxs-lookup"><span data-stu-id="6bf50-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="6bf50-204">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-204">**Example message**</span></span> | <span data-ttu-id="6bf50-205">*無法讀取 'c:\a.csproj' 的專案資訊。專案檔可能無效或遺漏目標所需的還原。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="6bf50-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="6bf50-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-207">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-207">**Issue**</span></span> | <span data-ttu-id="6bf50-208">無法解析相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="6bf50-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="6bf50-209">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-209">**Common causes**</span></span> | <span data-ttu-id="6bf50-210">封裝包含確切版本，而未限制範圍不是封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="6bf50-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="6bf50-211">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-211">**Example message**</span></span> | <span data-ttu-id="6bf50-212">*無法滿足 {id} 的衝突要求: {衝突 path} Framework: {目標圖表}*</span><span class="sxs-lookup"><span data-stu-id="6bf50-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="6bf50-213">NU1107 (先前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="6bf50-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-214">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-214">**Issue**</span></span> | <span data-ttu-id="6bf50-215">無法解析封裝之間的相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="6bf50-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="6bf50-216">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-216">**Common causes**</span></span> | <span data-ttu-id="6bf50-217">封裝名稱中有相依性條件約束，確切的版本上不允許其他封裝，以提高版本，如有需要。</span><span class="sxs-lookup"><span data-stu-id="6bf50-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="6bf50-218">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-218">**Example message**</span></span> | <span data-ttu-id="6bf50-219">*偵測到 NuGet.Versioning 版本衝突。參照套件，直接從專案以解決此問題。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning （= 3.5.0）]-> [<br/> NuGet.Configuration 4.0.0]-> [的 NuGet.Versioning （等於 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="6bf50-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="6bf50-220">NU1108 (先前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="6bf50-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-221">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-221">**Issue**</span></span> | <span data-ttu-id="6bf50-222">偵測到循環相依性。</span><span class="sxs-lookup"><span data-stu-id="6bf50-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="6bf50-223">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-223">**Common causes**</span></span> | <span data-ttu-id="6bf50-224">封裝被撰寫不正確。</span><span class="sxs-lookup"><span data-stu-id="6bf50-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="6bf50-225">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-225">**Example message**</span></span> | <span data-ttu-id="6bf50-226">*偵測到循環： a-> B-A >*</span><span class="sxs-lookup"><span data-stu-id="6bf50-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="6bf50-227">相容性錯誤</span><span class="sxs-lookup"><span data-stu-id="6bf50-227">Compatibility errors</span></span>

<span data-ttu-id="6bf50-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="6bf50-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="6bf50-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="6bf50-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-230">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-230">**Issue**</span></span> | <span data-ttu-id="6bf50-231">相依性專案未包含與目前的專案相容的架構。</span><span class="sxs-lookup"><span data-stu-id="6bf50-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="6bf50-232">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-232">**Common causes**</span></span> | <span data-ttu-id="6bf50-233">專案的目標 framework 是版本高於使用的專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="6bf50-234">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-234">**Example message**</span></span> | <span data-ttu-id="6bf50-235">*專案 ServerWeb 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。專案 ServerWeb 支援：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="6bf50-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="6bf50-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="6bf50-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-237">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-237">**Issue**</span></span> | <span data-ttu-id="6bf50-238">相依性封裝未包含任何與專案相容的資產。</span><span class="sxs-lookup"><span data-stu-id="6bf50-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="6bf50-239">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-239">**Common causes**</span></span> | <span data-ttu-id="6bf50-240">封裝不支援此專案的目標架構。</span><span class="sxs-lookup"><span data-stu-id="6bf50-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="6bf50-241">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-241">**Example message**</span></span> | <span data-ttu-id="6bf50-242">*封裝 System.ComponentModel.EventBasedAsync 4.0.11 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。封裝 System.ComponentModel.EventBasedAsync 4.0.11 支援：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = 4.5 版)<br/> -netcore50 (。NETCore，Version = v5.0)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可攜式 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，設定檔 = Profile259)<br/> -win8 (Windows，Version = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="6bf50-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="6bf50-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="6bf50-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-244">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-244">**Issue**</span></span> | <span data-ttu-id="6bf50-245">封裝不支援專案的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="6bf50-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="6bf50-246">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-246">**Common causes**</span></span> | <span data-ttu-id="6bf50-247">封裝不支援目前`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="6bf50-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="6bf50-248">變更`RuntimeIdentifier`如有需要在專案中使用的值。</span><span class="sxs-lookup"><span data-stu-id="6bf50-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="6bf50-249">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-249">**Example message**</span></span> | <span data-ttu-id="6bf50-250">*System.Example 1.0.0 提供 net461，a.dll 的編譯階段的參考組件，但沒有相容的執行階段組件。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="6bf50-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="6bf50-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-252">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-252">**Issue**</span></span> | <span data-ttu-id="6bf50-253">此封裝需要的功能或安裝的 NuGet 版本目前不支援的架構。</span><span class="sxs-lookup"><span data-stu-id="6bf50-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="6bf50-254">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-254">**Common causes**</span></span> | <span data-ttu-id="6bf50-255">升級 NuGet，若要修正此問題。</span><span class="sxs-lookup"><span data-stu-id="6bf50-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="6bf50-256">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-256">**Example message**</span></span> | <span data-ttu-id="6bf50-257">*'NuGet.Versioning' 封裝需要 NuGet 用戶端版本 '5.0.0' 或以上版本，但是目前 NuGet 版本是 '4.3.0'。若要升級 NuGet，請前往 http://docs.nuget.org/consume/installing-nuget。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="6bf50-258">無效的輸入的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-258">Invalid input warnings</span></span>

<span data-ttu-id="6bf50-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="6bf50-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="6bf50-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="6bf50-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-261">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-261">**Issue**</span></span> | <span data-ttu-id="6bf50-262">專案還原操作嘗試在找不到。</span><span class="sxs-lookup"><span data-stu-id="6bf50-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="6bf50-263">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-263">**Common causes**</span></span> | <span data-ttu-id="6bf50-264">專案遺漏。</span><span class="sxs-lookup"><span data-stu-id="6bf50-264">The project is missing.</span></span> |
| <span data-ttu-id="6bf50-265">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-265">**Example message**</span></span> | <span data-ttu-id="6bf50-266">*資料夾 'c:\projects\a' 沒有可還原的專案。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="6bf50-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="6bf50-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-268">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-268">**Issue**</span></span> | <span data-ttu-id="6bf50-269">`RuntimeSupports`包含無效的設定檔。</span><span class="sxs-lookup"><span data-stu-id="6bf50-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="6bf50-270">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-270">**Common causes**</span></span> | <span data-ttu-id="6bf50-271">中找不到支援的設定檔`runtime.json`從目前的相依性套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="6bf50-272">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-272">**Example message**</span></span> | <span data-ttu-id="6bf50-273">*未知的相容性設定檔： aaa*</span><span class="sxs-lookup"><span data-stu-id="6bf50-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="6bf50-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="6bf50-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-275">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-275">**Issue**</span></span> | <span data-ttu-id="6bf50-276">相依性專案不會匯入 NuGet 的還原目標。</span><span class="sxs-lookup"><span data-stu-id="6bf50-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="6bf50-277">這類似於 NU1105 但此處已略過專案，而不會引發還原失敗的所有忽略。</span><span class="sxs-lookup"><span data-stu-id="6bf50-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="6bf50-278">在複雜的解決方案通常會其他類型可能不支援還原的專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="6bf50-279">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-279">**Common causes**</span></span> | <span data-ttu-id="6bf50-280">這種情形，不會匯入一般 props/目標自動匯入還原的專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="6bf50-281">如果專案不需要還原可以忽略此參數。</span><span class="sxs-lookup"><span data-stu-id="6bf50-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="6bf50-282">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-282">**Example message**</span></span> | <span data-ttu-id="6bf50-283">*正在略過專案 'c:\a.csproj' 的還原。專案檔可能無效或遺漏目標所需的還原。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="6bf50-284">未預期的封裝版本警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-284">Unexpected package version warnings</span></span>

<span data-ttu-id="6bf50-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="6bf50-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="6bf50-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="6bf50-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-287">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-287">**Issue**</span></span> | <span data-ttu-id="6bf50-288">直接專案相依性是只有當更新的版本比指定的專案。</span><span class="sxs-lookup"><span data-stu-id="6bf50-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="6bf50-289">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-289">**Common causes**</span></span> | <span data-ttu-id="6bf50-290">另一個相依性套件需要更高的版本，然後兩點封裝。</span><span class="sxs-lookup"><span data-stu-id="6bf50-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="6bf50-291">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-291">**Example message**</span></span> | <span data-ttu-id="6bf50-292">*指定的相依性為 NuGet.Versioning (> = 3.5.0) 但 NuGet.Versioning 4.0.0 結果。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="6bf50-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="6bf50-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-294">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-294">**Issue**</span></span> | <span data-ttu-id="6bf50-295">封裝的相依性遺漏下限。</span><span class="sxs-lookup"><span data-stu-id="6bf50-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="6bf50-296">這不允許還原，若要尋找*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="6bf50-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="6bf50-297">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6bf50-298">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="6bf50-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6bf50-299">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-299">**Common causes**</span></span> | <span data-ttu-id="6bf50-300">這通常是撰寫錯誤的封裝。</span><span class="sxs-lookup"><span data-stu-id="6bf50-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="6bf50-301">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-301">**Example message**</span></span> | <span data-ttu-id="6bf50-302">*NuGet.Packaging 4.0.0 不提供相依性 NuGet.Versioning (> 3.5.0) 下限 （內含）。3.6.0 的近似最符合項目已解決。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="6bf50-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="6bf50-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-304">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-304">**Issue**</span></span> | <span data-ttu-id="6bf50-305">封裝的相依性指定找不到的版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="6bf50-306">較高的版本來取代，這不同於封裝所撰寫針對。</span><span class="sxs-lookup"><span data-stu-id="6bf50-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="6bf50-307">這表示找不到該還原*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="6bf50-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="6bf50-308">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6bf50-309">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="6bf50-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6bf50-310">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-310">**Common causes**</span></span> | <span data-ttu-id="6bf50-311">封裝來源不包含預期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="6bf50-312">如果封裝應該沒有釋出，這可能是封裝撰寫錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bf50-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="6bf50-313">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-313">**Example message**</span></span> | <span data-ttu-id="6bf50-314">NuGet.Packaging 4.0.0 取決於 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="6bf50-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="6bf50-315">5.0.0 的近似最符合項目已解決。</span><span class="sxs-lookup"><span data-stu-id="6bf50-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="6bf50-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="6bf50-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-317">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-317">**Issue**</span></span> | <span data-ttu-id="6bf50-318">專案相依性不會定義繫結至較低。</span><span class="sxs-lookup"><span data-stu-id="6bf50-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="6bf50-319">這表示找不到該還原*最符合項目*。</span><span class="sxs-lookup"><span data-stu-id="6bf50-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="6bf50-320">每個還原會浮動由上至下嘗試尋找可以使用較低版本。</span><span class="sxs-lookup"><span data-stu-id="6bf50-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6bf50-321">這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。</span><span class="sxs-lookup"><span data-stu-id="6bf50-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6bf50-322">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-322">**Common causes**</span></span> | <span data-ttu-id="6bf50-323">專案的*PackageReference* *版本*屬性應該更新為包含下限。</span><span class="sxs-lookup"><span data-stu-id="6bf50-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="6bf50-324">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-324">**Example message**</span></span> | <span data-ttu-id="6bf50-325">*專案相依性 NuGet.Versioning (< = 9.0.0) doe 包含下限 （內含）。相依性版本，以確保結果一致還原包含下限。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="6bf50-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="6bf50-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-327">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-327">**Issue**</span></span> | <span data-ttu-id="6bf50-328">相依性套件指定版本上的條件約束的封裝版本高於還原最後都會解析。</span><span class="sxs-lookup"><span data-stu-id="6bf50-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="6bf50-329">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-329">**Common causes**</span></span> | <span data-ttu-id="6bf50-330">最接近的 wins 解析封裝時。</span><span class="sxs-lookup"><span data-stu-id="6bf50-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="6bf50-331">圖形中的最接近的封裝可能會覆寫遠方的封裝。</span><span class="sxs-lookup"><span data-stu-id="6bf50-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="6bf50-332">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-332">**Example message**</span></span> | <span data-ttu-id="6bf50-333">*偵測到套件降級： 3.5.0 來從 4.0.0 NuGet.Versioning。直接從要選取不同版本的專案參考封裝。<br/>NuGet.Packaging 3.5.0]-> [NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0]-> [NuGet.Configuration 4.0.0]-> [NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="6bf50-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="6bf50-334">解決衝突的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="6bf50-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="6bf50-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-336">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-336">**Issue**</span></span> | <span data-ttu-id="6bf50-337">解析封裝高於允許的相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="6bf50-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="6bf50-338">在某些情況下，這是有意如此，可以隱藏的警告。</span><span class="sxs-lookup"><span data-stu-id="6bf50-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="6bf50-339">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-339">**Common causes**</span></span> | <span data-ttu-id="6bf50-340">直接在專案所參考的封裝將會覆寫從其他套件相依性條件約束。</span><span class="sxs-lookup"><span data-stu-id="6bf50-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="6bf50-341">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-341">**Example message**</span></span> | <span data-ttu-id="6bf50-342">*外部相依性條件約束的偵測到的套件版本： x 1.0.0 需要的 y （= 1.0.0），但 y 2.0.0 的版本是已解決。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="6bf50-343">封裝後援警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="6bf50-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="6bf50-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-345">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-345">**Issue**</span></span> | <span data-ttu-id="6bf50-346">*PackageTargetFallback/AssetTargetFallback*用來從封裝中選取的資產。</span><span class="sxs-lookup"><span data-stu-id="6bf50-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="6bf50-347">這是要讓使用者知道資產可能不相容的 100%的警告。</span><span class="sxs-lookup"><span data-stu-id="6bf50-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="6bf50-348">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-348">**Common causes**</span></span> | <span data-ttu-id="6bf50-349">封裝不支援專案架構。</span><span class="sxs-lookup"><span data-stu-id="6bf50-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="6bf50-350">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-350">**Example message**</span></span> | <span data-ttu-id="6bf50-351">*已還原封裝 'NuGet.Versioning'，'可攜式 net45 + win8' 改為使用專案目標 framework 'netstandard1.5'。此封裝可能無法完全相容，您的專案。*</span><span class="sxs-lookup"><span data-stu-id="6bf50-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="6bf50-352">摘要的警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="6bf50-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="6bf50-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-354">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-354">**Issue**</span></span> | <span data-ttu-id="6bf50-355">讀取摘要時，發生錯誤時`IgnoreFailedSources`設為 true，將它轉換成非嚴重警告。</span><span class="sxs-lookup"><span data-stu-id="6bf50-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="6bf50-356">這可能會包含任何訊息，而且是泛型。</span><span class="sxs-lookup"><span data-stu-id="6bf50-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="6bf50-357">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-357">**Common causes**</span></span> | <span data-ttu-id="6bf50-358">來源無效。</span><span class="sxs-lookup"><span data-stu-id="6bf50-358">The source is invalid.</span></span> |
| <span data-ttu-id="6bf50-359">**範例訊息**</span><span class="sxs-lookup"><span data-stu-id="6bf50-359">**Example message**</span></span> | <span data-ttu-id="6bf50-360">N/A</span><span class="sxs-lookup"><span data-stu-id="6bf50-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="6bf50-361">NuGet 的內部錯誤和警告</span><span class="sxs-lookup"><span data-stu-id="6bf50-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="6bf50-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="6bf50-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="6bf50-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="6bf50-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-364">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-364">**Issue**</span></span> | <span data-ttu-id="6bf50-365">從 NuGet 非特定的內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bf50-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="6bf50-366">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-366">**Common causes**</span></span> | <span data-ttu-id="6bf50-367">檢查記錄檔，如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6bf50-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="6bf50-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="6bf50-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6bf50-369">**問題**</span><span class="sxs-lookup"><span data-stu-id="6bf50-369">**Issue**</span></span> | <span data-ttu-id="6bf50-370">從 NuGet 非特定內部警告。</span><span class="sxs-lookup"><span data-stu-id="6bf50-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="6bf50-371">**常見的原因**</span><span class="sxs-lookup"><span data-stu-id="6bf50-371">**Common causes**</span></span> | <span data-ttu-id="6bf50-372">檢查記錄檔，如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6bf50-372">Check the logs for more information</span></span> |
