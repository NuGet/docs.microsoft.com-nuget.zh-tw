---
title: 建立及發行 .NET Standard NuGet 套件 - Windows 上的 Visual Studio
description: 在 Windows 上使用 Visual Studio 建立及發行 .NET Standard NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 9552f6c5291f950430bfb723cb713bf76a79ea66
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564608"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>快速入門：使用 Visual Studio 建立及發行 NuGet 套件 (.NET Standard，僅限 Windows)

使用 CLI 工具可以輕鬆在 Windows 上從 Visual Studio 中的 .NET Standard 類別庫建立 NuGet 套件，然後將其發行到 nuget.org。

> [!Note]
> 若您是使用 Visual Studio for Mac，請參閱[此資訊](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)以了解如何建立 NuGet 套件，或使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)來建立套件。

## <a name="prerequisites"></a>必要條件

1. 使用 .NET Core 相關工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2019。

1. 安裝 `dotnet` CLI (若尚未安裝)。

   針對 `dotnet` CLI，從 Visual Studio 2017 開始，`dotnet` CLI 會自動與任何 .NET Core 相關工作負載一起安裝。 否則，請安裝 [.NET Core SDK](https://www.microsoft.com/net/download/) 以取得 `dotnet` CLI。 使用 [SDK 樣式格式](../resources/check-project-format.md) (SDK 屬性) 的 .NET Standard 專案需要 `dotnet` CLI。 此文章中使用的 Visual Studio 2017 與更高版本中的預設 .NET Standard 類別庫範本使用 SDK 屬性。
   
   > [!Important]
   > 若您正在處理非 SDK 樣式專案，請改為依照[建立及發行 .NET Framework 套件 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) 中的程序建立及發行套件。 針對此文章，建議使用 `dotnet` CLI。 雖然您可以使用 `nuget.exe` CLI 發行任何 NuGet 套件，此文章中的某些步驟僅適用於 SDK 專案與 dotnet CLI。 nuget.exe CLI 是用於[非 SDK 樣式專案](../resources/check-project-format.md) (通常是 .NET Framework)。

1. 如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) \(英文\)。 建立新的帳戶會傳送一封確認電子郵件。 您必須確認帳戶，才可以上傳套件。

## <a name="create-a-class-library-project"></a>建立類別庫專案

您可以針對要封裝的程式碼使用現有的 .NET Standard 類別庫專案，或建立一個簡單的專案，如下所示：

1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]  、展開 [Visual C#] > [.NET Standard]  節點、選取 [類別庫 (.NET Standard)] 範本、將專案命名為 AppLogger，然後按一下 [確定]  。

   > [!Tip]
   > 除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。

1. 在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置]  以確定已適當建立專案。 DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。

當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。 不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。 不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：

```cs
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

## <a name="configure-package-properties"></a>設定套件屬性

1. 以滑鼠右鍵按一下 [方案總管] 中的專案，然後選擇 [屬性]  功能表命令，然後選取 [套件]  索引標籤。

   [套件]  索引標籤只會針對 Visual Studio 中的 SDK 樣式專案 (通常是 .NET Standard 或 .NET Core 類別庫專案) 顯示；若您是以非 SDK 樣式專案 (通常是 .NET Framework) 為目標，請[移轉專案](../consume-packages/migrate-packages-config-to-package-reference.md)或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。

    ![Visual Studio 專案中的 NuGet 套件屬性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > 針對公眾取用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。

1. 為套件指定唯一識別碼，並填入任何其他所需的屬性。 針對將 MSBuild 屬性 (SDK 樣式專案) 對應到 *.nuspec* 中的屬性，請參閱[封裝目標](../reference/msbuild-targets.md#pack-target)。 如需有關屬性的說明, 請參閱 [.nuspec 檔案參考](../reference/nuspec.md)。 此處的所有屬性都會移入 Visual Studio 針對專案建立的 `.nuspec` 資訊清單。

    > [!Important]
    > 您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。 針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。
    >
    > 如果您嘗試發行名稱已經存在的套件，則會看到錯誤。

1. (選擇性) 若要直接查看專案檔中的屬性，請以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [編輯 AppLogger.csproj]  。

   只有使用 SDK 樣式屬性的專案 (且必須使用 Visual Studio 2017 與更新版本) 才能使用此選項。 否則，以滑鼠右鍵按一下專案並選擇 [卸載專案]  。 接著，以滑鼠右鍵按一下卸載的專案並選擇 [編輯 AppLogger.csproj]  。

## <a name="run-the-pack-command"></a>執行 pack 命令

1. 設定要**發行**的組態。

1. 在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選取 [封裝]  命令：

    ![Visual Studio 專案捷徑功能表上的 NuGet 封裝命令](media/qs_create-vs-02-pack-command.png)

    若您沒有看到 **Pack** 命令，您的專案可能並不是 SDK 樣式專案，且您必須使用 `nuget.exe` CLI。 請[移轉專案](../consume-packages/migrate-packages-config-to-package-reference.md) 並使用 `dotnet` CLI，或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。

1. Visual Studio 會建置專案並建立 `.nupkg` 檔案。 檢查 [輸出]  視窗以取得詳細資料 (如下所示)，其中包含套件檔案的路徑。 另請注意，建置的組建是位於 `bin\Release\netstandard2.0`，以適用 .NET Standard 2.0 目標。

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(選擇性) 建置時產生套件

您可以設定 Visual Studio，在建置專案時自動產生 NuGet 套件。

1. 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [屬性]  。

2. 在 [套件]  索引標籤中，選取 [在建置時產生 NuGet 套件]  。

   ![建置時自動產生套件](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> 當您自動產生套件時，封裝的時間會增加專案的建置時間。

### <a name="optional-pack-with-msbuild"></a>(選擇性) 使用 MSBuild 進行封裝

當專案包含必要的套件資料時，NuGet 4.x+ 和 MSBuild 15.1+ 可支援 `pack` 目標，而這是使用 [封裝]  功能表命令的另一種替代方法。 請開啟命令提示字元，巡覽至專案資料夾並執行下列命令。 (若從 [開始] 功能表啟動 [適用於 Visual Studio 的開發人員命令提示字元]，其中就會設定好 MSBuild 的所有必要路徑，因此這是建議的做法。)

如需詳細資訊，請參閱[使用 MSBuild 建立套件](../create-packages/creating-a-package-msbuild.md)。

## <a name="publish-the-package"></a>發行套件

一旦擁有 `.nupkg` 檔案之後，您會使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>取得 API 金鑰

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>使用 dotnet CLI 或 nuget.exe CLI 發佈

選取您 CLI 工具的索引標籤，它可能是 **.NET Core CLI** (dotnet CLI) 或 **NuGet** (nuget.exe CLI)。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

此步驟是建議用於取代 `nuget.exe`的步驟。

您必須先開啟命令列，才能發行套件。

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nugettabnuget"></a>[NuGet](#tab/nuget)

這個步驟是使用 `dotnet.exe` 的替代方案。

1. 開啟命令列並變更到包含 `.nupkg` 檔案的資料夾。

1. 執行下列命令，指定套件名稱 (使用套件識別碼) 並使用您的 API 金鑰來取代金鑰值：

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

---

### <a name="publish-errors"></a>發行錯誤

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已發行的套件

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>新增讀我檔案和其他檔案

若要直接指定套件中要包含的檔案，請編輯專案檔並使用 `content` 屬性：

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

這會在套件根目錄中包含名稱為 `readme.txt` 的檔案。 Visual Studio 會在直接安裝套件之後，立即以純文字顯示該檔案的內容。 (不會針對安裝為相依性的套件顯示讀我檔案)。 例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：

![安裝時 NuGet 套件的讀我檔案顯示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> 只在專案根目錄新增 readme.txt，並不會導致其包含在產生的套件中。

## <a name="related-topics"></a>相關主題

- [建立套件](../create-packages/creating-a-package-dotnet-cli.md)
- [套件](../nuget-org/publish-a-package.md)
- [發行前套件](../create-packages/Prerelease-Packages.md)
- [支援多個目標架構](../create-packages/multiple-target-frameworks-project-file.md)
- [套件版本控制](../concepts/package-versioning.md)
- [建立當地語系化的套件](../create-packages/creating-localized-packages.md)
- [.NET Standard 程式庫文件](/dotnet/articles/standard/library)
- [從 .NET Framework 移轉到 .NET Core](/dotnet/articles/core/porting/index)
