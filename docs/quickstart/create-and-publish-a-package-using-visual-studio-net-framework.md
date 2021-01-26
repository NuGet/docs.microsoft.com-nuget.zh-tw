---
title: 在 Windows 上使用 Visual Studio 建立及發行 .NET Framework NuGet 套件
description: 在 Windows 上使用 Visual Studio 建立及發佈 .NET Framework NuGet 套件的逐步解說教學課程。
author: JonDouglas
ms.author: jodou
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7c030db769973e3b3c41da6523d57ab2cd769a9d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775743"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>快速入門：使用 Visual Studio 建立及發行套件 (.NET Framework，Windows)

從 .NET Framework 類別庫中建立 NuGet 套件，會涉及在 Windows 上於 Visual Studio 中建立 DLL，進而使用 nuget.exe 命令列工具來建立及發行套件。

> [!Note]
> 本快速入門僅適用于適用于 Windows 的 Visual Studio 2017 和更高版本。 Visual Studio for Mac 不包含這裡描述的功能。 請改為使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。

## <a name="prerequisites"></a>先決條件

1. 使用任何 .NET 相關的工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017 或更高版本。 Visual Studio 2017 會在安裝 .NET 工作負載時，自動包含 NuGet 功能。

1. 安裝 `nuget.exe` CLI，作法是從 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下載它、將該 `.exe` 檔案儲存至適當的資料夾，然後將該資料夾新增至您的 PATH 環境變數。

1. 如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)。 建立新的帳戶會傳送一封確認電子郵件。 您必須確認帳戶，才可以上傳套件。

## <a name="create-a-class-library-project"></a>建立類別庫專案

您可以對要封裝的程式碼使用現有的 .NET Framework 類別庫專案，或建立一個簡單的專案，如下所示：

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，選取 [Visual C#] 節點，選取 [類別庫 (.NET Framework)] 範本，將專案命名為 AppLogger，然後按一下 [確定]。

1. 在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置] 以確定已適當建立專案。 DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。

當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。 您也可以用任何方式設定目標 Framework。 請參閱 [UWP](../guides/create-uwp-packages.md) 和 [Xamarin](../guides/create-packages-for-xamarin.md) 指南以取得指導。

不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。 不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> 除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。 請參閱[使用 Visual Studio 建立及發佈套件 (.NET Standard)](create-and-publish-a-package-using-visual-studio.md)。

## <a name="configure-project-properties-for-the-package"></a>為套件設定專案屬性

NuGet 套件含有資訊清單 (`.nuspec` 檔案)，包含相關的中繼資料如套件識別碼、版本號碼、描述等等。 其中某些可以直接從專案屬性取得，如此就不必在專案和資訊清單中分別予以更新。 本章節說明應於何處設定適用的屬性。

1. 選取 [專案] > [屬性] 功能表命令，然後選取 [應用程式] 索引標籤。

1. 在 [組件名稱] 欄位中，為您的套件指定唯一識別碼。

    > [!Important]
    > 您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。 針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。
    >
    > 如果您嘗試發行名稱已經存在的套件，則會看到錯誤。

1. 選取 [組件資訊...] 按鈕會顯示對話方塊，您可以在其中輸入會帶入資訊清單中的其他屬性 (請參閱 [.nuspec 檔案參考 - 替代權杖](../reference/nuspec.md#replacement-tokens))。 最常使用的欄位是 **標題**、**描述**、**公司**、**著作權** 和 **組件版本**。 這些屬性最後會在主機上 (例如 nuget.org) 與您的套件一起顯示，因此請確認屬性的描述完整。

    ![Visual Studio 中 .NET Framework 專案的組件資訊](media/qs_create-vs-01b-project-properties.png)

1. 選擇性：若要查看並直接編輯屬性，請開啟專案中的 `Properties/AssemblyInfo.cs` 檔案。

1. 設定屬性後，請將專案組態設定為 **發行** 並重建專案以產生更新的 DLL。

## <a name="generate-the-initial-manifest"></a>產生初始資訊清單

有了 DLL，並完成專案屬性設定後，請使用 `nuget spec` 命令從專案中產生初始的 `.nuspec` 檔案。 這個步驟包含了相關的取代權杖，以從專案檔中取出資訊。

僅執行 `nuget spec` 一次即可產生初始的資訊清單。 更新套件時，請在專案中變更值或直接編輯資訊清單。

1. 開啟命令提示字元並巡覽至包含 `AppLogger.csproj` 檔案的專案資料夾。

1. 執行下列命令：`nuget spec AppLogger.csproj`。 藉由指定專案，NuGet 會建立符合專案名稱的資訊清單，在此情況下為 `AppLogger.nuspec`。 另外也會包含資訊清單中的取代權杖。

1. 在文字編輯器中開啟 `AppLogger.nuspec` 來檢視其內容，應如下所示：

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>編輯資訊清單

1. 如果您嘗試使用 `.nuspec` 檔案中的預設值來建立套件，NuGet 會產生錯誤，因此您必須編輯下列欄位後再繼續。 如需如何使用這些項目的描述，請參閱 [.nuspect 檔案參考 - 選擇性中繼資料元素](../reference/nuspec.md#optional-metadata-elements)。

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tags

1. 對於為供公開使用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人在 nuget.org 之類的來源上找到您的套件，並了解其用途。

1. 您也可同時在資訊清單新增任何其他項目，如 [.nuspec 檔案參考](../reference/nuspec.md)所述。

1. 儲存檔案後再繼續。

## <a name="run-the-pack-command"></a>執行 pack 命令

1. 從包含 `.nuspec` 檔案之資料夾中的命令提示字元，執行命令 `nuget pack`。

1. NuGet 會以 *identifier-version.nupkg* 的形式產生 `.nupkg` 檔案，可在目前的資料夾中找到。

## <a name="publish-the-package"></a>發行套件

一旦有檔案 `.nupkg` ，您就可以使用 `nuget.exe` 從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。針對 nuget.org，您必須使用 `nuget.exe` 4.1.0 或更高版本。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>取得 API 金鑰

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>使用 nuget push 發行

1. 開啟命令列並變更到包含 `.nupkg` 檔案的資料夾。

1. 執行下列命令，指定套件名稱並使用您的 API 金鑰來取代金鑰值：

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe 顯示發行程序的結果：

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

請參閱 [nuget push](../reference/cli-reference/cli-ref-push.md)。

### <a name="publish-errors"></a>發行錯誤

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已發行的套件

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>後續步驟

恭喜，您建立了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [建立套件](../create-packages/creating-a-package.md)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [發佈封裝](../nuget-org/publish-a-package.md)
- [發行前套件](../create-packages/Prerelease-Packages.md)
- [支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)
- [套件版本控制](../concepts/package-versioning.md)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
