---
title: 從 Visual Studio 使用 NuGet 套件的入門指南
description: 在 Visual Studio 專案中安裝並使用 NuGet 套件程序的逐步解說教學課程。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: c61f8929d34bc9ff1a84ee186636543da5bcee63
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="d4e02-103">快速入門：在 Visual Studio 中安裝並使用套件</span><span class="sxs-lookup"><span data-stu-id="d4e02-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="d4e02-104">NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="d4e02-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="d4e02-105">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="d4e02-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="d4e02-106">套件使用套件管理員 UI 或套件管理員主控台安裝到 Visual Studio 專案中。</span><span class="sxs-lookup"><span data-stu-id="d4e02-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="d4e02-107">本文示範使用熱門的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 套件和通用 Windows 平台 (UWP) 專案的程序。</span><span class="sxs-lookup"><span data-stu-id="d4e02-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="d4e02-108">相同的程序適用於任何其他 .NET 或 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="d4e02-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="d4e02-109">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="d4e02-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="d4e02-110">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="d4e02-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="d4e02-111">**從 nuget.org 開始**：瀏覽 nuget.org 是 .NET 開發人員通常用來尋找可在自己應用程式中重複使用之元件的方式。</span><span class="sxs-lookup"><span data-stu-id="d4e02-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="d4e02-112">您可以直接搜尋 nuget.org，或在 Visual Studio 中尋找並安裝套件，如本文所示。</span><span class="sxs-lookup"><span data-stu-id="d4e02-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4e02-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4e02-113">Prerequisites</span></span>

- <span data-ttu-id="d4e02-114">Visual Studio 2017，包含通用 Windows 平台開發工作負載，或</span><span class="sxs-lookup"><span data-stu-id="d4e02-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="d4e02-115">Visual Studio 2015 Update 3，包含通用 Windows 應用程式的工具。</span><span class="sxs-lookup"><span data-stu-id="d4e02-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="d4e02-116">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2017 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="d4e02-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="d4e02-117">建立專案</span><span class="sxs-lookup"><span data-stu-id="d4e02-117">Create a project</span></span>

<span data-ttu-id="d4e02-118">假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。</span><span class="sxs-lookup"><span data-stu-id="d4e02-118">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="d4e02-119">針對這個逐步解說，請使用簡單的通用 Windows (UWP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4e02-119">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="d4e02-120">使用 [檔案] > [新增專案]，然後選取 [Windows 通用] > [空白應用程式 (通用 Windows)]，在 Visual Studio 中建立專案。</span><span class="sxs-lookup"><span data-stu-id="d4e02-120">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="d4e02-121">當系統出現提示時，請接受目標版本和最低版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="d4e02-121">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="d4e02-122">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="d4e02-122">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="d4e02-123">若要安裝套件，您可以使用套件管理員 UI 或套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="d4e02-123">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="d4e02-124">當您安裝套件時，NuGet 會在您的專案檔或 `packages.config` 檔案中記錄相依性。</span><span class="sxs-lookup"><span data-stu-id="d4e02-124">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="d4e02-125">如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="d4e02-125">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="d4e02-126">套件管理員 UI</span><span class="sxs-lookup"><span data-stu-id="d4e02-126">Package Manager UI</span></span>

1. <span data-ttu-id="d4e02-127">在方案總管中以滑鼠右鍵按一下 [參考]，選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="d4e02-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="d4e02-129">選擇 "nuget.org" 作為 [套件來源]，選取 [瀏覽] 索引標籤、搜尋 [Newtonsoft.Json]、在清單中選取該套件，然後選取 [安裝]：</span><span class="sxs-lookup"><span data-stu-id="d4e02-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="d4e02-131">接受任何授權提示。</span><span class="sxs-lookup"><span data-stu-id="d4e02-131">Accept any license prompts.</span></span>

1. <span data-ttu-id="d4e02-132">(Visual Studio 2017) 如果系統提示您選取套件管理格式，請選取 [專案檔中的 PackageReference]：</span><span class="sxs-lookup"><span data-stu-id="d4e02-132">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![選取套件管理格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="d4e02-134">如果提示您檢閱變更，請選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d4e02-134">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="d4e02-135">套件管理員主控台</span><span class="sxs-lookup"><span data-stu-id="d4e02-135">Package Manager Console</span></span>

1. <span data-ttu-id="d4e02-136">選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="d4e02-136">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="d4e02-137">在主控台開啟之後，檢查 [預設專案] 下拉式清單是否顯示您要安裝套件的專案。</span><span class="sxs-lookup"><span data-stu-id="d4e02-137">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="d4e02-138">如果您在方案中只有一個專案，則已經選取該專案。</span><span class="sxs-lookup"><span data-stu-id="d4e02-138">If you have a single project in the solution, it is already selected.</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="d4e02-140">輸入命令 `Install-Package Newtonsoft.json` (請參閱 [Install-Package](../tools/ps-ref-install-package.md))。</span><span class="sxs-lookup"><span data-stu-id="d4e02-140">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="d4e02-141">主控台視窗會顯示命令的輸出。</span><span class="sxs-lookup"><span data-stu-id="d4e02-141">The console window shows output for the command.</span></span> <span data-ttu-id="d4e02-142">錯誤通常會指出套件與專案的目標 Framework 不相容。</span><span class="sxs-lookup"><span data-stu-id="d4e02-142">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="d4e02-143">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="d4e02-143">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="d4e02-144">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="d4e02-144">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="d4e02-145">開啟 `MainPage.xaml` 並使用下列內容取代現有的 `Grid` 元素：</span><span class="sxs-lookup"><span data-stu-id="d4e02-145">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="d4e02-146">開啟 `MainPage.xaml.cs` 檔案 (位於方案總管的 `MainPage.xaml` 節點下方)，然後將下列程式碼插入 `MainPage` 建構函式內：</span><span class="sxs-lookup"><span data-stu-id="d4e02-146">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="d4e02-147">即使在專案中新增了 Newtonsoft.Json 套件，`JsonConvert` 下方還是會出現紅色波浪線，因為您需要在程式碼檔案頂端使用 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="d4e02-147">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="d4e02-148">按 F5 或選取 [偵錯] > [開始偵錯]，來建置並執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="d4e02-148">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP 應用程式的初始輸出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="d4e02-150">選取按鈕以查看使用一些 JSON 文字取代的 TextBlock 內容：</span><span class="sxs-lookup"><span data-stu-id="d4e02-150">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![選取按鈕之後的 UWP 應用程式輸出](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="d4e02-152">相關文章</span><span class="sxs-lookup"><span data-stu-id="d4e02-152">Related articles</span></span>

- [<span data-ttu-id="d4e02-153">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="d4e02-153">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="d4e02-154">尋找及選擇套件</span><span class="sxs-lookup"><span data-stu-id="d4e02-154">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="d4e02-155">安裝套件的方式</span><span class="sxs-lookup"><span data-stu-id="d4e02-155">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="d4e02-156">設定 NuGet 行為</span><span class="sxs-lookup"><span data-stu-id="d4e02-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
