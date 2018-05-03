---
title: 使用 Team Foundation Build 的 NuGet 套件還原逐步解說 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 使用 Team Foundation Build (TFS 和 Visual Studio Team Services) 進行 NuGet 套件還原的逐步解說。
keywords: NuGet 套件還原、NuGet 和 TFS、NuGet 和 VSTS、NuGet 組建系統、Team Foundation Build、自訂 MSBuild 專案、雲端組建、持續整合
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f46a7402214bf965918a5195605027913a8c60c2
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="0713b-104">使用 Team Foundation Build 設定套件還原</span><span class="sxs-lookup"><span data-stu-id="0713b-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="0713b-105">本文提供有關如何針對 Git 與 Team Services 版本控制還原套件以作為 [Team Services 組建](/vsts/build-release/index)一部分的詳細逐步解說。</span><span class="sxs-lookup"><span data-stu-id="0713b-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="0713b-106">雖然這個逐步解說專屬於使用 Visual Studio Team Services 的案例，但是這些概念也適用於其他版本控制和建置系統。</span><span class="sxs-lookup"><span data-stu-id="0713b-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="0713b-107">適用於：</span><span class="sxs-lookup"><span data-stu-id="0713b-107">Applies To:</span></span>

- <span data-ttu-id="0713b-108">在任何 TFS 版本上執行的自訂 MSBuild 專案</span><span class="sxs-lookup"><span data-stu-id="0713b-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="0713b-109">Team Foundation Server 2012 或更早版本</span><span class="sxs-lookup"><span data-stu-id="0713b-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="0713b-110">移轉至 TFS 2013 或更新版本的自訂 Team Foundation Build 流程範本</span><span class="sxs-lookup"><span data-stu-id="0713b-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="0713b-111">已移除 Nuget 還原功能的建置流程範本</span><span class="sxs-lookup"><span data-stu-id="0713b-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="0713b-112">如果您搭配使用 Visual Studio Team Services 或 Team Foundation Server 2013 與其建置流程範本，則會在建置流程中進行自動套件還原。</span><span class="sxs-lookup"><span data-stu-id="0713b-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="0713b-113">一般方法</span><span class="sxs-lookup"><span data-stu-id="0713b-113">The general approach</span></span>

<span data-ttu-id="0713b-114">使用 NuGet 的優點在於，您可以使用它來避免將二進位檔簽入到版本設定系統。</span><span class="sxs-lookup"><span data-stu-id="0713b-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="0713b-115">因為開發人員必須在本機上開始工作之前複製整個存放庫 (包含完整歷程記錄)，所以如果您使用[分散式版本設定](http://en.wikipedia.org/wiki/Distributed_revision_control)系統 (例如 git)，則這特別有趣。</span><span class="sxs-lookup"><span data-stu-id="0713b-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="0713b-116">因為二進位檔案在儲存時通常不會進行差異壓縮，所以簽入二進位檔可能會造成明顯存放庫膨脹。</span><span class="sxs-lookup"><span data-stu-id="0713b-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="0713b-117">NuGet 現在已支援在建置期間[還原套件](../consume-packages/package-restore.md)較長的時間。</span><span class="sxs-lookup"><span data-stu-id="0713b-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="0713b-118">先前的實作具有要擴充建置流程之套件的無解問題，因為 NuGet 已在建置專案時還原套件。</span><span class="sxs-lookup"><span data-stu-id="0713b-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="0713b-119">不過，MSBuild 不允許在建置期間擴充建置；有人可能會認為這是 MSBuild 中的問題，但我認為這是無法避免的問題。</span><span class="sxs-lookup"><span data-stu-id="0713b-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="0713b-120">根據您需要擴充的層面，在還原套件時註冊可能會太晚。</span><span class="sxs-lookup"><span data-stu-id="0713b-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="0713b-121">這個問題的解決方法是確保套件在建置流程的第一個步驟中還原：</span><span class="sxs-lookup"><span data-stu-id="0713b-121">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="0713b-122">當您的建置流程在建置程式碼之前還原套件時，您不需要簽入 `.targets` 檔案</span><span class="sxs-lookup"><span data-stu-id="0713b-122">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="0713b-123">必須編寫套件，以允許在 Visual Studio 中載入。</span><span class="sxs-lookup"><span data-stu-id="0713b-123">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="0713b-124">否則，您可能仍然想要簽入 `.targets` 檔案，讓其他開發人員只需要開啟方案，而不需要先還原套件。</span><span class="sxs-lookup"><span data-stu-id="0713b-124">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="0713b-125">下列示範專案會示範如何設定組建，而使用此方式，則不需要簽入 `packages` 資料夾和 `.targets` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0713b-125">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="0713b-126">它也會示範如何在 Team Foundation Service 上設定這個範例專案的自動化建置。</span><span class="sxs-lookup"><span data-stu-id="0713b-126">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="0713b-127">存放庫結構</span><span class="sxs-lookup"><span data-stu-id="0713b-127">Repository structure</span></span>

<span data-ttu-id="0713b-128">我們的示範專案是一種簡單命令列工具，可使用命令列引數來查詢 Bing。</span><span class="sxs-lookup"><span data-stu-id="0713b-128">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="0713b-129">它的目標設為 .NET Framework 4，並使用許多 [BCL 套件](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http)、[Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl)、[Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) 和 [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build))。</span><span class="sxs-lookup"><span data-stu-id="0713b-129">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="0713b-130">存放庫的結構如下：</span><span class="sxs-lookup"><span data-stu-id="0713b-130">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="0713b-131">您可以看到我們尚未簽入 `packages` 資料夾，也未簽入任何 `.targets` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0713b-131">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="0713b-132">不過，我們已在建置期間簽入必要 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="0713b-132">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="0713b-133">遵循廣泛使用的慣例，我們已將它簽入共用的 `tools` 資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="0713b-133">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="0713b-134">原始程式碼是在 `src` 資料夾下方。</span><span class="sxs-lookup"><span data-stu-id="0713b-134">The source code is under the `src` folder.</span></span> <span data-ttu-id="0713b-135">雖然我們的示範僅使用單一方案，但是您可以輕鬆地想像此資料夾包含多個方案。</span><span class="sxs-lookup"><span data-stu-id="0713b-135">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="0713b-136">忽略檔案</span><span class="sxs-lookup"><span data-stu-id="0713b-136">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="0713b-137">目前 [NuGet 用戶端中有已知 Bug](https://nuget.codeplex.com/workitem/4072)，可讓用戶端仍然將 `packages` 資料夾新增至版本設定。</span><span class="sxs-lookup"><span data-stu-id="0713b-137">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="0713b-138">因應措施是停用原始檔控制整合。</span><span class="sxs-lookup"><span data-stu-id="0713b-138">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="0713b-139">若要這樣做，您需要在與解決方案平行的 `.nuget` 資料夾中有 `Nuget.Config ` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0713b-139">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="0713b-140">如果此資料夾尚未存在，則您需要建立它。</span><span class="sxs-lookup"><span data-stu-id="0713b-140">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="0713b-141">在 [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) 中，新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="0713b-141">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="0713b-142">為了與不想簽入 **packages** 資料夾的版本控制進行通訊，我們也新增了適用於 git (`.gitignore`) 和 TF 版本控制 (`.tfignore`) 的忽略檔案。</span><span class="sxs-lookup"><span data-stu-id="0713b-142">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="0713b-143">這些檔案說明您不想簽入檔案的模式。</span><span class="sxs-lookup"><span data-stu-id="0713b-143">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="0713b-144">`.gitignore` 檔案的內容如下：</span><span class="sxs-lookup"><span data-stu-id="0713b-144">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="0713b-145">`.gitignore` 檔案的[功能相當強大](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)。</span><span class="sxs-lookup"><span data-stu-id="0713b-145">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="0713b-146">例如，如果您想要通常不要簽入 `packages` 資料夾的內容，但想要進行先前之簽入 `.targets` 檔案的指引，則可能改為具有下列規則：</span><span class="sxs-lookup"><span data-stu-id="0713b-146">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="0713b-147">這會排除所有 `packages` 資料夾，但會重新包含所有內含的 `.targets` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0713b-147">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="0713b-148">但您可以在[這裡](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)找到 `.gitignore` 檔案的範本，此範本是特別為 Visual Studio 開發人員需求量身訂做。</span><span class="sxs-lookup"><span data-stu-id="0713b-148">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="0713b-149">TF 版本設定透過 [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) 檔案支援非常類似的機制。</span><span class="sxs-lookup"><span data-stu-id="0713b-149">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="0713b-150">語法幾乎相同：</span><span class="sxs-lookup"><span data-stu-id="0713b-150">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="0713b-151">build.proj</span><span class="sxs-lookup"><span data-stu-id="0713b-151">build.proj</span></span>

<span data-ttu-id="0713b-152">在我們的示範中，建置流程相當簡單。</span><span class="sxs-lookup"><span data-stu-id="0713b-152">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="0713b-153">我們將建立 MSBuild 專案以建置所有方案，同時確保先還原套件，再建置方案。</span><span class="sxs-lookup"><span data-stu-id="0713b-153">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="0713b-154">這個專案會有三個傳統目標 (`Clean`、`Build` 和 `Rebuild`) 以及一個新的目標 (`RestorePackages`)。</span><span class="sxs-lookup"><span data-stu-id="0713b-154">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="0713b-155">`Build` 和 `Rebuild` 目標都是根據 `RestorePackages`。</span><span class="sxs-lookup"><span data-stu-id="0713b-155">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="0713b-156">這確保您可以同時執行 `Build` 和 `Rebuild`，並且依賴所還原的套件。</span><span class="sxs-lookup"><span data-stu-id="0713b-156">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="0713b-157">`Clean`、`Build` 和 `Rebuild` 會叫用所有方案檔上的對應 MSBuild 目標。</span><span class="sxs-lookup"><span data-stu-id="0713b-157">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="0713b-158">`RestorePackages` 目標會叫用每個方案檔的 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="0713b-158">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="0713b-159">這是使用 [MSBuild 的批次功能](/visualstudio/msbuild/msbuild-batching)所完成。</span><span class="sxs-lookup"><span data-stu-id="0713b-159">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="0713b-160">結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="0713b-160">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="0713b-161">設定 Team Build</span><span class="sxs-lookup"><span data-stu-id="0713b-161">Configuring Team Build</span></span>

<span data-ttu-id="0713b-162">Team Build 提供各種流程範本。</span><span class="sxs-lookup"><span data-stu-id="0713b-162">Team Build offers various process templates.</span></span> <span data-ttu-id="0713b-163">在此示範中，我們將使用 Team Foundation Service。</span><span class="sxs-lookup"><span data-stu-id="0713b-163">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="0713b-164">內部部署 TFS 安裝極為類似。</span><span class="sxs-lookup"><span data-stu-id="0713b-164">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="0713b-165">Git 和 TF 版本設定具有不同的 Team Build 範本，因此下列步驟會根據使用的版本設定系統而不同。</span><span class="sxs-lookup"><span data-stu-id="0713b-165">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="0713b-166">在這兩種情況下，您只需要選取 build.proj 作為您想要建置的專案。</span><span class="sxs-lookup"><span data-stu-id="0713b-166">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="0713b-167">首先，請查看 git 的流程範本。</span><span class="sxs-lookup"><span data-stu-id="0713b-167">First, let's look at the process template for git.</span></span> <span data-ttu-id="0713b-168">在 git 範本中，透過 `Solution to build` 屬性選取組建：</span><span class="sxs-lookup"><span data-stu-id="0713b-168">In the git based template the build is selected via the property `Solution to build`:</span></span>

![git 的建置流程](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="0713b-170">請注意，此屬性是您存放庫中的位置。</span><span class="sxs-lookup"><span data-stu-id="0713b-170">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="0713b-171">因為 `build.proj` 位在根目錄中，所以我們只是使用 `build.proj`。</span><span class="sxs-lookup"><span data-stu-id="0713b-171">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="0713b-172">如果您將組建檔案置於稱為 `tools` 的資料夾下方，則值會是 `tools\build.proj`。</span><span class="sxs-lookup"><span data-stu-id="0713b-172">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="0713b-173">在 TF 版本設定範本中，會透過 `Projects` 屬性選取專案：</span><span class="sxs-lookup"><span data-stu-id="0713b-173">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC 的建置流程](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="0713b-175">相較於 git 範本，TF 版本設定支援選擇器 (右側有三個點的按鈕)。</span><span class="sxs-lookup"><span data-stu-id="0713b-175">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="0713b-176">因此，為了避免任何鍵入錯誤，建議您使用它們來選取專案。</span><span class="sxs-lookup"><span data-stu-id="0713b-176">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>