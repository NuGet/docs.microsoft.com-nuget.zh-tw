---
title: 使用 NuGet 套件的概觀和工作流程
description: 在專案中使用 NuGet 套件之程序的概觀，以及程序之其他特定部分的連結。
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 5f1856940a988e0585c29ccfd581d823e4f69921
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775069"
---
# <a name="package-consumption-workflow"></a>套件使用工作流程

在 nuget.org 與您組織可建立的私人套件庫之間，您可以找到數以萬計的高可用套件，以在您的應用程式和服務中使用。 但是不論來源為何，使用套件會遵循相同的一般工作流程。

![移至套件來源、尋找套件、將它安裝至專案，然後新增 using 陳述式和套件 API 呼叫的流程](media/Overview-01-GeneralFlow.png)

\*_Visual Studio 和 `dotnet.exe` 。此 `nuget install` 命令不會修改專案檔或檔案 `packages.config` ; 必須以手動方式管理專案。_

如需詳細資料，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)和[安裝套件後會發生什麼事](../concepts/package-installation-process.md)。

NuGet 會記住每個已安裝套件的身分識別和版本號碼，並將其記錄在專案檔 (使用 [PackageReference](../consume-packages/package-references-in-project-files.md)) 或 [`packages.config`](../reference/packages-config.md) 中，端視專案類型和 NuGet 版本而定。 使用 NuGet 4.0+ 時，儘管可在 Visual Studio 中透過[套件管理員 UI ](install-use-packages-visual-studio.md)來設定，但最好是使用 PackageReference。 在任何情況下，您隨時都可以查看適當的檔案，以查看您專案的完整相依性清單。

> [!Tip]
> 最好一律檢查您要在軟體中使用之每個套件的授權。 在 nuget.org 上，您可以在每個套件的描述頁面右側找到 [授權資訊] 連結。 如果套件未指定授權條款，請使用套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。 Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。

安裝套件時，NuGet 通常會檢查是否已經可以從其快取中使用套件。 您可以從命令列手動清除此快取，如[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

NuGet 也會確保套件所支援的目標架構與您的專案相容。 如果套件未包含相容的組件，則 NuGet 會顯示錯誤。 請參閱[解決不相容的套件錯誤](../concepts/dependency-resolution.md#resolving-incompatible-package-errors)。

將專案程式碼新增至來源存放庫時，您通常不會包含 NuGet 套件。 如果人員稍後複製存放庫或取得專案，其中包含 Visual Studio Team Services 這類系統上組建代理程式，則必須先還原必要套件，再執行組建置：

![複製存放庫並使用還原命令來還原 NuGet 套件的流程](media/Overview-02-RestoreFlow.png)

[套件還原](../consume-packages/package-restore.md)使用專案檔或 `packages.config` 中的資訊來重新安裝所有相依性。 請注意，所含的程序會有些差異，如[相依性解析](../concepts/dependency-resolution.md)中所述。 此外，上圖並沒有顯示套件管理員主控台的還原命令，原因是如果您在使用主控台，就代表您已經在使用 Visual Studio，它通常會自動還原套件並提供如同圖示的解決方案層級命令。

偶爾需要重新安裝已包含在專案中的套件，這也可能會重新安裝相依性。 使用 `nuget reinstall` 命令或 NuGet 套件管理員主控台，就可以輕鬆做到這項作業。 如需詳細資料，請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。

最後，NuGet 的行為是透過 `Nuget.Config` 檔案所驅動。 可以使用多個檔案來集中管理不同層級的特定設定，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)所述。

## <a name="ways-to-install-a-nuget-package"></a>安裝 NuGet 套件的方式

NuGet 套件會使用下表任一方法下載並安裝。

| 工具 | 描述 |
| --- | --- |
| [dotnet.exe CLI](install-use-packages-dotnet-cli.md) | 適用於 .NET Core 與 .NET Standard 程式庫，以及適用於以 .NET Framework 為目標的 SDK 樣式專案 CLI 工具 (請參閱 [ SDK 屬性](/dotnet/core/tools/csproj#additions))。 抓取所識別的封裝 \<package_name\> ，並將參考加入至專案檔。 此外，也會擷取並安裝相依性。 |
| Visual Studio | (Windows 和 Mac) 提供 UI，透過該 UI 可從指定套件來源瀏覽、選取套件及其相依性並安裝至專案。 將對於已安裝套件的參考新增至專案檔。<ul><li>[使用 Visual Studio 安裝和管理套件](install-use-packages-visual-studio.md)</li><li>[在專案中包含 NuGet 套件 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [套件管理員主控台 (Visual Studio)](install-use-packages-powershell.md) |  (僅限 Windows) 從選取的來源將所識別的封裝，並安裝 \<package_name\> 到方案中的指定專案，然後將參考新增至專案檔。 此外，也會擷取並安裝相依性。 |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | (所有平台) 適用於 .NET Framework 程式庫及以 .NET Standard 程式庫為目標的非 SDK 樣式專案 CLI 工具。 抓取所識別的封裝 \<package_name\> ，並將其內容展開至目前的目錄中的資料夾; 也可以取出檔案中列出的所有套件 `packages.config` 。 另外也會擷取並安裝相依性，但不會對專案檔或 `packages.config` 進行任何變更。 |
