---
title: NuGet 尋找-封裝 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 [尋找套件] PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327385"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio 套件管理員主控台)

*3.0 版 +;本主題說明在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中的命令。如需一般 PowerShell 的尋找封裝命令, 請參閱[PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

從封裝來源取得具有指定識別碼或關鍵字之遠端封裝的集合。

## <a name="syntax"></a>語法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| Id &lt;關鍵字&gt; | 具備搜尋封裝來源時要使用的關鍵字。 使用-ExactMatch, 只傳回套件識別碼符合關鍵字的封裝。 如果未指定任何關鍵字, `Find-Package`則會傳回前20個封裝的清單 (依下載), 或由-First 指定的數位。 請注意,-Id 是選擇性的, 也是無 op。 |
| Source | 要搜尋之封裝來源的 URL 或資料夾路徑。 本機資料夾路徑可以是絕對或相對於目前的資料夾。 如果省略, `Find-Package`則會搜尋目前選取的封裝來源。 |
| AllVersions | 顯示每個套件的所有可用版本, 而不只是最新版本。 |
| 第一個 | 要從清單開頭傳回的封裝數目;預設值為20。 |
| Skip | 省略所顯示&lt;清單&gt;中的第一個 int 封裝。  |
| IncludePrerelease | 在結果中包含發行前版本套件。 |
| ExactMatch | 指定使用&lt;關鍵字&gt;做為區分大小寫的封裝識別碼。 |
| StartWith | 傳回封裝識別碼開頭為&lt;關鍵字&gt;的封裝。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Find-Package`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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
