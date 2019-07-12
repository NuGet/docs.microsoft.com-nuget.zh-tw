---
title: NuGet 安裝套件的 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台的安裝套件的 PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842505"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio 套件管理員主控台)

*本主題描述內的命令[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。一般的 PowerShell Install-package 命令，請參閱 < [PowerShell PackageManagement 參考](/powershell/module/packagemanagement/?view=powershell-6)。*

會封裝及其相依性安裝到專案中。

## <a name="syntax"></a>語法

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Nuget 2.8 +`Install-Package`降級您的專案中現有的封裝。 比方說，如果您有安裝 Microsoft.AspNet.MVC 5.1.0-rc1，下列命令會降級至 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>參數

| 參數 | 說明 |
| --- | --- |
| ID | （必要）若要安裝封裝的識別碼。 (*3.0 +* ) 的識別碼可以是路徑或 URL`packages.config`檔案或`.nupkg`檔案。 -識別碼是選擇性參數本身。 |
| IgnoreDependencies | 安裝只需將此套件不及其相依性。 |
| ProjectName | 要安裝套件，將預設為預設專案的專案。 |
| Source | 要搜尋的套件來源 URL 或資料夾的路徑。 本機資料夾路徑可以是絕對的或相對於目前的資料夾。 如果省略，`Install-Package`搜尋目前選取的套件來源。 |
| 版本 | 若要安裝，封裝的版本預設為最新版本。 |
| IncludePrerelease | 會視為發行前版本套件進行安裝。 如果省略，則會被視為穩定的封裝。 |
| FileConflictAction | 當詢問您要覆寫或略過專案所參考的現有檔案時要採取的動作。 可能的值為*覆寫，忽略、 None、 OverwriteAll*，並 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 若要使用，相依性套件可以是下列其中一種版本：<br/><ul><li>*最低*（預設值）： 最低版本</li><li>*HighestPatch*： 具有最低的主要、 次要最低、 最高的修補程式版本</li><li>*HighestMinor*： 具有最低的主要版本、 最小、 最高的修補程式</li><li>*最高*（預設值更新套件不含任何參數）： 最高版本</li></ul>您可以設定預設值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中設定`Nuget.Config`檔案。 |
| WhatIf | 顯示執行命令，而不實際執行安裝時，會發生什麼情況。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Install-Package` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
