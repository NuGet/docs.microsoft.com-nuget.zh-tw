---
title: "建立和發行 NuGet 套件的入門指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "逐步解說教學課程，說明使用 nuget.exe 命令列介面和 Visual Studio 建立和發行 NuGet 套件。"
keywords: "NuGet 套件建立, NuGet 套件發行, NuGet 教學課程"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ab5235537d869047075b93f9d8255ae9e61dfedd
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="91134-104">建立及發行套件</span><span class="sxs-lookup"><span data-stu-id="91134-104">Create and publish a package</span></span>

<span data-ttu-id="91134-105">從 .NET 類別庫建立 NuGet 套件，並將它發行到 nuget.org 是個簡單的程序。下列步驟會引導您完成使用 NuGet 命令列介面 (CLI) 和 Visual Studio 的程序：</span><span class="sxs-lookup"><span data-stu-id="91134-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="91134-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="91134-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="91134-107">建立 .nuspec 套件資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="91134-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="91134-108">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="91134-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="91134-109">發行套件</span><span class="sxs-lookup"><span data-stu-id="91134-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="91134-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91134-110">Pre-requisites</span></span>

1. <span data-ttu-id="91134-111">從 [visualstudio.com](https://www.visualstudio.com/) 安裝任何版本的 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="91134-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="91134-112">從 [nuget.org/downloads](https://nuget.org/downloads) 下載最新版 `nuget.exe`，並將 `.exe` 儲存到您 PATH 中的位置，以安裝 NuGet CLI 工具 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="91134-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="91134-113">請注意，下載「是」工具本身，而非安裝程式。</span><span class="sxs-lookup"><span data-stu-id="91134-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="91134-114">為您想要封裝的程式碼建立適當的 .NET 類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="91134-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="91134-115">如果您還沒有專案，您可以建立一個簡單的專案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="91134-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="91134-116">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]，依序展開 [Visual C#] > [Windows] 節點、選取 [類別庫] 範本、將專案命名為 AppLogger，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="91134-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="91134-117">在產生的專案檔上按一下滑鼠右鍵，然後選取 [建置] 以確定已適當建立專案。</span><span class="sxs-lookup"><span data-stu-id="91134-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="91134-118">DLL 位於 Debug 資料夾 (如果您改為建置該組態則為 Release)。</span><span class="sxs-lookup"><span data-stu-id="91134-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="91134-119">當然，在真實的 NuGet 套件中，您將實作其他人可以用來建置應用程式的許多實用功能。</span><span class="sxs-lookup"><span data-stu-id="91134-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="91134-120">不過，對於此逐步解說，您將不會撰寫任何額外的程式碼，因為來自範本的類別庫已足夠建立套件。</span><span class="sxs-lookup"><span data-stu-id="91134-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="91134-121">建立 .nuspec 套件資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="91134-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="91134-122">每個 NuGet 套件需要資訊清單&mdash;`.nuspec` 檔案&mdash;來描述其內容和其相依性。</span><span class="sxs-lookup"><span data-stu-id="91134-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="91134-123">`nuget spec` 命令會為您建立此檔案，然後您可以自訂。</span><span class="sxs-lookup"><span data-stu-id="91134-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="91134-124">在此範例中，您從專案檔建立 `.nuspec`，您也可以透過其他方式建立資訊清單，如[建立套件](../create-packages/creating-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="91134-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="91134-125">開啟命令提示字元並巡覽至包含您專案檔的資料夾 (`.csproj`)。</span><span class="sxs-lookup"><span data-stu-id="91134-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="91134-126">執行 NuGet CLI `spec` 命令以產生資訊清單，它會以您的專案來命名，例如 `AppLogger.nuspec`：</span><span class="sxs-lookup"><span data-stu-id="91134-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="91134-127">在文字編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="91134-127">Open the file in a text editor.</span></span> <span data-ttu-id="91134-128">資訊清單看起來類似下列程式碼，其中 `<token>` 格式的權杖 (例如 `$id$`) 會在封裝程序期間取代為來自專案 Properties/AssemblyInfo.cs 檔案的值。</span><span class="sxs-lookup"><span data-stu-id="91134-128">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="91134-129">如需語彙基元的詳細資料，請參閱[建立 .nuspec 檔案](../create-packages/creating-a-package.md#creating-the-nuspec-file)。</span><span class="sxs-lookup"><span data-stu-id="91134-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="91134-130">選取在 nuget.org 中唯一的套件識別碼。我們建議使用[建立套件](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中描述的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="91134-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="91134-131">請務必更新作者和描述標記，否則您會在下一個步驟中收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="91134-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="91134-132">以下是更新的 `.nuspec` 檔案範例：</span><span class="sxs-lookup"><span data-stu-id="91134-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="91134-133">針對公眾使用而建置的套件，請特別注意 `<tags>` 項目，因為這些標籤可協助其他人找到您的套件，並了解其用途。</span><span class="sxs-lookup"><span data-stu-id="91134-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="91134-134">執行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="91134-134">Run the pack command</span></span>

<span data-ttu-id="91134-135">若要從專案建置 NuGet 套件 (`.nupkg` 檔案)，請執行 `pack` 命令：</span><span class="sxs-lookup"><span data-stu-id="91134-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="91134-136">此命令會使用來自 `.nuspec` 檔案的套件名稱和版本號碼，建立 `AppLogger.1.0.0.0.nupkg`。</span><span class="sxs-lookup"><span data-stu-id="91134-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="91134-137">如果您尚未更新 `.nuspec` 檔案中各種欄位的預設值，此命令會發出警告。</span><span class="sxs-lookup"><span data-stu-id="91134-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="91134-138">發行套件</span><span class="sxs-lookup"><span data-stu-id="91134-138">Publish the package</span></span>

<span data-ttu-id="91134-139">一旦您有 `.nupkg` 檔案，請使用 `push` 命令將它發行到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="91134-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="91134-140">(或者，您可以使用 [nuget.org 發行工作流程](../create-packages/publish-a-package.md#publish-to-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="91134-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="91134-141">您發行至 nuget.org 的套件可以讓其他開發人員公開看見。</span><span class="sxs-lookup"><span data-stu-id="91134-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="91134-142">若要私下裝載套件，請參閱[裝載套件](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="91134-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="91134-143">在 [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) 上建立免費帳戶，如果您已有帳戶則請登入。</span><span class="sxs-lookup"><span data-stu-id="91134-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="91134-144">建立新的帳戶會傳送一封確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="91134-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="91134-145">您必須確認帳戶，才可以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="91134-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="91134-146">登入之後，選取您的使用者名稱 (在右上方)，然後選取 [API 金鑰]。</span><span class="sxs-lookup"><span data-stu-id="91134-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="91134-147">選取 [建立]、提供您的金鑰名稱、選取 [API 金鑰] 下的 [選取範圍] > [推送]針對 [Glob 模式] 輸入 \*，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="91134-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="91134-148">建立金鑰之後，選取 [複製] 以擷取 CLI 中您需要的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="91134-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![將 API 金鑰複製到剪貼簿](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="91134-150">將您的金鑰儲存在安全的位置，並保守祕密。</span><span class="sxs-lookup"><span data-stu-id="91134-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="91134-151">如果意外洩漏您的金鑰，您一律可以隨時重新產生它。</span><span class="sxs-lookup"><span data-stu-id="91134-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="91134-152">如果您不再想要透過 CLI 推送套件，也可以移除 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="91134-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="91134-153">在命令提示字元中執行下列命令，指定套件名稱並將金鑰取代為在步驟 4 中複製的值：</span><span class="sxs-lookup"><span data-stu-id="91134-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="91134-154">nuget.exe 顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="91134-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="91134-155">從您在 nuget.org 上的設定檔，選取 [管理套件] 以查看您剛發行的套件。</span><span class="sxs-lookup"><span data-stu-id="91134-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="91134-156">您也會收到確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="91134-156">You also receive a confirmation email.</span></span> <span data-ttu-id="91134-157">請注意，可能需要一些時間才會編製套件的索引，並顯示在其他人可以找到它的搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="91134-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="91134-158">在這段期間，套件頁面會顯示下列訊息：</span><span class="sxs-lookup"><span data-stu-id="91134-158">During that time your package page shows the message below:</span></span>

    ![此套件尚未編製索引。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="91134-161">**病毒掃描**：會掃描所有上傳至 nuget.org 的套件是否有病毒，並在發現任何病毒時予以拒絕。</span><span class="sxs-lookup"><span data-stu-id="91134-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="91134-162">也會定期掃描 nuget.org 上列出的所有套件。</span><span class="sxs-lookup"><span data-stu-id="91134-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="91134-163">就是這麼容易！</span><span class="sxs-lookup"><span data-stu-id="91134-163">And that's it!</span></span> <span data-ttu-id="91134-164">您剛已將第一個 NuGet 套件發行至 [nuget.org](https://www.nuget.org/)，其他開發人員可以在他們自己的專案中使用它。</span><span class="sxs-lookup"><span data-stu-id="91134-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="91134-165">相關主題</span><span class="sxs-lookup"><span data-stu-id="91134-165">Related topics</span></span>

- [<span data-ttu-id="91134-166">建立套件</span><span class="sxs-lookup"><span data-stu-id="91134-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="91134-167">發行套件</span><span class="sxs-lookup"><span data-stu-id="91134-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="91134-168">支援多個目標架構</span><span class="sxs-lookup"><span data-stu-id="91134-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="91134-169">套件版本控制</span><span class="sxs-lookup"><span data-stu-id="91134-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="91134-170">建立當地語系化的套件</span><span class="sxs-lookup"><span data-stu-id="91134-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
