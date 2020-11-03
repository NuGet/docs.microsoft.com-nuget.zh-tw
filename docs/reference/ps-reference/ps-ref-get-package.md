---
title: NuGet Get-Package PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Get-Package PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237227"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Get-Package (封裝管理員主控台

*本主題說明 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內的命令。如需一般 PowerShell Get-Package 命令，請參閱 [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

抓取本機儲存機制中所安裝的套件清單、列出套件來源中搭配-ListAvailable 參數使用時可使用的封裝，或在搭配-Update 參數使用時，列出可用的更新。

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

如果沒有參數，會 `Get-Package` 顯示安裝在預設專案中的套件清單。

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 來源 | 封裝的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前資料夾的路徑。 如果省略，則會 `Get-Package` 搜尋目前選取的封裝來源。 搭配-ListAvailable 使用時，預設為 nuget.org。 |
| ListAvailable | 列出可從套件來源取得的封裝，預設為 nuget.org。除非指定-PageSize 和/或-First，否則會顯示50封裝的預設值。 |
| 更新 | 列出套件來源中有可用更新的套件。 |
| ProjectName | 要從中取得已安裝封裝的專案。 如果省略，則會傳回整個方案的已安裝專案。 |
| Filter | 篩選字串，用來將封裝清單套用至封裝識別碼、描述和標記，以縮小封裝的範圍。 |
| First | 要從清單開頭返回的封裝數目。 如果未指定，則預設為50。 |
| 跳過 | 省略 &lt; &gt; 所顯示清單中的第一個 int 封裝。  |
| AllVersions | 顯示每個套件的所有可用版本，而不是僅限最新版本。 |
| IncludePrerelease | 在結果中包含發行前版本套件。 |
| PageSize | *(3.0 +)* 搭配-ListAvailable (所需的) 時，要在提供提示繼續之前列出的封裝數目。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Get-Package` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```