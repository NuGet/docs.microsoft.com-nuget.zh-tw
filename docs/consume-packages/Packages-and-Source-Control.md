---
title: NuGet 套件和原始檔控制
description: 如何在版本設定和原始檔控制系統內處理 NuGet 套件的考量，以及如何以 git 和 TFVC 省略套件。
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 0338c3445b2a3d8169158171d97d1e874533a80a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551795"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="42986-103">在原始檔控制系統中省略 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="42986-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="42986-104">開發人員通常會省略其原始檔控制存放庫的 NuGet 套件，改為依賴[套件還原](package-restore.md)先重新安裝專案的相依性再建置。</span><span class="sxs-lookup"><span data-stu-id="42986-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="42986-105">依賴套件還原的原因包括：</span><span class="sxs-lookup"><span data-stu-id="42986-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="42986-106">分散式版本設定系統，例如 Git，包含存放庫內每個檔案每個版本的完整複本。</span><span class="sxs-lookup"><span data-stu-id="42986-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="42986-107">經常更新的二進位檔案會導致明顯膨脹，並會增加複製存放庫所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="42986-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="42986-108">當套件包含在存放庫中時，開發人員傾向直接參考磁碟上的套件內容，而不是透過 NuGet 參考套件，這會導致專案中的硬式編碼路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="42986-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="42986-109">清除任何未使用過的套件資料夾的解決方案會變得愈來愈困難，因為需要確保不刪除仍在使用的任何套件。</span><span class="sxs-lookup"><span data-stu-id="42986-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="42986-110">透過略過套件的方式，維護程式碼和來自其他相依人員的套件之間的清楚擁有權界限。</span><span class="sxs-lookup"><span data-stu-id="42986-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="42986-111">許多 NuGet 套件已在自己的原始檔控制存放庫中進行維護。</span><span class="sxs-lookup"><span data-stu-id="42986-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="42986-112">雖然套件還原是 NuGet 的預設行為，但仍需某些手動工作從原始檔控制省略套件，&mdash;也就是專案中的 `packages` 資料夾&mdash;，如本文所述。</span><span class="sxs-lookup"><span data-stu-id="42986-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="42986-113">使用 Git 省略套件</span><span class="sxs-lookup"><span data-stu-id="42986-113">Omitting packages with Git</span></span>

<span data-ttu-id="42986-114">使用 [.gitignore 檔案](https://git-scm.com/docs/gitignore)略過 NuGet 套件 (`.nupkg`) `packages` 資料夾，以及 `project.assets.json` 和其他項目。</span><span class="sxs-lookup"><span data-stu-id="42986-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="42986-115">如需參考，請參閱 [Visual Studio 專案的範例 `.gitignore`](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)：</span><span class="sxs-lookup"><span data-stu-id="42986-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="42986-116">`.gitignore` 檔案的重要部分為：</span><span class="sxs-lookup"><span data-stu-id="42986-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="42986-117">使用 Team Foundation 版本設定略過套件</span><span class="sxs-lookup"><span data-stu-id="42986-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="42986-118">如果可能，請先遵循下列指示再將專案新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="42986-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="42986-119">否則，請手動刪除存放庫的 `packages` 資料夾，並先簽入該變更再繼續。</span><span class="sxs-lookup"><span data-stu-id="42986-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="42986-120">停用原始檔控制與所選檔案的 TFVC 整合：</span><span class="sxs-lookup"><span data-stu-id="42986-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="42986-121">在解決方案資料夾 (`.sln` 檔案所在的資料夾) 中建立名為 `.nuget` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="42986-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="42986-122">提示：在 Windows 中，在 Windows 檔案總管中建立這個資料夾，要使用名稱 `.nuget.`「加」結尾後置點。</span><span class="sxs-lookup"><span data-stu-id="42986-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="42986-123">在該資料夾中，建立名為 `NuGet.Config` 的檔案，再開啟進行編輯。</span><span class="sxs-lookup"><span data-stu-id="42986-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="42986-124">新增下列文字作為最小值，其中 [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) 設定會指示 Visual Studio 略過 `packages` 資料夾中的所有內容：</span><span class="sxs-lookup"><span data-stu-id="42986-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="42986-125">如果您使用的是 TFS 2010 或更舊的版本，請隱匿工作區對應中的 `packages` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="42986-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="42986-126">在 TFS 2012 或更新版本，或使用 Visual Studio Team Services 的版本上，依[新增檔案到伺服器](/vsts/tfvc/add-files-server.md?view=vsts#tfignore)所述建立 `.tfignore` 檔案。</span><span class="sxs-lookup"><span data-stu-id="42986-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="42986-127">在該檔案中納入以下內容，明確忽略在存放庫層級和其他幾個中繼檔案中對 `\packages` 資料夾的修改。</span><span class="sxs-lookup"><span data-stu-id="42986-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="42986-128">(您可以在 Windows 檔案總管中，使用 `.tfignore.` 加結尾後置點的名稱來建立檔案，但可能需要先停用 [Hide known file extensions] \(隱藏已知副檔名) 選項。)：</span><span class="sxs-lookup"><span data-stu-id="42986-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="42986-129">將 `NuGet.Config` 和 `.tfignore` 新增至原始檔控制，並簽入變更。</span><span class="sxs-lookup"><span data-stu-id="42986-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
