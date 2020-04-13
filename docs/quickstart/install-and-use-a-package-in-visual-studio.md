---
title: 在 Visual Studio 中安裝並使用 NuGet 套件
description: 在 Visual Studio 專案中安裝並使用 NuGet 套件程序的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147483"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>快速入門:在可視化工作室(僅限 Windows)中安裝和使用包

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 套件使用 NuGet 套件管理員、[包管理器主控台](../consume-packages/install-use-packages-powershell)或[dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md)安裝到可視化工作室專案中。 此文章示範使用熱門的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件與 Windows Presentation Foundation (WPF) 專案的程序。 相同的程序適用於任何其他 .NET 或 .NET Core 專案。

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 建立參考之後，您可以透過其 API 呼叫套件。

> [!Tip]
> **從nuget.org開始**:流覽*nuget.org*是 .NET 開發人員通常如何在他們自己的應用程式中找到他們可以重用的元件。 您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。 如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>Prerequisites

- 包含 .NET 桌面開發工作負載的 Visual Studio 2019。

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。

如果您使用的是 Mac 的可視化工作室,請參閱[在 Visual Studio 中安裝和使用 Mac](install-and-use-a-package-in-visual-studio-mac.md)的套件。

## <a name="create-a-project"></a>建立專案

假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。

在此逐步解說中，請使用簡單的 WPF 應用程式。 使用 **"檔案** > **新專案**"在可視化工作室中創建專案,在搜索框中鍵入 **.NET,** 然後選擇**WPF 應用程式 (.NET Framework)。** 按 [下一步]  。 出現提示時，接受 [架構]**** 的預設值。

Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

若要安裝套件，您可以使用 NuGet 套件管理員或套件管理員主控台。 當您安裝套件時，NuGet 會在您的專案檔或 `packages.config` 檔案中 (視專案格式而定) 記錄相依性。 如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 套件管理員

1. 在方案總管中以滑鼠右鍵按一下 [參考]****，選擇 [管理 NuGet 套件]****。

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 選擇 "nuget.org" 作為 [套件來源]****，選取 [瀏覽]**** 索引標籤、搜尋 [Newtonsoft.Json]****、在清單中選取該套件，然後選取 [安裝]****：

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

    如果您需要 NuGet 套件管理員的詳細資訊，請參閱[使用 Visual Studio 安裝及管理套件](../consume-packages/install-use-packages-visual-studio.md)。

1. 接受任何授權提示。

1. (僅限 Visual Studio 2017) 如果系統提示您選取套件管理格式，請選取 [專案檔中的 PackageReference]****：

    ![選取套件管理格式](media/QS_Use-03b-SelectFormat.png)

1. 如果提示您檢閱變更，請選取 [確定]****。

### <a name="package-manager-console"></a>套件管理器主控台

1. 選擇 **「工具** > **NuGet 套件管理員** > **管理員主控台」** 選單命令。

1. 在主控台開啟之後，檢查 [預設專案]**** 下拉式清單是否顯示您要安裝套件的專案。 如果您在方案中只有一個專案，則已經選取該專案。

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-08-Console1.png)

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

1. 以使用 F5 或選擇**除錯** > **啟動除錯**來產生與執行應用程式:

    ![WPF 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. 選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：

    ![選取按鈕之後的 WPF 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>相關影片

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

在[頻道 9](https://channel9.msdn.com/Series/NuGet-101)和[YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)上查找更多 NuGet 影片。

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
