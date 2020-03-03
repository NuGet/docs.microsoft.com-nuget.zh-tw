---
title: 安裝 NuGet 用戶端工具
description: 有關安裝用戶端工具、dotnet 和 nuget 命令列介面 (CLI)，以及適用於 Visual Studio 的套件管理員的指導方針。
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 2769f0ef0373b26eedb4bac6242fee0e814310c5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230535"
---
# <a name="install-nuget-client-tools"></a>安裝 NuGet 用戶端工具

> **想要安裝套件嗎？請參閱[安裝 NuGet 套件的方式](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)。**

若要以套件取用者或建立者身分使用 NuGet，您可以使用命令列介面 (CLI) 工具以及 Visual Studio 中的 NuGet 功能。 本文簡要概述不同工具的功能、安裝它們的方式，以及它們相對的[功能可用性](#feature-availability)。 若要開始使用 NuGet 來取用套件，請參閱[安裝並使用套件 (dotnet CLI](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) 與[安裝並使用套件 (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md)。 若要開始建立 NuGet 套件，請參閱[建立及發佈 .NET Standard 套件 (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 和[建立及發佈 .NET Standard 套件 (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md)。

| 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 描述 | 下載&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | 適用於 .NET Core 與 .NET Standard 程式庫，以及以 .NET Framework 為目標之任何 [SDK 樣式專案](resources/check-project-format.md)的 CLI 工具。 隨附於 .NET Core SDK，並提供所有平台上的核心 NuGet 功能。 (從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | 適用於 .NET Framework 程式庫，以及以 .NET Standard 程式庫為目標之任何[非 SDK 樣式專案](resources/check-project-format.md)的 CLI 工具。 在 Windows 上提供所有的 NuGet 功能，於 Mono 執行時在 Mac 和 Linux 上提供大部分功能。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | 在 Windows 上， **NuGet 套件管理員**包含在 Visual Studio 2012 和更新版本中。 Visual Studio 提供[套件管理員 UI](consume-packages/install-use-packages-visual-studio.md) 和[套件管理員主控台](consume-packages/install-use-packages-powershell.md)，您可以透過它們執行大部分 NuGet 作業。 | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio for Mac](/visualstudio/mac/nuget-walkthrough) | 在 Mac 上，某些 NuGet 功能是直接內建的。 目前無法使用套件管理員主控台。 針對其他功能，請使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。  | [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | 在 Windows、Mac 或 Linux 上，NuGet 功能可透過 marketplace 延伸模組取得，或使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。 | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[MSBuild CLI](reference/msbuild-targets.md) 也提供還原和建立套件的能力，這主要用於組建伺服器。 MSBuild 並非適合用來搭配 NuGet 使用的一般用途工具。

套件管理員主控台命令只能在 Windows 上的 Visual Studio 內運作，無法在其他 PowerShell 環境中運作。

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>在 Visual Studio 2017 和更新版本上安裝
在 Visual Studio 2017 中啟動，此安裝程式包含 NuGet 套件管理員以及採用 .NET 的任何工作負載。 若要個別安裝或驗證已安裝套件管理員，請執行 Visual Studio 安裝程式，並核取 [個別元件] > [程式碼工具] > [NuGet 套件管理員] 下的選項。

### <a name="install-on-visual-studio-2015-and-older"></a>在 Visual Studio 2015 和更舊版本上安裝
Visual Studio 2013 和2015的 NuGet 擴充功能可以從[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)下載。

針對 Visual Studio 2010 及更早版本，安裝「適用於 Visual Studio 的 NuGet 套件管理員」擴充功能。 請注意，如果您在搜尋結果的第一頁中看不到此延伸模組，請嘗試將 [排序依據] 下拉式清單變更為 [大部分下載] 或按字母順序排序。

## <a name="cli-tools"></a>CLI 工具
您可以使用 `dotnet` CLI 或 `nuget.exe` CLI 來支援 IDE 中的 NuGet 功能。 `dotnet` CLI 會隨一些 Visual Studio 工作負載一起安裝，例如 .NET Core。 `nuget.exe` CLI 必須單獨安裝，如先前所述。

這兩個 NuGet CLI 工具是 `dotnet.exe` 和 `nuget.exe`。 請參閱[功能可用性](#feature-availability)以進行比較。

* 若要以 .NET Core 或 .NET Standard 為目標，請使用 dotnet CLI。 SDK 樣式的專案格式需要 `dotnet` CLI，該格式使用 [SDK 屬性](/dotnet/core/tools/csproj#additions)。
* 若以 .NET Framework 為目標 (限非 SDK 樣式專案)，請使用 `nuget.exe` CLI。 若專案是從 `packages.config` 移轉到 PackageReference，請使用 dotnet CLI。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe` 適用於所有平台 (Windows、Mac 和 Linux)，並提供核心 NuGet 功能，例如安裝、還原和發行套件。 `dotnet` 提供與 .NET Core 專案檔 (例如 `.csproj`) 的直接整合，這在大多數案例中很有幫助。 `dotnet` 也會針對每個平台直接建置，而且不會要求您安裝 Mono。

安裝：

- 在開發人員電腦上，安裝 [.NET Core SDK](https://aka.ms/dotnetcoregs)。 從 Visual Studio 2017 開始，dotnet CLI 會自動與任何 .NET Core 相關工作負載一起安裝。
- 針對組建伺服器，依照[在持續整合中使用 .NET Core SDK 和工具](/dotnet/core/tools/using-ci-with-cli)中的指示執行。

若要了解如何使用 dotnet CLI 的基本命令，請參閱[使用 dotnet CLI 安裝和使用套件](consume-packages/install-use-packages-dotnet-cli.md)。

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI (`nuget.exe`) 是適用於 Windows 的命令列公用程式，它提供所有 NuGet 功能，也可以在 Mac OSX 與 Linux 上使用 [Mono](https://www.mono-project.com/docs/getting-started/install/) 來執行，但有一些限制。

若要了解如何使用 `nuget.exe` CLI 的基本命令，請參閱[使用 nuget.exe CLI 安裝和使用套件](consume-packages/install-use-packages-nuget-cli.md)。

安裝：

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> 在 Windows 上使用 `nuget update -self`，將現有的 nuget.exe 更新為最新版本。

> [!Note]
> 最新建議的 NuGet CLI 一律可在 `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` 找到。 為了與舊版持續整合系統相容，先前的 URL `https://nuget.org/nuget.exe` 目前會提供[已被取代的 2.8.6 CLI 工具](https://github.com/NuGet/NuGetGallery/issues/5381)。

## <a name="feature-availability"></a>功能可用性

| 功能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| 搜尋套件 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 安裝/解除安裝套件 | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| 更新套件 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 還原套件 | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| 管理套件摘要 (來源) | | &#10004; | &#10004; | &#10004; | &#10004; |
| 管理摘要上的套件 | &#10004; | &#10004; | &#10004; | | |
| 設定摘要的 API 金鑰 | | &#10004; | &#10004; | | |
| 建立套件(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| 發行套件 | &#10004; | &#10004; | &#10004; | &#10004; |  |
| 複製套件 |  | &#10004; | &#10004; | | |
| 管理 *global-package* 和快取資料夾 | &#10004; | &#10004; | &#10004; | | |
| 管理 NuGet 組態 | | &#10004; | &#10004; | | |

(1) 不會影響專案檔；請改為使用 `dotnet.exe`。

(2) 只能搭配 `packages.config` 檔案運作，無法搭配方案 (`.sln`) 檔案運作。

(3) 各種進階的套件功能只能透過 CLI 取得，因為這些功能不會在 Visual Studio UI 工具中呈現。

(4) 可搭配 `.nuspec` 檔案運作，但無法搭配專案檔運作。

## <a name="upcoming-features"></a>即將推出的功能
如果您想要預覽即將推出的 NuGet 功能，請安裝[Visual Studio preview](https://www.visualstudio.com/vs/preview/)，其可與穩定的 Visual Studio 版本並存運作。 若要針對預覽回報問題或分享想法，請在 [NuGet GitHub 存放庫](https://github.com/Nuget/Home/issues) \(英文\) 上建立問題。

### <a name="related-topics"></a>相關主題

- [使用 Visual Studio 安裝和管理套件](consume-packages/install-use-packages-visual-studio.md)
- [使用 PowerShell 安裝和管理套件](consume-packages/install-use-packages-powershell.md)
- [使用 dotnet CLI 安裝和管理套件](consume-packages/install-use-packages-dotnet-cli.md)
- [使用 nuget.exe CLI 安裝和管理套件](consume-packages/install-use-packages-nuget-cli.md)
- [套件管理員主控台 PowerShell 參考](reference/powershell-reference.md)
- [建立套件](create-packages/creating-a-package.md)
- [發行套件](nuget-org/publish-a-package.md)

在 Windows 上工作的開發人員也可以探索 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) \(英文\)，這是一個開放原始碼的獨立工具，可讓您以視覺化方式瀏覽、建立和編輯 NuGet 套件。 例如，它非常適合用來對套件結構進行實驗性變更，而不需重建套件。
