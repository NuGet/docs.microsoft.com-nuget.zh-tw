---
title: 識別專案格式
description: 說明如何識別您的專案格式
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488485"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="c0cf6-103">識別專案格式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-103">Identify the project format</span></span>

<span data-ttu-id="c0cf6-104">NuGet 可搭配所有 .NET 專案使用。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="c0cf6-105">不過，專案格式 (SDK 樣式或非 SDK 樣式) 決定取用及建立 NuGet 套件時所需的一些工具與方法。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="c0cf6-106">SDK 樣式專案使用 [SDK 屬性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="c0cf6-107">識別您的專案類型非常重要，因為您用於取用及建立 NuGet 套件的方法與工具取決於專案格式。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="c0cf6-108">針對非 SDK 樣式專案，方法與工具也取決於專案是否已移轉為 `PackageReference` 格式。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="c0cf6-109">您的專案是否為 SDK 樣式取決於用於建立專案的方法。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="c0cf6-110">下表顯示預設專案格式與專案的關聯 CLI 工具 (當您使用 Visual Studio 2017 或更新版本建立專案時)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="c0cf6-111">專案&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="c0cf6-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="c0cf6-112">預設專案格式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-112">Default project format</span></span> | <span data-ttu-id="c0cf6-113">CLI 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="c0cf6-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="c0cf6-114">注意</span><span class="sxs-lookup"><span data-stu-id="c0cf6-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="c0cf6-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="c0cf6-115">.NET Standard</span></span> | <span data-ttu-id="c0cf6-116">SDK 樣式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-116">SDK-style</span></span> | [<span data-ttu-id="c0cf6-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="c0cf6-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="c0cf6-118">使用 Visual Studio 2017 之前版本建立的專案是非 SDK 樣式。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="c0cf6-119">使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="c0cf6-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c0cf6-120">.NET Core</span></span> | <span data-ttu-id="c0cf6-121">SDK 樣式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-121">SDK-style</span></span> | [<span data-ttu-id="c0cf6-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="c0cf6-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="c0cf6-123">使用 Visual Studio 2017 之前版本建立的專案是非 SDK 樣式。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="c0cf6-124">使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="c0cf6-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0cf6-125">.NET Framework</span></span> | <span data-ttu-id="c0cf6-126">非 SDK 樣式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-126">Non-SDK-style</span></span> | [<span data-ttu-id="c0cf6-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="c0cf6-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="c0cf6-128">使用其他方法建立的 .NET Framework 專案可能是 SDK 樣式專案。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="c0cf6-129">針對那些專案，請改為使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="c0cf6-130">[已移轉](../consume-packages/migrate-packages-config-to-package-reference.md) .NET 專案</span><span class="sxs-lookup"><span data-stu-id="c0cf6-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="c0cf6-131">非 SDK 樣式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-131">Non-SDK-style</span></span>| <span data-ttu-id="c0cf6-132">若要建立套件，請使用 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) 來建立套件。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="c0cf6-133">若要建立套件，建議使用 `msbuild -t:pack`。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="c0cf6-134">否則，請使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="c0cf6-135">已移轉的專案不是 SDK 樣式專案。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="c0cf6-136">檢查專案格式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-136">Check the project format</span></span>

<span data-ttu-id="c0cf6-137">若您不確定專案是否為 SDK 樣式格式，請查看專案檔 (針對 C#，這是 \*.csproj 檔案) 中 `<Project>` 元素中是否有 SDK 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="c0cf6-138">若它存在，則專案為 SDK 樣式專案。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="c0cf6-139">在 Visual Studio 中檢查專案格式</span><span class="sxs-lookup"><span data-stu-id="c0cf6-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="c0cf6-140">若您在 Visual Studio 中工作，您可以使用下列其中一種方法快速檢查專案格式：</span><span class="sxs-lookup"><span data-stu-id="c0cf6-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="c0cf6-141">以滑鼠右鍵按一下 [方案總管] 中的專案，然後選取 [編輯 myprojectname.csproj]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="c0cf6-142">只有使用 SDK 樣式屬性的專案 (且必須使用 Visual Studio 2017 與更新版本) 才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="c0cf6-143">否則，請使用其他方法。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-143">Otherwise, use the other method.</span></span>

   ![編輯專案檔](media/edit-project-file.png)

   <span data-ttu-id="c0cf6-145">SDK 樣式專案會在專案檔中顯示 [SDK 屬性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="c0cf6-146">從 [專案]\*\*\*\* 功能表，選擇 [卸載專案]\*\*\*\* (或以滑鼠右鍵按一下專案並選擇 [卸載專案]\*\*\*\*)。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="c0cf6-147">此專案將不會在專案檔中包括 SDK 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="c0cf6-148">它不是 SDK 樣式專案。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-148">It is not an SDK-style project.</span></span>

   ![卸載專案](media/unload-project.png)

   <span data-ttu-id="c0cf6-150">接著，以滑鼠右鍵按一下卸載的專案並選擇 [編輯 myprojectname.csproj]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c0cf6-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0cf6-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c0cf6-151">See also</span></span>

- [<span data-ttu-id="c0cf6-152">使用 dotnet CLI 建立 .NET Standard 套件</span><span class="sxs-lookup"><span data-stu-id="c0cf6-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="c0cf6-153">使用 Visual Studio 建立 .NET Standard 套件</span><span class="sxs-lookup"><span data-stu-id="c0cf6-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="c0cf6-154">建立和發佈 .NET 框架套件(視覺化工作室)</span><span class="sxs-lookup"><span data-stu-id="c0cf6-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="c0cf6-155">NuGet 封裝和還原為 MSBuild 目標</span><span class="sxs-lookup"><span data-stu-id="c0cf6-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
