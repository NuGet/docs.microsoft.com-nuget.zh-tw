---
title: NuGet Find-package PowerShell 參考 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中尋找封裝 PowerShell 命令的參考。
keywords: NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，尋找封裝
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 32b15ff415e77c3e063ded637a614fc8a04d5a0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>尋找套件 （在 Visual Studio 中的封裝管理員主控台）

*3.0 +; 版本本主題描述內的命令[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。一般的 PowerShell Find-package 命令，請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

從套件來源取得具有指定識別碼或關鍵字的遠端套件集。

## <a name="syntax"></a>語法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 識別碼&lt;關鍵字&gt; | （必要）若要搜尋的套件來源時使用的關鍵字。 使用 ExactMatch 傳回其封裝識別碼符合關鍵字的套件。 如果不指定任何關鍵字`Find-Package`傳回的前 20 套件下載，或數字的清單所指定的第一次。 請注意，-識別碼是選擇性，並執行任何作業。 |
| 原始程式檔 | 要搜尋的封裝來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Find-Package`搜尋目前選取的套件來源。 |
| AllVersions | 顯示所有可用的版本，每個封裝而不是最新的版本。 |
| First | 要從清單開頭傳回的套件數目預設為 20。 |
| Skip | 省略第一個&lt;int&gt;封裝從顯示的清單。  |
| IncludePrerelease | 在結果中包含套件發行前版本。 |
| ExactMatch | 指定使用&lt;關鍵字&gt;為區分大小寫的封裝識別碼。 |
| StartWith | 傳回封裝的封裝識別碼的開頭&lt;關鍵字&gt;。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Find-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
