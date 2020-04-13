---
title: 建立及發行 .NET Standard NuGet 套件 - Windows 上的 Visual Studio
description: 在 Windows 上使用 Visual Studio 建立及發行 .NET Standard NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429028"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="a4315-103">快速入門：使用 Visual Studio 建立及發行 NuGet 套件 (.NET Standard，僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="a4315-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="a4315-104">使用 CLI 工具可以輕鬆在 Windows 上從 Visual Studio 中的 .NET Standard 類別庫建立 NuGet 套件，然後將其發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="a4315-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="a4315-105">若您是使用 Visual Studio for Mac，請參閱[此資訊](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library)以了解如何建立 NuGet 套件，或使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)來建立套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4315-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4315-106">Prerequisites</span></span>

1. <span data-ttu-id="a4315-107">使用 .NET Core 相關工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="a4315-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="a4315-108">安裝 `dotnet` CLI (若尚未安裝)。</span><span class="sxs-lookup"><span data-stu-id="a4315-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="a4315-109">針對 `dotnet` CLI，從 Visual Studio 2017 開始，`dotnet` CLI 會自動與任何 .NET Core 相關工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="a4315-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="a4315-110">否則，請安裝 [.NET Core SDK](https://www.microsoft.com/net/download/) 以取得 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="a4315-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="a4315-111">使用 [SDK 樣式格式](../resources/check-project-format.md) (SDK 屬性) 的 .NET Standard 專案需要 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="a4315-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="a4315-112">此文章中使用的 Visual Studio 2017 與更高版本中的預設 .NET Standard 類別庫範本使用 SDK 屬性。</span><span class="sxs-lookup"><span data-stu-id="a4315-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="a4315-113">若您正在處理非 SDK 樣式專案，請改為依照[建立及發行 .NET Framework 套件 (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) 中的程序建立及發行套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="a4315-114">針對此文章，建議使用 `dotnet` CLI。</span><span class="sxs-lookup"><span data-stu-id="a4315-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="a4315-115">雖然您可以使用 `nuget.exe` CLI 發行任何 NuGet 套件，此文章中的某些步驟僅適用於 SDK 專案與 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="a4315-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="a4315-116">nuget.exe CLI 是用於[非 SDK 樣式專案](../resources/check-project-format.md) (通常是 .NET Framework)。</span><span class="sxs-lookup"><span data-stu-id="a4315-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="a4315-117">如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](../nuget-org/individual-accounts.md#add-a-new-individual-account) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a4315-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="a4315-118">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a4315-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="a4315-119">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="a4315-120">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="a4315-120">Create a class library project</span></span>

<span data-ttu-id="a4315-121">您可以針對要封裝的程式碼使用現有的 .NET Standard 類別庫專案，或建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4315-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="a4315-122">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]\*\*\*\*、展開 [Visual C#] > [.NET Standard]\*\*\*\* 節點、選取 [類別庫 (.NET Standard)] 範本、將專案命名為 AppLogger，然後按一下 [確定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="a4315-123">除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。</span><span class="sxs-lookup"><span data-stu-id="a4315-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="a4315-124">在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置]\*\*\*\* 以確定已適當建立專案。</span><span class="sxs-lookup"><span data-stu-id="a4315-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="a4315-125">DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。</span><span class="sxs-lookup"><span data-stu-id="a4315-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="a4315-126">當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。</span><span class="sxs-lookup"><span data-stu-id="a4315-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="a4315-127">不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="a4315-128">不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：</span><span class="sxs-lookup"><span data-stu-id="a4315-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="a4315-129">設定套件屬性</span><span class="sxs-lookup"><span data-stu-id="a4315-129">Configure package properties</span></span>

1. <span data-ttu-id="a4315-130">以滑鼠右鍵按一下 [方案總管] 中的專案，然後選擇 [屬性]\*\*\*\* 功能表命令，然後選取 [套件]\*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4315-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="a4315-131">[套件]\*\*\*\* 索引標籤只會針對 Visual Studio 中的 SDK 樣式專案 (通常是 .NET Standard 或 .NET Core 類別庫專案) 顯示；若您是以非 SDK 樣式專案 (通常是 .NET Framework) 為目標，請[移轉專案](../consume-packages/migrate-packages-config-to-package-reference.md)或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a4315-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio 專案中的 NuGet 套件屬性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="a4315-133">針對公眾取用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="a4315-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="a4315-134">為套件指定唯一識別碼，並填入任何其他所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="a4315-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="a4315-135">針對將 MSBuild 屬性 (SDK 樣式專案) 對應到 *.nuspec* 中的屬性，請參閱[封裝目標](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="a4315-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="a4315-136">如需有關屬性的說明, 請參閱 [.nuspec 檔案參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="a4315-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="a4315-137">此處的所有屬性都會移入 Visual Studio 針對專案建立的 `.nuspec` 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="a4315-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="a4315-138">您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a4315-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="a4315-139">針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。</span><span class="sxs-lookup"><span data-stu-id="a4315-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="a4315-140">如果您嘗試發行名稱已經存在的套件，則會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="a4315-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="a4315-141">(選擇性) 若要直接查看專案檔中的屬性，請以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [編輯 AppLogger.csproj]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="a4315-142">只有使用 SDK 樣式屬性的專案 (且必須使用 Visual Studio 2017 與更新版本) 才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="a4315-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="a4315-143">否則，以滑鼠右鍵按一下專案並選擇 [卸載專案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="a4315-144">接著，以滑鼠右鍵按一下卸載的專案並選擇 [編輯 AppLogger.csproj]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="a4315-145">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="a4315-145">Run the pack command</span></span>

1. <span data-ttu-id="a4315-146">設定要**發行**的組態。</span><span class="sxs-lookup"><span data-stu-id="a4315-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="a4315-147">在 [方案總管]\*\*\*\* 中，以滑鼠右鍵按一下專案，然後選取 [封裝]\*\*\*\* 命令：</span><span class="sxs-lookup"><span data-stu-id="a4315-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 專案捷徑功能表上的 NuGet 封裝命令](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="a4315-149">若您沒有看到 **Pack** 命令，您的專案可能並不是 SDK 樣式專案，且您必須使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="a4315-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="a4315-150">請[移轉專案](../consume-packages/migrate-packages-config-to-package-reference.md) 並使用 `dotnet` CLI，或改為參閱[建立及發行 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a4315-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="a4315-151">Visual Studio 會建置專案並建立 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a4315-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="a4315-152">檢查 [輸出]\*\*\*\* 視窗以取得詳細資料 (如下所示)，其中包含套件檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="a4315-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="a4315-153">另請注意，建置的組建是位於 `bin\Release\netstandard2.0`，以適用 .NET Standard 2.0 目標。</span><span class="sxs-lookup"><span data-stu-id="a4315-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="a4315-154">(選擇性) 建置時產生套件</span><span class="sxs-lookup"><span data-stu-id="a4315-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="a4315-155">您可以設定 Visual Studio，在建置專案時自動產生 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="a4315-156">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="a4315-157">在 [套件]\*\*\*\* 索引標籤中，選取 [在建置時產生 NuGet 套件]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a4315-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![建置時自動產生套件](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="a4315-159">當您自動產生套件時，封裝的時間會增加專案的建置時間。</span><span class="sxs-lookup"><span data-stu-id="a4315-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="a4315-160">(選擇性) 使用 MSBuild 進行封裝</span><span class="sxs-lookup"><span data-stu-id="a4315-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="a4315-161">作為使用**Pack**功能表命令的替代方法,NuGet 4.x+ 和 MSBuild 15.1+ 支援`pack`專案包含必要的包數據時 的目標。</span><span class="sxs-lookup"><span data-stu-id="a4315-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="a4315-162">請開啟命令提示字元，巡覽至專案資料夾並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="a4315-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="a4315-163">(若從 [開始] 功能表啟動 [適用於 Visual Studio 的開發人員命令提示字元]，其中就會設定好 MSBuild 的所有必要路徑，因此這是建議的做法。)</span><span class="sxs-lookup"><span data-stu-id="a4315-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="a4315-164">如需詳細資訊，請參閱[使用 MSBuild 建立套件](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="a4315-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="a4315-165">發行套件</span><span class="sxs-lookup"><span data-stu-id="a4315-165">Publish the package</span></span>

<span data-ttu-id="a4315-166">一旦擁有 `.nupkg` 檔案之後，您會使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="a4315-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="a4315-167">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="a4315-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="a4315-168">使用 dotnet CLI 或 nuget.exe CLI 發佈</span><span class="sxs-lookup"><span data-stu-id="a4315-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="a4315-169">選取您 CLI 工具的索引標籤，它可能是 **.NET Core CLI** (dotnet CLI) 或 **NuGet** (nuget.exe CLI)。</span><span class="sxs-lookup"><span data-stu-id="a4315-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="a4315-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a4315-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="a4315-171">此步驟是建議用於取代 `nuget.exe`的步驟。</span><span class="sxs-lookup"><span data-stu-id="a4315-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="a4315-172">您必須先開啟命令列，才能發行套件。</span><span class="sxs-lookup"><span data-stu-id="a4315-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="a4315-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="a4315-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="a4315-174">這個步驟是使用 `dotnet.exe` 的替代方案。</span><span class="sxs-lookup"><span data-stu-id="a4315-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="a4315-175">開啟命令列並變更到包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a4315-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="a4315-176">執行下列命令，指定套件名稱 (使用套件識別碼) 並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="a4315-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="a4315-177">nuget.exe 顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="a4315-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="a4315-178">請參閱 [nuget push](../reference/cli-reference/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="a4315-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="a4315-179">發行錯誤</span><span class="sxs-lookup"><span data-stu-id="a4315-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="a4315-180">管理已發行的套件</span><span class="sxs-lookup"><span data-stu-id="a4315-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="a4315-181">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="a4315-181">Adding a readme and other files</span></span>

<span data-ttu-id="a4315-182">若要直接指定套件中要包含的檔案，請編輯專案檔並使用 `content` 屬性：</span><span class="sxs-lookup"><span data-stu-id="a4315-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="a4315-183">這會在套件根目錄中包含名稱為 `readme.txt` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="a4315-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="a4315-184">Visual Studio 會在直接安裝套件之後，立即以純文字顯示該檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a4315-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="a4315-185">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="a4315-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="a4315-186">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="a4315-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="a4315-188">只在專案根目錄新增 readme.txt，並不會導致其包含在產生的套件中。</span><span class="sxs-lookup"><span data-stu-id="a4315-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="a4315-189">相關影片</span><span class="sxs-lookup"><span data-stu-id="a4315-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="a4315-190">在[頻道 9](https://channel9.msdn.com/Series/NuGet-101)和[YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)上查找更多 NuGet 影片。</span><span class="sxs-lookup"><span data-stu-id="a4315-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="a4315-191">相關主題</span><span class="sxs-lookup"><span data-stu-id="a4315-191">Related topics</span></span>

- [<span data-ttu-id="a4315-192">建立套件</span><span class="sxs-lookup"><span data-stu-id="a4315-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="a4315-193">發佈包</span><span class="sxs-lookup"><span data-stu-id="a4315-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="a4315-194">預發行套件</span><span class="sxs-lookup"><span data-stu-id="a4315-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="a4315-195">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="a4315-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="a4315-196">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="a4315-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="a4315-197">建立本地端</span><span class="sxs-lookup"><span data-stu-id="a4315-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="a4315-198">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="a4315-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="a4315-199">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="a4315-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
