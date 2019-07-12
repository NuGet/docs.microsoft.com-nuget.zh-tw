---
title: NuGet 取得套件的 PowerShell 參考
description: 取得封裝的 PowerShell 命令，在 Visual Studio 中的 NuGet 套件管理員主控台的參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842510"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio 套件管理員主控台)

*本主題描述內的命令[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell Get 封裝命令，請參閱 < [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

擷取安裝在本機存放庫的封裝清單，列出可用的封裝，從套件來源-ListAvailable 參數搭配使用時或列出可用的更新-Update 參數搭配使用時。

## <a name="syntax"></a>語法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

使用任何參數，`Get-Package`顯示的預設專案中安裝的套件清單。

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| Source | 封裝 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Get-Package`搜尋目前選取的套件來源。 當搭配-ListAvailable，預設值 nuget.org。 |
| ListAvailable | 列出可用的封裝，從套件來源，將預設為 nuget.org。除非指定-PageSize 和/或-第一個會顯示預設值為 50 的封裝。 |
| 更新 | 列出從套件來源有可用更新的封裝。 |
| ProjectName | 要從中取得安裝的套件的專案。 如果省略，則會傳回安裝整個方案的專案。 |
| 篩選器 | 篩選條件字串，用來縮小的封裝清單，將它套用到封裝識別碼、 描述和標記。 |
| 第一個 | 若要從清單開頭傳回的封裝數目。 如果未指定，預設值為 50。 |
| Skip | 省略第一個&lt;int&gt;套件從顯示的清單。  |
| AllVersions | 顯示每個封裝，而不是最新版本的所有可用版本。 |
| IncludePrerelease | 在結果中包含發行前版本的套件。 |
| PageSize | *（3.0 +)* 當封裝的數目-ListAvailable （必要），搭配送交提示以繼續之前，先列出。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Get-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。

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
