---
title: NuGet 套件的原始程式檔和組態檔轉換 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 套件可在安裝時轉換原始程式檔和組態檔 (XML) 的詳細資料。
keywords: NuGet 套件安裝、NuGet 套件轉換、修改組態檔、修改原始程式碼
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b2c25acdd37489a2965d29356742a826b62afa2c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>轉換原始程式碼和組態檔

針對使用 `packages.config` 的專案，NuGet 支援在套件安裝和解除安裝期間轉換原始程式碼和組態檔的能力。 只有在使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 將套件安裝在專案中時，才會套用原始程式碼轉換。

安裝套件時，**原始程式碼轉換**會將單向權杖取代套用到套件 `content` 或 `contentFiles` 資料夾中的檔案 (若是使用 `packages.config` 的客戶，為 `content`；若是 `PackageReference` 則為 `contentFiles`)，而權杖指的是 Visual Studio [套件屬性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)。 這可讓您將檔案插入至專案的命名空間，或自訂一般會移入 ASP.NET 專案之 `global.asax` 中的程式碼。

**組態檔轉換**可讓您修改目標專案中的現有檔案 (例如 `web.config` 和 `app.config`)。 例如，您的套件可能需要將項目新增至組態檔中的 `modules` 區段。 此轉換的完成是透過在專案中包含可描述要新增至組態檔之區段的特殊檔案。 解除安裝套件時，接著會反轉這些相同的變更，讓這項作業成為雙向轉換。

## <a name="specifying-source-code-transformations"></a>指定原始程式碼轉換

1. 您想要從套件插入專案中的檔案必須位在套件的 `content` 和 `contentFiles` 資料夾中。 例如，如果您想要將名為 `ContosoData.cs` 的檔案安裝在目標專案的 `Models` 資料夾中，該檔案就必須在套件的 `content\Models` 和 `contentFiles\{lang}\{tfm}\Models` 資料夾內。

1. 若要指示 NuGet 在安裝期間套用權杖取代，請將 `.pp` 附加至原始程式檔名稱。 安裝之後，檔案的副檔名將不會是 `.pp`。

    例如，若要在 `ContosoData.cs` 中進行轉換，請將套件中的檔案命名為 `ContosoData.cs.pp`。 它在安裝後會顯示為 `ContosoData.cs`。

1. 在原始程式檔中，使用表單 `$token$` 的不區分大小寫權杖指出 NuGet 應該取代為專案屬性的值：

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    安裝時，NuGet 會將 `$rootnamespace$` 取代為 `Fabrikam`，並假設目標專案的根命名空間是 `Fabrikam`。

`$rootnamespace$` 權杖是最常用的專案屬性，其他則列在[專案屬性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)中。 當然，請注意，某些屬性可能是專案類型所特有。

## <a name="specifying-config-file-transformations"></a>指定組態檔轉換

如下節所述，可以使用兩種方式進行組態檔轉換：

- 在套件的 `content` 資料夾中包含 `app.config.transform` 和 `web.config.transform` 檔案，其中 `.transform` 副檔名會告知 NuGet，這些檔案包含安裝套件時要與現有組態檔合併的 XML。 解除安裝套件時，會移除這個相同的 XML。
- 使用 [XDT 語法](https://msdn.microsoft.com/library/dd465326.aspx)描述所需的變更，以在套件的 `content` 資料夾中包含 `app.config.install.xdt` 和 `web.config.install.xdt` 檔案。 使用此選項，您也可以包含 `.uninstall.xdt` 檔案，以在從專案移除套件時反轉變更。

> [!Note]
> 轉換不會套用至 Visual Studio 中參考為連結的 `.config` 檔案。

使用 XDT 的優點是它提供語法以使用利用完整 XPath 支援進行項目和屬性比對來操作 XML DOM 結構，而不是僅合併兩個靜態檔案。 XDT 接著可以新增、更新或移除項目、將新項目放在特定位置，或取代/移除項目 (包含子節點)。 這可讓您直接建立解除安裝轉換，以取消在套件安裝期間完成的所有轉換。

### <a name="xml-transforms"></a>XML 轉換

套件之 `content` 資料夾中的 `app.config.transform` 和 `web.config.transform` 只會包含要合併至專案之現有 `app.config` 和 `web.config` 檔案的項目。

例如，假設專案一開始在 `web.config` 中包含下列內容：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

若要在套件安裝期間將 `MyNuModule` 項目新增至 `modules` 區段，請在套件的 `content` 資料夾中建立 `web.config.transform` 檔案，如下所示：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet 安裝套件之後，`web.config` 會顯示如下：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

請注意，NuGet 不會取代 `modules` 區段，而只是新增項目和屬性，以在其中合併新項目。 NuGet 不會變更任何現有項目或屬性。

解除安裝套件時，NuGet 會重新檢查 `.transform` 檔案，並從適當的 `.config` 檔案中移除它所含的項目。 請注意，此程序將不會影響 `.config` 檔案中您在套件安裝之後修改的任何列。

更廣泛的範例是 [ASP.NET 的錯誤記錄模組和處理常式 (ELMAH)](https://www.nuget.org/packages/elmah/) 套件會將許多項目新增至 `web.config`，然後在解除安裝套件時重新予以移除。

若要檢查其 `web.config.transform` 檔案，請從上面的連結下載 ELMAH 套件，並將套件延伸模組從 `.nupkg` 變更為 `.zip`，然後開啟該 ZIP 檔案中的 `content\web.config.transform`。

若要查看安裝和解除安裝套件的效果，請在 Visual Studio 中建立新的 ASP.NET 專案 (範本是在 [新增專案] 對話方塊的 [Visual C#] > [Web] 下方)，然後選取空白 ASP.NET 應用程式。 開啟 `web.config` 以查看其初始狀態。 接著以滑鼠右鍵按一下專案，並選取 [管理 NuGet 套件]，再瀏覽 nuget.org 上的 ELMAH，然後安裝最新版本。 請注意所有 `web.config` 變更。 現在解除安裝套件，而您會看到 `web.config` 還原成其先前狀態。

### <a name="xdt-transforms"></a>XDT 轉換

您可以使用 [XDT 語法](https://msdn.microsoft.com/library/dd465326.aspx)來修改組態檔。 您也可以在 `$` 分隔符號內包含屬性名稱 (不區分大小寫)，讓 NuGet 將權杖取代為[專案屬性](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)。

例如，下列 `app.config.install.xdt` 檔案會將 `appSettings` 項目從專案插入至包含 `FullPath`、`FileName` 和 `ActiveConfigurationSettings` 值的 `app.config`：

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

另一個範例假設專案一開始在 `web.config` 中包含下列內容：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

若要在套件安裝期間將 `MyNuModule` 項目新增至 `modules` 區段，則套件的 `web.config.install.xdt` 將會包含下列項目：

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

安裝套件之後，`web.config` 會如下：

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

若在套件解除安裝期間只要移除 `MyNuModule` 項目，則 `web.config.uninstall.xdt` 檔案應該包含下列項目：

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
