---
title: 在 Windows 上使用 Visual Studio 建立及發行 .NET Framework NuGet 套件
description: 在 Windows 上使用 Visual Studio 建立及發佈 .NET Framework NuGet 套件的逐步解說教學課程。
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380637"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="469f5-103">快速入門：使用 Visual Studio 建立及發行套件 (.NET Framework，Windows)</span><span class="sxs-lookup"><span data-stu-id="469f5-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="469f5-104">從 .NET Framework 類別庫中建立 NuGet 套件，會涉及在 Windows 上於 Visual Studio 中建立 DLL，進而使用 nuget.exe 命令列工具來建立及發行套件。</span><span class="sxs-lookup"><span data-stu-id="469f5-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="469f5-105">此快速入門僅適用於 Visual Studio 2017 和適用於 Windows 的更高版本。</span><span class="sxs-lookup"><span data-stu-id="469f5-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="469f5-106">Visual Studio for Mac 不包含這裡描述的功能。</span><span class="sxs-lookup"><span data-stu-id="469f5-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="469f5-107">請改為使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="469f5-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="469f5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="469f5-108">Prerequisites</span></span>

1. <span data-ttu-id="469f5-109">使用任何 .NET 相關的工作負載，從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="469f5-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="469f5-110">Visual Studio 2017 會在安裝 .NET 工作負載時，自動包含 NuGet 功能。</span><span class="sxs-lookup"><span data-stu-id="469f5-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="469f5-111">安裝 `nuget.exe` CLI，作法是從 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下載它、將該 `.exe` 檔案儲存至適當的資料夾，然後將該資料夾新增至您的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="469f5-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="469f5-112">如果您還沒有帳戶，請[在 nuget.org 上註冊一個免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="469f5-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="469f5-113">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="469f5-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="469f5-114">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="469f5-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="469f5-115">建立類別庫專案</span><span class="sxs-lookup"><span data-stu-id="469f5-115">Create a class library project</span></span>

<span data-ttu-id="469f5-116">您可以對要封裝的程式碼使用現有的 .NET Framework 類別庫專案，或建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="469f5-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="469f5-117">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]\*\*\*\*，選取 [Visual C#]\*\*\*\* 節點，選取 [類別庫 (.NET Framework)] 範本，將專案命名為 AppLogger，然後按一下 [確定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="469f5-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="469f5-118">在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置]\*\*\*\* 以確定已適當建立專案。</span><span class="sxs-lookup"><span data-stu-id="469f5-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="469f5-119">DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。</span><span class="sxs-lookup"><span data-stu-id="469f5-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="469f5-120">當然，在真實的 NuGet 套件中，您會實作其他人可以用來建置應用程式的許多實用功能。</span><span class="sxs-lookup"><span data-stu-id="469f5-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="469f5-121">您也可以用任何方式設定目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="469f5-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="469f5-122">請參閱 [UWP](../guides/create-uwp-packages.md) 和 [Xamarin](../guides/create-packages-for-xamarin.md) 指南以取得指導。</span><span class="sxs-lookup"><span data-stu-id="469f5-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="469f5-123">不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。</span><span class="sxs-lookup"><span data-stu-id="469f5-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="469f5-124">不過，如果您想要為套件新增一些函式程式碼，可以使用下列方式：</span><span class="sxs-lookup"><span data-stu-id="469f5-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="469f5-125">除非您有理由選擇，否則 .NET Standard 是 NuGet 套件的慣用目標，因為它能與範圍最廣泛的取用專案相容。</span><span class="sxs-lookup"><span data-stu-id="469f5-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="469f5-126">請參閱[使用 Visual Studio 建立及發佈套件 (.NET Standard)](create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="469f5-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="469f5-127">為套件設定專案屬性</span><span class="sxs-lookup"><span data-stu-id="469f5-127">Configure project properties for the package</span></span>

<span data-ttu-id="469f5-128">NuGet 套件含有資訊清單 (`.nuspec` 檔案)，包含相關的中繼資料如套件識別碼、版本號碼、描述等等。</span><span class="sxs-lookup"><span data-stu-id="469f5-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="469f5-129">其中某些可以直接從專案屬性取得，如此就不必在專案和資訊清單中分別予以更新。</span><span class="sxs-lookup"><span data-stu-id="469f5-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="469f5-130">本章節說明應於何處設定適用的屬性。</span><span class="sxs-lookup"><span data-stu-id="469f5-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="469f5-131">選取 [專案] > [屬性]\*\*\*\* 功能表命令，然後選取 [應用程式]\*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="469f5-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="469f5-132">在 [組件名稱]\*\*\*\* 欄位中，為您的套件指定唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="469f5-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="469f5-133">您必須為套件指定識別碼，此識別碼在 nuget.org 上或您使用的任何主機上都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="469f5-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="469f5-134">針對此逐步解說，我們建議在名稱中包含 "Sample" 或 "Test" (如同稍後發行步驟所做的)，讓套件能夠成為公開可見的 (儘管實際上不太可能會有人使用它)。</span><span class="sxs-lookup"><span data-stu-id="469f5-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="469f5-135">如果您嘗試發行名稱已經存在的套件，則會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="469f5-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="469f5-136">選取 [組件資訊...]\*\*\*\* 按鈕會顯示對話方塊，您可以在其中輸入會帶入資訊清單中的其他屬性 (請參閱 [.nuspec 檔案參考 - 替代權杖](../reference/nuspec.md#replacement-tokens))。</span><span class="sxs-lookup"><span data-stu-id="469f5-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="469f5-137">最常使用的欄位是**標題**、**描述**、**公司**、**著作權** 和 **組件版本**。</span><span class="sxs-lookup"><span data-stu-id="469f5-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="469f5-138">這些屬性最後會在主機上 (例如 nuget.org) 與您的套件一起顯示，因此請確認屬性的描述完整。</span><span class="sxs-lookup"><span data-stu-id="469f5-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio 中 .NET Framework 專案的組件資訊](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="469f5-140">選擇性：若要查看並直接編輯屬性，請開啟專案中的 `Properties/AssemblyInfo.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="469f5-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="469f5-141">設定屬性後，請將專案組態設定為**發行**並重建專案以產生更新的 DLL。</span><span class="sxs-lookup"><span data-stu-id="469f5-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="469f5-142">產生初始資訊清單</span><span class="sxs-lookup"><span data-stu-id="469f5-142">Generate the initial manifest</span></span>

<span data-ttu-id="469f5-143">有了 DLL，並完成專案屬性設定後，請使用 `nuget spec` 命令從專案中產生初始的 `.nuspec` 檔案。</span><span class="sxs-lookup"><span data-stu-id="469f5-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="469f5-144">這個步驟包含了相關的取代權杖，以從專案檔中取出資訊。</span><span class="sxs-lookup"><span data-stu-id="469f5-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="469f5-145">僅執行 `nuget spec` 一次即可產生初始的資訊清單。</span><span class="sxs-lookup"><span data-stu-id="469f5-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="469f5-146">更新套件時，請在專案中變更值或直接編輯資訊清單。</span><span class="sxs-lookup"><span data-stu-id="469f5-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="469f5-147">開啟命令提示字元並巡覽至包含 `AppLogger.csproj` 檔案的專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="469f5-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="469f5-148">執行下列命令：`nuget spec AppLogger.csproj`。</span><span class="sxs-lookup"><span data-stu-id="469f5-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="469f5-149">藉由指定專案，NuGet 會建立符合專案名稱的資訊清單，在此情況下為 `AppLogger.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="469f5-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="469f5-150">另外也會包含資訊清單中的取代權杖。</span><span class="sxs-lookup"><span data-stu-id="469f5-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="469f5-151">在文字編輯器中開啟 `AppLogger.nuspec` 來檢視其內容，應如下所示：</span><span class="sxs-lookup"><span data-stu-id="469f5-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="469f5-152">編輯資訊清單</span><span class="sxs-lookup"><span data-stu-id="469f5-152">Edit the manifest</span></span>

1. <span data-ttu-id="469f5-153">如果您嘗試使用 `.nuspec` 檔案中的預設值來建立套件，NuGet 會產生錯誤，因此您必須編輯下列欄位後再繼續。</span><span class="sxs-lookup"><span data-stu-id="469f5-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="469f5-154">如需如何使用這些項目的描述，請參閱 [.nuspect 檔案參考 - 選擇性中繼資料元素](../reference/nuspec.md#optional-metadata-elements)。</span><span class="sxs-lookup"><span data-stu-id="469f5-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="469f5-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="469f5-155">licenseUrl</span></span>
    - <span data-ttu-id="469f5-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="469f5-156">projectUrl</span></span>
    - <span data-ttu-id="469f5-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="469f5-157">iconUrl</span></span>
    - <span data-ttu-id="469f5-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="469f5-158">releaseNotes</span></span>
    - <span data-ttu-id="469f5-159">tags</span><span class="sxs-lookup"><span data-stu-id="469f5-159">tags</span></span>

1. <span data-ttu-id="469f5-160">對於為供公開使用而建置的套件，請特別注意 **Tags** 屬性，因為標籤可協助其他人在 nuget.org 之類的來源上找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="469f5-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="469f5-161">您也可同時在資訊清單新增任何其他項目，如 [.nuspec 檔案參考](../reference/nuspec.md)所述。</span><span class="sxs-lookup"><span data-stu-id="469f5-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="469f5-162">儲存檔案後再繼續。</span><span class="sxs-lookup"><span data-stu-id="469f5-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="469f5-163">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="469f5-163">Run the pack command</span></span>

1. <span data-ttu-id="469f5-164">從包含 `.nuspec` 檔案之資料夾中的命令提示字元，執行命令 `nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="469f5-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="469f5-165">NuGet 會以 *identifier-version.nupkg* 的形式產生 `.nupkg` 檔案，可在目前的資料夾中找到。</span><span class="sxs-lookup"><span data-stu-id="469f5-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="469f5-166">發行套件</span><span class="sxs-lookup"><span data-stu-id="469f5-166">Publish the package</span></span>

<span data-ttu-id="469f5-167">擁有`.nupkg`檔案後,將該檔發布到nuget.org`nuget.exe`使用 從nuget.org獲取的 API 金鑰。對於nuget.org您必須使用`nuget.exe`4.1.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="469f5-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="469f5-168">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="469f5-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="469f5-169">使用 nuget push 發行</span><span class="sxs-lookup"><span data-stu-id="469f5-169">Publish with nuget push</span></span>

1. <span data-ttu-id="469f5-170">開啟命令列並變更到包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="469f5-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="469f5-171">執行下列命令，指定套件名稱並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="469f5-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="469f5-172">nuget.exe 顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="469f5-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="469f5-173">請參閱 [nuget push](../reference/cli-reference/cli-ref-push.md)。</span><span class="sxs-lookup"><span data-stu-id="469f5-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="469f5-174">發行錯誤</span><span class="sxs-lookup"><span data-stu-id="469f5-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="469f5-175">管理已發行的套件</span><span class="sxs-lookup"><span data-stu-id="469f5-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="469f5-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="469f5-176">Next steps</span></span>

<span data-ttu-id="469f5-177">恭喜，您建立了您的第一個 NuGet 套件！</span><span class="sxs-lookup"><span data-stu-id="469f5-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="469f5-178">建立套件</span><span class="sxs-lookup"><span data-stu-id="469f5-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="469f5-179">若要深入探索 NuGet 所提供的功能，請選取下列連結。</span><span class="sxs-lookup"><span data-stu-id="469f5-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="469f5-180">發佈包</span><span class="sxs-lookup"><span data-stu-id="469f5-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="469f5-181">預發行套件</span><span class="sxs-lookup"><span data-stu-id="469f5-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="469f5-182">支援多個目標 Framework</span><span class="sxs-lookup"><span data-stu-id="469f5-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="469f5-183">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="469f5-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="469f5-184">建立本地端</span><span class="sxs-lookup"><span data-stu-id="469f5-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
