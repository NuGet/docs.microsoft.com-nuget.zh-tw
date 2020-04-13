---
title: 使用來自經過身份驗證的來源的套件
description: 在所有 NuGet 用戶端機制中使用來自經過身份驗證的來源的套件
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231788"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>使用來自經過身份驗證的來源的套件

除了nuget.org[公共來源](https://api.nuget.org/v3/index.json),NuGet 用戶端還能夠與檔案源和專用 HTTP 源進行互動。


要使用私有 HTTP 源進行身份驗證,這兩種方法是:

* 在[NuGet.config 中加入](../reference/nuget-config-file.md#packagesourcecredentials)認證
* 根據所使用的用戶端,使用眾多擴充性模型之一進行身份驗證。

## <a name="nuget-clients-authentication-extensibility"></a>NuGet 客戶端的驗證擴充性

對於各種 NuGet 用戶端,專用源提供程式本身負責身份驗證。
所有 NuGet 用戶端都有擴充性方法來支援此功能。 這些擴展可以是 Visual Studio 擴充,也可以是一個外掛程式,可以與 NuGet 通信以檢索認證。

### <a name="visual-studio"></a>Visual Studio

在 Visual Studio 中,NuGet 公開了一個介面,供應商可以實現該介面並將其提供給其客戶。 有關詳細資訊,請參閱有關如何創建 Visual Studio[認證提供程式](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的文件。

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>適用於視覺化工作室的可用 NuGet 認證提供者

可視化工作室中內置了一個憑據提供程式來支援 Azure DevOps。


可用的外掛程式認證提供者包括:

* [MyGet 視覺化工作室的認證提供者](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

當`nuget.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:

1. 在`NuGet.config`檔中查找憑據。
1. 使用 V2 外掛程式認證提供者
1. 使用 V1 外掛程式認證提供者
1. 然後,NuGet 會提示使用者在命令列上獲取憑據。

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe 和 V2 認證提供者

在版本`4.8`NuGet 中定義了一種新的身份驗證外掛程式機制,以下簡稱 V2 認證提供提供者。
有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe 和 V1 認證提供者

在版本`3.3`NuGet 中引入了身份驗證外掛程式的第一個版本。
有關這些提供程式的安裝和發現,請參閱[nuget.exe 認證提供者](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe 可用認證提供者

* [Azure DevOps V2 認證提供者](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later)或[Azure 專案認證提供者](https://github.com/microsoft/artifacts-credprovider)

使用 Visual Studio 2017 版本 15.9 及更高版本,Azure DevOps 認證提供程式捆綁在可視化工作室中。
如果`nuget.exe`使用來自該特定可視化工作室工具集的 MSBuild,則外掛程式將自動發現。

### <a name="dotnetexe"></a>dotnet.exe

當`dotnet.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:

1. 在`NuGet.config`檔中查找憑據。
1. 使用 V2 外掛程式認證提供者

預設情況下`dotnet.exe`,它不是互動式的,因此您可能需要傳遞標誌`--interactive`才能阻止該工具進行身份驗證。

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe 和 V2 認證提供者

在`2.2.100`SDK 版本中,NuGet 定義了適用於所有用戶端的身份驗證外掛程式機制。
有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe 的可用認證提供者

* [Azure 專案認證提供者](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

當`MSBuild.exe`需要憑據來使用源進行身份驗證時,它會以以下方式查找它們:

1. 在`NuGet.config`檔案中尋找認證
1. 使用 V2 外掛程式認證提供者

預設情況下`MSBuild.exe`不是互動`/p:NuGetInteractive=true`式的 ,因此您可能需要設置屬性以使工具阻止進行身份驗證。

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe 和 V2 認證提供者

在 Visual Studio 2019 更新 9 中,NuGet 定義了適用於所有用戶端的身份驗證外掛程式機制。
有關這些提供程式的安裝和發現,請參閱[NuGet 跨平台外掛程式](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-msbuildexe"></a>可用於 MSBuild.exe 可用認證提供者

* [Azure 專案認證提供者](https://github.com/microsoft/artifacts-credprovider)

使用 Visual Studio 2017 更新 9 及更高版本,Azure DevOps 認證提供提供程式捆綁在可視化工作室中。 無需執行其他步驟。
