---
title: 使用 nuget.exe CLI 建立 NuGet 套件
description: 設計和建立 NuGet 套件的詳細指南，包括檔案和版本控制。
author: JonDouglas
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ebaa14325e477c7d864f5c5e88d99f467194e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774712"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>使用 nuget.exe CLI 建立套件

不論套件的功能或所含程式碼為何，您都可以使用其中一個 CLI 工具 (`nuget.exe` 或 `dotnet.exe`) 將該功能封裝至可由任意數目的其他開發人員所共用和使用的元件。 若要安裝 NuGet CLI 工具，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。 請注意，Visual Studio 不會自動包含 CLI 工具。

- 針對非 SDK 樣式的專案 (通常是 .NET Framework 專案)，請依照此文章中所述的步驟建立套件。 如需使用 Visual Studio 與 `nuget.exe` CLI 的逐步指示，請參閱[建立及發佈 .NET Framework 套件](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)。

- 針對使用 [SDK 樣式格式](../resources/check-project-format.md)與任何其他 SDK 樣式專案的 .NET Core 與 .NET Standard 專案，請參閱[使用 dotnet CLI 建立 NuGet 套件](creating-a-package-dotnet-cli.md)。

- 針對從 `packages.config` 移轉至 [PackageReference](../consume-packages/package-references-in-project-files.md) 的專案，請使用 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。

技術上而言，NuGet 套件就只是已重新命名為 `.nupkg` 副檔名且其內容符合特定慣例的 ZIP 檔案。 本主題描述如何建立符合這些慣例之套件的詳細程序。

封裝開始於已編譯的程式碼 (組件)、符號 (和) 您想要以套件形式傳遞的其他檔案 (請參閱[概觀和工作流程](overview-and-workflow.md))。 此流程與編譯或產生進入套件的檔案無關，但您可以擷取專案檔中的資訊保持已編譯的組件與套件同步。

> [!Important]
> 此主題適用於非 SDK 樣式的專案，通常是使用 Visual Studio 2017 及更新版本與 NuGet 4.0+ 的 .NET Core 與 .NET Standard 專案以外的專案。

## <a name="decide-which-assemblies-to-package"></a>決定要封裝的組件

大部分的一般用途套件都會包含其他開發人員可以在其專屬專案中使用的一或多個組件。

- 一般而言，最好一個 NuGet 套件一個組件，前提是每個組件都可以獨立使用。 例如，如果您有與 `Parser.dll` 相依的 `Utilities.dll`，而且 `Parser.dll` 可以單獨使用，則會為每個項目建立一個套件。 這樣做可讓開發人員單獨使用 `Parser.dll` 和 `Utilities.dll`。

- 如果您的程式庫包含多個無法單獨使用的組件，則最好將它們結合成單一套件。 使用上述範例時，如果 `Parser.dll` 所包含的程式碼僅供 `Utilities.dll` 使用，則最好將 `Parser.dll` 放在相同的套件中。

- 同樣地，如果 `Utilities.dll` 與 `Utilities.resources.dll` 相依 (再提醒一次，後者無法單獨使用)，則請將這兩個放在相同的套件中。

資源其實是特殊案例。 將套件安裝至專案時，NuGet 會自動將組件參考新增至套件的 DLL，但「排除」名為 `.resources.dll` 的參考，因為它們假設為當地語系化附屬組件 (請參閱[建立當地語系化套件](creating-localized-packages.md))。 因此，本該含有基本套件程式碼的檔案請避免使用 `.resources.dll`。

如果您的程式庫包含 COM Interop 組件，請遵循[建立包含 COM Interop 組件的套件](author-packages-with-com-interop-assemblies.md)中的其他指導方針。

## <a name="the-role-and-structure-of-the-nuspec-file"></a>.nuspec 檔案的角色和結構

知道您想要封裝的檔案之後，下個步驟就是在 `.nuspec` XML 檔案中建立套件資訊清單。

資訊清單：

1. 描述套件內容而且本身包含在套件中。
1. 驅使建立套件並指示 NuGet 如何將套件安裝至專案。 例如，資訊清單會識別其他套件相依性；因此，安裝主要套件時，NuGet 也可以安裝這些相依性。
1. 包含必要和選擇性屬性，如下所述。 如需確切詳細資料 (包含這裡未提及的其他屬性)，請參閱 [.nuspec 參考](../reference/nuspec.md)。

必要屬性：

- 套件識別碼，其在裝載套件的資源庫內必須是唯一的。
- *Major.Minor.Patch[-Suffix]* 形式的特定版本號碼，其中 *-Suffix* 識別 [發行前版本](prerelease-packages.md)
- 主機上應該會出現套件標題 (例如 nuget.org)
- 作者和擁有者資訊。
- 套件的詳細描述。

常見的選擇性屬性：

- 版本資訊
- 著作權資訊
- [Visual Studio 中的套件管理員 UI](../consume-packages/install-use-packages-visual-studio.md) 的簡短描述
- 地區設定識別碼
- 專案 URL
- 授權為運算式或檔案 (`licenseUrl` 已被取代，請改用[ `license` nuspec 中繼資料元素](../reference/nuspec.md#license)) 
-  (的圖示檔 `iconUrl` 已被取代，請改用[ `icon` nuspec 中繼資料元素](../reference/nuspec.md#icon)) 
- 相依性和參考的清單
- 協助進行資源庫搜尋的標記

下列一般 (但虛構的) `.nuspec` 檔案具有可描述屬性的註解：

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
        <file src="icon.png" target="" />
    </files>
</package>
```

如需宣告相依性及指定版本號碼的詳細資料，請參閱 [packages.config](../reference/packages-config.md) 和[套件版本控制](../concepts/package-versioning.md)。 在 `dependency` 項目上使用 `include` 和 `exclude` 屬性，也可以將相依性中的資產直接用於套件中。 請參閱 [.nu-/spec 參考 - 相依性](../reference/nuspec.md#dependencies)。

因為資訊清單會包含在透過它所建立的套件中，所以檢查現有套件就可以找到任意數目的其他範例。 不錯的來源是您電腦上的 *global-packages* 資料夾，即下列命令所傳回的位置：

```cli
nuget locals -list global-packages
```

移至任何 *package\version* 資料夾，並將 `.nupkg` 檔案複製至 `.zip` 檔案，然後開啟該 `.zip` 檔案，並檢查其內的 `.nuspec`。

> [!Note]
> 從 Visual Studio 專案建立 `.nuspec` 時，資訊清單會包含建置套件時取代為專案中資訊的權杖。 請參閱[從 Visual Studio 專案建立 .nuspec](#from-a-visual-studio-project)。

## <a name="create-the-nuspec-file"></a>建立 .nuspec 檔案

建立完整資訊清單一般是從透過下列其中一種方法所產生的基本 `.nuspec` 檔案開始：

- [以慣例為基礎的工作目錄](#from-a-convention-based-working-directory)
- [組件 DLL](#from-an-assembly-dll)
- [Visual Studio 專案](#from-a-visual-studio-project)    
- [含預設值的新檔案](#new-file-with-default-values)

您接著手動編輯檔案，讓它描述您在最終套件中想要的確切內容。

> [!Important]
> 產生的 `.nuspec` 檔案會包含在使用 `nuget pack` 命令建立套件之前必須修改的預留位置。 如果 `.nuspec` 包含任何預留位置，則該命令會失敗。

### <a name="from-a-convention-based-working-directory"></a>從以慣例為基礎的工作目錄

因為 NuGet 套件只是使用 `.nupkg` 副檔名重新命名的 ZIP 檔案，所以通常很容易即可在本機檔系統上，建立所需的資料夾結構，然後直接從該結構建立 `.nuspec` 檔案。 `nuget pack` 命令接著會自動在該資料夾結構中新增所有檔案 (不包含任何以 `.` 開頭的資料夾，供您以相同的結構保留私人檔案)。

這種方法的優點是您不需要在資訊清單中指定想要包含在套件中的檔案 (如本主題中稍後所述)。 您可以只讓建置程序產生套件中完全相同的資料夾結構，而且可以輕鬆地包含可能不屬於專案的其他檔案：

- 應該插入至目標專案的內容和原始程式碼。
- PowerShell 指令碼
- 專案中現有組態檔和原始程式碼檔案的轉換。

資料夾慣例如下：

| 資料夾 | 描述 | 套件安裝時的動作 |
| --- | --- | --- |
| (root) | readme.txt 的位置 | 安裝套件時，Visual Studio 會顯示套件根目錄中的 readme.txt 檔案。 |
| lib/{tfm} | 所指定目標架構 Moniker (TFM) 的組件 (`.dll`)、文件 (`.xml`) 和符號 (`.pdb`) 檔案 | 組件會新增為編譯與執行階段的參考；`.xml` 與 `.pdb` 則會複製到專案資料夾。 請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)，以了解如何建立架構目標特定子資料夾。 |
| ref/{tfm} | 所指定目標 Framework Moniker (TFM) 的組件 (`.dll`) 與符號 (`.pdb`) 檔案 | 組件只會針對編譯階段新增為參考；因此不會有任何項目被複製到專案 bin 資料夾。 |
| runtimes | 架構特定組件 (`.dll`)、符號 (`.pdb`) 和原生資源 (`.pri`) 檔案 | 組件只會針對執行階段新增為參考；其他檔案則會複製至專案資料夾。 `/ref/{tfm}` 資料夾下一律必須有對應的 (TFM) `AnyCPU` 特定組件，才能提供對應的編譯階段組件。 請參閱[支援多個目標架構](supporting-multiple-target-frameworks.md)。 |
| 內容 | 任意檔案 | 內容會複製至專案根目錄。 請將 **content** 資料夾視為最後使用套件的目標應用程式的根目錄。 若要讓套件在應用程式的 */images* 資料夾中新增映像，請將它放在套件的 *content/images* 資料夾中。 |
| build | *(3.x+)* MSBuild `.targets` 與 `.props` 檔案 | 自動插入到專案中。 |
| buildMultiTargeting | 用於跨架構目標的 *(4.0+)* MSBuild `.targets` 與 `.props` 檔案 | 自動插入到專案中。 |
| buildTransitive | *(5.0+)* 可傳遞至任何取用專案的 MSBuild `.targets` 與 `.props` 檔案。 請參閱[功能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)頁面 \(英文\)。 | 自動插入到專案中。 |
| tools | 可從套件管理員主控台存取的 Powershell 指令碼和程式 | `tools` 資料夾只會新增至套件管理員主控台的 `PATH` 環境變數 (具體而言，建置專案時 *「不」* 會新增至針對 MSBuild 所設定的 `PATH`)。 |

因為您的資料夾結構可包含任意數目之目標架構的任意數目組件，所以建立可支援多重架構的套件時，需要使用此種方法。

在任何情況下，您擁有所要的資料夾結構之後，請在該資料夾中執行下列命令來建立 `.nuspec` 檔案：

```cli
nuget spec
```

同樣地，產生的 `.nuspec` 不會包含資料夾結構中檔案的明確參考。 建立套件時，NuGet 會自動包含所有檔案。 不過，您仍然需要編輯資訊清單之其他部分中的預留位置值。

### <a name="from-an-assembly-dll"></a>從組件 DLL

在從組件建立套件的簡單案例中，您可以使用下列命令，透過組件的中繼資料產生 `.nuspec` 檔案：

```cli
nuget spec <assembly-name>.dll
```

使用這種形式會將資訊清單中的少數預留位置取代為組件中的特定值。 例如，`<id>` 屬性設定為組件名稱，而且 `<version>` 設定為組件版本。 不過，資訊清單中的其他屬性在組件中沒有相符值，因此仍然會包含預留位置。

### <a name="from-a-visual-studio-project"></a>從 Visual Studio 專案

從 `.csproj` 或 `.vbproj` 檔案建立 `.nuspec` 十分方便，因為已安裝至這些專案的其他套件會自動參照為相依性。 只需要在與專案檔相同的資料夾中使用下列命令：

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

產生的 `<project-name>.nuspec` 檔案包含「權杖」，而權杖會在封裝時取代為專案中的值，包含已安裝之任何其他套件的參考。

如果您有要包含在 *.nuspec* 中的套件相依性，請改為使用 `nuget pack` 並從產生的 *.nupkg* 檔案內取得 *.nuspec* 檔案。 例如，使用下列命令。

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

在專案屬性的兩側，使用 `$` 符號分隔權杖。 例如，透過此方式產生之資訊清單中的 `<id>` 值一般會顯示如下：

```xml
<id>$id$</id>
```

在封裝時間，會將此權杖取代為專案檔中的 `AssemblyName` 值。 若要將專案值完全對應至 `.nuspec` 權杖，請參閱[取代權杖參考](../reference/nuspec.md#replacement-tokens)。

更新專案時，權杖可讓您不需要更新 `.nuspec` 中這類版本號碼的重要值  (如有需要，您一律可以將權杖取代為常值)。 

請注意，從 Visual Studio 專案工作時，有數個其他封裝選項可用，如後面的[執行 nuget pack 以產生 .nupkg 檔案](#run-nuget-pack-to-generate-the-nupkg-file)所述。

#### <a name="solution-level-packages"></a>方案層級套件

*僅限 NuGet 2.x。無法在 NuGet 3.0 + 中使用。*

NuGet 2.x 支援可安裝套件管理員主控台工具或其他命令的方案層級套件概念 (`tools` 資料夾內容)，但不會將參考、內容或組建自訂新增至方案中的任何專案。 這類套件在其直接 `lib`、`content` 或 `build` 資料夾中未包含任何檔案，而其相依性在各自的 `lib`、`content` 或 `build` 資料夾中沒有檔案。

NuGet 會追蹤 `.nuget` 資料夾的 `packages.config` 檔案中的已安裝方案層級套件，而不是專案的 `packages.config` 檔案。

### <a name="new-file-with-default-values"></a>含預設值的新檔案

下列命令會建立含預留位置的預設資訊清單，確保您是從正確的檔案結構開始：

```cli
nuget spec [<package-name>]
```

如果您省略 \<package-name\> ，則產生的檔案 `Package.nuspec` 為。 如果您提供 `Contoso.Utility.UsefulStuff` 這類名稱，則檔案是 `Contoso.Utility.UsefulStuff.nuspec`。

產生的 `.nuspec` 包含 `projectUrl` 這類值的預留位置。 請務必先編輯檔案，再用它來建立最終 `.nupkg` 檔案。

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>選擇唯一的套件識別碼並設定版本號碼

套件識別碼 (`<id>` 項目) 和版本號碼 (`<version>` 項目) 是資訊清單中的兩個最重要值，因為它們可以唯一識別套件中所含的確切程式碼。

**套件識別碼的最佳做法：**

- **唯一性**：在 nuget.org 內，或只要資源庫裝載套件時，識別碼就必須是唯一的。 決定識別碼之前，請搜尋適用的資源庫，檢查是否已在使用名稱。 若要避免衝突，不錯的模式是使用您的公司名稱作為識別碼的第一個部分，例如 `Contoso.`。
- **命名空間類似名稱**：遵循與 .NET 中命名空間類似的模式，即使用點標記法，而非連字號。 例如，使用 `Contoso.Utility.UsefulStuff`，而非 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。 套件識別碼符合程式碼中所使用的命名空間時，取用者也會發現它十分有用。
- **範例套件**：如果您產生的範例程式碼套件示範如何使用另一個套件，請將 `.Sample` 附加為識別碼的尾碼，如 `Contoso.Utility.UsefulStuff.Sample` 所示   (範例套件當然會相依于另一個套件。建立範例套件時，請 ) 使用稍早所述的慣例型工作目錄方法。 在 `content` 資料夾中，於稱為 `\Samples\<identifier>` 的資料夾中排列範例程式碼，而這與 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相同。

**套件版本的最佳做法：**

- 一般而言，請設定套件版本，使其符合程式庫，但這不是絕對必要。 將套件限制為單一組件時，這相當簡單，如[決定要封裝的組件](#decide-which-assemblies-to-package)稍早所述。 整體來說，請記住，解析相依性時，NuGet 本身會處理套件版本，而非組件版本。
- 使用非標準版本方式時，請務必考慮使用 NuGet 版本控制規則，如[套件版本控制](../concepts/package-versioning.md)中所述。

> 下面一系列的簡短部落格文章也有助於了解版本控制：
>
> - [第 1 部分：接受 DLL 挑戰](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部分：核心演算法](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部分：透過繫結重新導向的統一](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>新增讀我檔案和其他檔案

若要直接指定要包含在套件中的檔案，請在 `.nuspec` 檔案中使用 `<files>` 節點，而這在 `<metadata>` 標記「後面」：

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> 使用以慣例為基礎的工作目錄方法時，您可以將 readme.txt 放在套件根目錄中，而將其他內容放在 `content` 資料夾中。 資訊清單中不需要任何 `<file>` 項目。

當您在套件根目錄中包含名為 `readme.txt` 的檔案時，Visual Studio 會在直接安裝套件之後立即以純文字形式顯示該檔案的內容  (不會針對安裝為相依性的套件顯示讀我檔案)。 例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：

![安裝時 NuGet 套件的讀我檔案顯示](media/Create_01-ShowReadme.png)

> [!Note]
> 如果您在 `.nuspec` 檔案中包含空 `<files>` 節點，則 NuGet 不會包含不在 `lib` 資料夾套件中的任何其他內容。

## <a name="include-msbuild-props-and-targets-in-a-package"></a>在套件中包含 MSBuild 屬性和目標

在某些情況下，您可能想要在取用您套件的專案中新增自訂組建目標或屬性，例如在建置期間執行自訂工具或程序。 做法是在專案的 `\build` 資料夾內以 `<package_id>.targets` 或 `<package_id>.props` 形式放置檔案 (例如 `Contoso.Utility.UsefulStuff.targets`)。

根 `\build` 資料夾中的檔案視為適合所有目標架構。 若要提供架構專屬的檔案，請先將其置於適當的子資料夾中，如下所示：

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

接著，在 `.nuspec` 檔案中，請務必於 `<files>` 節點中參照這些檔案：

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

[NuGet 2.5 引進了](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)在套件中包含 MSBuild pros 和 targets 的做法，因此建議您將 `minClientVersion="2.5"` 屬性新增到 `metadata` 元素，以指出使用套件所需的最低 NuGet 用戶端版本。

當 NuGet 安裝含有 `\build` 檔案的套件時，會在指向 `.targets` 和 `.props` 檔案的專案檔中新增 MSBuild `<Import>` 項目。  (`.props` 會新增至專案檔頂端， `.targets` 並新增至底部。 ) 為 `<Import>` 每個目標 framework 新增個別的條件式 MSBuild 元素。

用於跨框架目標的 MSBuild `.props` 和 `.targets` 檔案可以放在 `\buildMultiTargeting` 資料夾中。 在套件安裝期間，NuGet 會將對應的 `<Import>` 元素新增到有條件的專案檔中，即未設定目標框架 (MSBuild 屬性 `$(TargetFramework)` 必須是空的)。

使用 NuGet 3.x 時，目標不會新增至專案，但會透過 `{projectName}.nuget.g.targets` 與 `{projectName}.nuget.g.props` 提供。

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>執行 nuget pack 以產生 .nupkg 檔案

使用組件或以慣例為基礎的工作目錄時，搭配執行 `nuget pack` 與 `.nuspec` 檔案，並將 `<project-name>` 取代為特定檔案名稱，以建立套件：

```cli
nuget pack <project-name>.nuspec
```

使用 Visual Studio 專案時，請搭配執行 `nuget pack` 與專案檔，這樣會自動載入專案的 `.nuspec` 檔案，並使用專案檔中的值來取代其內的任何權杖：

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> 因為專案是權杖值的來源，所以需要直接使用專案檔來進行權杖取代。 如果您搭配使用 `nuget pack` 與 `.nuspec` 檔案，則不會進行權杖取代。

在所有情況下，`nuget pack` 都會排除開頭為句點的資料夾；例如 `.git` 或 `.hg`。

NuGet 指出 `.nuspec` 檔案中是否有任何需要修正的錯誤；例如，忘記變更資訊清單中的預留位置值。

`nuget pack` 成功之後，您會有可發行至適合資源庫的 `.nupkg` 檔案，如[發行套件](../nuget-org/publish-a-package.md)中所述。

> [!Tip]
> 套件在建立後對其檢查的有用方式是在[套件總管](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具中開啟它。 這可提供套件內容和其資訊清單的圖形化檢視。 您也可以將所產生的 `.nupkg` 檔案重新命名為 `.zip` 檔案，並直接探索其內容。

### <a name="additional-options"></a>其他選項

您可以搭配使用各種命令列參數與 `nuget pack` 來排除檔案、覆寫資訊清單中的版本號碼、變更輸出資料夾，以及其他功能。 如需完整清單，請參閱 [pack 命令參考](../reference/cli-reference/cli-ref-pack.md)。

下列選項是 Visual Studio 專案通用的幾個選項：

- **參考的專案**：如果專案參考其他專案，則您可以使用 `-IncludeReferencedProjects` 選項，將參考的專案新增為套件的一部分或相依性：

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    這個包含程序是遞迴式，因此，如果 `MyProject.csproj` 參考專案 B 和 C，然後這些專案參考 D、E 和 F，則套件中會包含 B、C、D、E 和 F 中的檔案。

    如果參考的專案包含專屬 `.nuspec` 檔案，則 NuGet 會改為將該參考的專案新增為相依性。  您需要個別封裝和發行該專案。

- **組建組態**：NuGet 預設會使用專案檔中所設定的預設組建組態，通常是「偵錯」。 若要從不同組建組態來封裝檔案 (例如「發行」)，請搭配使用 `-properties` 選項與下列組態：

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **符號**：若要包含可讓取用者在偵錯工具中逐步執行您套件程式碼的符號，請使用 `-Symbols` 選項：

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>測試套件安裝

發行套件之前，您通常會想要測試將套件安裝至專案的程序。 測試可確定必要檔案最後都在專案的正確位置。

您可以使用一般[套件安裝步驟](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)，以在 Visual Studio 中或命令列上手動測試安裝。

自動化測試的基本程序如下：

1. 將 `.nupkg` 檔案複製至本機資料夾。
1. 使用 `nuget sources add -name <name> -source <path>` 命令，將資料夾新增至套件來源 (請參閱 [nuget sources](../reference/cli-reference/cli-ref-sources.md))。 請注意，您只需要在任何指定電腦上設定此本機來源一次。
1. 使用 `nuget install <packageID> -source <name>` 以從該來源安裝套件，其中 `<name>` 符合您指定至 `nuget sources` 的來源名稱。 指定來源可確保單獨從該來源安裝套件。
1. 檢查您的檔案系統，確認已正確安裝檔案。

## <a name="next-steps"></a>後續步驟

建立套件 (即 `.nupkg` 檔案) 之後，即可將它發行至您選擇的資源庫，如[發行套件](../nuget-org/publish-a-package.md)中所述。

您也可能想要擴充您套件的功能，或支援其他案例，如下列各主題中所述：

- [套件版本控制](../concepts/package-versioning.md)
- [支援多個目標 Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [原始程式檔和組態檔的轉換](../create-packages/source-and-config-file-transformations.md)
- [當地語系化](../create-packages/creating-localized-packages.md)
- [發行前版本](../create-packages/prerelease-packages.md)
- [設定套件類型](../create-packages/set-package-type.md)
- [建立包含 COM Interop 組件的套件](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後，請注意其他套件類型：

- [原生封裝](../guides/native-packages.md)
- [符號套件](../create-packages/symbol-packages-snupkg.md)
