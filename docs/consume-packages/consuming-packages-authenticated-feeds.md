---
title: 從經過驗證的摘要使用套件
description: 在所有 NuGet 用戶端案例中使用來自已驗證摘要的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901508"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>從經過驗證的摘要使用套件

除了 nuget.org [公用](https://api.nuget.org/v3/index.json)摘要，nuget 用戶端還能夠與檔案摘要和私用 HTTP 摘要互動。


若要使用私用 HTTP 摘要進行驗證，2種方法如下：

* 在[NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)中新增認證
* 視使用的用戶端而定，使用許多擴充性模型的其中一種進行驗證。

## <a name="nuget-clients-authentication-extensibility"></a>NuGet 用戶端的驗證擴充性

針對不同的 NuGet 用戶端，私用摘要提供者本身會負責驗證。
所有 NuGet 用戶端都具有可支援此功能的擴充方法。 這些是 Visual Studio 擴充功能或可與 NuGet 通訊以取得認證的外掛程式。

### <a name="visual-studio"></a>Visual Studio

在 Visual Studio 中，NuGet 會公開一個介面，讓摘要提供者可以執行並提供給客戶。 如需詳細資訊，請參閱有關 [如何建立 Visual Studio 認證提供者](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的檔。

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 的可用 NuGet 認證提供者

Visual Studio 內建的認證提供者可支援 Azure DevOps。


可用的外掛程式認證提供者包括：

* [適用于 Visual Studio 的 MyGet 認證提供者](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

`nuget.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：

1. 尋找檔案中的認證 `NuGet.config` 。
1. 使用 V2 外掛程式認證提供者
1. 使用 V1 外掛程式認證提供者
1. 接著，NuGet 會在命令列提示使用者輸入認證。

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe 和 V2 認證提供者

在 NuGet 版中 `4.8` ，定義了新的驗證外掛程式機制，此處稱為 V2 認證提供者。
若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe 和 V1 認證提供者

在 NuGet 版中 `3.3` 引進了第一版的驗證外掛程式。
若要安裝和探索這些提供者，請參閱 [nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe 可用的認證提供者

* [Azure DevOps V2 認證提供者](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) 或 [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

在 Visual Studio 2017 15.9 版和更新版本中，Azure DevOps 認證提供者會隨附于 Visual Studio。
如果 `nuget.exe` 從該特定的 Visual Studio 工具組使用 MSBuild，則會自動探索該外掛程式。

### <a name="dotnetexe"></a>dotnet.exe

`dotnet.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：

1. 尋找檔案中的認證 `NuGet.config` 。
1. 使用 V2 外掛程式認證提供者

根據預設 `dotnet.exe` ，您可能需要傳遞旗標， `--interactive` 才能讓工具封鎖以進行驗證。

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe 和 V2 認證提供者

在 SDK 版本中 `2.2.100` ，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。
若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe 可用的認證提供者

* [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

`MSBuild.exe`需要認證才能向摘要進行驗證時，會以下列方式尋找這些認證：

1. 在檔案中尋找認證 `NuGet.config`
1. 使用 V2 外掛程式認證提供者

依預設 `MSBuild.exe` 不是互動式的，因此您可能需要設定 `/p:NuGetInteractive=true` 屬性，以取得封鎖驗證的工具。

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe 和 V2 認證提供者

在 Visual Studio 2019 Update 9 中，NuGet 定義了可在所有用戶端中運作的驗證外掛程式機制。
若要安裝和探索這些提供者，請參閱 [NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe 可用的認證提供者

* [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

在 Visual Studio 2017 Update 9 和更新版本中，Azure DevOps 認證提供者會隨附于 Visual Studio。 不需要任何額外步驟。
