---
title: nuget.config 檔案參考
description: NuGet.Config 檔案參考，包括 config、bindingRedirects、packageRestore、solution 和 packageSource 區段。
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 38620058bccde876152328302a6049f011c149db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901859"
---
# <a name="nugetconfig-reference"></a>`nuget.config` 參考

NuGet 行為是由不同或檔案中的設定所控制， `NuGet.Config` `nuget.config` 如 [一般 NuGet](../consume-packages/configuring-nuget-behavior.md)設定中所述。

`nuget.config` 是包含最上層 `<configuration>` 節點的 XML 檔案，該節點則包含本主題中所述的區段項目。 每個區段包含零或多個專案。 請參閱[設定檔範例](#example-config-file)。 設定名稱會區分大小寫，而且值可以使用[環境變數](#using-environment-variables)。

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config 區段

包含可使用[ `nuget config` 命令](../reference/cli-reference/cli-ref-config.md)設定的其他設定。

`dependencyVersion` 並 `repositoryPath` 僅適用于使用的 `packages.config` 專案。 `globalPackagesFolder` 只適用于使用 PackageReference 格式的專案。

| Key | 值 |
| --- | --- |
| dependencyVersion (僅 `packages.config`) | 當未直接指定 `-DependencyVersion` 參數時，套件安裝、還原及更新的預設 `DependencyVersion` 值。 NuGet 套件管理員 UI 也使用此值。 值為 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。 |
| 使用僅限 PackageReference 的 globalPackagesFolder (專案)  | 預設全域套件資料夾的位置。 預設值為 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。 相對路徑可用於專案特有的 `nuget.config` 檔案。 這項設定是由環境變數所覆寫 `NUGET_PACKAGES` ，它的優先順序較高。 |
| repositoryPath (僅 `packages.config`) | 要在其中安裝 NuGet 套件的位置，而非預設 `$(Solutiondir)/packages` 資料夾。 相對路徑可用於專案特有的 `nuget.config` 檔案。 這項設定是由環境變數所覆寫 `NUGET_PACKAGES` ，它的優先順序較高。 |
| defaultPushSource | 識別在找不到任何其他套件來源可進行作業時，應該作為預設值使用的套件來源 URL 或路徑。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | 連線到套件來源時使用的 Proxy 設定；`http_proxy` 應該為 `http://<username>:<password>@<domain>` 格式。 密碼會加密，且無法手動新增。 對於 `no_proxy`，值是會略過 Proxy 伺服器的網域清單，並以逗號分隔。 您可以為那些值選擇使用 http_proxy 及 no_proxy 環境變數。 如需詳細資料，請參閱 [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (NuGet proxy 設定) (skolima.blogspot.com)。 |
| 因為 signaturevalidationmode | 指定驗證模式，用來驗證封裝安裝和還原的封裝簽章。 值為 `accept` 、 `require` 。 預設值為 `accept`。

**範例**：

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
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

控制建置期間的套件還原。

| Key | 值 |
| --- | --- |
| 已啟用 | 布林值，指出 NuGet 是否可以執行自動還原。 您也可以使用 `True` 值來設定 `EnableNuGetPackageRestore` 環境變數，而不是在設定檔中設定此金鑰。 |
| automatic | 布林值，指出 NuGet 是否應該在建置期間檢查遺漏的套件。 |

**範例**：

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>solution 區段

控制解決方案的 `packages` 資料夾是否會包含在原始檔控制。 本區段只適用於解決方案資料夾中的 `nuget.config` 檔。

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

`packageSources`、、 `packageSourceCredentials` `apikeys` 、 `activePackageSource` `disabledPackageSources` 和全都會 `trustedSigners` 一起運作，以設定在安裝、還原和更新作業期間，NuGet 與套件存放庫的搭配運作方式。

[ `nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)通常用來管理這些設定，但 `apikeys` 使用[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)來管理，以及 `trustedSigners` 使用[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)管理的例外。

請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。

### <a name="packagesources"></a>packageSources

列出所有已知的套件來源。 在還原作業期間，以及使用 PackageReference 格式的任何專案時，會忽略順序。 NuGet 會遵循使用專案進行安裝和更新作業的來源順序 `packages.config` 。

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

> [!Tip]
> 指定節點具有 `<clear />` 時，NuGet 會忽略先前針對該節點所定義的組態值。 [深入瞭解設定的套用方式](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

### <a name="packagesourcecredentials"></a>packageSourceCredentials

儲存來源的使用者名稱和密碼，通常使用 `nuget sources` 的 `-username` 和 `-password` 參數來指定。 依預設會加密密碼，除非同時使用了 `-storepasswordincleartext` 選項。
（選擇性）使用參數可以指定有效的驗證類型 `-validauthenticationtypes` 。

| Key | 值 |
| --- | --- |
| username | 純文字的來源使用者名稱。 |
| 密碼 | 加密的來源密碼。 只有在 Windows 上才支援加密的密碼，而且只有在同一部電腦上使用時，以及透過與原始加密相同的使用者才能解密。 |
| cleartextpassword | 未加密的來源密碼。 注意：環境變數可以用來改善安全性。 |
| validauthenticationtypes | 此來源的有效驗證類型清單（以逗號分隔）。 將此設定為， `basic` 如果伺服器通告 NTLM 或 Negotiate，而且您的認證必須使用基本機制傳送，例如，搭配內部部署 Azure DevOps Server 使用 PAT。 其他有效的值包括 `negotiate` 、 `kerberos` 、 `ntlm` 和 `digest` ，但這些值不太可能很有用。 |

**範例︰**

設定檔中，`<packageSourceCredentials>` 項目包含每個適用來源名稱的子節點 (名稱中的空格會取代為 `_x0020_`)。 也就是說，對於名為 "Contoso" 和 "Test Source" 的來源，在使用加密的密碼時設定檔時包含下列內容：

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

使用儲存在環境變數中的未加密密碼時：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

此外，也可以提供有效的驗證方法：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

儲存使用 API 金鑰驗證之來源的金鑰，如[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)所設定。

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

**範例︰**

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

## <a name="trustedsigners-section"></a>trustedSigners 區段

在安裝或還原時，儲存用來允許套件的受信任簽署者。 當使用者將設定為時，此清單不可以是空的 `signatureValidationMode` `require` 。 

您可以使用[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)來更新此區段。

**結構描述**：

受信任的簽署者有一個 `certificate` 專案集合，這些專案會登錄識別指定之簽署者的所有憑證。 受信任的簽署者可以是 `Author` 或 `Repository` 。

受信任的存放 *庫* 也會指定存放 `serviceIndex` 庫 (的，其必須是有效的 `https` uri) 而且可以選擇性地指定以分號分隔的清單， `owners` 以限制更多受該特定存放庫信任的物件。

用於憑證指紋的支援雜湊演算法為 `SHA256` 、 `SHA384` 和 `SHA512` 。

如果 `certificate` 指定為指定的 `allowUntrustedRoot` 憑證，則在 `true` 建立憑證鏈作為簽章驗證的一部分時，允許鏈至不受信任的根。

**範例**：

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders 區段

*(3.5 +)* 提供預先安裝封裝的方法，因此，如果在回溯資料夾中找到封裝，就不需要執行任何工作。 Fallback 封裝資料夾與全域封裝資料夾的資料夾和檔案結構完全相同： *nupkg* 存在，而且所有檔案都已解壓縮。

這項設定的查閱邏輯是：

- 查看全域封裝資料夾，查看是否已下載套件/版本。

- 查看 [回復] 資料夾中是否有套件/版本相符。

如果其中一項查閱成功，則不需要下載。

如果找不到相符項，則 NuGet 會檢查檔案來源，然後再檢查 HTTP 來源，然後下載套件。

| Key | 值 |
| --- | --- |
|  (的 [fallback] 資料夾名稱)  | Fallback 資料夾的路徑。 |

**範例**：

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement 區段

設定預設封裝管理格式（ *packages.config* 或 PackageReference）。 SDK 樣式的專案一律使用 PackageReference。

| Key | 值 |
| --- | --- |
| format | 指出預設封裝管理格式的布林值。 如果 `1` 為，則格式為 PackageReference。 如果 `0` 為，則 *packages.config* 格式。 |
| disabled | 布林值，指出是否要在第一次安裝套件時顯示提示以選取預設封裝格式。 `False` 隱藏提示。 |

**範例**：

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>使用環境變數

您可以在 `nuget.config` 值中使用環境變數 (NuGet 3.4+)，在執行階段套用設定。

例如，如果 Windows 上的 `HOME` 環境變數設為 `c:\users\username`，則設定檔中的 `%HOME%\NuGetRepository` 值會解析為 `c:\users\username\NuGetRepository`。

請注意，您必須使用 Windows 樣式的環境變數 (以% ) 作為開頭和結尾，即使是在 Mac/Linux 上也是如此。 `$HOME/NuGetRepository`無法解析設定檔中的 Having。 在 Mac/Linux 上，的值 `%HOME%/NuGetRepository` 會解析為 `/home/myStuff/NuGetRepository` 。

如果找不到環境變數，NuGet 會使用來自設定檔的常值。 例如， `%MY_UNDEFINED_VAR%/NuGetRepository` 將解析為 `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

下表顯示 NuGet.Config 檔案的環境變數語法和路徑分隔符號的支援。

### <a name="nugetconfig-environment-variable-support"></a>`NuGet.Config` 環境變數支援

| Syntax | Dir 分隔符號 | Windows nuget.exe | Windows dotnet.exe | Mono 中的 Mac nuget.exe ()  | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | 是 | 是 | 是 | 是 |
| `%MY_VAR%` | `\`  | 是 | 是 | 否 | 否 |
| `$MY_VAR` | `/`  | 否 | 否 | 否 | 否 |
| `$MY_VAR` | `\`  | 否 | 否 | 否 | 否 |


## <a name="example-config-file"></a>範例設定檔

以下是範例檔案 `nuget.config` ，其中說明許多設定，包括選擇性的設定：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
