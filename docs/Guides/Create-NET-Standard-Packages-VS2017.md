---
title: "使用 Visual Studio 2017 建立 .NET Standard 2.0 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "使用 NuGet 4.x 和 Visual Studio 2017 建立 .NET Standard 2.0 NuGet 套件的端對端逐步解說。"
keywords: "建立套件, .NET Standard 套件, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>使用 Visual Studio 2017 建立 .NET Standard 2.0 套件

*適用於 NuGet 4.x+ 和 Visual Studio 2017 Update 3 提供的 MSBuild 15.3+。對於舊版的 Visual Studio 2017，這些指示適用於 .NET Standard 1.4 到 1.6，方法是變更 \<TargetFramework\> 屬性。另請參閱[使用 Visual Studio 2015 建立 .NET Standard 套件](../guides/create-net-standard-packages-vs2015.md)，以便使用 NuGet 3.x+。*

[.NET Standard 程式庫](https://docs.microsoft.com/dotnet/articles/standard/library)是計劃提供所有 .NET 執行階段使用的 .NET API 正式規格，因此在 .NET 生態系統中能建立較強的一致性。 .NET Standard 程式庫定義一致的 BCL (基底類別庫) API 集合，以供所有 .NET 平台實作，而不論工作負載為何。 它可讓開發人員產生可跨所有 .NET 執行階段使用的 PCL，並減少 (如果無法消除) 共用程式碼中的平台專屬條件式編譯指示詞。

本指南將引導您使用 Visual Studio 2017 Update 3 和 NuGet 4.0，建立以 .NET Standard 程式庫 2.0 為目標的 nuget 套件。

1. [必要條件](#pre-requisites)
1. [建立類別庫專案](#create-the-netstandard-class-library-project)
1. [編輯 .csproj 檔案中的中繼資料](#edit-metadata-in-the-csproj-file)
1. [封裝元件](#package-the-component)
1. [相關主題](#related-topics)

## <a name="pre-requisites"></a>必要條件

本逐步解說需要 Visual Studio 2017 Update 3 與 **.NET Core 跨平台開發**工作負載。 您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，或使用 Professional Edition 和 Enterprise Edition。

需要的工作負載會如下所示出現在 Visual Studio 安裝程式：

![Visual Studio 安裝程式中的 .NET Core 跨平台開發工作負載](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>建立 .NET Standard 類別庫專案

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [.NET Standard] 節點、選取 [類別庫 (Net Standard)]、將名稱變更為 AppLogger，然後按一下 [確定]。

    ![建立新的類別庫專案](media/NuGet4-02-NewProject.png)

1. 將組建組態變更為 [發行]。
1. 以滑鼠右鍵按一下方案總管中的 `AppLogger` 專案、依序選取 [屬性]、[建置] 索引標籤，核取 [XML 文件檔] 的方塊，並將檔案名稱設為 `AppLogger.xml`。 然後儲存專案。

1. 將您的程式碼新增至元件，如下所示 (它很清楚只輸出訊息至主控台)：

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. (使用發行組態) 建置專案，並確認 DLL 和 XML 檔案已產生在 `bin\Release\netstandard2.0` 資料夾內。

## <a name="edit-metadata-in-the-csproj-file"></a>編輯 .csproj 檔案中的中繼資料

使用 NuGet 4.0 和 .NET Core 專案，套件中繼資料會直接包含在 `.csproj` 檔，而不是外部檔案，例如 `.nuspec`。 該中繼資料的完整描述位於 [NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md#pack-target)。

1. 以滑鼠右鍵按一下方案總管中的專案、選取 [編輯 AppLogger.csproj]，然後編輯第一個屬性群組以包含套件資訊，如下所示：

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. 儲存專案，然後以滑鼠右鍵按一下方案，並選取 [建置方案]，再次產生套件的所有檔案 (這次是使用正確的中繼資料)。


## <a name="package-the-component"></a>封裝元件

NuGet 4.0 支援在當專案包含所需的套件中繼資料時使用 MSBuild 15.1+ 版 (包括 Visual Studio 2017 Update 3 提供的 MSBuild 15.3) 的組件目標，如上一節所新增。 若要以這種方式叫用 MSBuild，只要在命令列上，在與 `.csproj` 檔案的相同資料夾中指定組件目標：

    msbuild /t:pack /p:Configuration=Release

如需 `msbuild /t:pack` 的其他選項，例如包含內容檔案、符號和原始程式碼，請參閱 [NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md#pack-target)。

在任何情況下，上述命令依預設會在它建立該組態時，在 `bin\Release` 資料夾中產生 `AppLogger.YOUR_NAME.1.0.0.nupkg`。 如果您省略 `/p` 參數，預設組態將為 `Debug`。 

在例如 [NuGet 套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)的工具中開啟此檔案，並展開所有節點，您將會看到下列內容：

![顯示 AppLogger 套件的 NuGet 套件總管](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> `.nupkg` 檔案只是一個使用不同副檔名的 ZIP 檔。 然後，您也可以將 `.nupkg` 變更為 `.zip` 來檢查套件內容，但是請記住要先還原副檔名，再將套件上傳至 nuget.org。

若要讓其他開發人員使用您的套件，請遵循[發行套件](../create-packages/publish-a-package.md)的指示。

## <a name="related-topics"></a>相關主題

- [專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)描述直接在專案檔中描述您套件的所有詳細資料。
- [NuGet 包裝及還原為 MSBuild 目標](../schema/msbuild-targets.md)描述使用 `msbuild /t:pack` 建立套件的所有選項。
- [.NET Standard 程式庫文件](https://docs.microsoft.com/dotnet/articles/standard/library)
- [從 .NET Framework 移轉到 .NET Core](https://docs.microsoft.com/dotnet/articles/core/porting/index)
