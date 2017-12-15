---
title: "NuGet 取得封裝的 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "取得封裝 PowerShell 命令，在 Visual Studio 中的 NuGet 封裝管理員主控台中的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，取得封裝"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3f93ab82e9fb769ee20070aa39ba8e3e05953839
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>取得封裝 （在 Visual Studio 中的封裝管理員主控台）

*本主題描述內的命令[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上的 Visual Studio 中。一般 PowerShell 取得封裝的命令，請參閱[PowerShell PackageManagement 參考](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6)。*

擷取安裝在本機儲存機制中的封裝清單，列出可用的封裝，從套件來源時使用-ListAvailable 參數或列出可用的更新，當搭配-Update 參數。

## <a name="syntax"></a>語法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

使用任何參數，`Get-Package`顯示的預設專案中安裝的封裝清單。

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| 來源 | 封裝的 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Get-Package`搜尋目前選取的套件來源。 當搭配使用-ListAvailable，預設為 nuget.org。 |
| ListAvailable | 列出可用的封裝，從套件來源，將預設為 nuget.org。除非已指定-PageSize 及/或-第一個會顯示預設值是 50 的封裝。 |
| 更新 | 列出從套件來源中有可用更新的封裝。 |
| ProjectName | 要從中取得已安裝的套件的專案。 如果省略，則傳回安裝整個方案的專案。 |
| 篩選器 | 篩選條件字串，用來縮小的封裝清單，將它套用到封裝識別碼、 描述和標記。 |
| First | 要從清單開頭傳回的套件數目。 如果未指定，預設值為 50。 |
| Skip | 省略第一個&lt;int&gt;封裝從顯示的清單。  |
| AllVersions | 顯示所有可用的版本，每個封裝而不是最新的版本。 |
| IncludePrerelease | 在結果中包含套件發行前版本。 |
| PageSize | *（3.0 +)*時搭配使用-ListAvailable （必要），封裝的數目，列出要繼續的提示之前。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Get-Package`支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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

