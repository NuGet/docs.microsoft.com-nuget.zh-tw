---
title: 在 Visual Studio 中使用主控台安裝及管理 NuGet 套件
description: 在 Visual Studio 中使用 NuGet 套件管理員主控台來處理套件的指示。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428951"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>在 Visual Studio 中使用套件管理員主控台安裝及管理套件 (PowerShell)

Nuget 套件管理員主控台可讓您使用 [NuGet PowerShell 命令](../reference/powershell-reference.md)來尋找、安裝、解除安裝及更新 NuGet 套件。 在套件管理員 UI 無法執行作業的情況下，則必須使用主控台。 若要在主控台中使用 `nuget.exe` CLI 命令，請參閱[在主控台中使用 nuget.exe CLI](#use-the-nugetexe-cli-in-the-console)。

主控台內建於 Windows 上的 Visual Studio 中。 它不包含在 Visual Studio for Mac 或 Visual Studio Code 中。

## <a name="find-and-install-a-package"></a>尋找並安裝套件

例如，尋找並安裝套件是透過三個簡單的步驟來完成：

1. 在 Visual Studio 中開啟專案/方案，然後使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。

1. 尋找您要安裝的套件。 如果您已經知道這一點，請跳到步驟 3。

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
> 主控台中可用的所有作業也可以使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 來完成。 不過，主控台命令會在 Visual Studio 內容與已儲存的專案/解決方案中運作，而且通常會比對等的 CLI 命令完成更多操作。 例如，透過主控台安裝套件會將參考新增至專案，而 CLI 命令則不會。 基於這個理由，使用 Visual Studio 的開發人員通常更喜歡使用主控台而不是 CLI。

> [!Tip]
> 許多主控台作業都取決於在 Visual Studio 中使用已知的路徑名稱開啟解決方案。 如果您有未儲存的解決方案或是沒有解決方案，則會看到錯誤「未開啟或儲存方案。 請確定您有已開啟和已儲存的方案。」 這表示主控台無法判斷解決方案資料夾。 儲存未儲存的方案，或建立並儲存方案 (如果您沒有開啟的方案)，應該可以更正錯誤。

## <a name="opening-the-console-and-console-controls"></a>開啟主控台與主控台控制項

1. 在 Visual Studio 中，使用 [工具] > [NuGet 套件管理員] > [套件管理器主控台] 命令來開啟主控台。 主控台是一個 Visual Studio 視窗，可依您的需要進行排列和定位 (請參閱[在 Visual Studio 中自訂視窗版面配置](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 根據預設，主控台命令會針對視窗頂端的控制項中設定的特定套件來源與專案進行操作：

    ![套件來源與專案的套件管理員主控台控制項](media/PackageManagerConsoleControls1.png)

1. 選取不同的套件來源和/或專案會變更後續命令的預設值。 若要在不變更預設值的情況下覆寫這些設定，大部分的命令都支援 `-Source` 與 `-ProjectName` 選項。

1. 若要管理套件來源，請選取齒輪圖示。 這是 [工具] > [選項] > [NuGet 套件管理員] > [套件來源] 對話方塊的捷徑，如[套件管理員 UI](install-use-packages-visual-studio.md#package-sources) 頁面所述。 此外，專案選取器右側的控制項可清除主控台的內容：

    ![套件管理員主控台設定與清除控制項](media/PackageManagerConsoleControls2.png)

1. 最右邊的按鈕會中斷長時間執行的命令。 例如，執行 `Get-Package -ListAvailable -PageSize 500` 會列出預設來源 (例如 nuget.org) 上的前 500 個套件，這可能需要幾分鐘的時間才能完成。

    ![套件管理員主控台停止控制項](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>安裝套件

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

請參閱 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)。

在主控台中安裝套件時執行的步驟，與[安裝套件時會發生什麼事](../concepts/package-installation-process.md)中所述相同，此外還會：

- 主控台會在其視窗中顯示適用的授權條款，並附帶隱含的合約。 如果您不同意這些條款，則應該立即將套件解除安裝。
- 此外，對套件的參考也會加入至專案檔中，並顯示在 [方案總管] 中的 [參考] 節點下，您必須儲存專案才能直接查看專案檔中的變更。

## <a name="uninstall-a-package"></a>解除安裝套件

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

請參閱 [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)。 如果您需要尋找識別碼，請使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 來查看目前安裝在預設專案中的所有套件。

解除安裝套件會執行下列動作：

- 從專案中移除套件的參考 (以及任何使用中的管理格式)。 參考不會再出現在 [方案總管] 中。 (您可能需要重建專案，才能看到它已從 **Bin** 資料夾中移除。)
- 反轉安裝套件時對 `app.config` 或 `web.config` 所做的任何變更。
- 如果沒有剩餘的套件使用這些相依性，則移除先前安裝的相依性。

## <a name="update-a-package"></a>更新套件

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

請參閱 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 與 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>尋找套件

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

請參閱 [Find-Package](../reference/ps-reference/ps-ref-find-package.md)。 在 Visual Studio 2013 與更早版本中，請改為使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)。

## <a name="availability-of-the-console"></a>主控台的可用性

從 Visual Studio 2017 開始，當您選取任何與 .NET 相關的工作負載時，會自動安裝 NuGet 和 NuGet 套件管理員；您還可以透過檢查 Visual Studio 安裝程式中的 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 選項來個別安裝。

此外，如果您想在 Visual Studio 2015 和更早版本中使用 NuGet 套件管理員，請查看 [工具] > [擴充功能和更新]，然後搜尋 NuGet 套件管理員擴充功能。 如果您無法在 Visual Studio 中使用擴充功能安裝程式，您可以直接從 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) \(英文\) 下載擴充功能。

Visual Studio for Mac 目前不提供套件管理員主控台。 但是，對等的命令則可透過 [NuGet CLI](../reference/nuget-exe-CLI-reference.md) 取得。 Visual Studio for Mac 確實有一個用於管理 NuGet 套件的 UI。 請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。

套件管理員主控台未隨附於 Visual Studio Code。

## <a name="extend-the-package-manager-console"></a>擴充套件管理員主控台

某些套件會為主控台安裝新命令。 例如，`MvcScaffolding` 會建立如下所示的 `Scaffold` 命令，以產生 ASP.NET MVC 控制器與檢視：

![安裝及使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>設定 NuGet PowerShell 設定檔

PowerShell 設定檔可讓您在任何使用 PowerShell 的地方提供常用的命令。 NuGet 支援 NuGet 專用設定檔，通常位於下列位置：

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

若要尋找設定檔，請在主控台中輸入 `$profile`：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

如需詳細資訊，請參閱 [Windows PowerShell 設定檔](https://technet.microsoft.com/library/bb613488.aspx)。

## <a name="use-the-nugetexe-cli-in-the-console"></a>在主控台中使用 nuget.exe CLI

若要讓 [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) 可在套件管理員主控台中使用，請從主控台安裝 [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) 套件：

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
