---
title: 安裝 NuGet 用戶端工具 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: 有關安裝用戶端工具、dotnet 和 nuget 命令列介面 (CLI)，以及適用於 Visual Studio 的套件管理員的指導方針。
keywords: dotnet.exe CLI, nuget.exe CLI, NuGet 用戶端工具, NuGet 套件管理員, NuGet 套件管理員主控台, NuGet for Visual Studio, NuGet 搶鮮版 (Beta) 通道
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e4dfe1102d1e0e2013136b0ae4975e5036e34642
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2018
---
# <a name="installing-nuget-client-tools"></a>安裝 NuGet 用戶端工具

> **想要安裝套件？請參閱[安裝 NuGet 套件的方式](consume-packages/ways-to-install-a-package.md)。**

若要以套件取用者或建立者身分使用 NuGet，您可以使用[命令列介面 (CLI) 工具](#cli-tools)以及 [Visual Studio 中的 NuGet 功能](#visual-studio)。 本文簡要概述不同工具的功能、安裝它們的方式，以及它們相對的[功能可用性](#feature-availability)。

| 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 描述 | 下載&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | 隨附於 .NET Core SDK，並提供所有平台上的核心 NuGet 功能。 | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | 在 Windows 上提供所有的 NuGet 功能，於 Mono 執行時在 Mac 和 Linux 上提供大部分功能。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | 在 Windows 上，透過套件管理員 UI 和套件管理員主控台提供 NuGet 功能；隨附 .NET 相關的工作負載。 在 Mac 上，透過 UI 提供特定功能。 在 Visual Studio Code 中，會透過延伸模組來提供 NuGet 功能。 | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) 也提供還原和建立套件的能力，這主要用於組建伺服器。 MSBuild 並非適合用來搭配 NuGet 使用的一般用途工具。

## <a name="cli-tools"></a>CLI 工具

這兩個 NuGet CLI 工具是 `dotnet.exe` 和 `nuget.exe`。 請參閱[功能可用性](#feature-availability)以進行比較。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe` 適用於所有平台 (Windows、Mac 和 Linux)，並提供核心 NuGet 功能，例如安裝、還原和發行套件。 `dotnet` 提供與 .NET Core 專案檔 (例如 `.csproj`) 的直接整合，這在大多數案例中很有幫助。 `dotnet` 也會針對每個平台直接建置，而且不會要求您安裝 Mono。

安裝：

- 在開發人員電腦上，安裝 [.NET Core SDK](https://aka.ms/dotnetcoregs)。
- 針對組建伺服器，依照[在持續整合中使用 .NET Core SDK 和工具](/dotnet/core/tools/using-ci-with-cli)中的指示執行。

如需詳細資訊，請參閱 [.NET Core 命令列介面工具](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x)。

### <a name="nugetexe-cli"></a>nuget.exe CLI

NuGet CLI `nuget.exe` 是適用於 Windows 的命令列公用程式，它提供所有 NuGet 功能，也可以在 Mac OSX 與 Linux 上使用 [Mono](http://www.mono-project.com/docs/getting-started/install/) 來執行，但有一些限制。 不同於 `dotnet`，`nuget.exe` CLI 不會影響專案檔，也不會在安裝套件時更新 `packages.config`。

安裝：

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> 在 Windows 上使用 `nuget update -self`，將現有的 nuget.exe 更新為最新版本。

> [!Note]
> 最新建議的 NuGet CLI 一律可在 `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` 找到。 為了與舊版持續整合系統相容，先前的 URL `https://nuget.org/nuget.exe` 目前會提供[已被取代的 2.8.6 CLI 工具](https://github.com/NuGet/NuGetGallery/issues/5381)。

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code：NuGet 功能可透過市集擴充功能取得，或者使用 `dotnet.exe` 或 `nuget.exe` CLI 工具來取得。

- Visual Studio for Mac：已直接內建特定的 NuGet 功能。 如需逐步解說，請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。 針對其他功能，請使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。

- Windows 上的 Visual Studio：**NuGet 套件管理員**隨附於 Visual Studio 2012 及更新版本。 套件管理員提供[套件管理員 UI](tools/package-manager-ui.md) 和[套件管理員主控台](tools/package-manager-console.md)，您可以透過它們執行大部分 NuGet 作業。
  - Visual Studio 2017 安裝程式會在採用 .NET 的任何工作負載包含 NuGet 套件管理員。 若要個別安裝，或確認已安裝套管理員，請執行 Visual Studio 2017 安裝程式，並核取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 下方選項。
  - 套件管理員 UI 和主控台對 Windows 上的 Visual Studio 而言是不同的。 它們目前無法供 Visual Studio for Mac 使用。
  - Visual Studio 不會自動納入 `nuget.exe` CLI，必須分開安裝，如先前所述。
  - 套件管理員主控台命令只能在 Windows 上的 Visual Studio 內運作，無法在其他 PowerShell 環境中運作。
  - 針對 Visual Studio 2010 及更早版本，安裝「適用於 Visual Studio 的 NuGet 套件管理員」擴充功能。
  - 您也可以從 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下載適用於 Visual Studio 2013 和 2015 的 NuGet 延伸模組。
  - 如果您想要預覽即將推出的 NuGet 功能，請安裝 [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/)，它能與穩定版本的 Visual Studio 並存運作。 若要針對預覽回報問題或分享想法，請在 [NuGet GitHub 存放庫](https://github.com/Nuget/Home/issues) \(英文\) 上建立問題。

## <a name="feature-availability"></a>功能可用性

| 功能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| 搜尋套件 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 安裝/解除安裝套件 | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| 更新套件 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 還原套件 | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| 管理套件摘要 (來源) | | &#10004; | &#10004; | &#10004; | &#10004; |
| 管理摘要上的套件 | &#10004;(1) | &#10004; | &#10004; | | |
| 設定摘要的 API 金鑰 | | &#10004; | &#10004; | | |
| 建立套件(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| 發行套件 | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| 複製套件 |  | &#10004; | &#10004; | | |
| 管理 *global-package* 和快取資料夾 | &#10004; | &#10004; | &#10004; | | |
| 管理 NuGet 組態 | | &#10004; | &#10004; | | |

(1) 僅限 nuget.org 上的套件

(2) 不會影響專案檔；請改為使用 `dotnet.exe`。

(3) 只能搭配 `packages.config` 檔案運作，無法搭配方案 (`.sln`) 檔案運作。

(4) 各種進階的套件功能只能透過 CLI 取得，因為這些功能不會在 Visual Studio UI 工具中呈現。

(5) 搭配 `.nuspec` 檔案運作，但無法搭配專案檔。

### <a name="related-topics"></a>相關主題

- [dotnet 命令](tools/dotnet-commands.md)
- [NuGet CLI 參考](tools/nuget-exe-cli-reference.md)
- [套件管理員 UI 參考](tools/package-manager-ui.md)
- [套件管理員主控台參考](tools/package-manager-console.md)
- [套件管理員主控台 PowerShell 參考](tools/powershell-reference.md)
- [建立套件](create-packages/creating-a-package.md)
- [發行套件](create-packages/publish-a-package.md)

在 Windows 上工作的開發人員也可以探索 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) \(英文\)，這是一個開放原始碼的獨立工具，可讓您以視覺化方式瀏覽、建立和編輯 NuGet 套件。 例如，它非常適合用來對套件結構進行實驗性變更，而不需重建套件。
