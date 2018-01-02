---
title: "安裝 NuGet 用戶端工具 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "安裝用戶端工具、命令列介面 (CLI) 和 Package Manager for Visual Studio 的指南。"
keywords: "nuget.exe CLI, NuGet 用戶端工具, NuGet 套件管理員, NuGet 套件管理員主控台, NuGet for Visual Studio, NuGet 搶鮮版 (Beta)通道"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>安裝 NuGet 用戶端工具

> [!Tip]
> **想要安裝套件？請參閱[快速入門 - 使用套件](../Quickstart/Use-a-Package.md)。**

有兩個主要的工具可幫助您建置、發行和取用 NuGet 套件：

1. [**NuGet CLI** ](#nuget-cli) 是適用於 Windows 的命令列公用程式，它提供所有 NuGet 功能，也可以在 Mac OSX 與 Linux 上使用 Mono 執行，或透過 .NET Core CLI 執行 (`dotnet`)。
1. [**Visual Studio 中的 NuGet 套件管理員**](#nuget-package-manager-in-visual-studio) (僅限 Windows) 是一種管理套件的 GUI 工具，並包含 PowerShell 主控台；透過它，您可以直接在 VisualStudio 內使用特定的 NuGet 命令。 套件管理員 UI 和主控台都包含在 Visual Studio (在 Windows 上) 2012 及更新版本中，且可以針對先前的版本手動安裝。

    使用 Visual Studio for Mac，NuGet 功能已直接內建。 如需逐步解說，請參閱[在專案中包含 NuGet 套件](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)。

    目前的 Visual Studio 程式碼沒有任何內建的 NuGet 支援。 請使用 NuGet CLI 或 [dotnet CLI](../Tools/dotnet-Commands.md)。

NuGet CLI 和套件管理員都支援下列作業：

- 搜尋套件
- 安裝套件
- 更新套件
- 解除安裝套件
- 還原套件 (在套件管理員中僅限 UI)
- 管理 NuGet 來源

下列功能只在 NuGet CLI 中受支援：

- 管理套件 (nuget.org 或私人摘要)
- 建立套件 
- 發行套件
- 管理 NuGet.Config
- 管理 NuGet 快取
- 複製套件

> [!Note]
> 另一個很好的工具是 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，這是一個開放原始碼的獨立工具，以視覺化方式瀏覽、建立和編輯 NuGet 套件。 例如，它很適用對套件結構進行實驗性的變更，而不必每次重建套件。
> 跨平台的 [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) 工具鏈，用來開發 .NET Core 應用程式，能支援數個 NuGet 命令，例如 delete、locals、push、pack 和 restore。 

## <a name="nuget-cli"></a>NuGet CLI

NuGet 命令列介面提供對所有 NuGet 功能的存取權，並可以在 Windows、Mac OSX 與 Linux 上執行，如下列各節中所述。

### <a name="windows"></a>Windows

**直接下載：**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> 在 NuGet 1.4+，您可以使用 `nuget update -self` 將現有的 nuget.exe 更新為最新版本。

**其他方法：**

- **Chocolatey**：使用 [Chocalatey](http://chocolatey.org) 用戶端安裝 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 套件。 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**：從 Visual Studio 的套件管理員主控台安裝 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 套件。

    > [!Note]
    > **對於 NuGet 2.x 使用者**：因為 NuGet 3.2 中導入的重大變更，[https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) 指向最新且穩定的 NuGet 2.x 版本，以防止連續整合系統可能的中斷。

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX 與 Linux

在 Mac OSX 與 Linux 上，有兩種方式可以執行 NuGet CLI：

- 安裝 [.NET Core SDK](https://www.microsoft.com/net/download/core)，其中包括核心 NuGet 功能。 下載項目也會列在 [github.com/dotnet/cli](https://github.com/dotnet/cli) 上。 如果您需要更完整的功能，請使用下方的第二個選項，使用 `nuget.exe` 搭配 Mono。

- 安裝 [Mono](http://www.mono-project.com/docs/getting-started/install/)，然後從 [nuget.org/downloads](https://nuget.org/downloads)，使用適用於 Windows 的 `nuget.exe` 命令列可執行檔 (3.2 版及更新版本)。 在 Mono 上執行 NuGet 受限於下列限制：

    - 已測試可運作的命令：
        - config
        - 刪除
        - help
        - install
        - 清單
        - push
        - setApiKey
        - sources
        - spec

    - 部分可運作的命令：
        - pack：搭配 `.nuspec` 檔案可運作，但無法搭配專案檔。
        - restore：搭配 `packages.config` 和 `project.json` 檔案可運作，但無法搭配解決方案 (`.sln`) 檔案運作。

    - 無法運作的命令：
        - 更新

### <a name="related-topics"></a>相關主題

- [NuGet CLI 參考](../tools/nuget-exe-cli-reference.md)
- [建立套件](../create-packages/creating-a-package.md)
- [發行套件](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Visual Studio 中的 NuGet 套件管理員

NuGet 套件管理員包含於 Windows 上的 Visual Studio 2012 及更新版本的所有版本。 它包含套件管理員 UI ([參考](../tools/package-manager-ui.md))，以及您可以用來存取特定套件所附之工具的套件管理員主控台 ([參考](../tools/package-manager-console.md))。

Visual Studio 2017 安裝程式會在採用 .NET 的任何工作負載包含 NuGet 套件管理員。 若要個別安裝，或確認已安裝套管理員，請執行 Visual Studio 2017 安裝程式，並核取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 下方選項。

> [!Note]
> 主控台需要 [PowerShell 2.0](http://support.microsoft.com/kb/968929)，這在 Windows 7 或更新版本以及 Windows Server 2008 R2 或更高版本上已經安裝。
>
> 套件管理員主控台命令也只在 Windows 上的 Visual Studio 內運作。 在該環境之外使用 NuGet CLI，包括使用 Visual Studio for Mac 和 Visual Studio Code。

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Visual Studio 2010 和更早版本的套件管理員安裝

*Visual Studio 2012 及更新版本不需要這些步驟，它們已經包含套件管理員。*

1. 在 Visual Studio 2010 和舊版中，按一下 [工具] > [延伸模組和更新]。
1. 巡覽至 [線上]，然後搜尋 [Visual Studio 的 NuGet 套件管理員]，然後按一下 [下載]。
1. 在 [安裝程式] 對話方塊中，按一下 [安裝]。
1. 安裝完成時，請重新啟動 Visual Studio。

> [!Tip]
> 如果您無法在 Visual Studio 中使用 [延伸模組和更新] 對話方塊 (例如，被 Proxy 封鎖)，可以直接在 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下載 Visual Studio 2013 和 2015 的延伸模組。

### <a name="updating-the-package-manager"></a>更新套件管理員

對於 Visual Studio 2015 Update 2 和更新版本，套件管理員會自動更新至最新穩定版本。

對於 Visual Studio 2015 Update 1 和更早版本，請選取 [工具] > [延伸模組和更新] 命令，然後按一下 [更新] 索引標籤，以查看是否有可用的套件管理員新版本。  

### <a name="nuget-previews"></a>NuGet 預覽

如果您想要預覽即將推出的 NuGet 功能，請安裝 [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/)，它能與穩定版本的 Visual Studio 並存運作。

請注意，先前的 Visual Studio 2015 NuGet 搶鮮版 (Beta)通道 (`https://dotnet.myget.org/F/nuget-beta/vsix/`) 已不再使用。

若要報告任何 NuGet 版本的問題或是分享想法，請在 [NuGet GitHub 儲存機制](https://github.com/Nuget/Home)上開啟問題。

### <a name="related-topics"></a>相關主題

- [套件管理員 UI 參考](../tools/package-manager-ui.md)
- [套件管理員主控台參考](../tools/package-manager-console.md)
- [套件管理員主控台 PowerShell 參考](../tools/powershell-reference.md)