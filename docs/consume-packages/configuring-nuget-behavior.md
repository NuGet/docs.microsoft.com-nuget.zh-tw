---
title: 常用的 NuGet 組態
description: NuGet.Config 檔案可全面和根據每個專案來控制 NuGet 行為，並使用 nuget config 命令進行修改。
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901469"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="c2453-103">常用的 NuGet 組態</span><span class="sxs-lookup"><span data-stu-id="c2453-103">Common NuGet configurations</span></span>

<span data-ttu-id="c2453-104">NuGet 行為是透過可存在於專案、使用者和整個電腦層級的一或多個 `NuGet.Config` (XML) 檔案中的累積設定來驅動。</span><span class="sxs-lookup"><span data-stu-id="c2453-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="c2453-105">全域 `NuGetDefaults.Config` 檔案還會特別設定套件來源。</span><span class="sxs-lookup"><span data-stu-id="c2453-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="c2453-106">設定適用於 CLI、套件管理員主控台和套件管理員 UI 中發出的所有命令。</span><span class="sxs-lookup"><span data-stu-id="c2453-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="c2453-107">組態檔位置和使用</span><span class="sxs-lookup"><span data-stu-id="c2453-107">Config file locations and uses</span></span>

| <span data-ttu-id="c2453-108">影響範圍</span><span class="sxs-lookup"><span data-stu-id="c2453-108">Scope</span></span> | <span data-ttu-id="c2453-109">`NuGet.Config` 檔案位置</span><span class="sxs-lookup"><span data-stu-id="c2453-109">`NuGet.Config` file location</span></span> | <span data-ttu-id="c2453-110">描述</span><span class="sxs-lookup"><span data-stu-id="c2453-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2453-111">解決方法</span><span class="sxs-lookup"><span data-stu-id="c2453-111">Solution</span></span> | <span data-ttu-id="c2453-112">目前的資料夾 (也稱為解決方案資料夾) 或最高到磁碟機根目錄的任何資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2453-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="c2453-113">在解決方案資料夾中，設定會套用到子資料夾中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="c2453-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="c2453-114">請注意，若設定檔放在專案資料夾中，它對於該專案沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="c2453-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="c2453-115">User</span><span class="sxs-lookup"><span data-stu-id="c2453-115">User</span></span> | <span data-ttu-id="c2453-116">**Windows：**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="c2453-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="c2453-117">**Mac/Linux：** `~/.config/NuGet/NuGet.Config` 或 `~/.nuget/NuGet/NuGet.Config` (因作業系統散發而異) </span><span class="sxs-lookup"><span data-stu-id="c2453-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="c2453-118">所有平臺都支援其他的支援。</span><span class="sxs-lookup"><span data-stu-id="c2453-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="c2453-119">這些程式無法由工具編輯。</span><span class="sxs-lookup"><span data-stu-id="c2453-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="c2453-120">**Windows：**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="c2453-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="c2453-121">**Mac/Linux：** `~/.config/NuGet/config/*.config` 或 `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="c2453-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="c2453-122">設定適用於所有作業，但會覆寫為任何專案層級設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="c2453-123">電腦</span><span class="sxs-lookup"><span data-stu-id="c2453-123">Computer</span></span> | <span data-ttu-id="c2453-124">**Windows：**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="c2453-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="c2453-125">**Mac/Linux：** `$XDG_DATA_HOME` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="c2453-126">如果 `$XDG_DATA_HOME` 為 Null 或空白，則會使用 `~/.local/share` 或 `/usr/local/share` (依 OS 發行版本而異)</span><span class="sxs-lookup"><span data-stu-id="c2453-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="c2453-127">設定適用於電腦上的所有作業，但會覆寫為任何使用者或專案層級設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="c2453-128">舊版 NuGet 的注意事項：</span><span class="sxs-lookup"><span data-stu-id="c2453-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="c2453-129">NuGet 3.3 和更早版本使用整個方案設定的 `.nuget` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2453-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="c2453-130">此資料夾不會用在 NuGet 3.4 + 中。</span><span class="sxs-lookup"><span data-stu-id="c2453-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="c2453-131">針對 NuGet 2.6 至3.x，Windows 上的電腦層級設定檔案位於 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` ，其中 `{IDE}` 可以是 `VisualStudio` `{Version}` Visual Studio 版本（例如 `14.0` ），而且 `{SKU}` 是 `Community` 、 `Pro` 或 `Enterprise` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config`, where `{IDE}` can be `VisualStudio`, `{Version}` was the Visual Studio version such as `14.0`, and `{SKU}` is either `Community`, `Pro`, or `Enterprise`.</span></span> <span data-ttu-id="c2453-132">若要將設定遷移至 NuGet 4.0 +，只要將配置檔案複製到 `%ProgramFiles(x86)%\NuGet\Config` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-132">To migrate settings to NuGet 4.0+, simply copy the config file to `%ProgramFiles(x86)%\NuGet\Config`.</span></span> <span data-ttu-id="c2453-133">在 Linux 上，這個先前的位置是 `/etc/opt` 和 Mac 上的 `/Library/Application Support` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-133">On Linux, this previous location was `/etc/opt`, and on Mac, `/Library/Application Support`.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="c2453-134">變更組態設定</span><span class="sxs-lookup"><span data-stu-id="c2453-134">Changing config settings</span></span>

<span data-ttu-id="c2453-135">`NuGet.Config` 檔案是包含索引鍵/值組的簡單 XML 文字檔，如 [NuGet 組態設定](../reference/nuget-config-file.md)主題中所述。</span><span class="sxs-lookup"><span data-stu-id="c2453-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="c2453-136">設定是使用 NuGet CLI [config 命令](../reference/cli-reference/cli-ref-config.md)進行管理：</span><span class="sxs-lookup"><span data-stu-id="c2453-136">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="c2453-137">預設會變更使用者層級組態檔。</span><span class="sxs-lookup"><span data-stu-id="c2453-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="c2453-138">若要變更不同檔案中的設定，請使用 `-configFile` 參數。</span><span class="sxs-lookup"><span data-stu-id="c2453-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="c2453-139">在此情況下，檔案可以使用任何檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c2453-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="c2453-140">索引鍵一定要區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="c2453-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="c2453-141">需要提高權限，才能在電腦層級設定檔中變更設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="c2453-142">雖然您可以在任何文字編輯器中修改檔案，但是如果組態檔包含格式不正確的 XML (標記不成對、引號無效等等)，則 NuGet (v3.4.3 和更新版本) 會以無訊息方式忽略整個組態檔。</span><span class="sxs-lookup"><span data-stu-id="c2453-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="c2453-143">這是偏好使用 `nuget config` 來管理設定的原因。</span><span class="sxs-lookup"><span data-stu-id="c2453-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="c2453-144">設定值</span><span class="sxs-lookup"><span data-stu-id="c2453-144">Setting a value</span></span>

<span data-ttu-id="c2453-145">Windows：</span><span class="sxs-lookup"><span data-stu-id="c2453-145">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="c2453-146">Mac/Linux：</span><span class="sxs-lookup"><span data-stu-id="c2453-146">Mac/Linux:</span></span>

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
> <span data-ttu-id="c2453-147">在 NuGet 3.4 和更新版本中，您可以在任何值中使用環境變數，就像在 `repositoryPath=%PACKAGEHOME%` (Windows) 和 `repositoryPath=$PACKAGEHOME` (Mac/Linux) 中一樣。</span><span class="sxs-lookup"><span data-stu-id="c2453-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="c2453-148">移除值</span><span class="sxs-lookup"><span data-stu-id="c2453-148">Removing a value</span></span>

<span data-ttu-id="c2453-149">若要移除值，請指定含空值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="c2453-149">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="c2453-150">建立新的組態檔</span><span class="sxs-lookup"><span data-stu-id="c2453-150">Creating a new config file</span></span>

<span data-ttu-id="c2453-151">將下面的範本複製至新的檔案，然後使用 `nuget config -configFile <filename>` 來設定值：</span><span class="sxs-lookup"><span data-stu-id="c2453-151">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="c2453-152">如何套用設定</span><span class="sxs-lookup"><span data-stu-id="c2453-152">How settings are applied</span></span>

<span data-ttu-id="c2453-153">多個 `NuGet.Config` 檔案可讓您將設定儲存至不同的位置，使其適用於單一專案、一組專案或所有專案。</span><span class="sxs-lookup"><span data-stu-id="c2453-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="c2453-154">這些設定都會共同套用至從命令列或 Visual Studio 叫用的任何 NuGet 作業，並優先使用「最接近」專案或目前資料夾的設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="c2453-155">具體來說，NuGet 會依下列順序從不同的組態檔載入設定：</span><span class="sxs-lookup"><span data-stu-id="c2453-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="c2453-156">檔案[ `NuGetDefaults.Config` ，其中](#nuget-defaults-file)包含僅與套件來源相關的設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-156">The [`NuGetDefaults.Config` file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="c2453-157">電腦層級檔案。</span><span class="sxs-lookup"><span data-stu-id="c2453-157">The computer-level file.</span></span>
1. <span data-ttu-id="c2453-158">使用者層級檔案。</span><span class="sxs-lookup"><span data-stu-id="c2453-158">The user-level file.</span></span>
1. <span data-ttu-id="c2453-159">使用 `-configFile` 所指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="c2453-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="c2453-160">從磁片磁碟機根目錄到目前資料夾的路徑中的每個資料夾中找到的檔案 (的叫用位置， `nuget.exe` 或包含 Visual Studio 專案) 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2453-160">Files found in every folder in the path from the drive root to the current folder (where `nuget.exe` is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="c2453-161">例如，如果在中叫用命令 `c:\A\B\C` ，NuGet 會在中尋找並載入設定檔 `c:\` ，然後再 `c:\A` `c:\A\B` 和最後 `c:\A\B\C` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-161">For example, if a command is invoked in `c:\A\B\C`, NuGet looks for and loads config files in `c:\`, then `c:\A`, then `c:\A\B`, and finally `c:\A\B\C`.</span></span>

<span data-ttu-id="c2453-162">NuGet 在這些檔案中找到設定時，會如下套用設定：</span><span class="sxs-lookup"><span data-stu-id="c2453-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="c2453-163">針對單一項目的項目，NuGet 已取代相同索引鍵的任何先前找到的值。</span><span class="sxs-lookup"><span data-stu-id="c2453-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="c2453-164">這表示「最接近」目前資料夾或專案的設定會覆寫任何其他稍早找到的設定。</span><span class="sxs-lookup"><span data-stu-id="c2453-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="c2453-165">例如，如果任何其他組態檔中有 `NuGetDefaults.Config` 中的 `defaultPushSource` 設定，則會予以覆寫。</span><span class="sxs-lookup"><span data-stu-id="c2453-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>
1. <span data-ttu-id="c2453-166">針對集合項目 (例如 `<packageSources>`)，NuGet 會將所有組態檔中的值結合成單一集合。</span><span class="sxs-lookup"><span data-stu-id="c2453-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>
1. <span data-ttu-id="c2453-167">指定節點具有 `<clear />` 時，NuGet 會忽略先前針對該節點所定義的組態值。</span><span class="sxs-lookup"><span data-stu-id="c2453-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="c2453-168">設定逐步解說</span><span class="sxs-lookup"><span data-stu-id="c2453-168">Settings walkthrough</span></span>

<span data-ttu-id="c2453-169">假設您在兩個不同的磁碟機上具有下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="c2453-169">Let's say you have the following folder structure on two separate drives:</span></span>

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

<span data-ttu-id="c2453-170">則在下列位置中會有四個具有指定內容的 `NuGet.Config` 檔案 </span><span class="sxs-lookup"><span data-stu-id="c2453-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="c2453-171">(此範例未包含電腦層級檔案，但其行為與使用者層級檔案類似)。</span><span class="sxs-lookup"><span data-stu-id="c2453-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="c2453-172">檔案 A。使用者層級檔案 (在 Windows 上為 `%appdata%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.config/NuGet/NuGet.Config`)：</span><span class="sxs-lookup"><span data-stu-id="c2453-172">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="c2453-173">檔案 B `disk_drive_2/NuGet.Config` ：</span><span class="sxs-lookup"><span data-stu-id="c2453-173">File B. `disk_drive_2/NuGet.Config`:</span></span>

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

<span data-ttu-id="c2453-174">File C. `disk_drive_2/Project1/NuGet.Config` ：</span><span class="sxs-lookup"><span data-stu-id="c2453-174">File C. `disk_drive_2/Project1/NuGet.Config`:</span></span>

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

<span data-ttu-id="c2453-175">File D. `disk_drive_2/Project2/NuGet.Config` ：</span><span class="sxs-lookup"><span data-stu-id="c2453-175">File D. `disk_drive_2/Project2/NuGet.Config`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="c2453-176">NuGet 接著會如下載入並套用設定，視其叫用位置而定：</span><span class="sxs-lookup"><span data-stu-id="c2453-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="c2453-177">**從 `disk_drive_1/users`** 叫用：只會使用使用者層級設定檔中所列的預設存放庫 () ，因為這是在上找到的唯一檔案 `disk_drive_1` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-177">**Invoked from `disk_drive_1/users`**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on `disk_drive_1`.</span></span>

- <span data-ttu-id="c2453-178">**從 `disk_drive_2/` 或 `disk_drive_/tmp`** 叫用：先載入 () 的使用者層級檔案，然後將 NuGet 移至的根目錄， `disk_drive_2` 並尋找 (B) 的檔案。</span><span class="sxs-lookup"><span data-stu-id="c2453-178">**Invoked from `disk_drive_2/` or `disk_drive_/tmp`**: The user-level file (A) is loaded first, then NuGet goes to the root of `disk_drive_2` and finds file (B).</span></span> <span data-ttu-id="c2453-179">NuGet 也會尋找中的設定檔， `/tmp` 但是找不到它。</span><span class="sxs-lookup"><span data-stu-id="c2453-179">NuGet also looks for a configuration file in `/tmp` but does not find one.</span></span> <span data-ttu-id="c2453-180">因此，會使用上的預設存放庫 `nuget.org` 、啟用套件還原，並在中展開套件 `disk_drive_2/tmp` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-180">As a result, the default repository on `nuget.org` is used, package restore is enabled, and packages get expanded in `disk_drive_2/tmp`.</span></span>

- <span data-ttu-id="c2453-181">**從 `disk_drive_2/Project1` 或 `disk_drive_2/Project1/Source`** 叫用：先載入) 的使用者層 (級檔案，然後 NuGet 會將檔案從的根目錄 (載入) `disk_drive_2` ，後面接著檔案 (C) 。</span><span class="sxs-lookup"><span data-stu-id="c2453-181">**Invoked from `disk_drive_2/Project1` or `disk_drive_2/Project1/Source`**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of `disk_drive_2`, followed by file (C).</span></span> <span data-ttu-id="c2453-182"> (C) 中的設定會覆寫 (B) 和 () 中的設定，因此 `repositoryPath` 會安裝套件， `disk_drive_2/Project1/External/Packages` 而不是 `disk_drive_2/tmp` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is `disk_drive_2/Project1/External/Packages` instead of `disk_drive_2/tmp`.</span></span> <span data-ttu-id="c2453-183">此外，因為 (C) 會清除 `<packageSources>`，所以 nuget.org 不再是來源，並且只留下 `https://MyPrivateRepo/ES/nuget`。</span><span class="sxs-lookup"><span data-stu-id="c2453-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="c2453-184">**從 `disk_drive_2/Project2` 或 `disk_drive_2/Project2/Source`** 叫用：先載入) 的使用者層 (級檔案，然後再載入 file (B) 和 file (D) 。</span><span class="sxs-lookup"><span data-stu-id="c2453-184">**Invoked from `disk_drive_2/Project2` or `disk_drive_2/Project2/Source`**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="c2453-185">因為未清除 `packageSources`，所以 `nuget.org` 和 `https://MyPrivateRepo/DQ/nuget` 都可以當成來源使用。</span><span class="sxs-lookup"><span data-stu-id="c2453-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="c2453-186">封裝會依照 `disk_drive_2/tmp` (B) 中的指定展開。</span><span class="sxs-lookup"><span data-stu-id="c2453-186">Packages get expanded in `disk_drive_2/tmp` as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="c2453-187">其他使用者範圍設定</span><span class="sxs-lookup"><span data-stu-id="c2453-187">Additional user wide configuration</span></span>

<span data-ttu-id="c2453-188">從5.7 開始，NuGet 已新增對其他使用者範圍設定檔的支援。</span><span class="sxs-lookup"><span data-stu-id="c2453-188">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="c2453-189">這可讓協力廠商在不提高許可權的情況下新增額外的使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="c2453-189">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="c2453-190">這些設定檔可在子資料夾內的 standard user wide configuration 資料夾中找到 `config` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-190">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="c2453-191">以或結尾的所有檔案 `.config` `.Config` 都將視為。</span><span class="sxs-lookup"><span data-stu-id="c2453-191">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="c2453-192">標準工具無法編輯這些檔案。</span><span class="sxs-lookup"><span data-stu-id="c2453-192">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="c2453-193">作業系統平台</span><span class="sxs-lookup"><span data-stu-id="c2453-193">OS Platform</span></span>  | <span data-ttu-id="c2453-194">其他設定</span><span class="sxs-lookup"><span data-stu-id="c2453-194">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="c2453-195">Windows</span><span class="sxs-lookup"><span data-stu-id="c2453-195">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="c2453-196">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c2453-196">Mac/Linux</span></span>    | <span data-ttu-id="c2453-197">`~/.config/NuGet/config/*.config` 或 `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="c2453-197">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="c2453-198">NuGet 預設檔案</span><span class="sxs-lookup"><span data-stu-id="c2453-198">NuGet defaults file</span></span>

<span data-ttu-id="c2453-199">`NuGetDefaults.Config` 檔案的存在是要指定從中安裝和更新套件的套件來源，以及使用 `nuget push` 控制用於發行套件的預設目標。</span><span class="sxs-lookup"><span data-stu-id="c2453-199">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="c2453-200">系統管理員可以輕鬆地 (例如，使用群組原則) 將一致的 `NuGetDefaults.Config` 檔案部署至開發人員並建置電腦，因此可以確保組織中的所有人都會使用正確的套件來源，而非 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c2453-200">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="c2453-201">`NuGetDefaults.Config` 檔案永遠不會導致從開發人員的 NuGet 組織移除套件來源。</span><span class="sxs-lookup"><span data-stu-id="c2453-201">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="c2453-202">這表示，如果開發人員已經使用 NuGet，因此已註冊 nuget.org 套件來源，則在建立 `NuGetDefaults.Config` 檔案之後不會予以移除。</span><span class="sxs-lookup"><span data-stu-id="c2453-202">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="c2453-203">此外， `NuGetDefaults.Config` NuGet 中的或其他任何機制都不會防止存取套件來源，例如 nuget.org。如果組織想要封鎖這類存取，則必須使用其他方法（例如防火牆）。</span><span class="sxs-lookup"><span data-stu-id="c2453-203">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="c2453-204">`NuGetDefaults.Config` 位置</span><span class="sxs-lookup"><span data-stu-id="c2453-204">`NuGetDefaults.Config` location</span></span>

<span data-ttu-id="c2453-205">下表描述 `NuGetDefaults.Config` 檔案應儲存的位置，視目標 OS 而定：</span><span class="sxs-lookup"><span data-stu-id="c2453-205">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="c2453-206">作業系統平台</span><span class="sxs-lookup"><span data-stu-id="c2453-206">OS Platform</span></span>  | <span data-ttu-id="c2453-207">`NuGetDefaults.Config` 位置</span><span class="sxs-lookup"><span data-stu-id="c2453-207">`NuGetDefaults.Config` Location</span></span> |
| --- | --- |
| <span data-ttu-id="c2453-208">Windows</span><span class="sxs-lookup"><span data-stu-id="c2453-208">Windows</span></span>      | <span data-ttu-id="c2453-209">**Visual Studio 2017 或 NuGet 4.x+：** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="c2453-209">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="c2453-210">**Visual Studio 2015 及更早版本或 NuGet 3.x 及更早版本：** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="c2453-210">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="c2453-211">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c2453-211">Mac/Linux</span></span>    | <span data-ttu-id="c2453-212">`$XDG_DATA_HOME` (一般為 `~/.local/share` 或 `/usr/local/share`，取決於 OS 發行版本)</span><span class="sxs-lookup"><span data-stu-id="c2453-212">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="c2453-213">NuGetDefaults.Config 設定</span><span class="sxs-lookup"><span data-stu-id="c2453-213">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="c2453-214">`packageSources`：此集合的意義與一般組態檔中的 `packageSources` 相同，並指定預設來源。</span><span class="sxs-lookup"><span data-stu-id="c2453-214">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="c2453-215">使用 `packages.config` 管理格式來安裝或更新專案中的套件時，NuGet 會依序使用來源。</span><span class="sxs-lookup"><span data-stu-id="c2453-215">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="c2453-216">對於使用 PackageReference 格式的專案，NuGet 首先使用本機來源，然後使用網路共用的來源，再使用 HTTP 來源，與組態檔中的順序無關。</span><span class="sxs-lookup"><span data-stu-id="c2453-216">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="c2453-217">NuGet 一律會略過還原作業的來源順序。</span><span class="sxs-lookup"><span data-stu-id="c2453-217">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="c2453-218">`disabledPackageSources`：此集合的意義與檔案中的意義相同 `NuGet.Config` ，其中每個受影響的來源都會依其名稱列出，並顯示 `true` / `false` 指出是否已停用的值。</span><span class="sxs-lookup"><span data-stu-id="c2453-218">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a `true`/`false` value indicating whether it's disabled.</span></span> <span data-ttu-id="c2453-219">這可讓來源名稱和 URL 保留在 `packageSources` 中，而不需要預設將它開啟。</span><span class="sxs-lookup"><span data-stu-id="c2453-219">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="c2453-220">然後，個別開發人員可以將來源的值設定為其他檔案，以重新啟用來源， `false` `NuGet.Config` 而不需要再次尋找正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="c2453-220">Individual developers can then re-enable the source by setting the source's value to `false` in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="c2453-221">這也適用於將組織的完整內部來源 URL 清單提供給開發人員，同時預設僅啟用個別小組的來源。</span><span class="sxs-lookup"><span data-stu-id="c2453-221">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="c2453-222">`defaultPushSource`：指定作業的預設目標 `nuget push` ，並覆寫的內建預設值 `nuget.org` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-222">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of `nuget.org`.</span></span> <span data-ttu-id="c2453-223">系統管理員可以部署此設定，以避免意外將內部套件發行至公用 `nuget.org` ，因為開發人員必須特別使用 `nuget push -Source` 發行至 `nuget.org` 。</span><span class="sxs-lookup"><span data-stu-id="c2453-223">Administrators can deploy this setting to avoid publishing internal packages to the public `nuget.org` by accident, as developers specifically need to use `nuget push -Source` to publish to `nuget.org`.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="c2453-224">NuGetDefaults.Config 範例和應用</span><span class="sxs-lookup"><span data-stu-id="c2453-224">Example NuGetDefaults.Config and application</span></span>

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
