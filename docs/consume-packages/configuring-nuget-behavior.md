---
title: 設定 NuGet 行為
description: NuGet.Config 檔案可全面和根據每個專案來控制 NuGet 行為，並使用 nuget config 命令進行修改。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c23b464ca39fd8d872f21846a7d6d34edf9dce93
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50088912"
---
# <a name="configuring-nuget-behavior"></a>設定 NuGet 行為

NuGet 行為是透過可存在於專案、使用者和整個電腦層級的一或多個 `NuGet.Config` (XML) 檔案中的累積設定來驅動。 全域 `NuGetDefaults.Config` 檔案還會特別設定套件來源。 設定適用於 CLI、套件管理員主控台和套件管理員 UI 中發出的所有命令。

## <a name="config-file-locations-and-uses"></a>組態檔位置和使用

| 範圍 | NuGet.Config 檔案位置 | 描述 |
| --- | --- | --- |
| 專案 | 目前的資料夾 (也稱為專案資料夾) 或最高到磁碟機根目錄的任何資料夾。| 在專案資料夾中，設定僅適用於該專案。 在包含多個專案子資料夾的父資料夾中，設定適用於這些子資料夾中的所有專案。 |
| 使用者 | Windows：`%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux：`~/.config/NuGet/NuGet.Config` 或 `~/.nuget/NuGet/NuGet.Config` (依 OS 發行版本而異) | 設定適用於所有作業，但會覆寫為任何專案層級設定。 |
| 電腦 | Windows：`%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux：`$XDG_DATA_HOME`。 如果 `$XDG_DATA_HOME` 為 Null 或空白，則會使用 `~/.local/share` 或 `/usr/local/share` (依 OS 發行版本而異)  | 設定適用於電腦上的所有作業，但會覆寫為任何使用者或專案層級設定。 |

舊版 NuGet 的注意事項：
- NuGet 3.3 和更早版本使用整個方案設定的 `.nuget` 資料夾。 NuGet 3.4+ 中不會使用這個檔案。
- 針對 NuGet 2.6 到 3.x，Windows 上的電腦層級組態檔位於 %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config，其中 *{IDE}* 可以是 *VisualStudio*、*{Version}* 是 Visual Studio 版本 (例如 *14.0*)，而 *{SKU}* 是 *Community*、*Pro* 或 *Enterprise*。 若要將設定移轉至 NuGet 4.0+，只需要將組態檔複製至 %ProgramFiles(x86)%\NuGet\Config。在 Linux 上，前述的這個位置是 /etc/opt，在 Mac 上則是 /Library/Application Support。

## <a name="changing-config-settings"></a>變更組態設定

`NuGet.Config` 檔案是包含索引鍵/值組的簡單 XML 文字檔，如 [NuGet 組態設定](../reference/nuget-config-file.md)主題中所述。

設定是使用 NuGet CLI [config 命令](../tools/cli-ref-config.md)進行管理：
- 預設會變更使用者層級組態檔。
- 若要變更不同檔案中的設定，請使用 `-configFile` 參數。 在此情況下，檔案可以使用任何檔案名稱。
- 索引鍵一定要區分大小寫。
- 需要提高權限，才能在電腦層級設定檔中變更設定。

> [!Warning]
> 雖然您可以在任何文字編輯器中修改檔案，但是如果組態檔包含格式不正確的 XML (標記不成對、引號無效等等)，則 NuGet (v3.4.3 和更新版本) 會以無訊息方式忽略整個組態檔。 這是偏好使用 `nuget config` 來管理設定的原因。

### <a name="setting-a-value"></a>設定值

Windows：

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux：

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> 在 NuGet 3.4 和更新版本中，您可以在任何值中使用環境變數，就像在 `repositoryPath=%PACKAGEHOME%` (Windows) 和 `repositoryPath=$PACKAGEHOME` (Mac/Linux) 中一樣。

### <a name="removing-a-value"></a>移除值

若要移除值，請指定含空值的索引鍵。

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>建立新的組態檔

將下面的範本複製至新的檔案，然後使用 `nuget config -configFile <filename>` 來設定值：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>如何套用設定

多個 `NuGet.Config` 檔案可讓您將設定儲存至不同的位置，使其適用於單一專案、一組專案或所有專案。 這些設定都會共同套用至從命令列或 Visual Studio 叫用的任何 NuGet 作業，並優先使用「最接近」專案或目前資料夾的設定。

具體來說，NuGet 會依下列順序從不同的組態檔載入設定：

1. [NuGetDefaults.Config 檔案](#nuget-defaults-file)，內含只與套件來源相關的設定。
1. 電腦層級檔案。
1. 使用者層級檔案。
1. 使用 `-configFile` 所指定的檔案。
1. 從磁碟機根目錄到目前資料夾 (叫用 nuget.exe 或包含 Visual Studio 專案之資料夾的位置) 之路徑的每個資料夾中找到的檔案。 例如，如果在 c:\A\B\C 中叫用命令，則 NuGet 會依序在 c:\,、c:\A、c:\A\B 和 c:\A\B\C 中尋找並載入組態檔。

NuGet 在這些檔案中找到設定時，會如下套用設定：

1. 針對單一項目的項目，NuGet 已取代相同索引鍵的任何先前找到的值。 這表示「最接近」目前資料夾或專案的設定會覆寫任何其他稍早找到的設定。 例如，如果任何其他組態檔中有 `NuGetDefaults.Config` 中的 `defaultPushSource` 設定，則會予以覆寫。

1. 針對集合項目 (例如 `<packageSources>`)，NuGet 會將所有組態檔中的值結合成單一集合。

1. 指定節點具有 `<clear />` 時，NuGet 會忽略先前針對該節點所定義的組態值。

### <a name="settings-walkthrough"></a>設定逐步解說

假設您在兩個不同的磁碟機上具有下列資料夾結構：

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

則在下列位置中會有四個具有指定內容的 `NuGet.Config` 檔案  (此範例未包含電腦層級檔案，但其行為與使用者層級檔案類似)。

檔案 A。使用者層級檔案 (在 Windows 上為 `%appdata%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.config/NuGet/NuGet.Config`)：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

檔案 B。disk_drive_2/NuGet.Config：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

檔案 C。disk_drive_2/Project1/NuGet.Config：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

檔案 D。disk_drive_2/Project2/NuGet.Config：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet 接著會如下載入並套用設定，視其叫用位置而定：

- **從 disk_drive_1/users 叫用**：只會使用使用者層級組態檔 (A) 中所列的預設存放庫，因為這是 disk_drive_1 上找到的唯一檔案。

- **從 disk_drive_2/ 或 disk_drive_/tmp 叫用**：會先載入使用者層級檔案 (A)，接著 NuGet 會移至 disk_drive_2 的根目錄，並找到檔案 (B)。 NuGet 也會在 /tmp 中尋找組態檔，但會找不到。 因此，會使用 nuget.org 上的預設存放庫、啟用套件還原，並展開 disk_drive_2/tmp 中的套件。

- **從 disk_drive_2/Project1 或 disk_drive_2/Project1/Source 叫用**：會先載入使用者層級檔案 (A)，接著 NuGet 會從 disk_drive_2 的根目錄依序載入檔案 (B) 和檔案 (C)。 (C) 中的設定會覆寫 (B) 和 (A) 中的設定，因此在其中安裝套件的 `repositoryPath` 是 disk_drive_2/Project1/External/Packages，而不是 *disk_drive_2/tmp*。 此外，因為 (C) 會清除 `<packageSources>`，所以 nuget.org 不再是來源，並且只留下 `https://MyPrivateRepo/ES/nuget`。

- **從 disk_drive_2/Project2 或 disk_drive_2/Project2/Source 叫用**：會先載入使用者層級檔案 (A)，接著載入檔案 (B) 和檔案 (D)。 因為未清除 `packageSources`，所以 `nuget.org` 和 `https://MyPrivateRepo/DQ/nuget` 都可以當成來源使用。 套件會在 (B) 中所指定的 disk_drive_2/tmp 內展開。

## <a name="nuget-defaults-file"></a>NuGet 預設檔案

`NuGetDefaults.Config` 檔案的存在是要指定從中安裝和更新套件的套件來源，以及使用 `nuget push` 控制用於發行套件的預設目標。 系統管理員可以輕鬆地 (例如，使用群組原則) 將一致的 `NuGetDefaults.Config` 檔案部署至開發人員並建置電腦，因此可以確保組織中的所有人都會使用正確的套件來源，而非 nuget.org。

> [!Important]
> `NuGetDefaults.Config` 檔案永遠不會導致從開發人員的 NuGet 組織移除套件來源。 這表示，如果開發人員已經使用 NuGet，因此已註冊 nuget.org 套件來源，則在建立 `NuGetDefaults.Config` 檔案之後不會予以移除。
>
> 甚至，`NuGetDefaults.Config` 以及 NuGet 中的任何其他機制都無法防止存取 nuget.org 這類套件來源。如果組織想要封鎖這類存取，必須使用其他方法 (例如防火牆)。

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config 位置

下表描述 `NuGetDefaults.Config` 檔案應儲存的位置，視目標 OS 而定：

| OS 平台  | NuGetDefaults.Config 位置 |
| --- | --- |
| Windows      | **Visual Studio 2017 或 NuGet 4.x+：** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 及更早版本或 NuGet 3.x 及更早版本：** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (一般為 `~/.local/share` 或 `/usr/local/share`，取決於 OS 發行版本)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config 設定

- `packageSources`：此集合的意義與一般組態檔中的 `packageSources` 相同，並指定預設來源。 使用 `packages.config` 管理格式來安裝或更新專案中的套件時，NuGet 會依序使用來源。 對於使用 PackageReference 格式的專案，NuGet 首先使用本機來源，然後使用網路共用的來源，再使用 HTTP 來源，與組態檔中的順序無關。 NuGet 一律會略過還原作業的來源順序。

- `disabledPackageSources`：此集合的意義也與 `NuGet.Config` 檔案相同；其中，會依名稱列出受影響的來源，以及指出是否停用的 true/false 值。 這可讓來源名稱和 URL 保留在 `packageSources` 中，而不需要預設將它開啟。 個別開發人員接著可以將其他 `NuGet.Config` 檔案中來源的值設定為 false 來重新啟用來源，而不需要重新尋找正確的 URL。 這也適用於將組織的完整內部來源 URL 清單提供給開發人員，同時預設僅啟用個別小組的來源。

- `defaultPushSource`：指定 `nuget push` 作業的預設目標，並覆寫內建預設值 nuget.org。因為開發人員特別需要使用 `nuget push -Source` 發行至 nuget.org，所以系統管理員可以部署此設定以避免意外將內部套件發行至公用 nuget.org。

### <a name="example-nugetdefaultsconfig-and-application"></a>NuGetDefaults.Config 範例和應用

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
