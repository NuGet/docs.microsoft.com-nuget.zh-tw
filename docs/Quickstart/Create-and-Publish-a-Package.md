---
title: "建立和發行 NuGet 套件的入門指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "逐步解說教學課程，說明使用 nuget.exe 命令列介面和 Visual Studio 建立和發行 NuGet 套件。"
keywords: "NuGet 套件建立, NuGet 套件發行, NuGet 教學課程"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ab5235537d869047075b93f9d8255ae9e61dfedd
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="create-and-publish-a-package"></a>建立及發行套件

從 .NET 類別庫建立 NuGet 套件，並將它發行到 nuget.org 是個簡單的程序。下列步驟會引導您完成使用 NuGet 命令列介面 (CLI) 和 Visual Studio 的程序：

- [必要條件](#install-pre-requisites)
- [建立 .nuspec 套件資訊清單檔](#create-the-nuspec-package-manifest-file)
- [執行 pack 命令](#run-the-pack-command)
- [發行套件](#publish-the-package)

## <a name="pre-requisites"></a>必要條件

1. 從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017。

1. 從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版 `nuget.exe`，並將 `.exe` 儲存到您 PATH 中的位置，以安裝 NuGet CLI 工具 `nuget.exe`。 請注意，下載「是」工具本身，而非安裝程式。

1. 為您想要封裝的程式碼建立適當的 .NET 類別庫專案。 如果您還沒有專案，您可以建立一個簡單的專案，如下所示：
    1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點、選取 [類別庫] 範本、將專案命名為 AppLogger，然後按一下 [確定]。
    1. 在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置] 以確定已適當建立專案。 DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。

    當然，在真實的 NuGet 套件中，您將實作其他人可以用來建置應用程式的許多實用功能。 不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。

## <a name="create-the-nuspec-package-manifest-file"></a>建立 .nuspec 套件資訊清單檔

每個 NuGet 套件需要資訊清單&mdash;`.nuspec` 檔案&mdash;來描述其內容和其相依性。 `nuget spec` 命令會為您建立此檔案，然後您可以自訂。 在此範例中，您從專案檔建立 `.nuspec`，您也可以透過其他方式建立資訊清單，如[建立套件](../create-packages/creating-a-package.md)中所述。

1. 開啟命令提示字元並巡覽至包含您專案檔的資料夾 (`.csproj`)。

1. 執行 NuGet CLI `spec` 命令以產生資訊清單，它會以您的專案來命名，例如 `AppLogger.nuspec`：

    ```
    nuget spec
    ```

1. 在文字編輯器中開啟檔案。 資訊清單看起來類似下列程式碼，其中 `<token>` 格式的權杖 (例如 `$id$`) 會在封裝程序期間取代為來自專案 Properties/AssemblyInfo.cs 檔案的值。 如需語彙基元的詳細資料，請參閱[建立 .nuspec 檔案](../create-packages/creating-a-package.md#creating-the-nuspec-file)。

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. 選取在 nuget.org 中唯一的套件識別碼。我們建議使用[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中描述的命名慣例。 請務必更新作者和描述標記，否則您會在下一個步驟中收到錯誤。 以下是更新的 `.nuspec` 檔案範例：

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 針對公眾使用而建置的套件，請特別注意 `<tags>` 項目，因為這些標籤可協助其他人找到您的套件，並了解其用途。

## <a name="run-the-pack-command"></a>執行 pack 命令

若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `pack` 命令：

```
nuget pack AppLogger.csproj
```

此命令會使用來自 `.nuspec` 檔案的套件名稱和版本號碼，建立 `AppLogger.1.0.0.0.nupkg`。 如果您尚未更新 `.nuspec` 檔案中各種欄位的預設值，此命令會發出警告。

## <a name="publish-the-package"></a>發行套件

一旦您有 `.nupkg` 檔案，請使用 `push` 命令將它發行到 nuget.org。 (或者，您可以使用 [nuget.org 發行工作流程](../create-packages/publish-a-package.md#publish-to-nugetorg)。

> [!Warning]
> 您發行至 nuget.org 的套件可以讓其他開發人員公開看見。 若要私下裝載套件，請參閱[裝載套件](../hosting-packages/overview.md)。

1. 在 [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) 上建立免費帳戶，如果您已有帳戶則請登入。 建立新的帳戶會傳送一封確認電子郵件。 您必須確認帳戶，才可以上傳套件。

1. 登入之後，選取您的使用者名稱 (在右上方)，然後選取 [API 金鑰]。

1. 選取 [建立]、提供您的金鑰名稱、選取 [API 金鑰] 下的 [選取範圍] > [推送]針對 [Glob 模式] 輸入 *，然後選取 [建立]。

1. 建立金鑰之後，選取 [複製] 以擷取 CLI 中您需要的存取金鑰：

    ![將 API 金鑰複製到剪貼簿](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > 將您的金鑰儲存在安全的位置，並保守祕密。 如果意外洩漏您的金鑰，您一律可以隨時重新產生它。 如果您不再想要透過 CLI 推送套件，也可以移除 API 金鑰。

1. 在命令提示字元中執行下列命令，指定套件名稱並將金鑰取代為在步驟 4 中複製的值：

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe 顯示發行程序的結果：

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. 從您在 nuget.org 上的設定檔，選取 [管理套件] 以查看您剛發行的套件。 您也會收到確認電子郵件。 請注意，可能需要一些時間才會編製套件的索引，並顯示在其他人可以找到它的搜尋結果中。 在這段期間，套件頁面會顯示下列訊息：

    ![此套件尚未編製索引。 編製索引完成後，它會出現在搜尋結果中，並且可供安裝/還原。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **病毒掃描**：會掃描所有上傳至 nuget.org 的套件是否有病毒，並在發現任何病毒時予以拒絕。 也會定期掃描 nuget.org 上列出的所有套件。

就是這麼容易！ 您剛已將第一個 NuGet 套件發行至 [nuget.org](https://www.nuget.org/)，其他開發人員可以在他們自己的專案中使用它。

## <a name="related-topics"></a>相關主題

- [建立套件](../create-packages/creating-a-package.md)
- [發行套件](../create-packages/publish-a-package.md)
- [支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)
- [套件版本控制](../reference/package-versioning.md)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
