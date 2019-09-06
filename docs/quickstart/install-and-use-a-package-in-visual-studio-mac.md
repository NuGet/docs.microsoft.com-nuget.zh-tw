---
title: 在 Visual Studio for Mac 中安裝和使用 NuGet 套件
description: 在 Visual Studio for Mac 專案中安裝和使用 NuGet 套件程式的逐步解說教學課程。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238474"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="9d002-103">快速入門：在 Visual Studio for Mac 中安裝和使用套件</span><span class="sxs-lookup"><span data-stu-id="9d002-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="9d002-104">NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="9d002-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="9d002-105">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="9d002-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="9d002-106">封裝會使用 NuGet 套件管理員安裝到 Visual Studio for Mac 專案中。</span><span class="sxs-lookup"><span data-stu-id="9d002-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="9d002-107">本文示範如何使用熱門的[Newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/)套件和 .net Core 主控台專案來處理常式。</span><span class="sxs-lookup"><span data-stu-id="9d002-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="9d002-108">相同的程式也適用于其他任何 Xamarin 或 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="9d002-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="9d002-109">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="9d002-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="9d002-110">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="9d002-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="9d002-111">**從 nuget.org 開始**：.NET 開發人員通常是透過瀏覽 *nuget.org* 來尋找可在自己應用程式中重複使用的元件。</span><span class="sxs-lookup"><span data-stu-id="9d002-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="9d002-112">您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。</span><span class="sxs-lookup"><span data-stu-id="9d002-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="9d002-113">如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="9d002-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d002-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d002-114">Prerequisites</span></span>

- <span data-ttu-id="9d002-115">適用于 Mac 的 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="9d002-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="9d002-116">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="9d002-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="9d002-117">如果您是在 Windows 上使用 Visual Studio，請參閱[在 Visual Studio 中安裝和使用套件（僅限 Windows）](install-and-use-a-package-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9d002-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="9d002-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="9d002-118">Create a project</span></span>

<span data-ttu-id="9d002-119">假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。</span><span class="sxs-lookup"><span data-stu-id="9d002-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="9d002-120">在此逐步解說中，請使用簡單的 .NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d002-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="9d002-121">在 Visual Studio for Mac 中使用 [檔案 **> 新方案**] 建立專案，然後選取 [ **.Net Core > 應用程式] > 主控台應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="9d002-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="9d002-122">按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9d002-122">Click **Next**.</span></span> <span data-ttu-id="9d002-123">出現提示時，接受**目標 Framework**的預設值。</span><span class="sxs-lookup"><span data-stu-id="9d002-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="9d002-124">Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。</span><span class="sxs-lookup"><span data-stu-id="9d002-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="9d002-125">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="9d002-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="9d002-126">若要安裝套件，您可以使用 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="9d002-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="9d002-127">當您安裝套件時，NuGet 會將相依性記錄在您的專案檔`packages.config`或檔案中（視專案格式而定）。</span><span class="sxs-lookup"><span data-stu-id="9d002-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="9d002-128">如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="9d002-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="9d002-129">NuGet 封裝管理員</span><span class="sxs-lookup"><span data-stu-id="9d002-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="9d002-130">在方案總管中，以滑鼠右鍵按一下 [相依性]，然後選擇 [**新增套件 ...** **]** 。</span><span class="sxs-lookup"><span data-stu-id="9d002-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="9d002-132">選擇 [nuget.org] 作為對話方塊左上角的 [**套件來源**]，然後搜尋 [ **Newtonsoft**]，在清單中選取該套件，然後選取 [**新增套件 ...** ]：</span><span class="sxs-lookup"><span data-stu-id="9d002-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="9d002-134">如果您需要 NuGet 套件管理員的詳細資訊，請參閱[使用 Visual Studio for Mac 安裝和管理套件](../consume-packages/install-use-packages-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9d002-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="9d002-135">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="9d002-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="9d002-136">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="9d002-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="9d002-137">`Program.cs`開啟檔案（位於 Solution Pad），並將檔案內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="9d002-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="9d002-138">藉由選取 [**執行] > 開始調試**程式來建立並執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="9d002-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="9d002-139">應用程式執行後，您會看到序列化的 JSON 輸出出現在主控台中：</span><span class="sxs-lookup"><span data-stu-id="9d002-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![主控台應用程式的輸出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="9d002-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d002-141">Next steps</span></span>
<span data-ttu-id="9d002-142">恭喜，您安裝並使用了您的第一個 NuGet 套件！</span><span class="sxs-lookup"><span data-stu-id="9d002-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d002-143">使用 Visual Studio for Mac 安裝和管理套件</span><span class="sxs-lookup"><span data-stu-id="9d002-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="9d002-144">若要深入探索 NuGet 所提供的功能，請選取下列連結。</span><span class="sxs-lookup"><span data-stu-id="9d002-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="9d002-145">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="9d002-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="9d002-146">專案檔中的套件參考</span><span class="sxs-lookup"><span data-stu-id="9d002-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
