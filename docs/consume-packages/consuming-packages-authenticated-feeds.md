---
title: 使用已驗證摘要中的套件
description: 在所有 NuGet 用戶端案例中使用來自已驗證摘要的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231788"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>使用已驗證摘要中的套件

除了 nuget.org[公用](https://api.nuget.org/v3/index.json)摘要以外，nuget 用戶端也能夠與檔案摘要和私人 HTTP 摘要互動。


若要使用私用 HTTP 摘要進行驗證，這2種方法是：

* 在[nuget.exe](../reference/nuget-config-file.md#packagesourcecredentials)中新增認證
* 根據使用的用戶端，使用許多擴充性模型其中之一進行驗證。

## <a name="nuget-clients-authentication-extensibility"></a>NuGet 用戶端的驗證擴充性

針對各種 NuGet 用戶端，私用摘要提供者本身會負責驗證。
所有 NuGet 用戶端都具有可支援此功能的擴充方法。 這些是可以與 NuGet 通訊以取得認證的 Visual Studio 擴充功能或外掛程式。

### <a name="visual-studio"></a>Visual Studio

在 Visual Studio 中，NuGet 會公開摘要提供者可以執行並提供給其客戶的介面。 如需詳細資訊，請參閱[如何建立 Visual Studio 認證提供者](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的檔。

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 可用的 NuGet 認證提供者

支援 Azure DevOps 的 Visual Studio 內建認證提供者。


可用的外掛程式認證提供者包括：

* [Visual Studio 的 MyGet 認證提供者](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

當 `nuget.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：

1. 尋找 `NuGet.config` 檔案中的認證。
1. 使用 V2 外掛程式認證提供者
1. 使用 V1 外掛程式認證提供者
1. 然後，NuGet 會在命令列上提示使用者提供認證。

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe 和 V2 認證提供者

在版本中，`4.8` NuGet 定義了新的驗證外掛程式機制，而這裡則稱為 V2 認證提供者。
如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe 和 V1 認證提供者

在版本中 `3.3` NuGet 引進了第一版的驗證外掛程式。
如需瞭解這些提供者的安裝和探索，請參閱[nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>適用于 nuget.exe 的認證提供者

* [Azure DevOps V2 認證提供](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later)者或[Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

在 Visual Studio 2017 15.9 版和更新版本中，Azure DevOps 認證提供者已配套 Visual Studio。
如果 `nuget.exe` 使用該特定 Visual Studio 工具組中的 MSBuild，則會自動探索外掛程式。

### <a name="dotnetexe"></a>dotnet .exe

當 `dotnet.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：

1. 尋找 `NuGet.config` 檔案中的認證。
1. 使用 V2 外掛程式認證提供者

根據預設 `dotnet.exe` 不是互動式的，因此您可能需要傳遞 `--interactive` 旗標，才能讓工具封鎖以進行驗證。

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet .exe 和 V2 認證提供者

在 SDK 的版本 `2.2.100` 中，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。
如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-dotnetexe"></a>Dotnet 可用的認證提供者

* [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>Msbuild.exe

當 `MSBuild.exe` 需要認證以向摘要進行驗證時，它會以下列方式尋找這些認證：

1. 在 `NuGet.config` 檔案中尋找認證
1. 使用 V2 外掛程式認證提供者

根據預設 `MSBuild.exe` 不是互動式的，因此您可能需要設定 `/p:NuGetInteractive=true` 屬性，才能讓工具封鎖以進行驗證。

#### <a name="msbuildexe-and-v2-credential-providers"></a>Msbuild.exe 和 V2 認證提供者

在 Visual Studio 2019 Update 9 中，NuGet 定義了適用于所有用戶端的驗證外掛程式機制。
如需這些提供者的安裝和探索，請參閱[NuGet 跨平臺外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-msbuildexe"></a>Msbuild.exe 可用的認證提供者

* [Azure Artifacts 認證提供者](https://github.com/microsoft/artifacts-credprovider)

在 Visual Studio 2017 Update 9 和更新版本中，Azure DevOps 認證提供者會與 Visual Studio 配套。 不需要其他步驟。
