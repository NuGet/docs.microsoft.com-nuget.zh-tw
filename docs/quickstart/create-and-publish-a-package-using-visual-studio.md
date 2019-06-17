---
title: 在 Windows 上使用 Visual Studio 建立及發行 .NET Standard 套件
description: 在 Windows 上使用 Visual Studio 2017 建立及發行 .NET Standard NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812988"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="9ebb7-103">快速入門：使用 Visual Studio 建立及發行 NuGet 套件 (.NET Standard，僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="9ebb7-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="9ebb7-104">使用 CLI 工具可以輕鬆在 Windows 上從 Visual Studio 中的 .NET Standard 類別庫建立 NuGet 套件，然後將其發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="9ebb7-105">本快速入門僅適用於 Windows 版 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="9ebb7-106">Visual Studio for Mac 不包含這裡描述的功能。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="9ebb7-107">請改為使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ebb7-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-108">Prerequisites</span></span>

1. <span data-ttu-id="9ebb7-109">使用任何 .NET 相關的工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="9ebb7-110">Visual Studio 2017 會在安裝 .NET 工作負載時，自動包含 NuGet 功能。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="9ebb7-111">安裝其中一個 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="9ebb7-112">針對 `dotnet` CLI，請安裝 [.NET Core SDK](https://www.microsoft.com/net/download/)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="9ebb7-113">使用 SDK 樣式格式 (SDK 屬性) 的 .NET Standard 專案需要 dotnet CLI。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="9ebb7-114">針對 `nuget.exe` CLI，作法是從 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下載它、將該 `.exe` 檔案儲存至適當的資料夾，然後將該資料夾新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="9ebb7-115">nuget.exe CLI 是用於非 SDK 樣式格式的 .NET Standard 程式庫。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="9ebb7-116">如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-116">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="9ebb7-117">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="9ebb7-118">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="9ebb7-119">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="9ebb7-119">Create a class library project</span></span>

<span data-ttu-id="9ebb7-120">您可以針對要封裝的程式碼使用現有的 .NET Standard 類別庫專案，或建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="9ebb7-121">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]  、展開 [Visual C#] > [.NET Standard]  節點、選取 [類別庫 (.NET Standard)] 範本、將專案命名為 AppLogger，然後按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="9ebb7-122">在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置]  以確定已適當建立專案。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="9ebb7-123">DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="9ebb7-124">當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="9ebb7-125">不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="9ebb7-126">不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="9ebb7-127">除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="9ebb7-128">設定套件屬性</span><span class="sxs-lookup"><span data-stu-id="9ebb7-128">Configure package properties</span></span>

1. <span data-ttu-id="9ebb7-129">選取 [專案] > [屬性]  功能表命令，然後選取 [套件]  索引標籤。([套件]  索引標籤只會出現於 .NET Standard 類別庫專案；如果您的目標是 .NET Framework，請參閱[建立及發佈 .NET Framework 套件](create-and-publish-a-package-using-visual-studio-net-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="9ebb7-130">如果未出現在 .NET Standard 專案中，您可能需要將 Visual Studio 2017 更新至最新版本。)</span><span class="sxs-lookup"><span data-stu-id="9ebb7-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Visual Studio 專案中的 NuGet 套件屬性](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="9ebb7-132">針對公眾取用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="9ebb7-133">為套件指定唯一識別碼，並填入任何其他所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="9ebb7-134">如需不同屬性的說明，請參閱 [.nuspec 檔案參考](../reference/nuspec.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="9ebb7-135">此處的所有屬性都會移入 Visual Studio 針對專案建立的 `.nuspec` 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="9ebb7-136">您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="9ebb7-137">針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="9ebb7-138">如果您嘗試發行名稱已經存在的套件，則會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="9ebb7-139">選擇性：若要直接查看專案檔中的屬性，請以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [編輯 AppLogger.csproj]  。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="9ebb7-140">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="9ebb7-140">Run the pack command</span></span>

1. <span data-ttu-id="9ebb7-141">設定要**發行**的組態。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="9ebb7-142">在 [方案總管]  中，以滑鼠右鍵按一下專案，然後選取 [封裝]  命令：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio 專案捷徑功能表上的 NuGet 封裝命令](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="9ebb7-144">Visual Studio 會建置專案並建立 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="9ebb7-145">檢查 [輸出]  視窗以取得詳細資料 (如下所示)，其中包含套件檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="9ebb7-146">另請注意，建置的組建是位於 `bin\Release\netstandard2.0`，以適用 .NET Standard 2.0 目標。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="9ebb7-147">替代選項：使用 MSBuild 封裝</span><span class="sxs-lookup"><span data-stu-id="9ebb7-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="9ebb7-148">當專案包含必要的套件資料時，NuGet 4.x+ 和 MSBuild 15.1+ 可支援 `pack` 目標，而這是使用 [封裝]  功能表命令的另一種替代方法。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="9ebb7-149">請開啟命令提示字元，巡覽至專案資料夾並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="9ebb7-150">(若從 [開始] 功能表啟動 [適用於 Visual Studio 的開發人員命令提示字元]，其中就會設定好 MSBuild 的所有必要路徑，因此這是建議的做法。)</span><span class="sxs-lookup"><span data-stu-id="9ebb7-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="9ebb7-151">接著可在 `bin\Release` 資料夾中找到套件。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="9ebb7-152">如需 `msbuild -t:pack` 的其他選項，請參閱 [NuGet 套件和還原為 MSBuild 目標](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9ebb7-153">發行套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-153">Publish the package</span></span>

<span data-ttu-id="9ebb7-154">一旦擁有 `.nupkg` 檔案之後，您會使用 `nuget.exe` CLI 或 `dotnet.exe` CLI 以及從 nuget.org 取得的 API 金鑰，將它發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="9ebb7-155">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="9ebb7-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="9ebb7-156">使用 dotnet nuget push 發行 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="9ebb7-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="9ebb7-157">這個步驟是使用 `nuget.exe` 的替代方案。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="9ebb7-158">使用 nuget push 發行 (nuget.exe CLI)</span><span class="sxs-lookup"><span data-stu-id="9ebb7-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="9ebb7-159">這個步驟是使用 `dotnet.exe` 的替代方案。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="9ebb7-160">變更為包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="9ebb7-161">執行下列命令，指定套件名稱並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="9ebb7-162">nuget.exe 顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="9ebb7-163">請參閱 [nuget push](../tools/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="9ebb7-164">發行錯誤</span><span class="sxs-lookup"><span data-stu-id="9ebb7-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="9ebb7-165">管理已發行的套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="9ebb7-166">新增讀我檔案和其他檔案</span><span class="sxs-lookup"><span data-stu-id="9ebb7-166">Adding a readme and other files</span></span>

<span data-ttu-id="9ebb7-167">若要直接指定套件中要包含的檔案，請編輯專案檔並使用 `content` 屬性：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="9ebb7-168">這會在套件根目錄中包含名稱為 `readme.txt` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="9ebb7-169">Visual Studio 會在直接安裝套件之後，立即以純文字顯示該檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="9ebb7-170">(不會針對安裝為相依性的套件顯示讀我檔案)。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="9ebb7-171">例如，以下是 HtmlAgilityPack 套件的讀我檔案顯示方式：</span><span class="sxs-lookup"><span data-stu-id="9ebb7-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![安裝時 NuGet 套件的讀我檔案顯示](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="9ebb7-173">只在專案根目錄新增 readme.txt，並不會導致其包含在產生的套件中。</span><span class="sxs-lookup"><span data-stu-id="9ebb7-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9ebb7-174">相關主題</span><span class="sxs-lookup"><span data-stu-id="9ebb7-174">Related topics</span></span>

- [<span data-ttu-id="9ebb7-175">建立套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9ebb7-176">套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="9ebb7-177">發行前套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="9ebb7-178">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="9ebb7-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9ebb7-179">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="9ebb7-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9ebb7-180">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9ebb7-181">.NET Standard 程式庫文件</span><span class="sxs-lookup"><span data-stu-id="9ebb7-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9ebb7-182">從 .NET Framework 移轉到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="9ebb7-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
