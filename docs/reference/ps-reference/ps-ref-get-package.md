---
title: NuGet 取得套件 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [取得封裝 PowerShell 的參考] 命令。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1c39fea2131b8f4b8a91314347a19366d5a582c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385189"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>取得套件（Visual Studio 中的套件管理員主控台）

*本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 的「取得封裝」命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

抓取本機存放庫中安裝的套件清單、在搭配-ListAvailable 參數使用時，列出封裝來源中可用的套件，或在搭配-Update 參數使用時，列出可用的更新。

## <a name="syntax"></a>語法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

如果沒有參數，`Get-Package` 會顯示安裝在預設專案中的封裝清單。

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 原始程式檔 | 封裝的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前的資料夾。 如果省略，`Get-Package` 會搜尋目前選取的封裝來源。 與-ListAvailable 搭配使用時，預設為 nuget.org。 |
| ListAvailable | 列出可從封裝來源取得的套件，預設為 nuget.org。除非指定了-PageSize 和/或-First，否則會顯示50套件的預設值。 |
| 更新 | 列出具有可從封裝來源取得更新的套件。 |
| ProjectName | 要從其中取得已安裝封裝的專案。 如果省略，則會傳回整個方案的已安裝專案。 |
| 篩選器 | 用來縮小封裝清單的篩選字串，方法是將它套用至套件識別碼、描述和標記。 |
| 第一個 | 要從清單開頭傳回的封裝數目。 如果未指定，則預設為50。 |
| 略過 | 從顯示的清單中省略第一個 &lt;int&gt; 封裝。  |
| AllVersions | 顯示每個套件的所有可用版本，而不只是最新版本。 |
| IncludePrerelease | 在結果中包含發行前版本套件。 |
| PageSize | *（3.0 +）* 與-ListAvailable （必要）搭配使用時，要列出的封裝數目，再讓提示繼續進行。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Get-Package` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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
