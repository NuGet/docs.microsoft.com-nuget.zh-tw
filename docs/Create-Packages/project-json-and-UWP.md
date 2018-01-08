---
title: "UWP 專案的 NuGet project.json 檔案 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "描述如何使用 project.json 檔案來追蹤通用 Windows 平台 (UWP) 專案中的 NuGet 相依性。"
keywords: "NuGet 相依性, NuGet 和 UWP, UWP 和 project.json, NuGet project.json 檔案"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40507e541997cea368052c373a4124d9c4a00a51
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="1e662-104">project.json 和 UWP</span><span class="sxs-lookup"><span data-stu-id="1e662-104">project.json and UWP</span></span>

<span data-ttu-id="1e662-105">本文件描述採用 NuGet 3+ 中功能的套件結構 (Visual Studio 2015 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="1e662-105">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="1e662-106">`.nuspec` 的 `minClientVersion` 屬性可以用來說明您需要這裡所述的功能，方法是將它設定為 3.1。</span><span class="sxs-lookup"><span data-stu-id="1e662-106">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="1e662-107">將 UWP 支援新增至現有套件</span><span class="sxs-lookup"><span data-stu-id="1e662-107">Adding UWP support to an existing package</span></span>

<span data-ttu-id="1e662-108">如果您有現有套件，而且想要新增 UWP 應用程式的支援，則不需要採用這裡所述的套件格式。</span><span class="sxs-lookup"><span data-stu-id="1e662-108">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="1e662-109">只有在您需要它所描述的功能，而且願意只與已更新為 NuGet 用戶端 3+ 版的用戶端合作時，才需要採用這種格式。</span><span class="sxs-lookup"><span data-stu-id="1e662-109">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="1e662-110">我已經將目標設為 netcore45</span><span class="sxs-lookup"><span data-stu-id="1e662-110">I already target netcore45</span></span>

<span data-ttu-id="1e662-111">如果您已經將目標設為 `netcore45`，而且不需要利用這裡的功能，則不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="1e662-111">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="1e662-112">UWP 應用程式可以使用 `netcore45` 套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-112">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="1e662-113">我想要利用 Windows 10 特定 API</span><span class="sxs-lookup"><span data-stu-id="1e662-113">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="1e662-114">在此情況下，您需要將 `uap10.0` 目標架構 Moniker (TFM 或 TxM) 新增至套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-114">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="1e662-115">在套件中建立新的資料夾，並將已編譯以使用 Windows 10 的組件新增至該資料夾。</span><span class="sxs-lookup"><span data-stu-id="1e662-115">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="1e662-116">我不需要 Windows 10 特定 API，但想要新的 .NET 功能或還沒有 netcore45</span><span class="sxs-lookup"><span data-stu-id="1e662-116">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="1e662-117">在此情況下，您需要將 `dotnet` TxM 新增至套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-117">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="1e662-118">與其他 TxM 不同，`dotnet` 不表示為介面區或平台。</span><span class="sxs-lookup"><span data-stu-id="1e662-118">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="1e662-119">它會指出您的套件適用於相依性所作用的任何平台。</span><span class="sxs-lookup"><span data-stu-id="1e662-119">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="1e662-120">使用 `dotnet` TxM 建置套件時，在 `.nuspec` 中，您可能會有許多其他 TxM 特定相依性，因為您需要定義相依的 BCL 套件，例如 `System.Text`、`System.Xml` 等等。這些相依性作用的位置定義您套件的運作位置。</span><span class="sxs-lookup"><span data-stu-id="1e662-120">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="1e662-121">如何找出我的相依性</span><span class="sxs-lookup"><span data-stu-id="1e662-121">How do I find out my dependencies</span></span>

<span data-ttu-id="1e662-122">有兩種方式可找出要列出的相依性：</span><span class="sxs-lookup"><span data-stu-id="1e662-122">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="1e662-123">使用 [NuSpec 相依性產生器](https://github.com/onovotny/ReferenceGenerator)**協力廠商**工具。</span><span class="sxs-lookup"><span data-stu-id="1e662-123">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="1e662-124">此工具會將這個程序自動化，並在建置時使用相依套件更新 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e662-124">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="1e662-125">它可透過 NuGet 套件 [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) 取得。</span><span class="sxs-lookup"><span data-stu-id="1e662-125">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>
2. <span data-ttu-id="1e662-126">(較難方式) 使用 `ILDasm` 查看 `.dll`，以查看執行階段實際需要的組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-126">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="1e662-127">然後判斷其各個所來自的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-127">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="1e662-128">如需協助建立支援 `dotnet` TxM 之套件的功能詳細資料，請參閱 [`project.json`](../Schema/project-json.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="1e662-128">See the [`project.json`](../Schema/project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="1e662-129">如果您的套件是要使用 PCL 專案，則強烈建議建立 `dotnet` 資料夾，以避免警告和潛在的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="1e662-129">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>


## <a name="directory-structure"></a><span data-ttu-id="1e662-130">目錄結構</span><span class="sxs-lookup"><span data-stu-id="1e662-130">Directory structure</span></span>

<span data-ttu-id="1e662-131">使用此格式的 NuGet 套件具有下列已知資料夾和行為：</span><span class="sxs-lookup"><span data-stu-id="1e662-131">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="1e662-132">資料夾</span><span class="sxs-lookup"><span data-stu-id="1e662-132">Folder</span></span> | <span data-ttu-id="1e662-133">「行為」</span><span class="sxs-lookup"><span data-stu-id="1e662-133">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="1e662-134">組建</span><span class="sxs-lookup"><span data-stu-id="1e662-134">Build</span></span> | <span data-ttu-id="1e662-135">在此資料夾中包含 MSBuild 目標和屬性檔，會以不同的方式整合至專案，但沒有任何變更。</span><span class="sxs-lookup"><span data-stu-id="1e662-135">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="1e662-136">工具</span><span class="sxs-lookup"><span data-stu-id="1e662-136">Tools</span></span> | <span data-ttu-id="1e662-137">未執行 `install.ps1` 和 `uninstall.ps1`。</span><span class="sxs-lookup"><span data-stu-id="1e662-137">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="1e662-138">`init.ps1` 會如常運作。</span><span class="sxs-lookup"><span data-stu-id="1e662-138">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="1e662-139">內容</span><span class="sxs-lookup"><span data-stu-id="1e662-139">Content</span></span> | <span data-ttu-id="1e662-140">內容不會自動複製至使用者的專案中。</span><span class="sxs-lookup"><span data-stu-id="1e662-140">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="1e662-141">更新的版本已規劃專案中的內容包含支援。</span><span class="sxs-lookup"><span data-stu-id="1e662-141">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="1e662-142">Lib</span><span class="sxs-lookup"><span data-stu-id="1e662-142">Lib</span></span> | <span data-ttu-id="1e662-143">針對許多套件，`lib` 的運作方式都與在 NuGet 2.x 中相同，但具有擴充選項，可在其內使用名稱，以及在使用套件時選擇正確子資料夾的較佳邏輯。</span><span class="sxs-lookup"><span data-stu-id="1e662-143">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="1e662-144">不過，與 `ref` 搭配使用時，`lib` 資料夾所包含的組件會實作 `ref` 資料夾中組件所定義的介面區。</span><span class="sxs-lookup"><span data-stu-id="1e662-144">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="1e662-145">參考</span><span class="sxs-lookup"><span data-stu-id="1e662-145">Ref</span></span> | <span data-ttu-id="1e662-146">`ref` 為選用資料夾，其中包含定義公用介面 (公用類型和方法) 的 .NET 組件，讓應用程式對其進行編譯。</span><span class="sxs-lookup"><span data-stu-id="1e662-146">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="1e662-147">此資料夾中的組件可能沒有實作，它們只用來定義編譯器的介面區。</span><span class="sxs-lookup"><span data-stu-id="1e662-147">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="1e662-148">如果套件沒有 `ref` 資料夾，則 `lib` 既是參考組件也是實作組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-148">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="1e662-149">執行階段</span><span class="sxs-lookup"><span data-stu-id="1e662-149">Runtimes</span></span> | <span data-ttu-id="1e662-150">`runtimes` 是選擇性資料夾，其中包含 OS 特定程式碼，例如 CPU 架構與 OS 特定或平台相依二進位檔。</span><span class="sxs-lookup"><span data-stu-id="1e662-150">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |


## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="1e662-151">套件中的 MSBuild 目標和屬性檔</span><span class="sxs-lookup"><span data-stu-id="1e662-151">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="1e662-152">NuGet 套件可以包含 `.targets` 和 `.props` 檔案，而這些檔案匯入至套件安裝所在的任何 MSBuild 專案。</span><span class="sxs-lookup"><span data-stu-id="1e662-152">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="1e662-153">在 NuGet 2.x 中，做法是將 `<Import>` 陳述式插入 `.csproj` 檔案中，而在 NuGet 3.0 中，則沒有特定「專案安裝」動作。</span><span class="sxs-lookup"><span data-stu-id="1e662-153">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="1e662-154">相反地，套件還原程序會寫入兩個檔案 `[projectname].nuget.props` 和 `[projectname].NuGet.targets`。</span><span class="sxs-lookup"><span data-stu-id="1e662-154">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="1e662-155">MSBuild 知道要尋找這兩個檔案，並在專案建置程序即將開始和即將結束時自動予以匯入。</span><span class="sxs-lookup"><span data-stu-id="1e662-155">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="1e662-156">其提供的行為與 NuGet 2.x 非常類似，但有一個主要差異：「在此情況下不保證目標/屬性檔順序」。</span><span class="sxs-lookup"><span data-stu-id="1e662-156">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="1e662-157">不過，MSBuild 確實會提供方法，透過 `<Target>` 定義的 `BeforeTargets` 和 `AfterTargets` 屬性來排序目標 (請參閱[目標項目 (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild))。</span><span class="sxs-lookup"><span data-stu-id="1e662-157">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](https://docs.microsoft.com/visualstudio/msbuild/target-element-msbuild).</span></span>


## <a name="lib-and-ref"></a><span data-ttu-id="1e662-158">Lib 和 Ref</span><span class="sxs-lookup"><span data-stu-id="1e662-158">Lib and Ref</span></span>

<span data-ttu-id="1e662-159">在 NuGet v3 中，`lib` 資料夾的行為沒有太大變更。</span><span class="sxs-lookup"><span data-stu-id="1e662-159">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="1e662-160">不過，所有組件都必須在 TxM 之後所命名的子資料夾內，而且無法再直接放在 `lib` 資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="1e662-160">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="1e662-161">TxM 是假設套件中指定資產作用的平台名稱。</span><span class="sxs-lookup"><span data-stu-id="1e662-161">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="1e662-162">就邏輯而言，這些是目標架構 Moniker (TFM) 的延伸模組，例如 `net45`、`net46`、`netcore50` 和 `dnxcore50` 全部都是 TxM 範例 (請參閱[目標架構](../Schema/Target-Frameworks.md))。</span><span class="sxs-lookup"><span data-stu-id="1e662-162">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../Schema/Target-Frameworks.md).</span></span> <span data-ttu-id="1e662-163">TxM 可以參照架構 (TFM) 以及其他平台特定介面區。</span><span class="sxs-lookup"><span data-stu-id="1e662-163">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="1e662-164">例如，UWP TxM (`uap10.0`) 代表 .NET 介面區，以及 UWP 應用程式的 Windows 介面區。</span><span class="sxs-lookup"><span data-stu-id="1e662-164">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="1e662-165">範例 lib 結構：</span><span class="sxs-lookup"><span data-stu-id="1e662-165">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="1e662-166">`lib` 資料夾包含在執行階段使用的組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-166">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="1e662-167">針對大部分套件，您只需要 `lib` 下每個目標 TxM 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1e662-167">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="1e662-168">參考</span><span class="sxs-lookup"><span data-stu-id="1e662-168">Ref</span></span>

<span data-ttu-id="1e662-169">有時，在編譯期間應該使用不同的組件 (.NET 參考組件現在會執行此作業)。</span><span class="sxs-lookup"><span data-stu-id="1e662-169">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="1e662-170">在這些情況下，使用稱為 `ref` (「參考組件」的簡稱) 的最上層資料夾。</span><span class="sxs-lookup"><span data-stu-id="1e662-170">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="1e662-171">大部分套件作者不需要 `ref` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1e662-171">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="1e662-172">它適用於套件，而套件需要提供編譯和 IntelliSense 的一致介面區，但不同的 TxM 有不同的實作。</span><span class="sxs-lookup"><span data-stu-id="1e662-172">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="1e662-173">這個的最大使用案例是在 NuGet 上傳遞 .NET Core 時所產生的 `System.*` 套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-173">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="1e662-174">這些套件有透過一組一致的參考組件統一的各種實作。</span><span class="sxs-lookup"><span data-stu-id="1e662-174">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="1e662-175">透過機械方式，將 `ref` 資料夾中所含的組件傳遞至編譯器的參考組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-175">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="1e662-176">針對已使用 csc.exe 的人員，這些是傳遞給 [C# /reference 選項](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)參數的組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-176">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](https://docs.microsoft.com/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="1e662-177">`ref` 資料夾的結構與 `lib` 相同，例如：</span><span class="sxs-lookup"><span data-stu-id="1e662-177">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


<span data-ttu-id="1e662-178">在此範例中，`ref` 目錄中的組件都會相同。</span><span class="sxs-lookup"><span data-stu-id="1e662-178">In this example the assemblies in the `ref` directories would all be identical.</span></span>


## <a name="runtimes"></a><span data-ttu-id="1e662-179">執行階段</span><span class="sxs-lookup"><span data-stu-id="1e662-179">Runtimes</span></span>

<span data-ttu-id="1e662-180">runtimes 資料夾包含在特定「執行階段」上執行所需的組件和原生程式庫，而執行階段一般是透過作業系統和 CPU 架構所定義。</span><span class="sxs-lookup"><span data-stu-id="1e662-180">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="1e662-181">這些執行階段是使用[執行階段識別碼 (RID)](https://docs.microsoft.com/dotnet/core/rid-catalog) (例如 `win`、`win-x86`、`win7-x86`、`win8-64` 等等) 進行識別。</span><span class="sxs-lookup"><span data-stu-id="1e662-181">These runtimes are identified using [Runtime Identifiers (RIDs)](https://docs.microsoft.com/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="1e662-182">原生重點</span><span class="sxs-lookup"><span data-stu-id="1e662-182">Native light-up</span></span>

<span data-ttu-id="1e662-183">下列範例示範具有數個平台之純受控 實作的套件，但在 Windows 8 上使用可呼叫 Windows 8 特定原生 API 的原生協助程式。</span><span class="sxs-lookup"><span data-stu-id="1e662-183">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="1e662-184">如果是上述套件，則會發生下列事項：</span><span class="sxs-lookup"><span data-stu-id="1e662-184">Given the above package the following things happen:</span></span>

- <span data-ttu-id="1e662-185">不在 Windows 8 時，會使用 `lib/net40/MyLibrary.dll` 組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-185">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="1e662-186">在 Windows 8 上時，會使用 `runtimes/win8-<architecture>/lib/MyLibrary.dll`，並且將 `native/MyNativeHelper.dll` 複製至組建輸出。</span><span class="sxs-lookup"><span data-stu-id="1e662-186">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="1e662-187">在上述範例中，`lib/net40` 組件是純受控程式碼，而 runtimes 資料夾中的組件將會 p/叫用到原生協助程式組件，以呼叫 Windows 8 特有的 API。</span><span class="sxs-lookup"><span data-stu-id="1e662-187">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="1e662-188">只會挑選單一 `lib` 資料夾，因此如果有執行階段特定資料夾，則會透過非執行階段特定 `lib` 來選擇它。</span><span class="sxs-lookup"><span data-stu-id="1e662-188">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it is chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="1e662-189">原生資料夾是加總，如果已存在，則會將它複製至組建輸出。</span><span class="sxs-lookup"><span data-stu-id="1e662-189">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="1e662-190">受控包裝函式</span><span class="sxs-lookup"><span data-stu-id="1e662-190">Managed wrapper</span></span>

<span data-ttu-id="1e662-191">另一種使用執行階段的方法是傳遞透過原生組件之純受控包裝函式的套件。</span><span class="sxs-lookup"><span data-stu-id="1e662-191">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="1e662-192">在此情況下，您可以建立套件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e662-192">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="1e662-193">在此情況下，沒有與該資料夾相同的最上層 `lib` 資料夾，因為沒有此套件的實作未依賴對應原生組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-193">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="1e662-194">在這兩種情況下，如果受控組件 `MyLibrary.dll` 完全相同，則可以將它放入最上層 `lib` 資料夾，但因為缺少原生組件並不會造成套件安裝失敗，所以如果它已安裝在不是 win-x86 或 win-x64 的平台上，則會使用最上層 lib，但不會複製任何原生組件。</span><span class="sxs-lookup"><span data-stu-id="1e662-194">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="1e662-195">編寫 NuGet 2 和 NuGet 3 的套件</span><span class="sxs-lookup"><span data-stu-id="1e662-195">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="1e662-196">如果您想要建立使用 `packages.config` 的專案以及使用 `project.json` 的套件可使用的套件，則下列項目適用：</span><span class="sxs-lookup"><span data-stu-id="1e662-196">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="1e662-197">Ref 和執行階段只作用於 NuGet 3。</span><span class="sxs-lookup"><span data-stu-id="1e662-197">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="1e662-198">NuGet 2 會同時忽略它們。</span><span class="sxs-lookup"><span data-stu-id="1e662-198">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="1e662-199">您無法依賴 `install.ps1` 或 `uninstall.ps1` 運作。</span><span class="sxs-lookup"><span data-stu-id="1e662-199">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="1e662-200">使用 `packages.config` 時，會執行這些檔案，但在使用 `project.json` 時則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="1e662-200">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="1e662-201">因此，您的套件需要可用，而不需要執行。</span><span class="sxs-lookup"><span data-stu-id="1e662-201">So your package needs to be usable without them running.</span></span> <span data-ttu-id="1e662-202">`init.ps1` 仍在 NuGet 3 上執行。</span><span class="sxs-lookup"><span data-stu-id="1e662-202">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="1e662-203">目標和屬性安裝不同，因此請確定您的套件在這兩個用戶端上如預期運作。</span><span class="sxs-lookup"><span data-stu-id="1e662-203">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="1e662-204">在 NuGet 3 中，lib 的子目錄必須是 TxM。</span><span class="sxs-lookup"><span data-stu-id="1e662-204">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="1e662-205">您無法將二進位檔放到 `lib` 資料夾根目錄。</span><span class="sxs-lookup"><span data-stu-id="1e662-205">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="1e662-206">使用 NuGet 3，不會自動複製內容。</span><span class="sxs-lookup"><span data-stu-id="1e662-206">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="1e662-207">您套件的取用者可以自行複製檔案，或使用工作執行器這類工具將複製檔案自動化。</span><span class="sxs-lookup"><span data-stu-id="1e662-207">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="1e662-208">原始程式檔和組態檔轉換不是由 NuGet 3 所執行。</span><span class="sxs-lookup"><span data-stu-id="1e662-208">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="1e662-209">如果您支援 NuGet 2 和 3，則 `minClientVersion` 應該是您套件所處理之 NuGet 2 用戶端的最低版本。</span><span class="sxs-lookup"><span data-stu-id="1e662-209">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="1e662-210">如果是現有套件，則不需要進行變更。</span><span class="sxs-lookup"><span data-stu-id="1e662-210">In the case of an existing package it shouldn't need to change.</span></span>