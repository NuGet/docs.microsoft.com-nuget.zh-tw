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
ms.openlocfilehash: 39212361e7cb2c214c3e83cef604d40cd057fd7e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio 專案系統的 NuGet 支援

為了在 Visual Studio 中支援協力廠商專案類型，NuGet 3.x+ 支援[通用專案系統 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)，而 NuGet 3.2+ 也支援非 CPS 專案類型。

若要與 NuGet 整合，專案系統必須通告其對此主題所述之所有專案功能的專屬支援。


> [!NOTE]
> 基於要在專案中安裝套件，請不要宣告您的專案實際上沒有的功能。 Visual Studio 和其他延伸模組的許多功能都取決於 NuGet 用戶端以外的專案功能。 您專案的錯誤公告功能可能導致這些元件故障，並降低您的使用者體驗。

## <a name="advertise-project-capabilities"></a>公告專案功能

NuGet 用戶端會根據[專案功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md) (如下表所述) 來判斷哪些套件與您的專案類型相容。


|功能|說明|
|----------------|-----------|
|AssemblyReferences|指出專案支援組件參考 (與 WinRTReferences 不同)|
|DeclaredSourceItems|指出專案是一般 MSBuild 專案 (非 DNX)，因為它會宣告專案本身中的來源項目 (而不是假設資料夾中的所有檔案都是編譯一部分的 `project.json` 檔案)。|
|UserSourceItems|指出允許使用者將任意檔案新增至其專案。|

針對 CPS 專案系統，已為您執行本節其餘部分所述之專案功能的實作詳細資料。 請參閱[宣告 CPS 專案中的專案功能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)。

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>實作 VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` 類別必須實作 `IVsBooleanSymbolPresenceChecker` 介面，其定義如下：

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


此介面的範例實作將會是：
    
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

請記得根據您專案系統實際支援的項目，來新增/移除 `ActualProjectCapabilities` 集的功能。 如需完整描述，請參閱[專案功能文件](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)。

## <a name="responding-to-queries"></a>回應查詢

專案會透過 `IVsHierarchy::GetProperty` 支援 `VSHPROPID_ProjectCapabilitiesChecker` 屬性，來宣告此功能。 它應該會傳回 `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` 的執行個體，其定義在 `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` 組件中。 參考此組件的方式是安裝[其 NuGet 套件](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)。

例如，您可能會將下列 `case` 陳述式新增至您 `IVsHierarchy::GetProperty` 方法的 `switch` 陳述式：

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```


## <a name="dte-support"></a>DTE 支援

NuGet 會呼叫 [DTE](https://msdn.microsoft.com/library/mt452175.aspx) (這是最上層 Visual Studio 自動化介面)，來驅動專案系統新增參考、內容項目和 MSBuild 匯入。 DTE 是一組您可能已實作的 COM 介面。

如果您的專案類型根據 CPS，則會為您實作 DTE。
