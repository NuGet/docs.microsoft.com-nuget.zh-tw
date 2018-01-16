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
# <a name="install-and-use-a-package"></a><span data-ttu-id="c1750-104">安裝並使用套件</span><span class="sxs-lookup"><span data-stu-id="c1750-104">Install and use a package</span></span>

<span data-ttu-id="c1750-105">NuGet 套件是可重複使用的程式碼單位，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="c1750-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="c1750-106">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="c1750-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="c1750-107">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="c1750-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="c1750-108">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="c1750-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="c1750-109">本主題的其餘部分會引導您完成在通用 Windows 平台 (UWP) 專案中使用套件管理員 UI 安裝熱門 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 套件的程序。</span><span class="sxs-lookup"><span data-stu-id="c1750-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="c1750-110">然後，顯示使用套件的範例。</span><span class="sxs-lookup"><span data-stu-id="c1750-110">It then shows an example of using the package.</span></span> <span data-ttu-id="c1750-111">您可以對專案中使用的每一個 NuGet 套件，以虛擬方式使用類似的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c1750-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="c1750-112">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="c1750-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="c1750-113">建立專案</span><span class="sxs-lookup"><span data-stu-id="c1750-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="c1750-114">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c1750-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="c1750-115">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="c1750-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="c1750-116">**開始使用 nuget.org**：從 nuget.org 安裝套件是常見的工作流程，.NET 開發人員使用它尋找可在自己的應用程式中重複使用的元件。</span><span class="sxs-lookup"><span data-stu-id="c1750-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="c1750-117">您一律可以直接搜尋 nuget.org 或在 Visual Studio 中尋找並安裝套件，如本主題中所示。</span><span class="sxs-lookup"><span data-stu-id="c1750-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="c1750-118">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="c1750-118">Install pre-requisites</span></span>

<span data-ttu-id="c1750-119">本教學課程需要 Visual Studio 2015 Update 3 與通用 Windows 應用程式的工具，或 Visual Studio 2017 與通用 Windows 平台開發工作負載。</span><span class="sxs-lookup"><span data-stu-id="c1750-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="c1750-120">如已安裝 Visual Studio，您可以再次執行安裝程式以新增 UWP 工具。</span><span class="sxs-lookup"><span data-stu-id="c1750-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="c1750-121">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="c1750-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="c1750-122">建立專案</span><span class="sxs-lookup"><span data-stu-id="c1750-122">Create a project</span></span>

<span data-ttu-id="c1750-123">若要安裝 NuGet 套件，您需要一些 Visual Studio 的 .NET 型專案。</span><span class="sxs-lookup"><span data-stu-id="c1750-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="c1750-124">在此逐步解說中，您可以使用簡單的 Windows Presentation Foundation (WPF) 或通用 Windows (UWP) 應用程式：</span><span class="sxs-lookup"><span data-stu-id="c1750-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="c1750-125">若為 WPF (Windows 7 +)，請選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#]、選取 [Windows 傳統桌面] > [WPF 應用程式 (.NET Framework)]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c1750-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="c1750-126">若為 UWP (Windows 10)，請改用 [Windows 通用] > [空白應用程式 (通用 Windows)]。</span><span class="sxs-lookup"><span data-stu-id="c1750-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="c1750-127">當系統出現提示時，請接受目標版本和最低版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="c1750-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="c1750-128">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c1750-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="c1750-129">在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="c1750-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="c1750-131">選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：</span><span class="sxs-lookup"><span data-stu-id="c1750-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="c1750-133">如果提示您選取套件管理格式，請在 PackageReference (建議選項) 和 `packages.config` 之間選擇：</span><span class="sxs-lookup"><span data-stu-id="c1750-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![選取套件參考格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="c1750-135">如果提示您檢閱變更，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c1750-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="c1750-136">以滑鼠右鍵按一下方案總管中的解決方案，然後選取 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="c1750-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="c1750-137">這會還原所有列在 [參考] 下的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="c1750-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="c1750-138">如需詳細資料，請參閱[套件還原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="c1750-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="c1750-139">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="c1750-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="c1750-140">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="c1750-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="c1750-141">開啟 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP)，並以下列內容取代現有的 `Grid` 項目：</span><span class="sxs-lookup"><span data-stu-id="c1750-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="c1750-142">在方案總管中展開 `MainWindow.xaml`(WPF) 或 `MainPage.xaml` (UWP) 節點，開啟 `.cs` 檔案，然後將下列程式碼插入到 `MainWindow` 或 `MainPage` 類別內，在建構函式之後：</span><span class="sxs-lookup"><span data-stu-id="c1750-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="c1750-143">即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c1750-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="c1750-144">將滑鼠停留在加了底線的 `JsonConvert` 的上方，您會看到燈泡及選項 [顯示可能的修正]：</span><span class="sxs-lookup"><span data-stu-id="c1750-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![燈泡與顯示可能的修正命令](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="c1750-146">按一下 [顯示可能的修正] (或燈泡) 並選取第一個建議的修正 `using Newtonsoft.Json;`。</span><span class="sxs-lookup"><span data-stu-id="c1750-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="c1750-147">這會將必要的程式碼新增至檔案最上方。</span><span class="sxs-lookup"><span data-stu-id="c1750-147">This adds the necessary line to the top of the file.</span></span>

    ![燈泡讓您可以選擇新增 using 陳述式](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="c1750-149">建置並執行應用程式，請按 F5 或選取 [偵錯] > [開始偵錯] (UWP 會出現在這裡，WPF 也類似)：</span><span class="sxs-lookup"><span data-stu-id="c1750-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="c1750-151">選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：</span><span class="sxs-lookup"><span data-stu-id="c1750-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![選取按鈕之後的 UWP 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="c1750-153">相關主題</span><span class="sxs-lookup"><span data-stu-id="c1750-153">Related topics</span></span>

- [<span data-ttu-id="c1750-154">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="c1750-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="c1750-155">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="c1750-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="c1750-156">設定 NuGet 行為</span><span class="sxs-lookup"><span data-stu-id="c1750-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
