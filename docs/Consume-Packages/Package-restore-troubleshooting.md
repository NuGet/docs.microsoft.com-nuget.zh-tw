---
title: 針對 Visual Studio 中的 NuGet 套件還原進行疑難排解 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Visual Studio 中常見的 NuGet 還原錯誤描述，以及如何針對這些錯誤進行疑難排解。
keywords: NuGet 套件還原, 還原套件, 進行疑難排解, 疑難排解
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="92416-104">對套件還原錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="92416-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="92416-105">本文著重於還原套件時常見的錯誤及其解決步驟。</span><span class="sxs-lookup"><span data-stu-id="92416-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="92416-106">如需還原套件的完整詳細資料，請參閱[套件還原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="92416-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="92416-107">如果此處的指示不適用於您的情況，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，讓我們能更仔細審視您的案例。</span><span class="sxs-lookup"><span data-stu-id="92416-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="92416-108">請勿使用可能出現在本頁面的「本頁對您有幫助嗎？」</span><span class="sxs-lookup"><span data-stu-id="92416-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="92416-109">控制項，因為這無法讓我們與您連絡以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="92416-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="92416-110">適用於 Visual Studio 使用者的快速解決方案</span><span class="sxs-lookup"><span data-stu-id="92416-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="92416-111">如果您使用 Visual Studio，請先以下列方式啟用套件還原。</span><span class="sxs-lookup"><span data-stu-id="92416-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="92416-112">否則，請繼續瀏覽後續各節。</span><span class="sxs-lookup"><span data-stu-id="92416-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="92416-113">選取 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="92416-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="92416-114">設定 [套件還原] 下的兩個選項。</span><span class="sxs-lookup"><span data-stu-id="92416-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="92416-115">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="92416-115">Select **OK**.</span></span>
1. <span data-ttu-id="92416-116">再次建置您的專案。</span><span class="sxs-lookup"><span data-stu-id="92416-116">Build your project again.</span></span>

![在 [工具/選項] 中啟用 NuGet 套件還原](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="92416-118">這些設定也可以在您的 `NuGet.config` 檔案中變更；請參閱[同意](#consent)一節。</span><span class="sxs-lookup"><span data-stu-id="92416-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="92416-119">此專案參考的 NuGet 套件不在這部電腦上</span><span class="sxs-lookup"><span data-stu-id="92416-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="92416-120">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="92416-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="92416-121">當您嘗試建置包含一或多個 NuGet 套件參考的專案，但這些套件目前並未在電腦上或專案中安裝時，就會發生這項錯誤。</span><span class="sxs-lookup"><span data-stu-id="92416-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="92416-122">使用 PackageReference 管理格式時，此錯誤表示套件並未如[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述安裝在 *global-packages* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="92416-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="92416-123">當使用 `packages.config` 時，此錯誤表示套件並未安裝在解決方案跟目錄的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="92416-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="92416-124">當您從原始檔控制或另一個下載處取得專案的原始程式碼時，通常就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="92416-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="92416-125">套件通常會從原始檔控制或下載中省略，因為可以從類似 nuget.org 的套件摘要中還原 (請參閱[套件和原始檔控制](Packages-and-Source-Control.md))。</span><span class="sxs-lookup"><span data-stu-id="92416-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="92416-126">包含套件反而會使存放庫膨脹，或建立不必要的大型 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="92416-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="92416-127">請使用下列其中一種方法來還原套件：</span><span class="sxs-lookup"><span data-stu-id="92416-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="92416-128">在 Visual Studio 中，選取 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令，設定 [套件還原] 下的兩個選項，然後選取 [確定]，以啟用套件還原。</span><span class="sxs-lookup"><span data-stu-id="92416-128">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="92416-129">然後再次建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="92416-129">Then build the solution again.</span></span>
- <span data-ttu-id="92416-130">若是 .NET Core 專案，請執行 `dotnet restore` 或 `dotnet build` (會自動執行還原)。</span><span class="sxs-lookup"><span data-stu-id="92416-130">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="92416-131">在命令列上執行 `nuget restore` (除了以 `dotnet` 建立的專案在此情況下會使用 `dotnet restore`)。</span><span class="sxs-lookup"><span data-stu-id="92416-131">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="92416-132">對於使用 PackageReference 格式的專案，在命令列上執行 `msbuild /t:restore`。</span><span class="sxs-lookup"><span data-stu-id="92416-132">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="92416-133">成功還原之後，套件應該存在於 *global-packages* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="92416-133">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="92416-134">對於使用 PackageReference 的專案，還原應重新建立 `obj/project.assets.json` 檔案；針對使用 `packages.config` 的專案，套件應該會出現在專案的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="92416-134">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="92416-135">專案現在應可順利建置。</span><span class="sxs-lookup"><span data-stu-id="92416-135">The project should now build successfully.</span></span> <span data-ttu-id="92416-136">如果沒有，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們與您連絡。</span><span class="sxs-lookup"><span data-stu-id="92416-136">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="92416-137">找不到資產檔案 project.assets.json</span><span class="sxs-lookup"><span data-stu-id="92416-137">Assets file project.assets.json not found</span></span>

<span data-ttu-id="92416-138">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="92416-138">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="92416-139">當使用 PackageReference 管理格式時，`project.assets.json` 檔案會維護專案的相依性關係圖，此圖是用來確認電腦上已安裝所有必要套件的。</span><span class="sxs-lookup"><span data-stu-id="92416-139">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="92416-140">因為此檔案是透過套件還原動態產生的，因此通常不會新增到原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="92416-140">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="92416-141">因此當使用不會自動還原套件的 `msbuild` 之類的工具建立專案時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="92416-141">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="92416-142">在此情況下，請在執行 `msbuild /t:restore` 後接著執行 `msbuild`，或使用 `dotnet build` (會自動還原套件)。</span><span class="sxs-lookup"><span data-stu-id="92416-142">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="92416-143">您也可以使用[上一節](#missing)中的任何一個套件還原方法。</span><span class="sxs-lookup"><span data-stu-id="92416-143">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="92416-144">有一或多個 NuGet 套件必須還原，但因為未獲得同意而無法還原</span><span class="sxs-lookup"><span data-stu-id="92416-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="92416-145">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="92416-145">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="92416-146">此錯誤指出您的 NuGet 組態已停用套件還原。</span><span class="sxs-lookup"><span data-stu-id="92416-146">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="92416-147">您可以在 Visual Studio 中變更適用的設定，如先前在[適用於 Visual Studio 使用者的快速解決方案](#quick-solution-for-visual-studio-users)所述。</span><span class="sxs-lookup"><span data-stu-id="92416-147">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="92416-148">您也可以直接在適用的 `nuget.config` 檔案上編輯這些設定 (在 Windows 上通常為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。</span><span class="sxs-lookup"><span data-stu-id="92416-148">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="92416-149">請確認 `packageRestore` 底下的 `enabled` 和 `automatic` 金鑰設定為 True：</span><span class="sxs-lookup"><span data-stu-id="92416-149">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="92416-150">如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="92416-150">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="92416-151">其他可能的情況</span><span class="sxs-lookup"><span data-stu-id="92416-151">Other potential conditions</span></span>

- <span data-ttu-id="92416-152">您可能會因為遺失檔案而遇到建置錯誤，會有訊息指出應使用 NuGet 還原加以下載。</span><span class="sxs-lookup"><span data-stu-id="92416-152">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="92416-153">不過，執行還原時有可能會顯示「所有套件均已安裝，沒有可還原的項目」。</span><span class="sxs-lookup"><span data-stu-id="92416-153">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="92416-154">在此情況下，請刪除 `packages` 資料夾 (使用 `packages.config` 時) 或 `obj/project.assets.json` 檔案 (使用 PackageReference 時)，並再次執行還原。</span><span class="sxs-lookup"><span data-stu-id="92416-154">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="92416-155">如果錯誤持續發生，請從命令列使用 `nuget locals all -clear` 或 `dotnet locals all --clear` 以清除 *global-packages* 和快取資料夾，如[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="92416-155">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="92416-156">從原始檔控制取得專案時，您的專案資料夾可能會設定成唯讀。</span><span class="sxs-lookup"><span data-stu-id="92416-156">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="92416-157">請變更資料夾的權限，然後再次嘗試還原套件。</span><span class="sxs-lookup"><span data-stu-id="92416-157">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="92416-158">您使用的可能是舊版 NuGet。</span><span class="sxs-lookup"><span data-stu-id="92416-158">You may be using an old version of NuGet.</span></span> <span data-ttu-id="92416-159">請查看 [nuget.org/downloads](https://www.nuget.org/downloads) 以取得最新的建議版本。</span><span class="sxs-lookup"><span data-stu-id="92416-159">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="92416-160">若是 Visual Studio 2015，建議使用 3.6.0。</span><span class="sxs-lookup"><span data-stu-id="92416-160">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="92416-161">如果您遇到其他問題，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們向您取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="92416-161">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>