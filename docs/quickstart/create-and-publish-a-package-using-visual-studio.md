---
title: 在 Windows 上使用 Visual Studio 建立及發行 .NET Standard NuGet 套件
description: 在 Windows 上使用 Visual Studio 建立及發行 .NET Standard NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419911"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="29c0e-103">快速入門：使用 Visual Studio 建立及發行 NuGet 套件 (.NET Standard，僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="29c0e-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="29c0e-104">使用 CLI 工具可以輕鬆在 Windows 上從 Visual Studio 中的 .NET Standard 類別庫建立 NuGet 套件，然後將其發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="29c0e-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="29c0e-105">若您是使用 Visual Studio for Mac，請參閱[此資訊](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)以了解如何建立 NuGet 套件，或使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)來建立套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29c0e-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="29c0e-106">Prerequisites</span></span>

1. <span data-ttu-id="29c0e-107">使用 .NET Core 相關的工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="29c0e-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="29c0e-108">安裝 `dotnet` CLI (若尚未安裝)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="29c0e-109">針對 `dotnet` CLI，從 Visual Studio 2017 開始，`dotnet` CLI 會自動與任何 .NET Core 相關工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="29c0e-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="29c0e-110">否則，請安裝 [.NET Core SDK](https://www.microsoft.com/net/download/) 以取得 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="29c0e-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="29c0e-111">使用 [SDK 樣式格式](../resources/check-project-format.md) (SDK 屬性) 的 .NET Standard 專案需要 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="29c0e-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="29c0e-112">此文章中使用的 Visual Studio 2017 與更高版本中的預設類別庫範本使用 SDK 屬性。</span><span class="sxs-lookup"><span data-stu-id="29c0e-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="29c0e-113">針對此文章，建議使用 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="29c0e-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="29c0e-114">雖然您可以使用 `nuget.exe` CLI 發行任何 NuGet 套件，此文章中的某些步驟僅適用於 SDK 專案與 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="29c0e-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="29c0e-115">nuget.exe CLI 是用於[非 SDK 樣式專案](../resources/check-project-format.md) (通常是 .NET Framework)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="29c0e-116">若您正在處理非 SDK 樣式專案，請依照[建立及發行 .NET Framework 套件 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) 中的程序建立及發行套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="29c0e-117">如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="29c0e-118">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="29c0e-119">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="29c0e-120">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="29c0e-120">Create a class library project</span></span>

<span data-ttu-id="29c0e-121">您可以針對要封裝的程式碼使用現有的 .NET Standard 類別庫專案，或建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="29c0e-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="29c0e-122">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]  、展開 [Visual C#] > [.NET Standard]  節點、選取 [類別庫 (.NET Standard)] 範本、將專案命名為 AppLogger，然後按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="29c0e-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="29c0e-123">在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置]  以確定已適當建立專案。</span><span class="sxs-lookup"><span data-stu-id="29c0e-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="29c0e-124">DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="29c0e-125">當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。</span><span class="sxs-lookup"><span data-stu-id="29c0e-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="29c0e-126">不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="29c0e-127">不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：</span><span class="sxs-lookup"><span data-stu-id="29c0e-127">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="29c0e-128">除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。</span><span class="sxs-lookup"><span data-stu-id="29c0e-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="29c0e-129">設定套件屬性</span><span class="sxs-lookup"><span data-stu-id="29c0e-129">Configure package properties</span></span>

1. <span data-ttu-id="29c0e-130">以滑鼠右鍵按一下 [方案總管] 中的專案，然後選擇 [屬性]  功能表命令，然後選取 [套件]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="29c0e-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="29c0e-131">[套件]  索引標籤只會針對 Visual Studio 中的 SDK 樣式專案 (通常是 .NET Standard 或 .NET Core 類別庫專案) 顯示；若您是以非 SDK 樣式專案 (通常是 .NET Framework) 為目標，請[移轉專案](../reference/migrate-packages-config-to-package-reference.md)並使用 `dotnet` CLIL，或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)或參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="29c0e-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio 專案中的 NuGet 套件屬性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="29c0e-133">針對公眾取用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="29c0e-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="29c0e-134">為套件指定唯一識別碼，並填入任何其他所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="29c0e-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="29c0e-135">如需不同屬性的說明，請參閱 [.nuspec 檔案參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="29c0e-136">此處的所有屬性都會移入 Visual Studio 針對專案建立的 `.nuspec` 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="29c0e-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="29c0e-137">您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="29c0e-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="29c0e-138">針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="29c0e-139">如果您嘗試發行名稱已經存在的套件，則會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="29c0e-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="29c0e-140">選擇性：若要直接查看專案檔中的屬性，請以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [編輯 AppLogger.csproj]  。</span><span class="sxs-lookup"><span data-stu-id="29c0e-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="29c0e-141">只有使用 SDK 樣式屬性的專案 (且必須使用 Visual Studio 2017 與更新版本) 才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="29c0e-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="29c0e-142">否則，以滑鼠右鍵按一下專案並選擇 [卸載專案]  。</span><span class="sxs-lookup"><span data-stu-id="29c0e-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="29c0e-143">接著，以滑鼠右鍵按一下卸載的專案並選擇 [編輯 AppLogger.csproj]  。</span><span class="sxs-lookup"><span data-stu-id="29c0e-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="29c0e-144">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="29c0e-144">Run the pack command</span></span>

1. <span data-ttu-id="29c0e-145">設定要**發行**的組態。</span><span class="sxs-lookup"><span data-stu-id="29c0e-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="29c0e-146">在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選取 [封裝]  命令：</span><span class="sxs-lookup"><span data-stu-id="29c0e-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 專案捷徑功能表上的 NuGet 封裝命令](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="29c0e-148">若您沒有看到 **Pack** 命令，您的專案可能並不是 SDK 樣式專案，且您必須使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="29c0e-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="29c0e-149">請[移轉專案](../reference/migrate-packages-config-to-package-reference.md) 並使用 `dotnet` CLI，或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="29c0e-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="29c0e-150">Visual Studio 會建置專案並建立 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="29c0e-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="29c0e-151">檢查 [輸出]  視窗以取得詳細資料 (如下所示)，其中包含套件檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="29c0e-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="29c0e-152">另請注意，建置的組建是位於 `bin\Release\netstandard2.0`，以適用 .NET Standard 2.0 目標。</span><span class="sxs-lookup"><span data-stu-id="29c0e-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="29c0e-153">替代選項：使用 MSBuild 封裝</span><span class="sxs-lookup"><span data-stu-id="29c0e-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="29c0e-154">當專案包含必要的套件資料時，NuGet 4.x+ 和 MSBuild 15.1+ 可支援 `pack` 目標，而這是使用 [封裝]  功能表命令的另一種替代方法。</span><span class="sxs-lookup"><span data-stu-id="29c0e-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="29c0e-155">請開啟命令提示字元，巡覽至專案資料夾並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="29c0e-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="29c0e-156">(若從 [開始] 功能表啟動 [適用於 Visual Studio 的開發人員命令提示字元]，其中就會設定好 MSBuild 的所有必要路徑，因此這是建議的做法。)</span><span class="sxs-lookup"><span data-stu-id="29c0e-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="29c0e-157">接著可在 `bin\Release` 資料夾中找到套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="29c0e-158">如需 `msbuild -t:pack` 的其他選項，請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="29c0e-159">發行套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-159">Publish the package</span></span>

<span data-ttu-id="29c0e-160">一旦擁有 `.nupkg` 檔案之後，您會使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="29c0e-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="29c0e-161">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="29c0e-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="29c0e-162">使用 dotnet nuget push 發行 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="29c0e-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="29c0e-163">此步驟是建議用於取代 `nuget.exe`的步驟。</span><span class="sxs-lookup"><span data-stu-id="29c0e-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="29c0e-164">您必須先開啟命令列，才能發行套件。</span><span class="sxs-lookup"><span data-stu-id="29c0e-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="29c0e-165">使用 nuget push 發行 (nuget.exe CLI)</span><span class="sxs-lookup"><span data-stu-id="29c0e-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="29c0e-166">這個步驟是使用 `dotnet.exe` 的替代方案。</span><span class="sxs-lookup"><span data-stu-id="29c0e-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="29c0e-167">開啟命令列並變更到包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="29c0e-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="29c0e-168">執行下列命令，指定套件名稱 (使用套件識別碼) 並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="29c0e-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="29c0e-169">nuget.exe 顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="29c0e-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="29c0e-170">請參閱 [nuget push](../reference/cli-reference/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="29c0e-171">發行錯誤</span><span class="sxs-lookup"><span data-stu-id="29c0e-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="29c0e-172">管理已發行的套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="29c0e-173">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="29c0e-173">Adding a readme and other files</span></span>

<span data-ttu-id="29c0e-174">若要直接指定套件中要包含的檔案，請編輯專案檔並使用 `content` 屬性：</span><span class="sxs-lookup"><span data-stu-id="29c0e-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="29c0e-175">這會在套件根目錄中包含名稱為 `readme.txt` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="29c0e-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="29c0e-176">Visual Studio 會在直接安裝套件之後，立即以純文字顯示該檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="29c0e-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="29c0e-177">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="29c0e-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="29c0e-178">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="29c0e-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="29c0e-180">只在專案根目錄新增 readme.txt，並不會導致其包含在產生的套件中。</span><span class="sxs-lookup"><span data-stu-id="29c0e-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="29c0e-181">相關主題</span><span class="sxs-lookup"><span data-stu-id="29c0e-181">Related topics</span></span>

- [<span data-ttu-id="29c0e-182">建立套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="29c0e-183">套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="29c0e-184">發行前套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="29c0e-185">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="29c0e-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="29c0e-186">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="29c0e-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="29c0e-187">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="29c0e-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="29c0e-188">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="29c0e-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="29c0e-189">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="29c0e-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
