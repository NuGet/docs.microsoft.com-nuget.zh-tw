---
title: "安裝 NuGet 套件的方式 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "描述將 NuGet 套件安裝到專案的程序，包括在磁碟上及適用的專案檔會發生什麼情況。"
keywords: "安裝 NuGet, NuGet 套件耗用量, 安裝 NuGet 套件, NuGet 套件參考"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>安裝 NuGet 套件的不同方式

NuGet 套件會使用下列任一種方法來下載並安裝 (如果您尚未安裝這些項目，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md))：

| 方法 | 描述 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (所有平台) 下載 \<package_name\> 所識別的套件、在目前目錄的資料夾中展開其內容，並將參考新增到專案檔。 此外，也請下載並安裝相依性。<ul><li>[安裝並使用套件 (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet 命令](../tools/dotnet-commands.md)</li></ul> |
| 套件管理員 UI (Visual Studio) | (Windows 和 Mac) 提供 UI，透過該 UI 可瀏覽、選取套件及其相依性並安裝至專案。 將對於已安裝套件的參考新增至專案檔。<ul><li>[安裝並使用套件 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[套件管理員 UI 參考 (Windows)](../tools/package-manager-ui.md)</li><li>[在專案中包含 NuGet 套件 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 套件管理員主控台 (Visual Studio)<br/>`Install-Package <package_name>` | (僅限 Windows) 下載 \<package_name\> 所識別的套件並安裝到方案中的指定專案，然後將參考新增到專案檔。 此外，也請下載並安裝相依性。<ul><li>[安裝並使用套件 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[套件管理員主控台指南](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (所有平台) 下載 \<package_name\> 所識別的套件，並在目前目錄的資料夾中展開其內容；也可以下載 `packages.config` 檔案中列出的所有套件。 此外，也請下載並安裝相依性，但不要對專案檔進行任何變更。<ul><li>[安裝命令](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>一般安裝程序

NuGet 通常會執行下列動作，然後要求安裝套件：

1. 取得套件：
    - 檢查要求的套件是否已經存在快取中 (請參閱[管理 NuGet 快取](managing-the-nuget-cache.md))。
    - 如果套件不在快取中，請嘗試從組態檔中所列的來源下載套件，從清單的第一個項目開始。 此行為可讓您在於 nuget.org 上尋找套件之前，先使用私人套件摘要 (請參閱[設定 NuGet 行為](configuring-nuget-behavior.md))。
    - 如果已成功從其中一個來源取得套件，NuGet 就會將它新增至快取。 否則，安裝會失敗。

1. 在專案中展開套件。
    - 展開的意思是將套件的內容解壓縮到適當的子資料夾。 系統也會在子資料夾中放置 `.nupkg` 本身的複本。
    - 如果將套件安裝到 Visual Studio 或 .NET Core 專案，就只會展開與專案目標 Framework 相關的檔案。 使用 nuget.exe 命令列安裝時，會展開所有組件。

1. 如果將套件安裝於 Visual Studio 或 dotnet CLI 內，就會將參考新增至適當的專案檔 (或 `packages.config`，適用於 Visual Studio 中的某些專案類型)。

## <a name="related-topics"></a>相關主題

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)
- [管理 NuGet 快取](managing-the-nuget-cache.md)
