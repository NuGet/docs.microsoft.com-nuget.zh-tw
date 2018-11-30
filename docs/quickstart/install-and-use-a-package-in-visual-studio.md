---
title: 從 Visual Studio 使用 NuGet 套件的入門指南
description: 在 Visual Studio 專案中安裝並使用 NuGet 套件程序的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 15268ae33d56042a765420e5076dac49db6cce04
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671171"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>快速入門：在 Visual Studio 中安裝並使用套件

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 套件使用套件管理員 UI 或套件管理員主控台安裝到 Visual Studio 專案中。 本文示範使用熱門的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 套件和通用 Windows 平台 (UWP) 專案的程序。 相同的程序適用於任何其他 .NET 或 .NET Core 專案。

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 建立參考之後，您可以透過其 API 呼叫套件。

> [!Tip]
> **從 nuget.org 開始**：瀏覽 nuget.org 是 .NET 開發人員通常用來尋找可在自己應用程式中重複使用之元件的方式。 您可以直接搜尋 nuget.org，或在 Visual Studio 中尋找並安裝套件，如本文所示。

## <a name="prerequisites"></a>必要條件

- Visual Studio 2017，包含通用 Windows 平台開發工作負載，或
- Visual Studio 2015 Update 3，包含通用 Windows 應用程式的工具。

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2017 Community Edition，或使用 Professional Edition 或 Enterprise Edition。

## <a name="create-a-project"></a>建立專案

假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。

針對這個逐步解說，請使用簡單的通用 Windows (UWP) 應用程式。 使用 [檔案] > [新增專案]，然後選取 [Windows 通用] > [空白應用程式 (通用 Windows)]，在 Visual Studio 中建立專案。 當系統出現提示時，請接受目標版本和最低版本的預設值。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

若要安裝套件，您可以使用套件管理員 UI 或套件管理員主控台。 當您安裝套件時，NuGet 會在您的專案檔或 `packages.config` 檔案中記錄相依性。 如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。

### <a name="package-manager-ui"></a>套件管理員 UI

1. 在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

1. 接受任何授權提示。

1. (Visual Studio 2017) 如果系統提示您選取套件管理格式，請選取 [專案檔中的 PackageReference]：

    ![選取套件管理格式](media/QS_Use-03b-SelectFormat.png)

1. 如果提示您檢閱變更，請選取 [確定]。

### <a name="package-manager-console"></a>套件管理員主控台

1. 選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台] 功能表命令。

1. 在主控台開啟之後，檢查 [預設專案] 下拉式清單是否顯示您要安裝套件的專案。 如果您在方案中只有一個專案，則已經選取該專案。

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-08-Console1.png)

1. 輸入命令 `Install-Package Newtonsoft.Json` (請參閱 [Install-Package](../tools/ps-ref-install-package.md))。 主控台視窗會顯示命令的輸出。 錯誤通常會指出套件與專案的目標 Framework 不相容。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。

1. 開啟 `MainPage.xaml` 並使用下列內容取代現有的 `Grid` 元素：

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 開啟 `MainPage.xaml.cs` 檔案 (位於方案總管的 `MainPage.xaml` 節點下方)，然後將下列程式碼插入 `MainPage` 建構函式內：

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

1. 按 F5 或選取 [偵錯] > [開始偵錯]，來建置並執行應用程式：

    ![UWP 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. 選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：

    ![選取按鈕之後的 UWP 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>相關文章

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [安裝套件的方式](../consume-packages/ways-to-install-a-package.md)
- [設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)
