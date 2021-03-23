---
title: 封裝撰寫的最佳作法
description: 建立高品質 NuGet 套件的最佳作法一般指南。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859066"
---
# <a name="package-authoring-best-practices"></a>封裝撰寫的最佳作法

本指南的目的是要為 NuGet 套件作者提供建立和發佈高品質套件的輕量參考。 它主要會著重于封裝特定的最佳作法，例如中繼資料和封裝。 如需建立高品質程式庫的更深入建議，請參閱 .NET [開放原始碼程式庫指引](https://docs.microsoft.com/dotnet/standard/library-guidance/)。

## <a name="types-of-recommendations"></a>建議類型

每篇文章都呈現四種類型的建議：**優先**、**考慮**、**避免** 與 **禁止**。 建議的類型指出應遵循的程度。

您應該一律遵循 **優先** 類型的建議。 例如：

✔️包含描述其用途之套件的簡短描述。

相反地，請 **考慮** 建議一般遵循建議，但規則有合法的例外狀況：

✔️ 請考慮選擇具有符合 NuGet 的前置詞保留[準則](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)之前置詞的 NuGet 套件名稱。

**避免** 建議指的是通常不建議採行的建議，但有時違反規則尚屬合理情況：

❌ 避免需要精確版本的 NuGet 套件參考。

最後，**禁止** 類型的建議表示在多數情況下都不應採取的動作：

❌ 請勿使用 `LicenseUrl` 中繼資料屬性。

## <a name="create-a-nuget-package"></a>建立 NuGet 套件

建立 NuGet 套件的最新建議方法是從 [SDK 樣式專案](https://docs.microsoft.com/nuget/resources/check-project-format)。 SDK 樣式的專案屬性（包括 [目標 framework](https://docs.microsoft.com/dotnet/standard/frameworks) 和 [套件中繼資料](#package-metadata)）是在 [專案](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)檔中定義。

在 [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) 或 [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)中定義必要的屬性和封裝，以從您的 SDK 樣式專案建立套件。

✔️確實會建立 SDK 樣式的專案，並使用 Visual Studio 或 dotnet CLI) 套件建立 (套件。

如需有關套件建立的詳細指引，包括必要的用戶端工具、專案檔範例和命令，請參閱 [使用 DOTNET CLI 建立 NuGet 套件](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)。

若要協助決定要作為目標的 .NET framework，請參閱我們 [的跨平臺目標的最新指導](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting)方針。

## <a name="package-metadata"></a>套件中繼資料

中繼資料是任何 NuGet 套件的基礎元件。 您的中繼資料品質可能會大幅影響套件的可探索性、可用性和可信度。

在 Visual Studio 中，指定套件中繼資料的建議方式是將專案 > [專案名稱] 屬性 > 封裝中。

您也可以 [直接在專案檔中指定](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties)封裝中繼資料元素。

以下是資料表對應和描述可用的封裝中繼資料元素：

| Visual Studio 屬性名稱                   | [專案檔/MSBuild 屬性名稱](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nuspec 屬性名稱](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | 描述                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | 封裝名稱或識別碼。                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | NuGet 套件版本。                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | 以逗號分隔的套件作者清單，通常使用個人或組織的「美觀名稱」。                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | 套件的描述。                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | 套件的著作權詳細資料。                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | SPDX 授權運算式。       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | 自訂授權檔案的路徑。                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | 專案首頁的 URL。                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | 封裝圖示影像檔案的路徑。                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | 用來建立封裝之來源存放庫的 URL。                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | 存放庫 URL 指向 (也就是 "git" ) 的存放庫類型。                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | 以空格分隔的標記與關鍵字清單，能描述套件。 標記會在搜尋套件時使用。 |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | 這一版封裝中所做變更的描述。                                                 |

### <a name="package-id"></a>封裝識別碼

如果您要發佈全新的封裝：

✔️選擇的套件識別碼是唯一的，而且與 NuGet.org 上現有的套件清楚區別。
> 您可以藉由在 NuGet.org 上搜尋識別碼，或檢查下列連結是否存在來檢查封裝識別碼是否唯一和 differentiable： https://www.nuget.org/packages/<package name \> 。

✔️考慮選擇具有符合 NuGet [首碼保留準則](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)之前置詞的 nuget 套件名稱。
> 保留套件的前置詞識別碼，可讓您取得已驗證的核取記號： ![ 影像](media/Verified-check-mark.png)
> 
> 若要深入瞭解，請參閱 [套件識別碼前置詞保留檔](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) 。

### <a name="package-version"></a>封裝版本

✔️考慮使用 [SemVer](https://semver.org/) 來為您的 NuGet 套件版本。
> 基本上，這表示使用主要的. Patch [-搶鮮版（發行前版本）格式。

如果封裝不穩定或處於預覽狀態，✔️會將套件發佈為 [發行前版本的套件](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) 。

如需更先進的指引，請參閱 [.net 程式庫版本設定指南](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) 。

### <a name="authors"></a>Authors

✔️請將 [作者] 欄位用於您或您組織的「美觀名稱」。
> 例如，如果我的 NuGet.org 使用者名稱是 "jdoe"，則針對作者欄位使用 "Jane Doe" 可協助取用者將我辨識為作者。 如果我組織的 NuGet.org 使用者名稱是 "ContosoToolkit"，則使用 "Contoso Corporation" 可能更容易辨識，並可激發更多消費者信任。
### <a name="description"></a>描述

✔️包含 (最多4000個字元) 描述套件的簡短描述。
> 套件描述是 NuGet 搜尋中最重要的其中一個欄位，可能是潛在客戶的第一件事，就是判斷套件是否適合它們。

### <a name="copyright"></a>著作權

✔️考慮使用 "著作權 (c) <姓名/公司 <年份）來 copyrighting 您的套件 \> \> 。
>著作權注意事項基本上表示無法在沒有您的許可權的情況下複製您的工作。 您可以輕鬆地在套件中包含著作權聲明，而不會造成任何損害！

範例：著作權 (c) Contoso 2020

### <a name="licensing"></a>授權

✔️ [在您的封裝中包含授權運算式或授權檔案](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> [!IMPORTANT]
> 沒有授權的專案預設為 [專有著作權](https://choosealicense.com/no-permission/)，表示您尚未授與任何人使用您專案的許可權。

❌ 請勿使用已被取代的 `LicenseUrl` 中繼資料屬性。
> 如此一來，當 URL 的授權變更追溯變更先前套件版本的顯示授權時，就會發生法律上的混淆。

#### <a name="if-your-package-is-open-source"></a>如果您的套件是[開放原始](https://opensource.org/osd)碼

✔️ [選擇開放原始碼授權](https://choosealicense.com/) 以使套件成為開放原始碼。
> *「開放原始碼授權是符合開放原始碼定義的授權-簡單來說，這些授權可讓軟體自由使用、修改及共用。」* -開放原始碼計畫。 若要深入瞭解開放原始碼軟體和開放原始碼的計畫，請參閱 https://opensource.org/ 。

✔️考慮 [將授權運算式包含在您的封裝中](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> 如果授權運算式可以使用您的套件，或如果授權已變更，則會以更清楚的方式呈現授權運算式，並讓取用者更清楚。 
> [!Note]
> NuGet.org 只接受開放原始碼計畫或免費 Software Foundation 核准之授權的授權運算式。

#### <a name="if-your-package-is-not-open-source"></a>如果您的套件不是開放原始碼

✔️ [包含套件中的授權檔案](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> 任何 ( .txt 或 md) 的授權檔都可以新增至您的封裝，包括非標準授權。 

### <a name="project-url"></a>專案 URL

✔️考慮包含關聯專案、存放庫或公司網站的連結。
> 您的專案網站應該有使用者需要知道的套件，而且可能是使用者尋找檔的位置。

### <a name="icon"></a>圖示

✔️考慮 [包含套件的圖示](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) ，以協助以視覺化方式區分。 它是相對較小的加法，可改善對封裝品質的認知。
> 圖示可以特定于個別套件，也可以是品牌標誌。

✔️使用128x128 的影像，並具有透明背景 (PNG) ，以獲得最佳的觀看結果。
> NuGet 會自動將您的映射調整為顯示的用戶端。

❌ 請勿使用已被取代的 `IconUrl` 中繼資料屬性。

### <a name="repository-type-and-url"></a>存放庫類型和 URL

✔️考慮設定 [來源連結](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) ，以自動將原始檔控制中繼資料新增至您的 NuGet 套件，並讓您的程式庫更容易進行偵錯工具。
> 來源連結會自動將 `Repository URL` 和新增 `Repository Type` 至套件中繼資料。 它也會新增與套件版本相關聯的特定認可。

### <a name="tags"></a>標籤

✔️包含多個標記，其中包含與您的套件相關的重要詞彙，以增強可探索性。
> 標籤會以 Nuget.exe 的搜尋演算法來考慮，對於不在封裝識別碼中但相關的詞彙特別有用。

例如，如果我發佈了封裝以將字串記錄到主控台，就會包含：「記錄、記錄、主控台、字串、輸出」

### <a name="release-notes"></a>版本資訊

✔️考慮包含版本資訊，其中每個更新都會描述所做的變更。
> 雖然版本資訊不需要特定格式，但建議您包括：
>
> 1. 重大變更
> 2. 新功能
> 3. 錯誤修正
> 
> 如果您已經在存放庫中追蹤版本資訊或變更記錄，也可以包含相關檔案的連結。

## <a name="related-topics"></a>相關主題

- [建立及發行套件 (dotnet CLI)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [建立及發行套件 (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
