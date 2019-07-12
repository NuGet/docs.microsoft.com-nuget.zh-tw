---
title: 安裝和管理 Visual Studio 中使用主控台的 NuGet 套件
description: 使用 Visual Studio 中的 NuGet 套件管理員主控台，使用封裝的指示。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842588"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>安裝和管理封裝與封裝管理員主控台在 Visual Studio (PowerShell)

NuGet 套件管理員主控台可讓您使用[NuGet PowerShell 命令](../tools/powershell-reference.md)尋找、 安裝、 解除安裝和更新 NuGet 套件。 必須在套件管理員 UI 不會提供方法，來執行作業的情況下使用主控台。 若要使用`nuget.exe`CLI 命令，在主控台中，請參閱[使用 nuget.exe CLI，在主控台中](#using-the-nugetexe-cli-in-the-console)。

主控台內建在 Windows 上的 Visual Studio。 不隨附於 Visual Studio for Mac 或 Visual Studio Code。

## <a name="find-and-install-a-package"></a>尋找並安裝封裝

例如，尋找及安裝套件是使用三個簡單步驟：

1. 在 Visual Studio 中開啟專案/方案，然後開啟 主控台使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。

1. 尋找您想要安裝的封裝。 如果您已經知道這個，請跳至步驟 3。

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
> 在主控台中可用的所有作業也都適用於[NuGet CLI](../tools/nuget-exe-cli-reference.md)。 不過，主控台命令的 Visual Studio 和儲存的專案/方案內容中運作，而且通常超過其對等的 CLI 命令完成。 比方說，安裝套件，以透過主控台將參考加入專案而 CLI 命令則否。 基於這個理由，通常使用 Visual Studio 中的開發人員會偏好使用 cli 主控台。

> [!Tip]
> 許多的主控台作業取決於 Visual Studio 中開啟具有已知的路徑名稱的解決方案。 如果您有未儲存的方案或沒有解決方案，您可以看到下列錯誤: 」 方案是未開啟，或未儲存。 請確定您有開啟且已儲存解決方案。 」 這表示主控台無法判斷方案資料夾。 正在儲存未儲存的解決方案，或建立及儲存的解答，如果您還沒有開啟，應該更正錯誤。

## <a name="opening-the-console-and-console-controls"></a>開啟的主控台和主控台控制項

1. 開啟主控台，在 Visual Studio 中使用**工具 > NuGet 套件管理員 > Package Manager Console**命令。 「 主控台 」 可以安排在程式碼中，置於您隨心所欲的 Visual Studio 視窗 (請參閱[自訂視窗版面配置，在 Visual Studio 中的](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 根據預設，主控台命令對特定的套件來源，以及專案在視窗頂端的控制項中的設定：

    ![封裝來源和專案的套件管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. 選取不同的套件來源及/或專案變更這些預設值，後續的命令。 若要 overrride 而不需要變更預設值，這些設定大部分的命令支援`-Source`和`-ProjectName`選項。

1. 若要管理的套件來源，選取齒輪圖示。 這是捷徑**工具 > 選項 > NuGet 套件管理員 > 套件來源**上所述的對話方塊[套件管理員 UI](package-manager-ui.md#package-sources)頁面。 此外，右邊的專案選取器控制項清除主控台的內容：

    ![套件管理員主控台設定和清除控制項](media/PackageManagerConsoleControls2.png)

1. 最右邊的按鈕時，中斷長時間執行命令。 例如，執行`Get-Package -ListAvailable -PageSize 500`列出前 500 個封裝上的預設來源 （例如 nuget.org)，這可能需要幾分鐘才能完成。

    ![套件管理員主控台停止控制項](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>安裝套件

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

請參閱[Install-package](../tools/ps-ref-install-package.md)。

在主控台中安裝的套件執行相同的步驟，在所述[安裝套件時，會發生什麼事](../concepts/package-installation-process.md)，加上下列各項：

- 主控台會顯示適用的授權條款，在其視窗中使用隱含的合約。 如果您不同意這些條款，您應該立即解除安裝封裝。
- 套件的參考也會新增至專案檔，而且會出現在**方案總管**下方**參考** 節點，您需要儲存專案，以直接查看專案檔中的變更。

## <a name="uninstalling-a-package"></a>解除安裝套件

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

請參閱[解除安裝封裝](../tools/ps-ref-uninstall-package.md)。 使用[取得封裝](../tools/ps-ref-get-package.md)，查看目前安裝在預設專案中，如果您要尋找識別項的所有封裝。

解除安裝套件時，會執行下列動作：

- 移除參考封裝專案 （及正在使用中的任何管理格式）。 參考不會再出現在**方案總管 中**。 (您可能需要重建專案，以查看它移除了**Bin**資料夾。)
- 反轉所做的變更`app.config`或`web.config`安裝封裝。
- 如果沒有任何剩餘的套件會使用這些相依性移除先前安裝相依性。

## <a name="updating-a-package"></a>更新套件

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

請參閱[取得封裝](../tools/ps-ref-get-package.md)和[更新套件](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>尋找套件

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

請參閱[Find-package](../tools/ps-ref-find-package.md)。 在 Visual Studio 2013 和舊版中，使用[取得封裝](../tools/ps-ref-get-package.md)改。

## <a name="availability-of-the-console"></a>在主控台的可用性

從 Visual Studio 2017，NuGet 和 NuGet 套件管理員會自動安裝時選取任何。NET 相關的工作負載;您也可以安裝其個別檢查**個別元件 > 程式碼工具 > NuGet 套件管理員**Visual Studio 安裝程式中的選項。

此外，如果您缺少的 NuGet 套件管理員，在 Visual Studio 2015 和更早版本，請檢查**工具 > 擴充功能和更新...** 並搜尋 NuGet 套件管理員延伸模組。 如果您無法使用 Visual Studio 中的延伸模組安裝程式，您可以下載的擴充功能，直接從[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。

套件管理員主控台不是目前使用 Visual Studio for mac。 對等的命令，不過，都是透過[NuGet CLI](nuget-exe-CLI-reference.md)。 Visual Studio for Mac 有 UI 來管理 NuGet 套件。 請參閱[在專案中的包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。

套件管理員主控台不會包含使用 Visual Studio Code 的。

## <a name="extending-the-package-manager-console"></a>擴充套件管理員主控台

有些套件會安裝新的命令主控台。 例如，`MvcScaffolding`會建立類似的命令`Scaffold`如下所示，如此就會產生 ASP.NET MVC 控制器和檢視：

![安裝和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>設定 NuGet PowerShell 設定檔

PowerShell 設定檔可讓您無論在何處使用 PowerShell 將常用命令提供。 NuGet 支援 NuGet 特定設定檔通常位於下列位置找到：

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

若要尋找設定檔，請輸入`$profile`在主控台中：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

如需詳細資訊，請參閱[Windows PowerShell 設定檔](https://technet.microsoft.com/library/bb613488.aspx)。

## <a name="using-the-nugetexe-cli-in-the-console"></a>使用 nuget.exe CLI，在主控台中

若要讓[ `nuget.exe` CLI](nuget-exe-cli-reference.md)可用在套件管理員主控台中，安裝[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)從主控台的封裝：

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
