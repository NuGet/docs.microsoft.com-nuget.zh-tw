---
title: "使用 NuGet 套件的入門指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "在專案中安裝與使用 NuGet 套件程序的逐步解說教學課程。"
keywords: "安裝 NuGet, NuGet 套件耗用量, 安裝 NuGet 套件, NuGet 套件參考, 使用 NuGet 套件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a>安裝並使用套件

NuGet 套件是可重複使用的程式碼單位，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。

[!INCLUDE [install-methods](../includes/install-methods.md)]

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 建立參考之後，您可以透過其 API 呼叫套件。

本主題的其餘部分會引導您完成在通用 Windows 平台 (UWP) 專案中使用套件管理員 UI 安裝熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 套件的程序。 然後，顯示使用套件的範例。 您可以對專案中使用的每一個 NuGet 套件，以虛擬方式使用類似的工作流程。

- [安裝必要條件](#install-pre-requisites)
- [建立專案](#create-a-project)
- [新增 Newtonsoft.Json NuGet 套件](#add-the-newtonsoftjson-nuget-package)
- [在應用程式中使用 Newtonsoft.Json API](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **開始使用 nuget.org**：從 nuget.org 安裝套件是常見的工作流程，.NET 開發人員使用它尋找可在自己的應用程式中重複使用的元件。 您一律可以直接搜尋 nuget.org 或在 Visual Studio 中尋找並安裝套件，如本主題中所示。

## <a name="install-pre-requisites"></a>安裝必要條件

本教學課程需要 Visual Studio 2015 Update 3 與通用 Windows 應用程式的工具，或 Visual Studio 2017 與通用 Windows 平台開發工作負載。 如已安裝 Visual Studio，您可以再次執行安裝程式以新增 UWP 工具。

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，或使用 Professional Edition 或 Enterprise Edition。 

## <a name="create-a-project"></a>建立專案

若要安裝 NuGet 套件，您需要一些 Visual Studio 的 .NET 型專案。 在此逐步解說中，您可以使用簡單的 Windows Presentation Foundation (WPF) 或通用 Windows (UWP) 應用程式：

- 若為 WPF (Windows 7 +)，請選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#]、選取 [Windows 傳統桌面] > [WPF 應用程式 (.NET Framework)]，然後選取 [確定]。
- 若為 UWP (Windows 10)，請改用 [Windows 通用] > [空白應用程式 (通用 Windows)]。 當系統出現提示時，請接受目標版本和最低版本的預設值。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

1. 在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

1. 如果提示您選取套件管理格式，請在 PackageReference (建議選項) 和 `packages.config` 之間選擇：

    ![選取套件參考格式](media/QS_Use-03b-SelectFormat.png)

1. 如果提示您檢閱變更，請選取 [確定]。

1. 以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [建置方案]。 這會還原所有列在 [參考] 下的 NuGet 套件。 如需詳細資料，請參閱[套件還原](../consume-packages/package-restore.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。

1. 開啟 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP)，並以下列內容取代現有的 `Grid` 項目：

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 在方案總管中展開 `MainWindow.xaml`(WPF) 或 `MainPage.xaml` (UWP) 節點，開啟 `.cs` 檔案，然後將下列程式碼插入到 `MainWindow` 或 `MainPage` 類別內，在建構函式之後：

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

1. 即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要 `using` 陳述式。 將滑鼠停留在加了底線的 `JsonConvert` 的上方，您會看到燈泡及選項 [顯示可能的修正]：

    ![燈泡與顯示可能的修正命令](media/QS_Use-04-ShowPotentialFixes.png)


1. 按一下 [顯示可能的修正] (或燈泡) 並選取第一個建議的修正 `using Newtonsoft.Json;`。 這會將必要的程式碼新增至檔案最上方。

    ![燈泡讓您可以選擇新增 using 陳述式](media/QS_Use-05-AddUsing.png)

1. 建置並執行應用程式，請按 F5 或選取 [偵錯] > [開始偵錯] (UWP 會出現在這裡，WPF 也類似)：

    ![UWP 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. 選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：

    ![選取按鈕之後的 UWP 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>相關主題

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)
