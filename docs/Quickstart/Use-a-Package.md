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
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="e21a6-104">安裝並使用套件</span><span class="sxs-lookup"><span data-stu-id="e21a6-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="e21a6-105">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="e21a6-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="e21a6-106">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="e21a6-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="e21a6-107">本主題的其餘部分會引導您完成在通用 Windows 平台 (UWP) 專案中使用套件管理員 UI 安裝熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 套件的程序。</span><span class="sxs-lookup"><span data-stu-id="e21a6-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="e21a6-108">然後，顯示使用套件的範例。</span><span class="sxs-lookup"><span data-stu-id="e21a6-108">It then shows an example of using the package.</span></span> <span data-ttu-id="e21a6-109">您可以對專案中使用的每一個 NuGet 套件，以虛擬方式使用類似的工作流程。</span><span class="sxs-lookup"><span data-stu-id="e21a6-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="e21a6-110">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="e21a6-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="e21a6-111">建立專案</span><span class="sxs-lookup"><span data-stu-id="e21a6-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="e21a6-112">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e21a6-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="e21a6-113">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="e21a6-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="e21a6-114">**開始使用 nuget.org**：從 nuget.org 安裝套件是常見的工作流程，.NET 開發人員使用它尋找可在自己的應用程式中重複使用的元件。</span><span class="sxs-lookup"><span data-stu-id="e21a6-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="e21a6-115">您一律可以直接搜尋 nuget.org 或在 Visual Studio 中尋找並安裝套件，如本主題中所示。</span><span class="sxs-lookup"><span data-stu-id="e21a6-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="e21a6-116">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="e21a6-116">Install pre-requisites</span></span>

<span data-ttu-id="e21a6-117">本教學課程需要 Visual Studio 2015 Update 3 與通用 Windows 應用程式的工具，或 Visual Studio 2017 與通用 Windows 平台開發工作負載。</span><span class="sxs-lookup"><span data-stu-id="e21a6-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="e21a6-118">如已安裝 Visual Studio，您可以再次執行安裝程式以新增 UWP 工具。</span><span class="sxs-lookup"><span data-stu-id="e21a6-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="e21a6-119">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="e21a6-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="e21a6-120">建立專案</span><span class="sxs-lookup"><span data-stu-id="e21a6-120">Create a project</span></span>

<span data-ttu-id="e21a6-121">若要安裝 NuGet 套件，您需要一些 Visual Studio 的 .NET 型專案。</span><span class="sxs-lookup"><span data-stu-id="e21a6-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="e21a6-122">在此逐步解說中，您可以使用簡單的 Windows Presentation Foundation (WPF) 或通用 Windows (UWP) 應用程式：</span><span class="sxs-lookup"><span data-stu-id="e21a6-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="e21a6-123">若為 WPF (Windows 7 +)，請選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#]、選取 [Windows 傳統桌面] > [WPF 應用程式 (.NET Framework)]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e21a6-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="e21a6-124">若為 UWP (Windows 10)，請改用 [Windows 通用] > [空白應用程式 (通用 Windows)]。</span><span class="sxs-lookup"><span data-stu-id="e21a6-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="e21a6-125">當系統出現提示時，請接受目標版本和最低版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="e21a6-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="e21a6-126">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e21a6-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="e21a6-127">在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="e21a6-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="e21a6-129">選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：</span><span class="sxs-lookup"><span data-stu-id="e21a6-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="e21a6-131">如果提示您選取套件管理格式，請在 PackageReference (建議選項) 和 `packages.config` 之間選擇：</span><span class="sxs-lookup"><span data-stu-id="e21a6-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![選取套件參考格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="e21a6-133">如果提示您檢閱變更，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e21a6-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="e21a6-134">以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="e21a6-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="e21a6-135">這會還原所有列在 [參考] 下的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="e21a6-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="e21a6-136">如需詳細資料，請參閱[套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="e21a6-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="e21a6-137">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="e21a6-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="e21a6-138">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="e21a6-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="e21a6-139">開啟 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP)，並以下列內容取代現有的 `Grid` 項目：</span><span class="sxs-lookup"><span data-stu-id="e21a6-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="e21a6-140">在方案總管中展開 `MainWindow.xaml`(WPF) 或 `MainPage.xaml` (UWP) 節點，開啟 `.cs` 檔案，然後將下列程式碼插入到 `MainWindow` 或 `MainPage` 類別內，在建構函式之後：</span><span class="sxs-lookup"><span data-stu-id="e21a6-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="e21a6-141">即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e21a6-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="e21a6-142">將滑鼠停留在加了底線的 `JsonConvert` 的上方，您會看到燈泡及選項 [顯示可能的修正]：</span><span class="sxs-lookup"><span data-stu-id="e21a6-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![燈泡與顯示可能的修正命令](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="e21a6-144">按一下 [顯示可能的修正] (或燈泡) 並選取第一個建議的修正 `using Newtonsoft.Json;`。</span><span class="sxs-lookup"><span data-stu-id="e21a6-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="e21a6-145">這會將必要的程式碼新增至檔案最上方。</span><span class="sxs-lookup"><span data-stu-id="e21a6-145">This adds the necessary line to the top of the file.</span></span>

    ![燈泡讓您可以選擇新增 using 陳述式](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="e21a6-147">建置並執行應用程式，請按 F5 或選取 [偵錯] > [開始偵錯] (UWP 會出現在這裡，WPF 也類似)：</span><span class="sxs-lookup"><span data-stu-id="e21a6-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="e21a6-149">選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：</span><span class="sxs-lookup"><span data-stu-id="e21a6-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![選取按鈕之後的 UWP 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="e21a6-151">相關主題</span><span class="sxs-lookup"><span data-stu-id="e21a6-151">Related topics</span></span>

- [<span data-ttu-id="e21a6-152">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="e21a6-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e21a6-153">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="e21a6-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e21a6-154">設定 NuGet 行為</span><span class="sxs-lookup"><span data-stu-id="e21a6-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
