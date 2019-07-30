---
title: 在 Visual Studio 中安裝並使用 NuGet 套件
description: 在 Visual Studio 專案中安裝並使用 NuGet 套件程序的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: a2be42aeb322cfd0ab43c9cec6ad1b063cbc3089
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462487"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="42d48-103">快速入門：在 Visual Studio 中安裝並使用套件 (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="42d48-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="42d48-104">NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="42d48-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="42d48-105">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="42d48-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="42d48-106">套件使用 NuGet 套件管理員或套件管理員主控台安裝到 Visual Studio 專案中。</span><span class="sxs-lookup"><span data-stu-id="42d48-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="42d48-107">此文章示範使用熱門的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) \(英文\) 套件與 Windows Presentation Foundation (WPF) 專案的程序。</span><span class="sxs-lookup"><span data-stu-id="42d48-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="42d48-108">相同的程序適用於任何其他 .NET 或 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="42d48-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="42d48-109">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="42d48-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="42d48-110">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="42d48-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="42d48-111">**從 nuget.org 開始**：.NET 開發人員通常是透過瀏覽 *nuget.org* 來尋找可在自己應用程式中重複使用的元件。</span><span class="sxs-lookup"><span data-stu-id="42d48-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="42d48-112">您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。</span><span class="sxs-lookup"><span data-stu-id="42d48-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="42d48-113">如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="42d48-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42d48-114">先決條件</span><span class="sxs-lookup"><span data-stu-id="42d48-114">Prerequisites</span></span>

- <span data-ttu-id="42d48-115">包含 .NET 桌面開發工作負載的 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="42d48-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="42d48-116">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="42d48-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="42d48-117">如果您使用的是 Visual Studio for Mac，請參閱[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="42d48-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="42d48-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="42d48-118">Create a project</span></span>

<span data-ttu-id="42d48-119">假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。</span><span class="sxs-lookup"><span data-stu-id="42d48-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="42d48-120">在此逐步解說中，請使用簡單的 WPF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42d48-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="42d48-121">使用 [檔案] > [新增專案]  在 Visual Studio 中建立專案、在搜尋方塊中輸入 **.NET**，然後選取 [WPF 應用程式 (.NET Framework)]  。</span><span class="sxs-lookup"><span data-stu-id="42d48-121">Create a project in Visual Studio using **File > New Project...**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="42d48-122">按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="42d48-122">Click **Next**.</span></span> <span data-ttu-id="42d48-123">出現提示時，接受 [架構]  的預設值。</span><span class="sxs-lookup"><span data-stu-id="42d48-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="42d48-124">Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。</span><span class="sxs-lookup"><span data-stu-id="42d48-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="42d48-125">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="42d48-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="42d48-126">若要安裝套件，您可以使用 NuGet 套件管理員或套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="42d48-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="42d48-127">當您安裝套件時，NuGet 會在您的專案檔或 `packages.config` 檔案中 (視專案格式而定) 記錄相依性。</span><span class="sxs-lookup"><span data-stu-id="42d48-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="42d48-128">如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="42d48-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="42d48-129">NuGet 封裝管理員</span><span class="sxs-lookup"><span data-stu-id="42d48-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="42d48-130">在方案總管中以滑鼠右鍵按一下 [參考]  ，選擇 [管理 NuGet 套件]  。</span><span class="sxs-lookup"><span data-stu-id="42d48-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="42d48-132">選擇 "nuget.org" 作為 [套件來源]  ，選取 [瀏覽]  索引標籤、搜尋 [Newtonsoft.Json]  、在清單中選取該套件，然後選取 [安裝]  ：</span><span class="sxs-lookup"><span data-stu-id="42d48-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="42d48-134">如果您需要 NuGet 套件管理員的詳細資訊，請參閱[使用 Visual Studio 安裝及管理套件](../consume-packages/install-use-packages-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="42d48-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="42d48-135">接受任何授權提示。</span><span class="sxs-lookup"><span data-stu-id="42d48-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="42d48-136">(僅限 Visual Studio 2017) 如果系統提示您選取套件管理格式，請選取 [專案檔中的 PackageReference]  ：</span><span class="sxs-lookup"><span data-stu-id="42d48-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![選取套件管理格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="42d48-138">如果提示您檢閱變更，請選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="42d48-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="42d48-139">套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="42d48-139">Package Manager Console</span></span>

1. <span data-ttu-id="42d48-140">選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台]  功能表命令。</span><span class="sxs-lookup"><span data-stu-id="42d48-140">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="42d48-141">在主控台開啟之後，檢查 [預設專案]  下拉式清單是否顯示您要安裝套件的專案。</span><span class="sxs-lookup"><span data-stu-id="42d48-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="42d48-142">如果您在方案中只有一個專案，則已經選取該專案。</span><span class="sxs-lookup"><span data-stu-id="42d48-142">If you have a single project in the solution, it is already selected.</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="42d48-144">輸入命令 `Install-Package Newtonsoft.Json` (請參閱 [Install-Package](../reference/ps-reference/ps-ref-install-package.md))。</span><span class="sxs-lookup"><span data-stu-id="42d48-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="42d48-145">主控台視窗會顯示命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="42d48-145">The console window shows output for the command.</span></span> <span data-ttu-id="42d48-146">錯誤通常會指出套件與專案的目標 Framework 不相容。</span><span class="sxs-lookup"><span data-stu-id="42d48-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="42d48-147">如果您需要套件管理員主控台的詳細資訊，請參閱[使用套件管理員主控台安裝及管理套件](../consume-packages/install-use-packages-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="42d48-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="42d48-148">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="42d48-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="42d48-149">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="42d48-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="42d48-150">開啟 `MainWindow.xaml` 並使用下列內容取代現有的 `Grid` 元素：</span><span class="sxs-lookup"><span data-stu-id="42d48-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="42d48-151">開啟 `MainWindow.xaml.cs` 檔案 (位於方案總管的 `MainWindow.xaml` 節點下方)，然後將下列程式碼插入 `MainWindow` 類別內：</span><span class="sxs-lookup"><span data-stu-id="42d48-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="42d48-152">即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要在程式碼檔案頂端使用 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="42d48-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="42d48-153">按 F5 或選取 [偵錯] > [開始偵錯]  ，來建置並執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="42d48-153">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![WPF 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="42d48-155">選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：</span><span class="sxs-lookup"><span data-stu-id="42d48-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![選取按鈕之後的 WPF 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="42d48-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42d48-157">Next steps</span></span>

<span data-ttu-id="42d48-158">恭喜，您安裝並使用了您的第一個 NuGet 套件！</span><span class="sxs-lookup"><span data-stu-id="42d48-158">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42d48-159">使用 Visual Studio 安裝及管理套件</span><span class="sxs-lookup"><span data-stu-id="42d48-159">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="42d48-160">使用套件管理員主控台安裝及合併套件</span><span class="sxs-lookup"><span data-stu-id="42d48-160">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="42d48-161">若要深入探索 NuGet 所提供的功能，請選取下列連結。</span><span class="sxs-lookup"><span data-stu-id="42d48-161">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="42d48-162">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="42d48-162">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="42d48-163">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="42d48-163">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="42d48-164">專案檔中的套件參考</span><span class="sxs-lookup"><span data-stu-id="42d48-164">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
