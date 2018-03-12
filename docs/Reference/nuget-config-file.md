---
title: "NuGet.Config 檔案參考 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。"
keywords: "NuGet.Config 檔案, NuGet 組態參考, NuGet 組態選項"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c76ebcb06adc5e5b862647de6b6f4e19bde87b91
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="nugetconfig-reference"></a>NuGet.Config 參考

NuGet 行為受到不同 `NuGet.Config` 檔案中的設定所控制，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)中所述。

`NuGet.Config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。 每一個區段包含零個或更多 `<add>` 項目與 `key` 和 `value` 屬性。 請參閱[設定檔範例](#example-config-file)。 設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。

本主題內容：

- [config 區段](#config-section)
- [bindingRedirects 區段](#bindingredirects-section)
- [packageRestore 區段](#packagerestore-section)
- [solution 區段](#solution-section)
- [套件來源區段](#package-source-sections)：
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [使用環境變數](#using-environment-variables)
- [設定檔範例](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config 區段

包含其他組態設定，可以使用 [`nuget config` 命令](../tools/cli-ref-config.md)設定。

注意：`dependencyVersion` 和 `repositoryPath` 僅適用於使用 `packages.config` 的專案。 `globalPackagesFolder` 僅適用於使用 PackageReference 格式的專案。

| Key | 值 |
| --- | --- |
| dependencyVersion (僅 `packages.config`) | 當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。 NuGet 套件管理員 UI 也使用此值。 值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。 |
| globalPackagesFolder (不使用 `packages.config` 的專案) | 預設全域套件資料夾的位置。 預設值為 `%USERPROFILE%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。 相對路徑可用於專案特有的 `Nuget.Config` 檔案。 |
| repositoryPath (僅 `packages.config`) | 要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。 相對路徑可用於專案特有的 `Nuget.Config` 檔案。 |
| defaultPushSource | 識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | 連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。 密碼會加密，且無法手動新增。 對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。 您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。 如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。 |

**範例**：

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects 區段

設定 NuGet 在安裝套件時，是否自動繫結重新導向。

| Key | 值 |
| --- | --- |
| skip | 布林值，指出是否略過自動繫結重新導向。 預設為 false。 |

**範例**：

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore 區段

*忽略所有的目前版本 （2.7 +）*

控制建置期間的套件還原。

| Key | 值 |
| --- | --- |
| enabled | 布林值，指出 NuGet 是否可以執行自動還原。 您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。 |
| 自動 | 布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。 |

**範例**：

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>solution 區段

控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。 本區段只適用於解決方案資料夾中的 `Nuget.Config` 檔。

| Key | 值 |
| --- | --- |
| disableSourceControlIntegration | 布林值，指出當使用原始檔控制時是否要忽略 packages 資料夾。 預設值為 false。 |

**範例**：

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>套件來源區段

`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起運作，以設定 NuGet 在安裝、還原及更新作業期間，如何處理套件儲存機制。

[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用來管理這些設定，但 `apikeys` 例外，它是使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)來管理。

請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。

### <a name="packagesources"></a>packageSources

列出所有已知的套件來源。 在還原作業期間，以及與任何使用 PackageReference 格式的專案，會忽略順序。 NuGet 尊重安裝的來源順序，並使用專案以更新 operations `packages.config`。

| Key | 值 |
| --- | --- |
| (要指派給套件來源的名稱) | 套件來源的路徑或 URL。 |

**範例**：

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。 依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。

| Key | 值 |
| --- | --- |
| username | 純文字的來源使用者名稱。 |
| 密碼 | 加密的來源密碼。 |
| cleartextpassword | 未加密的來源密碼。 |

**範例：**

設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020+`)。 也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

使用未加密的密碼時：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

為使用 API 金鑰驗證的來源儲存金鑰，如同以 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)所設。

| Key | 值 |
| --- | --- |
| (來源 URL) | 加密的 API 金鑰。 |

**範例**：

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

識別目前已停用的來源。 可以是空的。

| Key | 值 |
| --- | --- |
| (來源名稱) | 布林值，指出是否停用來源。 |

**範例：**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(僅 2.x，在 3.x+ 中已被取代)*

識別目前作用中的來源，或表示所有來源的彙總。

| Key | 值 |
| --- | --- |
| (來源名稱) 或 `All` | 如果金鑰是來源的名稱，則值是來源路徑或 URL。 若為 `All`，值應該是 `(Aggregate source)` 以結合未以其他方式停用的所有套件來源。 |

**範例**：

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>使用環境變數

您可以在 `NuGet.Config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。

例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。

同樣地，如果 Mac/Linux 上的 `HOME` 設為 `/home/myStuff`，則設定檔中的 `$HOME/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository`。

如果找不到環境變數，NuGet 會使用來自設定檔的常值。

## <a name="example-config-file"></a>範例設定檔

以下是 `NuGet.Config` 檔範例，說明多項設定：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
