---
title: 在 Mac 視覺化工作室中安裝與使用 NuGet 套件
description: 有關在 Mac Visual Studio 中安裝和使用 NuGet 包的過程的演練教程。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238474"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="7e128-103">快速入門:在 Mac 可視化工作室中安裝和使用套件</span><span class="sxs-lookup"><span data-stu-id="7e128-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="7e128-104">NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。</span><span class="sxs-lookup"><span data-stu-id="7e128-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="7e128-105">請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。</span><span class="sxs-lookup"><span data-stu-id="7e128-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="7e128-106">使用 NuGet 套件管理員將程式包安裝到 Mac 視覺化工作室專案。</span><span class="sxs-lookup"><span data-stu-id="7e128-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="7e128-107">本文演示了使用流行的[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)包和 .NET 核心控制台項目的過程。</span><span class="sxs-lookup"><span data-stu-id="7e128-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="7e128-108">相同的流程適用於任何其他 Xamarin 或 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="7e128-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="7e128-109">安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。</span><span class="sxs-lookup"><span data-stu-id="7e128-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="7e128-110">建立參考之後，您可以透過其 API 呼叫套件。</span><span class="sxs-lookup"><span data-stu-id="7e128-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="7e128-111">**從nuget.org開始**:流覽*nuget.org*是 .NET 開發人員通常如何在他們自己的應用程式中找到他們可以重用的元件。</span><span class="sxs-lookup"><span data-stu-id="7e128-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="7e128-112">您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。</span><span class="sxs-lookup"><span data-stu-id="7e128-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="7e128-113">如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="7e128-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e128-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7e128-114">Prerequisites</span></span>

- <span data-ttu-id="7e128-115">視覺工作室 2019 為 Mac.</span><span class="sxs-lookup"><span data-stu-id="7e128-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="7e128-116">您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。</span><span class="sxs-lookup"><span data-stu-id="7e128-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="7e128-117">如果您在 Windows 上使用視覺化工作室,請參閱[在可視化工作室(僅限 Windows)中安裝和使用套件](install-and-use-a-package-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="7e128-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7e128-118">建立專案</span><span class="sxs-lookup"><span data-stu-id="7e128-118">Create a project</span></span>

<span data-ttu-id="7e128-119">假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。</span><span class="sxs-lookup"><span data-stu-id="7e128-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="7e128-120">在本演練中,請使用簡單的 .NET 核心控制台應用。</span><span class="sxs-lookup"><span data-stu-id="7e128-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="7e128-121">使用**檔案>新解決方案**在 Visual Studio 中為 Mac 建立專案 **> >...**</span><span class="sxs-lookup"><span data-stu-id="7e128-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="7e128-122">按 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="7e128-122">Click **Next**.</span></span> <span data-ttu-id="7e128-123">在提示時接受**目標框架**的預設值。</span><span class="sxs-lookup"><span data-stu-id="7e128-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="7e128-124">Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。</span><span class="sxs-lookup"><span data-stu-id="7e128-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="7e128-125">新增 Newtonsoft.Json NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="7e128-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="7e128-126">要安裝包,請使用 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="7e128-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="7e128-127">安裝包時,NuGet 會記錄專案檔`packages.config`或 檔中的依賴項(具體取決於專案格式)。</span><span class="sxs-lookup"><span data-stu-id="7e128-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="7e128-128">如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="7e128-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="7e128-129">NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="7e128-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="7e128-130">在解決方案資源管理器中,右鍵單擊**依賴項**並選擇 **"添加包..."**</span><span class="sxs-lookup"><span data-stu-id="7e128-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![專案參考的管理 NuGet 套件命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="7e128-132">選擇對話框左上角的「nuget.org」作為**包源**,然後搜索**Newtonsoft.Json,** 在清單中選擇該包,然後選擇 **「添加包...":**</span><span class="sxs-lookup"><span data-stu-id="7e128-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![尋找 Newtonsoft.Json 套件](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="7e128-134">如果您想瞭解有關 NuGet 套件管理員的詳細資訊,請參閱使用[Mac 的 Visual Studio 安裝與管理套件](../consume-packages/install-use-packages-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="7e128-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="7e128-135">在應用程式中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="7e128-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="7e128-136">在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="7e128-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="7e128-137">開啟`Program.cs`檔案(位於解決方案板中),並將檔案內容取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="7e128-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

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

1. <span data-ttu-id="7e128-138">以選擇 **「執行>啟動除錯**產生與執行應用:</span><span class="sxs-lookup"><span data-stu-id="7e128-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="7e128-139">套用執行後,您將看到序列化的 JSON 輸出顯示在控制台中:</span><span class="sxs-lookup"><span data-stu-id="7e128-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![主控台應用輸出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="7e128-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e128-141">Next steps</span></span>
<span data-ttu-id="7e128-142">恭喜，您安裝並使用了您的第一個 NuGet 套件！</span><span class="sxs-lookup"><span data-stu-id="7e128-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e128-143">使用 Mac 的視覺化工作室安裝和管理套件</span><span class="sxs-lookup"><span data-stu-id="7e128-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="7e128-144">若要深入探索 NuGet 所提供的功能，請選取下列連結。</span><span class="sxs-lookup"><span data-stu-id="7e128-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7e128-145">套件耗用量的概觀及工作流程</span><span class="sxs-lookup"><span data-stu-id="7e128-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="7e128-146">專案檔中的套件參考</span><span class="sxs-lookup"><span data-stu-id="7e128-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
