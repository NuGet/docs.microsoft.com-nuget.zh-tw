---
title: 將專案檔中的 NuGet 套件設為多個目標
description: 將目標設為單一 NuGet 套件內多個 .NET Framework 版本之各種方法的描述。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 8c1d8a479747f6f7bce388c1555589543c8824a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020064"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="0dbb2-103">在您的專案檔中支援多個 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="0dbb2-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="0dbb2-104">當您第一次建立專案時，我們建議您建立 .NET Standard 類別庫，因為它可為最廣泛的使用專案提供相容性。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="0dbb2-105">根據預設，若使用 .NET Standard，您必須將[跨平台支援](/dotnet/standard/library-guidance/cross-platform-targeting)新增至 .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="0dbb2-106">不過，在某些情節下，您可能也需要包含以特定架構為目標的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="0dbb2-107">此文章顯示如何針對 [SDK 樣式](../resources/check-project-format.md)專案執行此作業。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="0dbb2-108">針對 SDK 樣式專案，您可以在專案檔中設定多目標架構 ([TFM](/dotnet/standard/frameworks)) 的支援，然後使用 `dotnet pack` 或 `msbuild /t:pack` 來建立套件。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="0dbb2-109">nuget.exe CLI 不支援封裝 SDK 樣式專案，因此您應該只使用 `dotnet pack` 或 `msbuild /t:pack`。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="0dbb2-110">我們建議您改為在專案檔中包含通常位於 `.nuspec` 檔案中的[所有屬性](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="0dbb2-111">若要在非 SDK 樣式專案中以多個 .NET Framework 版本為目標，請參閱[支援多個 .NET Framework 版本](supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="0dbb2-112">建立支援多個 .NET Framework 版本的專案</span><span class="sxs-lookup"><span data-stu-id="0dbb2-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="0dbb2-113">在 Visual Studio 中建立新 .NET Standard 類別庫，或使用 `dotnet new classlib`。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="0dbb2-114">我們建議您建立 .NET Standard 類別庫，以獲得最佳相容性。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="0dbb2-115">編輯 *.csproj* 檔案以支援目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="0dbb2-116">例如，</span><span class="sxs-lookup"><span data-stu-id="0dbb2-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="0dbb2-117">變更為：</span><span class="sxs-lookup"><span data-stu-id="0dbb2-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="0dbb2-118">請務必將 XML 元素從單數變更為複數 (將 "s" 新增至開頭和結束標籤)。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="0dbb2-119">如果您有任何只能在一個 TFM 中運作的程式碼，您可以使用 `#if NET45` 或 `#if NETSTANDARD20` 來分隔 TFM 相依程式碼。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="0dbb2-120">(如需詳細資訊，請參閱[如何使用多目標](/dotnet/core/tutorials/libraries#how-to-multitarget)。)例如，您可以使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="0dbb2-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="0dbb2-121">將任何您想要的 NuGet 中繼資料以 MSBuild 屬性新增至 *.csproj*。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="0dbb2-122">如需可用套件中繼資料與 MSBuild 屬性名稱的清單，請參閱[套件目標](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="0dbb2-123">另請參閱[控制相依性資產](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="0dbb2-124">如果您想要將組建相關屬性與 NuGet 中繼資料分開，您可以使用不同的 `PropertyGroup`，或將 NuGet 屬性放在另一個檔案中，並使用 MSBuild 的 `Import` 指示詞來包含它。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="0dbb2-125">從 MSBuild 15.0 開始也支援 `Directory.Build.Props` 與 `Directory.Build.Targets`。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="0dbb2-126">現在，使用 `dotnet pack`，所產生的 *.nupkg* 會以 .NET Standard 2.0 與 .NET Framework 4.5 為目標。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="0dbb2-127">以下是使用上述步驟與 .NET Core SDK 2.2 所產生的 *.csproj* 檔案。</span><span class="sxs-lookup"><span data-stu-id="0dbb2-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="0dbb2-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0dbb2-128">See also</span></span>

* [<span data-ttu-id="0dbb2-129">如何指定目標 Framework</span><span class="sxs-lookup"><span data-stu-id="0dbb2-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="0dbb2-130">跨平台目標</span><span class="sxs-lookup"><span data-stu-id="0dbb2-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
