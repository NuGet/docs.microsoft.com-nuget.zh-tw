---
title: 在 Visual Studio 中安裝並使用 NuGet 套件
description: 在 Visual Studio 專案中安裝並使用 NuGet 套件程序的逐步解說教學課程。
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775529"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>快速入門：僅在 Visual Studio (Windows 中安裝和使用套件) 

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 使用 NuGet 封裝管理員、 [封裝管理員主控台](../consume-packages/install-use-packages-powershell.md)或 [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md)將套件安裝到 Visual Studio 專案。 此文章示範使用熱門的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件與 Windows Presentation Foundation (WPF) 專案的程序。 相同的程序適用於任何其他 .NET 或 .NET Core 專案。

安裝之後，請在程式碼中參考封裝， `using <namespace>` 其中包含您所使用之 \<namespace\> 套件的特定位置。 建立參考之後，您可以透過其 API 呼叫套件。

> [!Tip]
> **從 Nuget.org 開始**：流覽 *nuget.org* 是 .net 開發人員通常如何尋找可在自己的應用程式中重複使用的元件。 您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。 如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>先決條件

- 包含 .NET 桌面開發工作負載的 Visual Studio 2019。

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。

如果您是使用 Visual Studio for Mac，請參閱 [在 Visual Studio for Mac 中安裝和使用套件](install-and-use-a-package-in-visual-studio-mac.md)。

## <a name="create-a-project"></a>建立專案

假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。

在此逐步解說中，請使用簡單的 WPF 應用程式。 **使用**[檔案新專案] 在 Visual Studio 中建立專案  >  ****、在 [搜尋] 方塊中輸入 **.net** ，然後選取 [ **WPF 應用程式] ( .NET Framework)**。 按一下 [下一步] 。 出現提示時，接受 [架構] 的預設值。

Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

若要安裝套件，您可以使用 NuGet 套件管理員或套件管理員主控台。 當您安裝套件時，NuGet 會在您的專案檔或 `packages.config` 檔案中 (視專案格式而定) 記錄相依性。 如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 套件管理員

1. 在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

    如果您需要 NuGet 套件管理員的詳細資訊，請參閱[使用 Visual Studio 安裝及管理套件](../consume-packages/install-use-packages-visual-studio.md)。

1. 接受任何授權提示。

1. (僅限 Visual Studio 2017) 如果系統提示您選取套件管理格式，請選取 [專案檔中的 PackageReference]：

    ![選取套件管理格式](media/QS_Use-03b-SelectFormat.png)

1. 如果提示您檢閱變更，請選取 [確定]。

### <a name="package-manager-console"></a>套件管理器主控台

1. 選取 [**工具**]  >  **NuGet 封裝管理員**  >  **封裝管理員主控台** 功能表命令。

1. 在主控台開啟之後，檢查 [預設專案] 下拉式清單是否顯示您要安裝套件的專案。 如果您在方案中只有一個專案，則已經選取該專案。

    ![選取封裝的專案](media/QS_Use-08-Console1.png)

1. 輸入命令 `Install-Package Newtonsoft.Json` (請參閱 [Install-Package](../reference/ps-reference/ps-ref-install-package.md))。 主控台視窗會顯示命令的輸出。 錯誤通常會指出套件與專案的目標 Framework 不相容。

   如果您需要套件管理員主控台的詳細資訊，請參閱[使用套件管理員主控台安裝及管理套件](../consume-packages/install-use-packages-powershell.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。

1. 開啟 `MainWindow.xaml` 並使用下列內容取代現有的 `Grid` 元素：

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 開啟 `MainWindow.xaml.cs` 檔案 (位於方案總管的 `MainWindow.xaml` 節點下方)，然後將下列程式碼插入 `MainWindow` 類別內：

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. 即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要在程式碼檔案頂端使用 `using` 陳述式：

    ```cs
    using Newtonsoft.Json;
    ```

1. 按 F5 或選取 [ **Debug**  >  **開始調試** 程式]，以建立並執行應用程式：

    ![WPF 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. 選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：

    ![選取按鈕之後的 WPF 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>相關影片

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

在 [Channel 9](https://channel9.msdn.com/Series/NuGet-101) 和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)上尋找更多的 NuGet 影片。

## <a name="next-steps"></a>後續步驟

恭喜，您安裝並使用了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [使用 Visual Studio 安裝和管理套件](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [使用套件管理員主控台安裝集合併套件](../consume-packages/install-use-packages-powershell.md)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)
