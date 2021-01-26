---
title: NuGet Find-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Find-Package PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777514"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Find-Package (封裝管理員主控台

*3.0 版 +;本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Find-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

從套件來源取得具有指定識別碼或關鍵字的遠端封裝集合。

## <a name="syntax"></a>語法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 識別碼 &lt; 關鍵字&gt; |  (在搜尋套件來源時，需要使用) 關鍵字。 使用-ExactMatch 只傳回套件識別碼符合關鍵字的封裝。 如果未指定任何關鍵字，則會 `Find-Package` 依下載傳回前20個封裝的清單，或依-First 指定的數位。 請注意，-Id 是選擇性的，且不會有任何作用。 |
| 來源 | 要搜尋之套件來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。 如果省略，則會 `Find-Package` 搜尋目前選取的封裝來源。 |
| AllVersions | 顯示每個套件的所有可用版本，而不是僅限最新版本。 |
| First | 要從清單開頭傳回的封裝數目;預設值為20。 |
| 跳過 | 省略 &lt; &gt; 所顯示清單中的第一個 int 封裝。  |
| IncludePrerelease | 在結果中包含發行前版本套件。 |
| ExactMatch | 指定為使用 &lt; 關鍵字 &gt; 做為區分大小寫的套件識別碼。 |
| StartWith | 傳回封裝識別碼開頭為關鍵字的 &lt; 封裝 &gt; 。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Find-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```