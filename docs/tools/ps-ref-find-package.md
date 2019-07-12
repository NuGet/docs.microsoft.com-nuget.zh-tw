---
title: NuGet Find-package PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台中尋找封裝 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842527"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio 套件管理員主控台)

*版本 3.0 + 中;本主題描述內的命令[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell 尋找套件命令，請參閱 < [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

取得具有指定識別碼或關鍵字的遠端封裝一組從套件來源。

## <a name="syntax"></a>語法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| 識別碼&lt;關鍵字&gt; | （必要）搜尋套件來源時要使用的關鍵字。 您可以使用-ExactMatch 傳回套件識別碼符合關鍵字的封裝。 如果不指定任何關鍵字，`Find-Package`傳回下載項目，或數字的前 20 個套件的清單所指定的第一次。 請注意，-識別碼是選擇性的並執行任何作業。 |
| Source | 要搜尋的套件來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Find-Package`搜尋目前選取的套件來源。 |
| AllVersions | 顯示每個封裝，而不是最新版本的所有可用版本。 |
| 第一個 | 若要從清單開頭傳回封裝的數目預設值為 20。 |
| Skip | 省略第一個&lt;int&gt;套件從顯示的清單。  |
| IncludePrerelease | 在結果中包含發行前版本的套件。 |
| ExactMatch | 指定使用&lt;關鍵字&gt;做為區分大小寫的套件識別碼。 |
| StartWith | 傳回封裝的封裝識別碼的開頭&lt;關鍵字&gt;。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Find-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。

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
