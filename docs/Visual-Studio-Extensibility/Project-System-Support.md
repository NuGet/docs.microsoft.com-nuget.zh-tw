---
title: "Visual Studio 專案系統的 NuGet 支援 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "針對協力廠商專案類型，將 NuGet 整合至 Visual Studio 專案系統。"
keywords: "Visual Studio 中的 NuGet、自訂專案類型、Visual Studio 專案"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="e129a-104">Visual Studio 專案系統的 NuGet 支援</span><span class="sxs-lookup"><span data-stu-id="e129a-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="e129a-105">為了在 Visual Studio 中支援協力廠商專案類型，NuGet 3.x+ 支援[通用專案系統 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)，而 NuGet 3.2+ 也支援非 CPS 專案類型。</span><span class="sxs-lookup"><span data-stu-id="e129a-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="e129a-106">若要與 NuGet 整合，專案系統必須通告其對此主題所述之所有專案功能的專屬支援。</span><span class="sxs-lookup"><span data-stu-id="e129a-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="e129a-107">基於要在專案中安裝套件，請不要宣告您的專案實際上沒有的功能。</span><span class="sxs-lookup"><span data-stu-id="e129a-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="e129a-108">Visual Studio 和其他延伸模組的許多功能都取決於 NuGet 用戶端以外的專案功能。</span><span class="sxs-lookup"><span data-stu-id="e129a-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="e129a-109">您專案的錯誤公告功能可能導致這些元件故障，並降低您的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="e129a-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="e129a-110">公告專案功能</span><span class="sxs-lookup"><span data-stu-id="e129a-110">Advertise project capabilities</span></span>

<span data-ttu-id="e129a-111">NuGet 用戶端會根據[專案功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md) (如下表所述) 來判斷哪些套件與您的專案類型相容。</span><span class="sxs-lookup"><span data-stu-id="e129a-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="e129a-112">功能</span><span class="sxs-lookup"><span data-stu-id="e129a-112">Capability</span></span>|<span data-ttu-id="e129a-113">描述</span><span class="sxs-lookup"><span data-stu-id="e129a-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="e129a-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="e129a-114">AssemblyReferences</span></span>|<span data-ttu-id="e129a-115">指出專案支援組件參考 (與 WinRTReferences 不同)</span><span class="sxs-lookup"><span data-stu-id="e129a-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="e129a-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="e129a-116">DeclaredSourceItems</span></span>|<span data-ttu-id="e129a-117">指出專案是一般 MSBuild 專案 (非 DNX)，因為它會宣告專案本身中的來源項目 (而不是假設資料夾中的所有檔案都是編譯一部分的 `project.json` 檔案)。</span><span class="sxs-lookup"><span data-stu-id="e129a-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="e129a-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="e129a-118">UserSourceItems</span></span>|<span data-ttu-id="e129a-119">指出允許使用者將任意檔案新增至其專案。</span><span class="sxs-lookup"><span data-stu-id="e129a-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="e129a-120">針對 CPS 專案系統，已為您執行本節其餘部分所述之專案功能的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e129a-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="e129a-121">請參閱[宣告 CPS 專案中的專案功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)。</span><span class="sxs-lookup"><span data-stu-id="e129a-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="e129a-122">實作 VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="e129a-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="e129a-123">`VsProjectCapabilitiesPresenceChecker` 類別必須實作 `IVsBooleanSymbolPresenceChecker` 介面，其定義如下：</span><span class="sxs-lookup"><span data-stu-id="e129a-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```


<span data-ttu-id="e129a-124">此介面的範例實作將會是：</span><span class="sxs-lookup"><span data-stu-id="e129a-124">A sample implementation of this interface would then be:</span></span>
    
```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="e129a-125">請記得根據您專案系統實際支援的項目，來新增/移除 `ActualProjectCapabilities` 集的功能。</span><span class="sxs-lookup"><span data-stu-id="e129a-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="e129a-126">如需完整描述，請參閱[專案功能文件](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="e129a-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="e129a-127">回應查詢</span><span class="sxs-lookup"><span data-stu-id="e129a-127">Responding to queries</span></span>

<span data-ttu-id="e129a-128">專案會透過 `IVsHierarchy::GetProperty` 支援 `VSHPROPID_ProjectCapabilitiesChecker` 屬性，來宣告此功能。</span><span class="sxs-lookup"><span data-stu-id="e129a-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="e129a-129">它應該會傳回 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` 的執行個體，其定義在 `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 組件中。</span><span class="sxs-lookup"><span data-stu-id="e129a-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="e129a-130">參考此組件的方式是安裝[其 NuGet 套件](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)。</span><span class="sxs-lookup"><span data-stu-id="e129a-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="e129a-131">例如，您可能會將下列 `case` 陳述式新增至您 `IVsHierarchy::GetProperty` 方法的 `switch` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="e129a-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="e129a-132">DTE 支援</span><span class="sxs-lookup"><span data-stu-id="e129a-132">DTE Support</span></span>

<span data-ttu-id="e129a-133">NuGet 會呼叫 [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017) (這是最上層 Visual Studio 自動化介面)，來驅動專案系統新增參考、內容項目和 MSBuild 匯入。</span><span class="sxs-lookup"><span data-stu-id="e129a-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="e129a-134">DTE 是一組您可能已實作的 COM 介面。</span><span class="sxs-lookup"><span data-stu-id="e129a-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="e129a-135">如果您的專案類型根據 CPS，則會為您實作 DTE。</span><span class="sxs-lookup"><span data-stu-id="e129a-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
