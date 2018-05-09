---
title: Visual Studio 範本中的 NuGet 套件
description: 將 NuGet 套件包含為 Visual Studio 專案和項目範本一部分的指示。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 801e107afb498d7a3353bd36d71eb7b0f0201910
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="packages-in-visual-studio-templates"></a>Visual Studio 範本中的套件

當建立專案或項目時，Visual Studio 專案及物件範本通常需要確認特定套件已安裝。 例如，ASP.NET MVC 3 範本會安裝 jQuery、Modernizr 和其他套件。

若要支援此作業，範本作者可以指示 NuGet 安裝必要的套件，而不是個別的程式庫。 開發人員稍後便可以隨時輕鬆地更新那些套件。

若要深入了解撰寫範本自身，請參閱[如何：建立專案範本](/visualstudio/ide/how-to-create-project-templates)或[建立自訂專案與項目範本](/visualstudio/extensibility/creating-custom-project-and-item-templates)。

本節的其餘部分描述在撰寫範本以正確包含 NuGet 套件時要採取的特定步驟。

- [將套件新增至範本](#adding-packages-to-a-template)
- [最佳做法](#best-practices)

如需範例，請參閱 [NuGetInVsTemplates 範例](https://bitbucket.org/marcind/nugetinvstemplates)。

## <a name="adding-packages-to-a-template"></a>將套件新增至範本

具現化範本時，會叫用[範本精靈](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)來載入要安裝的套件清單，以及何處可以找到這些套件的相關資訊。 套件可以內嵌在 VSIX 中、內嵌在範本中，或位於本機硬碟上，在此情況下您會使用登錄機碼來參考檔案路徑。 這些位置的詳細資料稍後會在本節中提供。

預先安裝的套件使用[範本精靈](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)來運作。 範本具現化時，會叫用特殊的精靈。 精靈會載入需要安裝的套件清單，並將該資訊傳遞至適當的 NuGet API。

要在範本中包含套件的步驟：

1. 在您的 `vstemplate` 檔案中，藉由新增 [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) 項目新增對 NuGet 範本精靈的參考：

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` 是一個組件，它只包含 `TemplateWizard` 類別，這是簡單的包裝函式，它會呼叫 `NuGet.VisualStudio.dll` 中的實際實作。 組件版本永遠不會變更，以便專案/項目範本繼續使用新版的 NuGet。

1. 在專案中新增要安裝的套件清單：

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    精靈支援多個 `<package>` 元素以支援多個套件來源。 同時需要 `id` 和 `version` 屬性，這表示即使有較新版本，也將會安裝該特定版本的套件。 這可防止套件更新中斷範本，讓使用範本的開發人員能選擇是否更新套件。

1. 指定 NuGet 可以找到套件的儲存機制，如下列各節中所述。

### <a name="vsix-package-repository"></a>VSIX 套件儲存機制

Visual Studio 專案/項目範本的建議部署方法是 [VSIX 延伸模組](/visualstudio/extensibility/shipping-visual-studio-extensions)，因為它可讓您將多個專案/項目範本封裝在一起，並可讓開發人員輕鬆地使用 VS 延伸模組管理員或 Visual Studio 組件庫探索您的範本。 延伸模組的更新也很容易使用 [Visual Studio 延伸模組管理員自動更新機制](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)部署。

VSIX 本身可以作為範本所需的套件來源：

1. 修改 `.vstemplate` 檔案中的 `<packages>` 項目，如下所示：

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` 屬性指定存放庫的類型為 `extension`，而 `repositoryId` 是 VSIX 本身的唯一識別碼 (這是延伸模組檔案 `vsixmanifest` 的 `ID` 屬性值，請參閱 [VSIX 延伸結構描述 2.0 參考](/visualstudio/extensibility/vsix-extension-schema-2-0-reference))。

1. 將您 `nupkg` 檔案放在 VSIX 內稱為 `Packages` 的資料夾。

1. 在 `vsixmanifest` 檔案中將必要套件檔案新增為 `<Asset>` (請參閱 [VSIX 延伸結構描述 2.0 參考](/visualstudio/extensibility/vsix-extension-schema-2-0-reference))：

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. 請注意，您可以在與您專案範本相同的 VSIX 中提供套件，或者可以在對您的案例更有意義時將它們放在個別的 VSIX 中。 不過，請勿參考您無法控制的任何 VSIX，因為該延伸模組的變更可能會破壞您的範本。

### <a name="template-package-repository"></a>範本套件儲存機制

如果您只散發單一專案/項目範本，且不需要將多個範本封裝在一起，您可以使用較簡單但較多限制的方法，將套件直接包含在專案/項目範本 ZIP 檔案：

1. 修改 `.vstemplate` 檔案中的 `<packages>` 項目，如下所示：

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` 屬性有 `template` 值，且 `repositoryId` 屬性不是必要。

1. 將套件放在專案/項目範本 ZIP 檔案的根資料夾。

請注意，在包含多個範本的 VSIX 中使用這種方法，會在一或多個套件是範本皆通用時導致不必要的膨脹。 在這種情況下，請使用 [VSIX 作為儲存機制](#vsix-package-repository)，如上一節中所述。

### <a name="registry-specified-folder-path"></a>登錄指定的資料夾路徑

使用 MSI 安裝的 SDK 可以直接在開發人員的電腦上安裝 NuGet 套件。 這樣當使用專案或項目範本時它們便立即可用，而不需要在這段時間擷取它們。 ASP.NET 範本使用此方法。

1. 讓 MSI 將套件安裝至電腦。 您可以只安裝 `.nupkg` 檔案，或是與展開的內容一起安裝，以在使用範本時節省額外的步驟。 在此情況下，請遵循 NuGet 的標準資料夾結構，其中 `.nupkg` 檔案位於根資料夾，然後每個套件會有子資料夾，並以識別碼/版本組作為子資料夾名稱。

1. 寫入登錄機碼來識別套件位置：

    - 機碼位置：可能是整部機器的 `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`，或者如果是每個使用者安裝的範本和套件，可以選擇使用 `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - 機碼名稱：使用您獨有的名稱。 例如，VS 2012 的 ASP.NET MVC 4 範本使用 `AspNetMvc4VS11`。
    - 值：packages 資料夾的完整路徑。

1. 在 `.vstemplate` 檔案的 `<packages>` 項目中，新增屬性 `repository="registry"` 並在 `keyName` 屬性指定您的登錄機碼名稱。

    - 如果您已預先解壓縮套件，請使用 `isPreunzipped="true"` 屬性。
    - *(NuGet 3.2+)* 如果您想要在套件安裝結束時強制設計階段組建，請新增 `forceDesignTimeBuild="true"` 屬性。
    - 新增 `skipAssemblyReferences="true"` 以便進行最佳化，因為範本本身已經包含必要的參考。

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>最佳作法

1. 宣告對 NuGet VSIX 的相依性，方法是在您的 VSIX 資訊清單中新增對它的參考：

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. 藉由在 `.vstemplate` 檔案中包含 [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates)，要求在建立時儲存專案/項目範本。

1. 範本不包含 `packages.config` 檔案，而且不包含安裝 NuGet 套件時將會新增的任何參考或內容。
