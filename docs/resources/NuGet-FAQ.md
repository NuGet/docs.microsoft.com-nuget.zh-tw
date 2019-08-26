---
title: NuGet 常見問題集
description: 在命令列上和 Visual Studio 中使用 NuGet 的常見問題和解答
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9b12b1fa27308cf41b58b0c244ea648d3eecdc95
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520388"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="150ae-103">NuGet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="150ae-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="150ae-104">**執行 NuGet 所需的作業為何？**</span><span class="sxs-lookup"><span data-stu-id="150ae-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="150ae-105">[安裝指南](../install-nuget-client-tools.md)包含 UI 和命令列工具的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="150ae-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="150ae-106">**NuGet 支援 Mono 嗎？**</span><span class="sxs-lookup"><span data-stu-id="150ae-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="150ae-107">命令列工具 `nuget.exe` 會在 Mono 3.2+ 下建置並執行，而且可以在 Mono 中建立套件。</span><span class="sxs-lookup"><span data-stu-id="150ae-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="150ae-108">雖然 `nuget.exe` 完整運作於 Windows 上，但是 Linux 和 OS X 上已有已知問題。請參閱 GitHub 上的 [Mono 問題](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。</span><span class="sxs-lookup"><span data-stu-id="150ae-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="150ae-109">[圖形化用戶端](https://github.com/mrward/monodevelop-nuget-addin)可作為 MonoDevelop 的增益集。</span><span class="sxs-lookup"><span data-stu-id="150ae-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="150ae-110">**如何判斷套件所包含的內容，以及它對我的應用程式而言是否穩定而且有用？**</span><span class="sxs-lookup"><span data-stu-id="150ae-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="150ae-111">了解套件的主要來源是其在 nuget.org 上的清單頁面 (或另一個私人摘要)。</span><span class="sxs-lookup"><span data-stu-id="150ae-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="150ae-112">nuget.org 上的每個套件頁面都會包含套件的描述、其版本歷程記錄和使用量統計資料。</span><span class="sxs-lookup"><span data-stu-id="150ae-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="150ae-113">套件頁面上的 [資訊]  區段也會包含專案網站的連結，而在專案網站中，您一般可以找到許多範例和其他文件協助您了解如何使用套件。</span><span class="sxs-lookup"><span data-stu-id="150ae-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="150ae-114">如需詳細資訊，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="150ae-115">Visual Studio 中的 NuGet</span><span class="sxs-lookup"><span data-stu-id="150ae-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="150ae-116">**在不同的 Visual Studio 產品中，如何支援 NuGet？**</span><span class="sxs-lookup"><span data-stu-id="150ae-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="150ae-117">Windows 上的 Visual Studio 支援[套件管理員 UI](../consume-packages/install-use-packages-visual-studio.md) 和[套件管理員主控台](../consume-packages/install-use-packages-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="150ae-118">Visual Studio for Mac 具有內建 NuGet 功能，如[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)中所述。</span><span class="sxs-lookup"><span data-stu-id="150ae-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="150ae-119">Visual Studio Code (所有平台) 沒有任何直接 NuGet 整合。</span><span class="sxs-lookup"><span data-stu-id="150ae-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="150ae-120">請使用 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 或 [dotnet CLI](../reference/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="150ae-121">Azure DevOps 提供[還原 NuGet 套件的建置步驟](/vsts/build-release/tasks/package/nuget)。</span><span class="sxs-lookup"><span data-stu-id="150ae-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="150ae-122">您也可以[在 Azure DevOps 上裝載私人 NuGet 套件摘要](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="150ae-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="150ae-123">**如何檢查已安裝 NuGet 工具的確切版本？**</span><span class="sxs-lookup"><span data-stu-id="150ae-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="150ae-124">在 Visual Studio 中，使用 [說明] > [關於 Microsoft Visual Studio]  命令，並查看 [NuGet 套件管理員]  旁邊所顯示的版本。</span><span class="sxs-lookup"><span data-stu-id="150ae-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="150ae-125">或者，啟動 [套件管理員主控台] ([工具] > [NuGet 套件管理員] > [套件管理員主控台]  )，並輸入 `$host` 以查看 NuGet 的相關資訊 (包含版本)。</span><span class="sxs-lookup"><span data-stu-id="150ae-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="150ae-126">**NuGet 支援哪些程式設計語言？**</span><span class="sxs-lookup"><span data-stu-id="150ae-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="150ae-127">NuGet 一般適用於 .NET 語言，並且設計目的是將 .NET 程式庫帶入專案中。</span><span class="sxs-lookup"><span data-stu-id="150ae-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="150ae-128">在某些專案類型中，它也支援 MSBuild 和 Visual Studio 自動化，因此在各種程度上也支援其他專案和語言。</span><span class="sxs-lookup"><span data-stu-id="150ae-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="150ae-129">最新版的 NuGet 支援 C#、Visual Basic、F#、WiX 和 C++。</span><span class="sxs-lookup"><span data-stu-id="150ae-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="150ae-130">**NuGet 支援哪些專案範本？**</span><span class="sxs-lookup"><span data-stu-id="150ae-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="150ae-131">NuGet 完整支援各種專案範本，例如 Windows、Web、Cloud、SharePoint、Wix 等等。</span><span class="sxs-lookup"><span data-stu-id="150ae-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="150ae-132">**如何更新屬於 Visual Studio 範本的套件？**</span><span class="sxs-lookup"><span data-stu-id="150ae-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="150ae-133">移至套件管理員 UI 中的 [更新]  索引標籤，然後選取 [全部更新]  ，或使用套件管理員主控台中的 [`Update-Package` 命令](../reference/ps-reference/ps-ref-update-package.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="150ae-134">若要更新範本本身，您需要手動更新範本存放庫。</span><span class="sxs-lookup"><span data-stu-id="150ae-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="150ae-135">請參閱有關本主題的 [Xavier Decoster 部落格](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="150ae-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="150ae-136">請注意，您必須自負這項作業的風險；因為，如果所有相依性的最新版本彼此不相容，則手動更新可能會損毀範本。</span><span class="sxs-lookup"><span data-stu-id="150ae-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="150ae-137">**可以在 Visual Studio 外部使用 NuGet 嗎？**</span><span class="sxs-lookup"><span data-stu-id="150ae-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="150ae-138">是，NuGet 只能直接從命令列運作。</span><span class="sxs-lookup"><span data-stu-id="150ae-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="150ae-139">請參閱[安裝指南](../install-nuget-client-tools.md)和 [CLI 參考](../reference/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="150ae-140">NuGet 命令列</span><span class="sxs-lookup"><span data-stu-id="150ae-140">NuGet command line</span></span>

<span data-ttu-id="150ae-141">**如何取得最新版的 NuGet 命令列工具？**</span><span class="sxs-lookup"><span data-stu-id="150ae-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="150ae-142">請參閱[安裝指南](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-142">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="150ae-143">若要檢查目前安裝之工具的版本，請使用 `nuget help`。</span><span class="sxs-lookup"><span data-stu-id="150ae-143">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="150ae-144">**nuget.exe 的授權為何？**</span><span class="sxs-lookup"><span data-stu-id="150ae-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="150ae-145">您可以根據 MIT 授權的規定來轉散發 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="150ae-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="150ae-146">您負責更新和維護您選擇要轉散發的任何 nuget.exe 複本。</span><span class="sxs-lookup"><span data-stu-id="150ae-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="150ae-147">**可以擴充 NuGet 命令列工具嗎？**</span><span class="sxs-lookup"><span data-stu-id="150ae-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="150ae-148">是，可以將自訂命令新增至 `nuget.exe`，如 [Rob Reynold 文章](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="150ae-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="150ae-149">NuGet 套件管理員主控台 (Windows 上的 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="150ae-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="150ae-150">**如何在套件管理員主控台中存取 DTE 物件？**</span><span class="sxs-lookup"><span data-stu-id="150ae-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="150ae-151">Visual Studio 自動化物件模型中的最上層物件稱為 DTE (開發工具環境) 物件。</span><span class="sxs-lookup"><span data-stu-id="150ae-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="150ae-152">此主控台透過名為 `$DTE` 的變數提供這個項目。</span><span class="sxs-lookup"><span data-stu-id="150ae-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="150ae-153">如需詳細資訊，請參閱＜Visual Studio 擴充性＞文件中的 [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) (自動化模型概觀)。</span><span class="sxs-lookup"><span data-stu-id="150ae-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="150ae-154">**我嘗試將 $DTE 變數轉換為類型 DTE2，但得到錯誤：Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". (無法將類型 "EnvDTE.DTEClass" 的 "EnvDTE.DTEClass" 值轉換為類型 "EnvDTE80.DTE2"。)有什麼問題？**</span><span class="sxs-lookup"><span data-stu-id="150ae-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="150ae-155">這是 PowerShell 如何與 COM 物件互動的已知問題。</span><span class="sxs-lookup"><span data-stu-id="150ae-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="150ae-156">請嘗試下列動作：</span><span class="sxs-lookup"><span data-stu-id="150ae-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="150ae-157">`Get-Interface` 是 NuGet PowerShell 主機所新增的 Helper 函式。</span><span class="sxs-lookup"><span data-stu-id="150ae-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="150ae-158">建立並發行套件</span><span class="sxs-lookup"><span data-stu-id="150ae-158">Creating and publishing packages</span></span>

<span data-ttu-id="150ae-159">**如何在摘要中列出我的套件？**</span><span class="sxs-lookup"><span data-stu-id="150ae-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="150ae-160">請參閱[建立並發行套件](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="150ae-161">**我的程式庫有多個版本將目標設為不同的 .NET Framework 版本。如何建置支援此項目的單一套件？**</span><span class="sxs-lookup"><span data-stu-id="150ae-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="150ae-162">請參閱[支援多個 .NET Framework 版本和設定檔](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="150ae-163">**如何設定我自己的存放庫或摘要？**</span><span class="sxs-lookup"><span data-stu-id="150ae-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="150ae-164">請參閱[裝載套件概觀](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="150ae-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="150ae-165">**如何將套件大量上傳至 NuGet 摘要？**</span><span class="sxs-lookup"><span data-stu-id="150ae-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="150ae-166">請參閱[大量發行 NuGet 套件](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。</span><span class="sxs-lookup"><span data-stu-id="150ae-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="150ae-167">使用套件</span><span class="sxs-lookup"><span data-stu-id="150ae-167">Working with packages</span></span>

<span data-ttu-id="150ae-168">**專案層級套件與方案層級套件之間的差異為何？**</span><span class="sxs-lookup"><span data-stu-id="150ae-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="150ae-169">只要在方案中安裝方案層級套件 (NuGet 3.x+) 一次，就可以用於方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="150ae-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="150ae-170">專案層級套件會安裝在使用它的每個專案中。</span><span class="sxs-lookup"><span data-stu-id="150ae-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="150ae-171">方案層級套件也可能會安裝可從套件管理員主控台內呼叫的新命令。</span><span class="sxs-lookup"><span data-stu-id="150ae-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="150ae-172">**可以在沒有網際網路連線的情況下安裝 NuGet 套件嗎？**</span><span class="sxs-lookup"><span data-stu-id="150ae-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="150ae-173">是，請參閱 Scott Hanselman 的部落格文章 [How to access NuGet when nuget.org is down (or you're on a plane](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (如何在 nuget.org 關閉 (或您在飛機上) 時存取 NuGet) (hanselman.com)。</span><span class="sxs-lookup"><span data-stu-id="150ae-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="150ae-174">**如何將套件從預設套件資料夾安裝至不同位置？**</span><span class="sxs-lookup"><span data-stu-id="150ae-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="150ae-175">請使用 `nuget config -set repositoryPath=<path>` 在 `Nuget.Config` 中設定 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 設定。</span><span class="sxs-lookup"><span data-stu-id="150ae-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="150ae-176">**如何避免將 NuGet 套件資料夾新增至原始檔控制嗎？**</span><span class="sxs-lookup"><span data-stu-id="150ae-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="150ae-177">將 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="150ae-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="150ae-178">此索引鍵作用於方案層級，因此需要新增至 `$(Solutiondir)\.nuget\Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="150ae-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="150ae-179">從 Visual Studio 啟用套件還原時會自動建立這個檔案。</span><span class="sxs-lookup"><span data-stu-id="150ae-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="150ae-180">**如何關閉套件還原？**</span><span class="sxs-lookup"><span data-stu-id="150ae-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="150ae-181">請參閱[啟用和停用套件還原](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="150ae-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="150ae-182">**安裝含遠端相依性的本機套件時，為什麼收到「無法解決相依性錯誤」？**</span><span class="sxs-lookup"><span data-stu-id="150ae-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="150ae-183">將本機套件安裝至專案時，您需要選取**所有**來源。</span><span class="sxs-lookup"><span data-stu-id="150ae-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="150ae-184">這會彙總所有摘要，而不是只使用一個。</span><span class="sxs-lookup"><span data-stu-id="150ae-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="150ae-185">出現此錯誤的原因是本機存放庫使用者經常會因公司原則而想要避免不小心安裝遠端套件。</span><span class="sxs-lookup"><span data-stu-id="150ae-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="150ae-186">**我在同一個資料夾中有多個專案，我該如何為每個專案使用不同的 packages.config 檔案？**</span><span class="sxs-lookup"><span data-stu-id="150ae-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="150ae-187">在不同專案位於不同資料夾的大部分專案中，這在 NuGet 識別每個專案中的 `packages.config` 檔案時不是問題。</span><span class="sxs-lookup"><span data-stu-id="150ae-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="150ae-188">相同的資料夾中有 NuGet 3.3+ 和多個專案時，您可以將專案名稱插入至使用模式 `packages.{project-name}.config` 的 `packages.config` 檔案名稱，而且 NuGet 會使用該檔案。</span><span class="sxs-lookup"><span data-stu-id="150ae-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="150ae-189">因為每個專案檔都包含它自己的相依性清單，所以使用 PackageReference 時，這不是問題。</span><span class="sxs-lookup"><span data-stu-id="150ae-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="150ae-190">**我在存放庫清單中看不到 nuget.org，要如何取得它？**</span><span class="sxs-lookup"><span data-stu-id="150ae-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="150ae-191">將 `https://api.nuget.org/v3/index.json` 新增至來源清單，或者</span><span class="sxs-lookup"><span data-stu-id="150ae-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="150ae-192">刪除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)，讓 NuGet 重新加以建立。</span><span class="sxs-lookup"><span data-stu-id="150ae-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
