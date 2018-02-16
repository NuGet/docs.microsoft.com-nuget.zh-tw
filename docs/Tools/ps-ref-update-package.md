---
title: "NuGet 的更新套件的 PowerShell 參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "在 Visual Studio 中的 NuGet 封裝管理員主控台的更新套件的 PowerShell 命令的參考。"
keywords: "NuGet 封裝管理員主控台中，NuGet Powershell 命令，NuGet Powershell 參考資料，更新套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ebb5a420e469c70a9dd790231a92fedbc4713b6
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>更新套件 （在 Visual Studio 中的封裝管理員主控台）

*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

更新為較新版本的封裝和其相依性或在專案中，所有封裝。

## <a name="syntax"></a>語法

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 +`Update-Package`可用降級專案中現有的封裝。 例如，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級 5.0.0 來：

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

2.7 及更早版本的 NuGet 提供的錯誤訊息已安裝較新版本。

## <a name="parameters"></a>參數

|  參數 | 描述 |
| --- | --- |
| ID | 要更新之封裝的識別碼。 如果省略，更新所有封裝。 -Id 參數是選擇性的。 |
| IgnoreDependencies | 略過更新封裝的相依性。 |
| ProjectName | 包含要更新的封裝，將預設為所有專案的專案名稱。 |
| 版本 | 要用於升級，將預設為最新版本的版本。 在 NuGet 3.0 + 版本的值必須是其中一個*Lowest、 最高、 HighestMinor*，或*HighestPatch* （相當於-安全）。 |
| 安全 | 限制升級至具有相同主要和次要版本與目前已安裝封裝的唯一版本。 |
| 原始程式檔 | 要搜尋的封裝來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Uninstall-Package`搜尋目前選取的套件來源。 |
| IncludePrerelease | 包含套件發行前版本的更新。 |
| 重新安裝 | Resintalls 封裝使用其目前已安裝的版本。 請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。 |
| FileConflictAction | 當詢問您要覆寫或略過專案所參考的現有檔案時要採取動作。 可能的值為*覆寫，忽略、 None、 OverwriteAll*，和*IgnoreAll* （3.0 +）。 |
| DependencyVersion | 若要使用，可以是下列其中之一的相依性套件的版本：<br/><ul><li>*最低*（預設值）： 最低版本</li><li>*HighestPatch*： 具有最低主要、 次要最低、 最高的修補程式的版本</li><li>*HighestMinor*： 具有最低主要版本、 最小、 最高的修補程式</li><li>*最高*（預設值更新套件不含任何參數）： 最高的版本</li></ul>您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。 |
| ToHighestPatch | 限制升級至只具有相同的次要版本與目前已安裝封裝的版本。 |
| ToHighestMinor | 限制升級至只具有相同主要版本與目前已安裝封裝的版本。 |
| WhatIf | 顯示執行命令，而不需實際執行更新時，會發生什麼情況。 |

這些參數接受管線輸入或萬用字元的字元。

### <a name="common-parameters"></a>一般參數

`Update-Package` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

### <a name="examples"></a>範例

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```