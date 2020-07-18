---
title: 針對 Visual Studio 中的 NuGet 套件還原進行疑難排解
description: Visual Studio 中常見的 NuGet 還原錯誤描述，以及如何針對這些錯誤進行疑難排解。
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b162990eae2160961f560b6c6ee73e47cb4121d6
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451147"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="24ceb-103">對套件還原錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="24ceb-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="24ceb-104">本文著重於還原套件時常見的錯誤及其解決步驟。</span><span class="sxs-lookup"><span data-stu-id="24ceb-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="24ceb-105">套件還原會嘗試將所有套件相依性安裝到符合專案檔 (*.csproj*) 或您的 *packages.config* 檔案中套件參考的正確狀態。</span><span class="sxs-lookup"><span data-stu-id="24ceb-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="24ceb-106">（在 Visual Studio 中，參考會出現在 [相依性**\ NuGet]** 或 [**參考**] 節點下的方案總管中）。若要遵循還原套件所需的步驟，請參閱[還原封裝](../consume-packages/package-restore.md#restore-packages)。</span><span class="sxs-lookup"><span data-stu-id="24ceb-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="24ceb-107">如果專案檔 (*.csproj*) 或您的 *packages.config* 檔案中的套件參考不正確 (不符合您在套件還原之後所需的狀態)，則您需要安裝套件或更新套件，而不是使用套件還原。</span><span class="sxs-lookup"><span data-stu-id="24ceb-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="24ceb-108">如果此處的指示不適用於您的情況，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，讓我們能更仔細審視您的案例。</span><span class="sxs-lookup"><span data-stu-id="24ceb-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="24ceb-109">請勿使用可能出現在本頁面的「本頁對您有幫助嗎？」</span><span class="sxs-lookup"><span data-stu-id="24ceb-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="24ceb-110">控制項，因為這無法讓我們與您連絡以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="24ceb-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="24ceb-111">適用於 Visual Studio 使用者的快速解決方案</span><span class="sxs-lookup"><span data-stu-id="24ceb-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="24ceb-112">如果您使用 Visual Studio，請先以下列方式啟用套件還原。</span><span class="sxs-lookup"><span data-stu-id="24ceb-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="24ceb-113">否則，請繼續瀏覽後續各節。</span><span class="sxs-lookup"><span data-stu-id="24ceb-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="24ceb-114">選取 [工具] > [NuGet 套件管理員] > [套件管理員設定]\*\*\*\* 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="24ceb-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="24ceb-115">設定 [套件還原]\*\*\*\* 下的兩個選項。</span><span class="sxs-lookup"><span data-stu-id="24ceb-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="24ceb-116">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="24ceb-116">Select **OK**.</span></span>
1. <span data-ttu-id="24ceb-117">再次建置您的專案。</span><span class="sxs-lookup"><span data-stu-id="24ceb-117">Build your project again.</span></span>

![在 [工具/選項] 中啟用 NuGet 套件還原](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="24ceb-119">這些設定也可以在您的 `NuGet.config` 檔案中變更；請參閱[同意](#consent)一節。</span><span class="sxs-lookup"><span data-stu-id="24ceb-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="24ceb-120">如果您的專案是使用整合 MSBuild 套件還原的舊版專案，您可能需要[遷移](package-restore.md#migrate-to-automatic-package-restore-visual-studio)至自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="24ceb-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="24ceb-121">此專案參考的 NuGet 套件不在這部電腦上</span><span class="sxs-lookup"><span data-stu-id="24ceb-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="24ceb-122">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="24ceb-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="24ceb-123">當您嘗試建置包含一或多個 NuGet 套件參考的專案，但這些套件目前並未安裝在電腦上或位於專案中時，就會發生這項錯誤。</span><span class="sxs-lookup"><span data-stu-id="24ceb-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="24ceb-124">使用[PackageReference](package-references-in-project-files.md)管理格式時，錯誤表示封裝未安裝在 [*全域套件*] 資料夾中，如[管理全域套件和](managing-the-global-packages-and-cache-folders.md)快取資料夾中所述。</span><span class="sxs-lookup"><span data-stu-id="24ceb-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="24ceb-125">當使用 [packages.config](../reference/packages-config.md) 時，此錯誤表示套件並未安裝在解決方案根目錄的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="24ceb-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="24ceb-126">當您從原始檔控制或另一個下載處取得專案的原始程式碼時，通常就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="24ceb-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="24ceb-127">套件通常會從原始檔控制或下載中省略，因為可以從類似 nuget.org 的套件摘要中還原 (請參閱[套件和原始檔控制](Packages-and-Source-Control.md))。</span><span class="sxs-lookup"><span data-stu-id="24ceb-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="24ceb-128">包含套件反而會使存放庫膨脹，或建立不必要的大型 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="24ceb-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="24ceb-129">如果您的專案檔包含套件位置的絕對路徑，而您又移動了專案，也會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="24ceb-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="24ceb-130">請使用下列其中一種方法來還原套件：</span><span class="sxs-lookup"><span data-stu-id="24ceb-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="24ceb-131">如果您移動了專案檔，請直接編輯檔案以更新套件參考。</span><span class="sxs-lookup"><span data-stu-id="24ceb-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="24ceb-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([自動還原](package-restore.md#restore-packages-automatically-using-visual-studio)或[手動還原](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="24ceb-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="24ceb-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="24ceb-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="24ceb-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="24ceb-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="24ceb-135">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="24ceb-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="24ceb-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="24ceb-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="24ceb-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="24ceb-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="24ceb-138">成功還原之後，套件應該存在於 *global-packages* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="24ceb-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="24ceb-139">對於使用 PackageReference 的專案，還原應重新建立 `obj/project.assets.json` 檔案；針對使用 `packages.config` 的專案，套件應該會出現在專案的 `packages` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="24ceb-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="24ceb-140">專案現在應可順利建置。</span><span class="sxs-lookup"><span data-stu-id="24ceb-140">The project should now build successfully.</span></span> <span data-ttu-id="24ceb-141">如果沒有，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們與您連絡。</span><span class="sxs-lookup"><span data-stu-id="24ceb-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="24ceb-142">找不到資產檔案 project.assets.json</span><span class="sxs-lookup"><span data-stu-id="24ceb-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="24ceb-143">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="24ceb-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="24ceb-144">當使用 PackageReference 管理格式時，`project.assets.json` 檔案會維護專案的相依性關係圖，此圖是用來確認電腦上已安裝所有必要套件的。</span><span class="sxs-lookup"><span data-stu-id="24ceb-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="24ceb-145">因為此檔案是透過套件還原動態產生的，因此通常不會新增到原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="24ceb-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="24ceb-146">因此當使用不會自動還原套件的 `msbuild` 之類的工具建立專案時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="24ceb-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="24ceb-147">在此情況下，請在執行 `msbuild -t:restore` 後接著執行 `msbuild`，或使用 `dotnet build` (會自動還原套件)。</span><span class="sxs-lookup"><span data-stu-id="24ceb-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="24ceb-148">您也可以使用[上一節](#missing)中的任何一個套件還原方法。</span><span class="sxs-lookup"><span data-stu-id="24ceb-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="24ceb-149">有一或多個 NuGet 套件必須還原，但因為未獲得同意而無法還原</span><span class="sxs-lookup"><span data-stu-id="24ceb-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="24ceb-150">完整的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="24ceb-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="24ceb-151">此錯誤指出您的 NuGet 組態已停用套件還原。</span><span class="sxs-lookup"><span data-stu-id="24ceb-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="24ceb-152">您可以在 Visual Studio 中變更適用的設定，如先前在[適用於 Visual Studio 使用者的快速解決方案](#quick-solution-for-visual-studio-users)所述。</span><span class="sxs-lookup"><span data-stu-id="24ceb-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="24ceb-153">您也可以直接在適用的 `nuget.config` 檔案上編輯這些設定 (在 Windows 上通常為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。</span><span class="sxs-lookup"><span data-stu-id="24ceb-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="24ceb-154">請確認 `packageRestore` 底下的 `enabled` 和 `automatic` 金鑰設定為 True：</span><span class="sxs-lookup"><span data-stu-id="24ceb-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="24ceb-155">如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。</span><span class="sxs-lookup"><span data-stu-id="24ceb-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="24ceb-156">其他可能的情況</span><span class="sxs-lookup"><span data-stu-id="24ceb-156">Other potential conditions</span></span>

- <span data-ttu-id="24ceb-157">您可能會因為遺失檔案而遇到建置錯誤，會有訊息指出應使用 NuGet 還原加以下載。</span><span class="sxs-lookup"><span data-stu-id="24ceb-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="24ceb-158">不過，執行還原時有可能會顯示「所有套件均已安裝，沒有可還原的項目」。</span><span class="sxs-lookup"><span data-stu-id="24ceb-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="24ceb-159">在此情況下，請刪除 `packages` 資料夾 (使用 `packages.config` 時) 或 `obj/project.assets.json` 檔案 (使用 PackageReference 時)，並再次執行還原。</span><span class="sxs-lookup"><span data-stu-id="24ceb-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="24ceb-160">如果錯誤持續發生，請從命令列使用 `nuget locals all -clear` 或 `dotnet nuget locals all --clear` 以清除 *global-packages* 和快取資料夾，如[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="24ceb-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="24ceb-161">從原始檔控制取得專案時，您的專案資料夾可能會設定成唯讀。</span><span class="sxs-lookup"><span data-stu-id="24ceb-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="24ceb-162">請變更資料夾的權限，然後再次嘗試還原套件。</span><span class="sxs-lookup"><span data-stu-id="24ceb-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="24ceb-163">您使用的可能是舊版 NuGet。</span><span class="sxs-lookup"><span data-stu-id="24ceb-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="24ceb-164">請查看 [nuget.org/downloads](https://www.nuget.org/downloads) 以取得最新的建議版本。</span><span class="sxs-lookup"><span data-stu-id="24ceb-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="24ceb-165">若是 Visual Studio 2015，建議使用 3.6.0。</span><span class="sxs-lookup"><span data-stu-id="24ceb-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="24ceb-166">如果您遇到其他問題，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們向您取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="24ceb-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
