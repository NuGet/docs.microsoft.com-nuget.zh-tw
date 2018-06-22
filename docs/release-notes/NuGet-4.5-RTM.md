---
title: NuGet 4.5 RTM 版本資訊
description: NuGet 4.5 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820712"
---
# <a name="nuget-45-rtm-release-notes"></a>NuGet 4.5 RTM 版本資訊

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)。

## <a name="known-issues"></a>已知問題

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題 

.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。 [這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools

#### <a name="issue"></a>問題

NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>因應措施

您必須在專案檔中手動編輯 DotNetCLIToolReferences。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>重定目標 Framework 版本可能會導致不完整的 Intellisense

#### <a name="issue"></a>問題

在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。 當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>因應措施

請執行手動還原。

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core 專案中的套件如包含具有無效簽章的組件，可能會觸發無限的還原迴圈。

#### <a name="issue"></a>問題

有時候，當您使用的套件包含具有無效簽章的組件時，或套件版本使用 'DateTime' 指示器設定時，會導致套件自動還原為在無限迴圈中執行 [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)。

#### <a name="workaround"></a>因應措施

此問題目前沒有因應措施。

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM 時間範圍中已修正的問題

針對 NuGet 4.4 RTM 中已修正的問題，請參閱 [NuGet 4.4 RTM 版本資訊](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>功能

- 停用自動推送符號套件 - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Bug

- 15.5p1 中的 [迴歸]：跳過 Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)
- 還原後遺失套件中的資產 - [#5995](https://github.com/NuGet/Home/issues/5995)
- 外掛程式認證提供者不會使用包含空格的 URI - [#5982](https://github.com/NuGet/Home/issues/5982)
- 如果無法還原套件，則即使開啟最少詳細資訊，還是應該在輸出中列印錯誤 - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - 方案層級的 dotnetcore restore 未遵循 ProjectReference 和 ReferenceOutputAssembly，而錯誤導致隨機組建失敗 - [#5490](https://github.com/NuGet/Home/issues/5490)
- 使用物件方法，PMC 中的自動完成無法正確運作 - [#4800](https://github.com/NuGet/Home/issues/4800)
- Visual Studio 2015 工具組的 nuget.exe 還原失敗 - [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc 在 vs2017 中具現化極為耗費資源 - [#4205](https://github.com/NuGet/Home/issues/4205)
- 慢速以取得慢速連線的相依性資訊 - [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package w/ 如果多個套件共用通用相依性，則 -RemoveDependencies 會失敗 - [#4026](https://github.com/NuGet/Home/issues/4026)
- 完成 NuGet.Core.nupkg 以進行發行 - [#3581](https://github.com/NuGet/Home/issues/3581)
- 將 -IncludeProjectReferences 用於 csproj + project.json 時，NuGet 套件會從目錄名稱解析相依性識別碼 - [#3566](https://github.com/NuGet/Home/issues/3566)
- 'NuGet.ProxyCache' 的類型初始設定式已擲出例外狀況 - [#3144](https://github.com/NuGet/Home/issues/3144)
- Kudu 的 Nuget 還原效能問題 - [#3087](https://github.com/NuGet/Home/issues/3087)
- 搜尋早於註冊 Blob 時，UI 用戶端無法顯示任何錯誤或警告 - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -更新產生不正確的查詢 - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>4.5 RTM 中已修正之 GitHub 問題的連結

[問題清單](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
