---
title: "NuGet 封裝管理員主控台指南 |Microsoft 文件"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords: vs.nuget.packagemanager.console
description: "使用 Visual Studio 中的 NuGet 封裝管理員主控台，使用封裝的指示。"
keywords: "NuGet 封裝管理員主控台中，NuGet powershell 管理 NuGet 封裝"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b89c51812cee0f64c6f5c39cd9d86bc4a0be068e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="package-manager-console"></a>封裝管理員主控台

NuGet 封裝管理員主控台內建在 Windows 2012 及更新版本的 Visual Studio 中。 （它不包含在 Visual Studio for Mac 或 Visual Studio 程式碼）。

在主控台可讓您使用[NuGet PowerShell 命令](../tools/powershell-reference.md)尋找、 安裝、 解除安裝和更新 NuGet 套件。 在 「 封裝管理員 」 UI 不提供方法來執行作業的情況下，必須使用主控台。 若要使用`nuget.exe`命令在主控台中，請參閱[使用主控台中的 nuget.exe CLI](#using-the-nugetexe-cli-in-the-console)。

例如，尋找和安裝封裝是使用三個簡單步驟完成：

1. 在 Visual Studio 中，開啟 專案/方案，並開啟主控台使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。

1. 尋找您想要安裝的套件。 如果您已經知道這個，請跳至步驟 3。

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. 執行安裝命令：

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> 也可以使用完成所有作業都可在主控台[NuGet CLI](../tools/nuget-exe-cli-reference.md)。 不過，主控台命令的 Visual Studio，並儲存的專案/方案內容中運作，而且通常超過其對等的 CLI 命令完成。 比方說，安裝套件，以透過主控台將參考加入專案而不 CLI 命令。 基於這個理由，通常使用 Visual Studio 中的開發人員會習慣使用 CLI 至主控台。

> [!Tip]
> 許多的主控台作業取決於 Visual Studio 中開啟具有已知的路徑名稱的解決方案。 如果您有未儲存的方案或沒有解決方案，您可以看到下列錯誤:"是未開啟或儲存方案。 請確定您有已開啟和已儲存的方案。 」 這表示主控台無法判斷方案資料夾。 儲存未儲存的方案，或建立及儲存方案，如果您還沒有開啟，應該更正錯誤。

## <a name="opening-the-console-and-console-controls"></a>開啟的主控台和主控台控制項

1. 開啟主控台，在 Visual Studio 使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。 主控台的 Visual Studio 視窗可以排列和定位不過嗎 (請參閱[自訂 Visual Studio 中的視窗配置](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 根據預設，主控台命令做為針對特定的封裝來源和專案集合中的控制項視窗的頂端：

    ![封裝來源和專案的封裝管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. 選取不同的封裝來源及/或專案就會變更後續命令的這些預設值。 若要 overrride 而不需要變更預設值，這些設定大部分的命令支援`-Source`和`-ProjectName`選項。

1. 若要管理的封裝來源，請選取齒輪圖示。 這是捷徑**工具 > 選項 > NuGet 套件管理員 > 的封裝來源**對話方塊上所述[封裝管理員 UI](Package-Manager-UI.md#package-sources)頁面。 此外，右邊的專案選擇器控制項清除主控台的內容：

    ![封裝管理員主控台設定和清除控制項](media/PackageManagerConsoleControls2.png)

1. 最右邊的按鈕會中斷長時間執行命令。 例如，執行`Get-Package -ListAvailable -PageSize 500`列出的前 500 套件上的預設來源 （例如 nuget.org)，這可能需要幾分鐘才能完成。

    ![封裝管理員主控台停止控制](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>安裝封裝

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

請參閱[Install-package](../tools/ps-ref-install-package.md)。

安裝封裝，執行下列動作：

- 與隱含協議的 [主控台] 視窗中顯示適用之授權條款。 如果您不同意這些條款，您應該立即解除安裝封裝。
- 將參考加入至專案中參考的格式是使用中。 接著會出現在 方案總管 和 適用的參考格式檔案參考。 不過，請注意，與 PackageReference，需要儲存專案以直接查看專案檔中的變更。
- 會快取封裝：
  - PackageReference： 封裝已經快取`%USERPROFILE%\.nuget\packages`和鎖定的檔案也就是`project.assets.json`會更新。
  - `packages.config`： 建立`packages`在方案根目錄和複製子資料夾內的套件檔案的資料夾。 `package.config`更新檔案。
- 更新`app.config`及/或`web.config`如果封裝使用[來源和組態檔案轉換](../create-packages/source-and-config-file-transformations.md)。
- 若還未出現在專案中，會安裝任何相依性。 中所述，這可能會更新處理序中的封裝版本[相依性解析](../consume-packages/dependency-resolution.md)。
- Visual Studio 視窗中顯示封裝的讀我檔案，如果有的話。

> [!Tip]
> 安裝封裝的主要優點之一`Install-Package`主控台中的命令時，會加入專案的參考，就如同您使用 「 封裝管理員 」 UI。 相反地， `nuget install` CLI 命令只會下載套件，並不會自動加入的參考。

## <a name="uninstalling-a-package"></a>解除安裝封裝

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

請參閱[解除安裝封裝](../tools/ps-ref-uninstall-package.md)。 使用[Get 封裝](../tools/ps-ref-get-package.md)，查看目前安裝在預設專案中，如果您要尋找識別項的所有封裝。

解除安裝封裝，執行下列動作：

- 移除參考封裝專案 （及任何參考格式正在使用中）。 參考不會再出現在 [方案總管] 中。 (您可能需要重建專案，以查看它從移除**Bin**資料夾。)
- 反轉所做的變更`app.config`或`web.config`已經安裝封裝。
- 如果沒有剩餘的封裝，請使用這些依存性移除先前安裝相依性。

> [!Tip]
> 像`Install-Package`、`Uninstall-Package`命令有不同於管理在專案中，參考的優點`nuget uninstall`CLI 命令。

## <a name="updating-a-package"></a>更新封裝

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

請參閱[Get 封裝](../tools/ps-ref-get-package.md)和[更新套件](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>尋找封裝

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

請參閱[Find-package](../tools/ps-ref-find-package.md)。 在 Visual Studio 2013 和舊版中，使用[Get 封裝](../tools/ps-ref-get-package.md)改為。

## <a name="availability-of-the-console"></a>在主控台的可用性

在 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動安裝時選取任何。網路相關的工作負載;您也可以安裝它個別藉由檢查**個別元件 > 程式碼工具 > NuGet 套件管理員**選項在 Visual Studio 2017 安裝程式。

此外，如果您遺漏的 NuGet 封裝管理員 Visual Studio 2015 中及更早版本，請檢查**工具 > 擴充功能和更新...** ，並搜尋 NuGet 套件管理員擴充功能。 如果您無法使用 Visual Studio 中的擴充功能安裝程式，您可以下載擴充功能直接從[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)。

Package Manager Console 不是目前適用於 Visual Studio for mac。 對等的命令，不過，可透過[NuGet CLI](nuget-exe-CLI-reference.md)。 Visual Studio for Mac 並沒有使用者介面來管理 NuGet 封裝。 請參閱[您的專案中包括的 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。

Package Manager Console 未隨附於 Visual Studio 程式碼。

## <a name="extending-the-package-manager-console"></a>延伸封裝管理員主控台

有些封裝安裝主控台的新命令。 例如，`MvcScaffolding`建立類似的命令`Scaffold`如下所示，如此就會產生 ASP.NET MVC 控制器和檢視：

![安裝和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell 設定檔設定

PowerShell 設定檔可讓您開放常用的命令使用，只要您使用 PowerShell。 NuGet 支援特定的 NuGet 設定檔，通常在下列位置找到：

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

若要尋找的設定檔，請輸入`$profile`主控台中：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

如需詳細資訊，請參閱[Windows PowerShell 設定檔](https://technet.microsoft.com/library/bb613488.aspx)。

## <a name="using-the-nugetexe-cli-in-the-console"></a>使用主控台中的 nuget.exe CLI

若要讓[ `nuget.exe` CLI](nuget-exe-CLI-Reference.md)可用在封裝管理員主控台中，安裝[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)封裝從主控台：

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
