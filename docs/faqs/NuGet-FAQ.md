---
title: NuGet 常見問題集
description: 在命令列上和 Visual Studio 中使用 NuGet 以及使用 NuGet 資源庫的常見問題和解答。
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: 290055a306306e944695d3a6ac970819882ee0c6
ms.sourcegitcommit: 046717af2eba9ff6f619a0533844dee56a600d1c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2019
ms.locfileid: "55648266"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="93a25-103">NuGet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="93a25-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="93a25-104">**執行 NuGet 所需的作業為何？**</span><span class="sxs-lookup"><span data-stu-id="93a25-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="93a25-105">[安裝指南](../install-nuget-client-tools.md)包含 UI 和命令列工具的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="93a25-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="93a25-106">**NuGet 支援 Mono 嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="93a25-107">命令列工具 `nuget.exe` 會在 Mono 3.2+ 下建置並執行，而且可以在 Mono 中建立套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="93a25-108">雖然 `nuget.exe` 完整運作於 Windows 上，但是 Linux 和 OS X 上已有已知問題。請參閱 GitHub 上的 [Mono 問題](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。</span><span class="sxs-lookup"><span data-stu-id="93a25-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="93a25-109">[圖形化用戶端](https://github.com/mrward/monodevelop-nuget-addin)可作為 MonoDevelop 的增益集。</span><span class="sxs-lookup"><span data-stu-id="93a25-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="93a25-110">**如何判斷套件所包含的內容，以及它對我的應用程式而言是否穩定而且有用？**</span><span class="sxs-lookup"><span data-stu-id="93a25-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="93a25-111">了解套件的主要來源是其在 nuget.org 上的清單頁面 (或另一個私人摘要)。</span><span class="sxs-lookup"><span data-stu-id="93a25-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="93a25-112">nuget.org 上的每個套件頁面都會包含套件的描述、其版本歷程記錄和使用量統計資料。</span><span class="sxs-lookup"><span data-stu-id="93a25-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="93a25-113">套件頁面上的 [資訊] 區段也會包含專案網站的連結，而在專案網站中，您一般可以找到許多範例和其他文件協助您了解如何使用套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="93a25-114">如需詳細資訊，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="93a25-115">Visual Studio 中的 NuGet</span><span class="sxs-lookup"><span data-stu-id="93a25-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="93a25-116">**在不同的 Visual Studio 產品中，如何支援 NuGet？**</span><span class="sxs-lookup"><span data-stu-id="93a25-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="93a25-117">Windows 上的 Visual Studio 支援[套件管理員 UI](../tools/package-manager-ui.md) 和[套件管理員主控台](../tools/package-manager-console.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="93a25-118">Visual Studio for Mac 具有內建 NuGet 功能，如[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)中所述。</span><span class="sxs-lookup"><span data-stu-id="93a25-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="93a25-119">Visual Studio Code (所有平台) 沒有任何直接 NuGet 整合。</span><span class="sxs-lookup"><span data-stu-id="93a25-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="93a25-120">請使用 [NuGet CLI](../tools/nuget-exe-cli-reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="93a25-121">Azure DevOps 提供[還原 NuGet 套件的建置步驟](/vsts/build-release/tasks/package/nuget)。</span><span class="sxs-lookup"><span data-stu-id="93a25-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="93a25-122">您也可以[在 Azure DevOps 上裝載私人 NuGet 套件摘要](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="93a25-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="93a25-123">**如何檢查已安裝 NuGet 工具的確切版本？**</span><span class="sxs-lookup"><span data-stu-id="93a25-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="93a25-124">在 Visual Studio 中，使用 [說明] > [關於 Microsoft Visual Studio] 命令，並查看 [NuGet 套件管理員] 旁邊所顯示的版本。</span><span class="sxs-lookup"><span data-stu-id="93a25-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="93a25-125">或者，啟動 [套件管理員主控台] ([工具] > [NuGet 套件管理員] > [套件管理員主控台])，並輸入 `$host` 以查看 NuGet 的相關資訊 (包含版本)。</span><span class="sxs-lookup"><span data-stu-id="93a25-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="93a25-126">**NuGet 支援哪些程式設計語言？**</span><span class="sxs-lookup"><span data-stu-id="93a25-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="93a25-127">NuGet 一般適用於 .NET 語言，並且設計目的是將 .NET 程式庫帶入專案中。</span><span class="sxs-lookup"><span data-stu-id="93a25-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="93a25-128">在某些專案類型中，它也支援 MSBuild 和 Visual Studio 自動化，因此在各種程度上也支援其他專案和語言。</span><span class="sxs-lookup"><span data-stu-id="93a25-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="93a25-129">最新版的 NuGet 支援 C#、Visual Basic、F#、WiX 和 C++。</span><span class="sxs-lookup"><span data-stu-id="93a25-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="93a25-130">**NuGet 支援哪些專案範本？**</span><span class="sxs-lookup"><span data-stu-id="93a25-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="93a25-131">NuGet 完整支援各種專案範本，例如 Windows、Web、Cloud、SharePoint、Wix 等等。</span><span class="sxs-lookup"><span data-stu-id="93a25-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="93a25-132">**如何更新屬於 Visual Studio 範本的套件？**</span><span class="sxs-lookup"><span data-stu-id="93a25-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="93a25-133">移至套件管理員 UI 中的 [更新] 索引標籤，然後選取 [全部更新]，或使用套件管理員主控台中的 [`Update-Package` 命令](../tools/ps-ref-update-package.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="93a25-134">若要更新範本本身，您需要手動更新範本存放庫。</span><span class="sxs-lookup"><span data-stu-id="93a25-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="93a25-135">請參閱有關本主題的 [Xavier Decoster 部落格](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。</span><span class="sxs-lookup"><span data-stu-id="93a25-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="93a25-136">請注意，您必須自負這項作業的風險；因為，如果所有相依性的最新版本彼此不相容，則手動更新可能會損毀範本。</span><span class="sxs-lookup"><span data-stu-id="93a25-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="93a25-137">**可以在 Visual Studio 外部使用 NuGet 嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="93a25-138">是，NuGet 只能直接從命令列運作。</span><span class="sxs-lookup"><span data-stu-id="93a25-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="93a25-139">請參閱[安裝指南](../install-nuget-client-tools.md)和 [CLI 參考](../tools/nuget-exe-cli-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="93a25-140">NuGet 命令列</span><span class="sxs-lookup"><span data-stu-id="93a25-140">NuGet command line</span></span>

<span data-ttu-id="93a25-141">**如何取得最新版的 NuGet 命令列工具？**</span><span class="sxs-lookup"><span data-stu-id="93a25-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="93a25-142">請參閱[安裝指南](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="93a25-143">**nuget.exe 的授權為何？**</span><span class="sxs-lookup"><span data-stu-id="93a25-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="93a25-144">您可以根據 MIT 授權的規定來轉散發 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="93a25-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="93a25-145">您負責更新和維護您選擇要轉散發的任何 nuget.exe 複本。</span><span class="sxs-lookup"><span data-stu-id="93a25-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="93a25-146">**可以擴充 NuGet 命令列工具嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="93a25-147">是，可以將自訂命令新增至 `nuget.exe`，如 [Rob Reynold 文章](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。</span><span class="sxs-lookup"><span data-stu-id="93a25-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="93a25-148">NuGet 套件管理員主控台 (Windows 上的 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="93a25-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="93a25-149">**如何在套件管理員主控台中存取 DTE 物件？**</span><span class="sxs-lookup"><span data-stu-id="93a25-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="93a25-150">Visual Studio 自動化物件模型中的最上層物件稱為 DTE (開發工具環境) 物件。</span><span class="sxs-lookup"><span data-stu-id="93a25-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="93a25-151">此主控台透過名為 `$DTE` 的變數提供這個項目。</span><span class="sxs-lookup"><span data-stu-id="93a25-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="93a25-152">如需詳細資訊，請參閱＜Visual Studio 擴充性＞文件中的 [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) (自動化模型概觀)。</span><span class="sxs-lookup"><span data-stu-id="93a25-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="93a25-153">**我嘗試將 $DTE 變數轉換為類型 DTE2，但得到錯誤：Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". (無法將類型 "EnvDTE.DTEClass" 的 "EnvDTE.DTEClass" 值轉換為類型 "EnvDTE80.DTE2"。)有什麼問題？**</span><span class="sxs-lookup"><span data-stu-id="93a25-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="93a25-154">這是 PowerShell 如何與 COM 物件互動的已知問題。</span><span class="sxs-lookup"><span data-stu-id="93a25-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="93a25-155">請嘗試下列動作：</span><span class="sxs-lookup"><span data-stu-id="93a25-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="93a25-156">`Get-Interface` 是 NuGet PowerShell 主機所新增的 Helper 函式。</span><span class="sxs-lookup"><span data-stu-id="93a25-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="93a25-157">建立並發行套件</span><span class="sxs-lookup"><span data-stu-id="93a25-157">Creating and publishing packages</span></span>

<span data-ttu-id="93a25-158">**如何在摘要中列出我的套件？**</span><span class="sxs-lookup"><span data-stu-id="93a25-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="93a25-159">請參閱[建立並發行套件](../quickstart/create-and-publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="93a25-160">**我的程式庫有多個版本將目標設為不同的 .NET Framework 版本。如何建置支援此項目的單一套件？**</span><span class="sxs-lookup"><span data-stu-id="93a25-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="93a25-161">請參閱[支援多個 .NET Framework 版本和設定檔](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="93a25-162">**如何設定我自己的存放庫或摘要？**</span><span class="sxs-lookup"><span data-stu-id="93a25-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="93a25-163">請參閱[裝載套件概觀](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="93a25-164">**如何將套件大量上傳至 NuGet 摘要？**</span><span class="sxs-lookup"><span data-stu-id="93a25-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="93a25-165">請參閱[大量發行 NuGet 套件](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。</span><span class="sxs-lookup"><span data-stu-id="93a25-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="93a25-166">使用套件</span><span class="sxs-lookup"><span data-stu-id="93a25-166">Working with packages</span></span>

<span data-ttu-id="93a25-167">**專案層級套件與方案層級套件之間的差異為何？**</span><span class="sxs-lookup"><span data-stu-id="93a25-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="93a25-168">只要在方案中安裝方案層級套件 (NuGet 3.x+) 一次，就可以用於方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="93a25-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="93a25-169">專案層級套件會安裝在使用它的每個專案中。</span><span class="sxs-lookup"><span data-stu-id="93a25-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="93a25-170">方案層級套件也可能會安裝可從套件管理員主控台內呼叫的新命令。</span><span class="sxs-lookup"><span data-stu-id="93a25-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="93a25-171">**可以在沒有網際網路連線的情況下安裝 NuGet 套件嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="93a25-172">是，請參閱 Scott Hanselman 的部落格文章 [How to access NuGet when nuget.org is down (or you're on a plane](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (如何在 nuget.org 關閉 (或您在飛機上) 時存取 NuGet) (hanselman.com)。</span><span class="sxs-lookup"><span data-stu-id="93a25-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="93a25-173">**如何將套件從預設套件資料夾安裝至不同位置？**</span><span class="sxs-lookup"><span data-stu-id="93a25-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="93a25-174">請使用 `nuget config -set repositoryPath=<path>` 在 `Nuget.Config` 中設定 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 設定。</span><span class="sxs-lookup"><span data-stu-id="93a25-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="93a25-175">**如何避免將 NuGet 套件資料夾新增至原始檔控制嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="93a25-176">將 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="93a25-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="93a25-177">此索引鍵作用於方案層級，因此需要新增至 `$(Solutiondir)\.nuget\Nuget.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="93a25-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="93a25-178">從 Visual Studio 啟用套件還原時會自動建立這個檔案。</span><span class="sxs-lookup"><span data-stu-id="93a25-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="93a25-179">**如何關閉套件還原？**</span><span class="sxs-lookup"><span data-stu-id="93a25-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="93a25-180">請參閱[啟用和停用套件還原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="93a25-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="93a25-181">**安裝含遠端相依性的本機套件時，為什麼收到「無法解決相依性錯誤」？**</span><span class="sxs-lookup"><span data-stu-id="93a25-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="93a25-182">將本機套件安裝至專案時，您需要選取**所有**來源。</span><span class="sxs-lookup"><span data-stu-id="93a25-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="93a25-183">這會彙總所有摘要，而不是只使用一個。</span><span class="sxs-lookup"><span data-stu-id="93a25-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="93a25-184">出現此錯誤的原因是本機存放庫使用者經常會因公司原則而想要避免不小心安裝遠端套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="93a25-185">**我在同一個資料夾中有多個專案，我該如何為每個專案使用不同的 packages.config 檔案？**</span><span class="sxs-lookup"><span data-stu-id="93a25-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="93a25-186">在不同專案位於不同資料夾的大部分專案中，這在 NuGet 識別每個專案中的 `packages.config` 檔案時不是問題。</span><span class="sxs-lookup"><span data-stu-id="93a25-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="93a25-187">相同的資料夾中有 NuGet 3.3+ 和多個專案時，您可以將專案名稱插入至使用模式 `packages.{project-name}.config` 的 `packages.config` 檔案名稱，而且 NuGet 會使用該檔案。</span><span class="sxs-lookup"><span data-stu-id="93a25-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="93a25-188">因為每個專案檔都包含它自己的相依性清單，所以使用 PackageReference 時，這不是問題。</span><span class="sxs-lookup"><span data-stu-id="93a25-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="93a25-189">**我在存放庫清單中看不到 nuget.org，要如何取得它？**</span><span class="sxs-lookup"><span data-stu-id="93a25-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="93a25-190">將 `https://api.nuget.org/v3/index.json` 新增至來源清單，或者</span><span class="sxs-lookup"><span data-stu-id="93a25-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="93a25-191">刪除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)，讓 NuGet 重新加以建立。</span><span class="sxs-lookup"><span data-stu-id="93a25-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="93a25-192">**如果套件未提供特定授權資訊，則預設授權條款是什麼？**</span><span class="sxs-lookup"><span data-stu-id="93a25-192">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="93a25-193">每個套件都是受套件隨附的條款所控管。</span><span class="sxs-lookup"><span data-stu-id="93a25-193">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="93a25-194">您應該先檢閱適用的條款，再存取、下載或取得任何套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-194">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="93a25-195">在 nuget.org 上，使用套件頁面上的 [授權資訊] 連結。</span><span class="sxs-lookup"><span data-stu-id="93a25-195">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="93a25-196">如果套件未指定授權條款，請使用 nuget.org 套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="93a25-196">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="93a25-197">Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="93a25-197">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="93a25-198">在 nuget.org 上管理套件</span><span class="sxs-lookup"><span data-stu-id="93a25-198">Managing packages on nuget.org</span></span>

<span data-ttu-id="93a25-199">**我可以在上傳套件之後編輯套件中繼資料嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-199">**Can I edit package metadata after it's been uploaded?**</span></span>

<span data-ttu-id="93a25-200">NuGet 建議簽署所有套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-200">NuGet recommends all packages to be signed.</span></span> <span data-ttu-id="93a25-201">套件簽署的設計原則是已簽署的套件內容必須是不可變的，其中包含 nuspec。</span><span class="sxs-lookup"><span data-stu-id="93a25-201">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="93a25-202">編輯套件中繼資料會導致 nuspec 變更，並讓現有簽章失效。</span><span class="sxs-lookup"><span data-stu-id="93a25-202">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="93a25-203">建議修改現有工作流程，使其不需要在建立套件之後編輯套件中繼資料。</span><span class="sxs-lookup"><span data-stu-id="93a25-203">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="93a25-204">請注意，會自動從您套件本身產生針對套件所列出的相依性，而且無法進行編輯。</span><span class="sxs-lookup"><span data-stu-id="93a25-204">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="93a25-205">此外，將套件上傳至 [int.nugettest.org](https://int.nugettest.org) 是測試及驗證您套件的好方法，完全無須將套件設為可在公開資源庫中使用。</span><span class="sxs-lookup"><span data-stu-id="93a25-205">In addition, uploading packages to [int.nugettest.org](https://int.nugettest.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="93a25-206">**可以保留將在未來發行之套件的名稱嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-206">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="93a25-207">可以。</span><span class="sxs-lookup"><span data-stu-id="93a25-207">Yes.</span></span> <span data-ttu-id="93a25-208">要求帳戶的套件識別碼前置詞，即可在 [nuget.org](https://www.nuget.org/) 上保留套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="93a25-208">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="93a25-209">若要要求套件識別碼首碼，請遵循[文件](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)中的指示。</span><span class="sxs-lookup"><span data-stu-id="93a25-209">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="93a25-210">**如何宣告套件擁有權？**</span><span class="sxs-lookup"><span data-stu-id="93a25-210">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="93a25-211">請參閱[在 nuget.org 上管理套件擁有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="93a25-211">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="93a25-212">**如何處理違反我軟體授權的套件擁有者？**</span><span class="sxs-lookup"><span data-stu-id="93a25-212">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="93a25-213">鼓勵 NuGet 社群合作，以解決套件擁有者與其他軟體擁有者之間可能發生的任何爭議。</span><span class="sxs-lookup"><span data-stu-id="93a25-213">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="93a25-214">我們已製作可在要求 nuget.org 管理員仲裁之前遵循的[爭議解決程序](../policies/dispute-resolution.md)。</span><span class="sxs-lookup"><span data-stu-id="93a25-214">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="93a25-215">**建議將測試套件上傳至 nuget.org 嗎？**</span><span class="sxs-lookup"><span data-stu-id="93a25-215">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="93a25-216">基於測試目的，您可以使用 [int.nugettest.org](https://int.nugettest.org) 或替代的公開 NuGet 伺服器，例如 [myget.org](https://myget.org) 或 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。</span><span class="sxs-lookup"><span data-stu-id="93a25-216">For test purposes, you can use [int.nugettest.org](https://int.nugettest.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="93a25-217">請注意，上傳到 int.nugettest.org 的套件不會保留。</span><span class="sxs-lookup"><span data-stu-id="93a25-217">Note that packages uploaded to int.nugettest.org may not be preserved.</span></span>

<span data-ttu-id="93a25-218">**我可以上傳至 nuget.org 的套件大小上限為何？**</span><span class="sxs-lookup"><span data-stu-id="93a25-218">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="93a25-219">nuget.org 允許最多 250MB 的套件，但建議盡可能保持 1MB 的套件，並使用相依性將套件連結在一起。</span><span class="sxs-lookup"><span data-stu-id="93a25-219">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="93a25-220">根據經驗法則，套件只包含一個組件來避免發生衝突。</span><span class="sxs-lookup"><span data-stu-id="93a25-220">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="93a25-221">NuGet 使用 HTTP 來下載套件，因此較大的套件與較小的套件相較之下更有可能會讓安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="93a25-221">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="93a25-222">可能會在多個套件之間共用相依性，讓 NuGet 套件取用者的總下載大小變小。</span><span class="sxs-lookup"><span data-stu-id="93a25-222">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="93a25-223">相依性大部分是靜態的，而且永遠不會變更。</span><span class="sxs-lookup"><span data-stu-id="93a25-223">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="93a25-224">使用程式碼修正 Bug 時，可能不需要更新相依性。</span><span class="sxs-lookup"><span data-stu-id="93a25-224">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="93a25-225">如果您組合相依性，則每次最後都會得到較大的套件。</span><span class="sxs-lookup"><span data-stu-id="93a25-225">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="93a25-226">將 NuGet 套件分割為相關相依性，以更精細地調整您套件取用者的升級。</span><span class="sxs-lookup"><span data-stu-id="93a25-226">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="93a25-227">無法存取 nuget.org</span><span class="sxs-lookup"><span data-stu-id="93a25-227">nuget.org not accessible</span></span>

<span data-ttu-id="93a25-228">**為何無法從 nuget.org 下載套件或將套件上傳至其中？**</span><span class="sxs-lookup"><span data-stu-id="93a25-228">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="93a25-229">首先，請確定您使用最新版的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="93a25-229">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="93a25-230">如果該版本持續失敗，請[連絡支援人員](https://www.nuget.org/policies/Contact)，並提供其他連線疑難排解資訊，包含：</span><span class="sxs-lookup"><span data-stu-id="93a25-230">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="93a25-231">您所使用的 NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="93a25-231">The version of NuGet you're using</span></span>
- <span data-ttu-id="93a25-232">您所使用的套件來源</span><span class="sxs-lookup"><span data-stu-id="93a25-232">The package sources you're using</span></span>
- <span data-ttu-id="93a25-233">含詳細之詳細資訊的還原記錄</span><span class="sxs-lookup"><span data-stu-id="93a25-233">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="93a25-234">MTR 或 Fiddler 追蹤 (請參閱下面)</span><span class="sxs-lookup"><span data-stu-id="93a25-234">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="93a25-235">您的地理區域</span><span class="sxs-lookup"><span data-stu-id="93a25-235">Your geographical area</span></span>
- <span data-ttu-id="93a25-236">您的機器是否有 Proxy 或防火牆保護？</span><span class="sxs-lookup"><span data-stu-id="93a25-236">Whether your machine is behind a proxy or firewall?</span></span>
- <span data-ttu-id="93a25-237">您的機器是否位於雲端提供者的資料中心 (Azure、AWS 等)？</span><span class="sxs-lookup"><span data-stu-id="93a25-237">Is your machine located on a cloud providers' data center (Azure, AWS etc)?</span></span> <span data-ttu-id="93a25-238">如果是的話，請提供提供者的名稱及區域。</span><span class="sxs-lookup"><span data-stu-id="93a25-238">If yes, please provide the name of the provider and the region.</span></span>

<span data-ttu-id="93a25-239">*擷取 MTR：*</span><span class="sxs-lookup"><span data-stu-id="93a25-239">*To capture MTR:*</span></span>

- <span data-ttu-id="93a25-240">從 [http://winmtr.net/download/](http://winmtr.net/) 下載 WinMTR</span><span class="sxs-lookup"><span data-stu-id="93a25-240">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="93a25-241">輸入 `api.nuget.org` 作為主機名稱，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="93a25-241">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="93a25-242">等到 [已傳送] 資料行 >= 100。</span><span class="sxs-lookup"><span data-stu-id="93a25-242">Wait until the **Sent** column is >= 100.</span></span>

    ![擷取 MTR](media/mtr.png)

- <span data-ttu-id="93a25-244">將文字複製至剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="93a25-244">Copy text to clipboard.</span></span>

<span data-ttu-id="93a25-245">*擷取 Fiddler：*</span><span class="sxs-lookup"><span data-stu-id="93a25-245">*To capture Fiddler:*</span></span>

- <span data-ttu-id="93a25-246">安裝最新版的 [Fiddler](http://www.telerik.com/download/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="93a25-246">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="93a25-247">啟動 Fiddler，並使用 [檔案] > [擷取流量] 功能表來停用擷取流量。</span><span class="sxs-lookup"><span data-stu-id="93a25-247">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="93a25-248">移除所有工作階段 (選取清單中的所有項目，並按 **Delete** 鍵)。</span><span class="sxs-lookup"><span data-stu-id="93a25-248">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="93a25-249">設定 Fiddler 擷取 HTTPS 流量，方法是核取 [工具] > [Fiddler 選項] 功能表的 [HTTPS] 索引標籤中的 [Decrypt HTTPS traffic] (將 HTTPS 流量解密)。</span><span class="sxs-lookup"><span data-stu-id="93a25-249">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="93a25-250">關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="93a25-250">Close Visual Studio.</span></span>
- <span data-ttu-id="93a25-251">啟用 [檔案] > [擷取流量] 功能表。</span><span class="sxs-lookup"><span data-stu-id="93a25-251">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="93a25-252">啟動 Visual Studio 或 nuget.exe，然後執行無法運作的動作。</span><span class="sxs-lookup"><span data-stu-id="93a25-252">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="93a25-253">這些動作所產生的流量應該會顯示在 Fiddler 中。</span><span class="sxs-lookup"><span data-stu-id="93a25-253">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="93a25-254">執行動作之後，請使用 [檔案] > [儲存] > [所有工作階段] 來儲存所擷取的工作階段。</span><span class="sxs-lookup"><span data-stu-id="93a25-254">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="93a25-255">注意：可能必須將 `HTTP_PROXY` 環境變數設定為 `http://127.0.0.1:8888`，以透過 Fiddler 路由傳送 NuGet 流量。</span><span class="sxs-lookup"><span data-stu-id="93a25-255">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="93a25-256">如果該作業失敗，請嘗試[這篇 StackOverflow 文章所提及的祕訣](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。</span><span class="sxs-lookup"><span data-stu-id="93a25-256">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

## <a name="what-is-the-api-endpoint-for-nugetorg"></a><span data-ttu-id="93a25-257">nuget.org 的 API 端點為何？</span><span class="sxs-lookup"><span data-stu-id="93a25-257">What is the API endpoint for nuget.org?</span></span>

<span data-ttu-id="93a25-258">若要對 NuGet 用戶端使用 nuget.org 作為套件存放庫，您必須使用以下 V3 API 端點：</span><span class="sxs-lookup"><span data-stu-id="93a25-258">To use  nuget.org as a package repository with NuGet clients, you would need to use the following V3 API endpoint:</span></span> 

**`https://api.nuget.org/v3/index.json`**

<span data-ttu-id="93a25-259">舊版用戶端仍可以使用 v2 通訊協定連接到 nuget.org。但請注意，使用 v2 通訊協定會造成 NuGet 用戶端 3.0 或更新版本的服務變得緩慢且較不穩定：</span><span class="sxs-lookup"><span data-stu-id="93a25-259">Older clients can still use the v2 protocol to reach nuget.org. However, please note, NuGet clients 3.0 or later will have slower and less-reliable service using the v2 protocol:</span></span>

<span data-ttu-id="93a25-260">`https://www.nuget.org/api/v2/` (已淘汰！！！)**請注意：**"www."</span><span class="sxs-lookup"><span data-stu-id="93a25-260">`https://www.nuget.org/api/v2/` (DEPRECATED!!!) **Note:** the "www."</span></span> <span data-ttu-id="93a25-261">非常重要。</span><span class="sxs-lookup"><span data-stu-id="93a25-261">is important.</span></span>

<span data-ttu-id="93a25-262">此外，*NuGet.exe List* 僅適用於 v2 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="93a25-262">Additionally, *NuGet.exe List* only works with the v2 protocol.</span></span>

## <a name="nugetorg-account-management"></a><span data-ttu-id="93a25-263">nuget.org 帳戶管理</span><span class="sxs-lookup"><span data-stu-id="93a25-263">nuget.org account management</span></span>

### <a name="how-to-create-a-new-nugetorg-account"></a><span data-ttu-id="93a25-264">如何建立新的 nuget.org 帳戶？</span><span class="sxs-lookup"><span data-stu-id="93a25-264">How to create a new nuget.org account?</span></span>

<span data-ttu-id="93a25-265">您必須擁有個人 Microsoft 帳戶或 Azure Active Directory (AAD) 帳戶才能建立 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-265">To create a nuget.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="93a25-266">如果沒有的話，您可以[建立](https://signup.live.com)帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-266">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="93a25-267">如果您擁有 MSA 或 AAD 帳戶，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-267">Follow the following steps if you have a MSA or AAD account.</span></span>
1. <span data-ttu-id="93a25-268">前往 [nuget.org 登入頁面](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="93a25-268">Go to the [nuget.org login page](https://www.nuget.org/users/account/LogOn).</span></span>
1. <span data-ttu-id="93a25-269">按一下 [使用 Microsoft 帳戶登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93a25-269">Click on **Sign in with Microsoft** button.</span></span>
1. <span data-ttu-id="93a25-270">輸入您的 MSA/AAD 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="93a25-270">Enter your MSA/AAD account details.</span></span>
1. <span data-ttu-id="93a25-271">請接受要提供給 *NuGet.org* 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="93a25-271">Please accept the permissions to be given to the *NuGet.org* application.</span></span>
1. <span data-ttu-id="93a25-272">系統會將您重新導向至 nuget.org，並向您要求註冊使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="93a25-272">You will be redirected to nuget.org, and asked to register a username.</span></span>
1. <span data-ttu-id="93a25-273">在輸入方塊中指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="93a25-273">Specify the username in the input box.</span></span> <span data-ttu-id="93a25-274">請注意，使用者名稱**會**區分大小寫，且往後無法再變更/重新命名。</span><span class="sxs-lookup"><span data-stu-id="93a25-274">Please note that the username **is** case sensitive and cannot be changed/renamed later.</span></span>
1. <span data-ttu-id="93a25-275">按一下 [註冊] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93a25-275">Click on **Register** button.</span></span>

<span data-ttu-id="93a25-276">您現在擁有 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-276">You now have a nuget.org account.</span></span> <span data-ttu-id="93a25-277">您可以在[帳戶設定](https://www.nuget.org/account)頁面上進行帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="93a25-277">You can perfrom account management on the [account settings](https://www.nuget.org/account) page.</span></span>

### <a name="how-to-recover-nugetorg-password-login"></a><span data-ttu-id="93a25-278">如何復原 nuget.org 密碼登入？</span><span class="sxs-lookup"><span data-stu-id="93a25-278">How to recover nuget.org password login?</span></span>

<span data-ttu-id="93a25-279">請注意，[nuget.org 密碼登入已中止](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html)，您只能使用個人 Microsoft 帳戶 (MSA) 或 Azure Active Directory (AAD) 帳戶登入 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="93a25-279">Please note that the [nuget.org Password login has been discontinued](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) and the only way to log in to nuget.org is with a personal Microsoft account (MSA) or Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="93a25-280">不過，如果您無法存取建立關聯的 MSA/AAD 帳戶，就必須使用密碼登入來復原 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-280">However, in case you are unable to access your associated MSA/AAD accounts you might need to use password login for recovering your nuget.org account.</span></span> <span data-ttu-id="93a25-281">在此情況下，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-281">In this situation follow the steps below.</span></span>
- <span data-ttu-id="93a25-282">**需求：** 對於您要復原密碼的帳戶，您必須能夠存取與該帳戶建立關聯的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="93a25-282">**Requirement:** You will need to have access to the email that is associated with the account for which you need to recover the password.</span></span>
- <span data-ttu-id="93a25-283">前往[忘記密碼頁面](https://www.nuget.org/account/ForgotPassword)</span><span class="sxs-lookup"><span data-stu-id="93a25-283">Go to the [Forgot password page](https://www.nuget.org/account/ForgotPassword)</span></span>
- <span data-ttu-id="93a25-284">輸入與您欲還原之 nuget.org 帳戶建立關聯的**電子郵件**地址。</span><span class="sxs-lookup"><span data-stu-id="93a25-284">Enter the **email** address that is associated with the nuget.org account you wish to recover.</span></span>
- <span data-ttu-id="93a25-285">按一下 [傳送] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93a25-285">Click the **Send** button.</span></span>
- <span data-ttu-id="93a25-286">您會收到寄給指定電子郵件地址帳戶，且附有重設密碼連結的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="93a25-286">You will get an email to the specified email address account with a link to reset your password.</span></span> <span data-ttu-id="93a25-287">按一下此連結，然後設定新密碼。</span><span class="sxs-lookup"><span data-stu-id="93a25-287">Click on this link and set the new password.</span></span> <span data-ttu-id="93a25-288">若您找不到電子郵件，請檢查「垃圾郵件」資料夾。</span><span class="sxs-lookup"><span data-stu-id="93a25-288">If you can't find the mail check your "junk" folder.</span></span>
- <span data-ttu-id="93a25-289">完成後，您便可在 NuGet 上以使用者名稱/密碼登入。</span><span class="sxs-lookup"><span data-stu-id="93a25-289">Once done, you can now login with username/password on NuGet.</span></span>
- <span data-ttu-id="93a25-290">若要以使用者名稱/密碼登入，請使用 [nuget.org 登入頁面](https://www.nuget.org/users/account/LogOn)上的**使用 Nuget.org 帳戶登入**連結。</span><span class="sxs-lookup"><span data-stu-id="93a25-290">To login with username/password, use the **Sign in using Nuget.org account** link on the  [nuget.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a><span data-ttu-id="93a25-291">哪一個 Microsoft 帳戶連結到我的 nuget.org 帳戶？</span><span class="sxs-lookup"><span data-stu-id="93a25-291">Which Microsoft account is linked to my nuget.org account?</span></span>

<span data-ttu-id="93a25-292">若您忘了哪一個 Microsoft 帳戶與您的 nuget.org 帳戶建立關聯，請遵循下列步驟以取得協助。</span><span class="sxs-lookup"><span data-stu-id="93a25-292">If you have forgotten which Microsoft account is associated with your nuget.org account, please follow the steps below to get assistance.</span></span>
1. <span data-ttu-id="93a25-293">前往 [nuget.org 登入頁面](https://www.nuget.org/users/account/LogOn)，然後按一下 **Need assistance signing in?** (需要登入上的協助嗎？) 連結。</span><span class="sxs-lookup"><span data-stu-id="93a25-293">Go to [nuget.org login page](https://www.nuget.org/users/account/LogOn) and click on **Need assistance signing in?** link.</span></span>
1. <span data-ttu-id="93a25-294">這將會顯示提供協助的快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="93a25-294">This will show you the pop-up dialog box for assistance.</span></span> <span data-ttu-id="93a25-295">遵循此對話方塊中的步驟，以了解與您 nuget.org 帳戶建立關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-295">Follow the steps in this dialog box to understand the associated Microsoft account(s) for your nuget.org account.</span></span>

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a><span data-ttu-id="93a25-296">如何變更我用來登入 nuget.org 的 Microsoft 帳戶？</span><span class="sxs-lookup"><span data-stu-id="93a25-296">How to change the Microsoft account I use for nuget.org login?</span></span>
<span data-ttu-id="93a25-297">若您想要為 nuget.org 使用者變更 Microsoft 帳戶，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-297">If you wish to change the Microsoft account for nuget.org user, follow the steps below.</span></span> <span data-ttu-id="93a25-298">假設您電子郵件為 `account1@outlook.com` 的 Microsoft 帳戶與使用者名稱為 `MyNuGetAccount` 的 nuget.org 帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-298">Lets say your Microsoft account with email `account1@outlook.com` is associated with your nuget.org account with username `MyNuGetAccount`.</span></span> <span data-ttu-id="93a25-299">且您希望將登入帳戶變更成電子郵件為 `account2@outlook.com` 的另一個 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="93a25-299">You wish to change the login to another Microsoft account with email `account2@outlook.com`</span></span>
1. <span data-ttu-id="93a25-300">請使用 **目前關聯的 Microsoft 帳戶**登入，也就是按一下 [使用 Microsoft 帳戶登入] 後，[登入頁面](https://www.nuget.org/users/account/LogOn)上的 `account1@outlook.com`。</span><span class="sxs-lookup"><span data-stu-id="93a25-300">Please sign in using **currently associated Microsoft account** i.e. `account1@outlook.com` on the [login page](https://www.nuget.org/users/account/LogOn) after clicking **Sign in with Microsoft**.</span></span>
1. <span data-ttu-id="93a25-301">登入後，前往[帳戶設定](https://www.nuget.org/account)頁面。</span><span class="sxs-lookup"><span data-stu-id="93a25-301">Once logged in, go to your [account settings](https://www.nuget.org/account) page.</span></span>
1. <span data-ttu-id="93a25-302">展開**登入帳戶**區段。</span><span class="sxs-lookup"><span data-stu-id="93a25-302">Expand the section for **Login Account**.</span></span> <span data-ttu-id="93a25-303">按一下 [變更帳戶] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93a25-303">Click on the **Change Account** button.</span></span>
1. <span data-ttu-id="93a25-304">系統會將您重新導向至 Microsoft 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="93a25-304">You will now be redirected to the microsoft login page.</span></span> <span data-ttu-id="93a25-305">請使用您想要變更關聯的帳戶登入，亦即 `account2@outlook.com`。**注意**：您可能需要在登入流程期間按一下 [Sign out and sign in with different account] \(登出並以其它帳戶登入\)，才能使用其他 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="93a25-305">Please sign in with the account that you wish to change the association to i.e. `account2@outlook.com`. **Note**: you might need to click on **Sign out and sign in with different account** during the sign in flow to be able to login with a different Microsoft account.</span></span>
1. <span data-ttu-id="93a25-306">若您看到以下錯誤訊息，請參閱 [Microsoft 帳戶已與另一個 nuget.org 帳戶連結](#microsoft-account-is-linked-with-another-nugetorg-account)，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="93a25-306">If you see an error like below, see [Microsoft account is linked with another nuget.org account](#microsoft-account-is-linked-with-another-nugetorg-account) for more details.</span></span>
    ><span data-ttu-id="93a25-307">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'.This could happen if it is already linked to another NuGet account.Contact support for more information. (無法更新擁有 'account2 account2@outlook.com' 的 Microsoft 帳戶。若此帳戶已連結到另一個 NuGet 帳戶，就可能發生此情形。請連絡支援人員以取得詳細資訊。)_</span><span class="sxs-lookup"><span data-stu-id="93a25-307">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information._</span></span>

1. <span data-ttu-id="93a25-308">使用第二個帳戶成功登入後，系統會將您重新導向回 nuget.org 帳戶設定頁面，您現在應該會看到新的 Microsoft 帳戶已作為登入帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-308">Once you have successfully signed in with your second account, you will be redirected back to your nuget.org account settings page and you should now see the new Microsoft account associated as the login account.</span></span> <span data-ttu-id="93a25-309">接下來您應在登入 nuget.org 時，使用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-309">Going forward you should use this account when signing into nuget.org.</span></span>

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a><span data-ttu-id="93a25-310">Microsoft 帳戶已與另一個 nuget.org 帳戶連結。</span><span class="sxs-lookup"><span data-stu-id="93a25-310">Microsoft account is linked with another nuget.org account.</span></span>

<span data-ttu-id="93a25-311">若您嘗試變更 Microsoft 登入，並看到以下錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="93a25-311">If you tried changing your Microsoft login and saw the error below:</span></span>
> <span data-ttu-id="93a25-312">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'.This could happen if it is already linked to another NuGet account.Contact support for more information. (無法更新擁有 'account2 account2@outlook.com' 的 Microsoft 帳戶。若此帳戶已連結到另一個 NuGet 帳戶，就可能發生此情形。請連絡支援人員以取得詳細資訊。)_</span><span class="sxs-lookup"><span data-stu-id="93a25-312">_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information._</span></span>

<span data-ttu-id="93a25-313">假設您嘗試將 Microsoft 帳戶登入從使用者名稱為 `MyNuGetAccount1` 之 nuget.org 使用者的 `account1@outlook.com` 變更為電子郵件為 `account2@outlook.com` 的另一個 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-313">Lets say you were trying to change Microsoft account login from `account1@outlook.com` for nuget.org user with username `MyNuGetAccount1` to another Microsoft account with email `account2@outlook.com`.</span></span> <span data-ttu-id="93a25-314">然後看到以上錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="93a25-314">And you see the error above.</span></span>

<span data-ttu-id="93a25-315">**以上錯誤訊息代表什麼意思？**</span><span class="sxs-lookup"><span data-stu-id="93a25-315">**What does the error above mean?**</span></span>

<span data-ttu-id="93a25-316">這代表有與 Microsoft 帳戶建立關聯的另一個 nuget.org 帳戶，且您嘗試將其變更為以上範例中，電子郵件為 `<account2@outlook.com>` 且與另一個 nuget.org 帳戶 (使用者名稱為 `MyNuGetAccount2`) 建立關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-316">It means that there is another nuget.org account which is associated with the Microsoft account that you are trying to change it to i.e. in above example the Microsoft account with email `<account2@outlook.com>` is associated with another nuget.org account with, say, username `MyNuGetAccount2`.</span></span>

<span data-ttu-id="93a25-317">您無法使用連結到其他 nuget.org 帳戶的 Microsoft 帳戶，變更關聯的登入。</span><span class="sxs-lookup"><span data-stu-id="93a25-317">You cannot change the associated login with a Microsoft account that is linked to a different nuget.org account.</span></span>

<span data-ttu-id="93a25-318">**我忘了我有另一個的 nuget.org 帳戶，我要如何找出哪一個是我的 nuget.org 帳戶？**</span><span class="sxs-lookup"><span data-stu-id="93a25-318">**I forgot I had another nuget.org account, how do I find out which nuget.org account it is?**</span></span>

<span data-ttu-id="93a25-319">在[登入頁面](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "登入頁面")上以第二個 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="93a25-319">Login with the second Microsoft account on the [login page](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "login page").</span></span> <span data-ttu-id="93a25-320">這會將您登入至目前與第二個 Microsoft 帳戶建立關聯的 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-320">This will log you into the nuget.org account that is currently associated with the second Microsoft account.</span></span> <span data-ttu-id="93a25-321">您接著可以檢視此帳戶上的已更新套件，及進行帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="93a25-321">You can then view the uploaded packages and perform account management on this account.</span></span>

<span data-ttu-id="93a25-322">**我不在乎第二個 nuget.org 帳戶，且想要使用第二個 Microsoft 帳戶變更第一個 nuget.org 帳戶的登入。該怎麼做？**</span><span class="sxs-lookup"><span data-stu-id="93a25-322">**I do not care about this second nuget.org account, I want to change my login for first nuget.org account with the second Microsoft account. What do I do?**</span></span>

<span data-ttu-id="93a25-323">如果您不在乎第二個 nuget.org 帳戶，但仍想使用電子郵件為 `account2@outlook.com` 的關聯 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-323">If you wish to not care about the second nuget.org account and still want to re-use the associated Microsoft account with email `account2@outlook.com`.</span></span> 

<span data-ttu-id="93a25-324">您可以透過刪除 nuget.org 帳戶，解除 Microsoft 帳戶與 nuget.org 帳戶間的關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-324">You can release the association between the Microsoft account and nuget.org account by deleting the nuget.org account.</span></span>
1. <span data-ttu-id="93a25-325">請遵循這些步驟，以[刪除第二個 nuget.org 帳戶 `MyNuGetAccount2` 的使用者](#how-to-delete-my-nugetorg-account)。</span><span class="sxs-lookup"><span data-stu-id="93a25-325">Follow the steps to [delete user](#how-to-delete-my-nugetorg-account) for the second nuget.org account `MyNuGetAccount2`.</span></span> 
1. <span data-ttu-id="93a25-326">刪除此帳戶後，即可重試這些步驟來[變更 Microsoft 帳戶登入](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)。</span><span class="sxs-lookup"><span data-stu-id="93a25-326">Once this account is deleted, you can retry the steps to [change Microsoft account login](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).</span></span>

<span data-ttu-id="93a25-327">**等一下，我也需要這第二個帳戶。我不想要失去此帳戶，但要變更第一個帳戶的關聯帳戶登入。**</span><span class="sxs-lookup"><span data-stu-id="93a25-327">**Wait, I care about this second account too. I do not want to lose this account but change my associated account logins for first account.**</span></span>

<span data-ttu-id="93a25-328">您必須建立/使用第三個 Microsoft 帳戶，也就是電子郵件為 `account3@outlook.com` 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-328">You will need to create/use a third Microsoft account, say, with email `account3@outlook.com`.</span></span> 
1. <span data-ttu-id="93a25-329">首先，您應使用第二個 Microsoft 帳戶 (nuget.org 上的 `account2@outlook.com`) 登入。遵循上述步驟來變更關聯的登入，並將第三個 Microsoft 帳戶與此 nuget.org 帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-329">First you should login with your second Microsoft account, `account2@outlook.com` on nuget.org. Follow the steps above to change associated logins and associate the third Microsoft account with this nuget.org account.</span></span>
1. <span data-ttu-id="93a25-330">完成後，電子郵件為 `account2@outlook.com` 的第二個 Microsoft 帳戶就可以與第一個 nuget.org 帳戶 `MyNuGetAccount1` 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-330">Once done, your second Microsoft account with email `account2@outlook.com` is free to be associated to your first nuget.org account, `MyNuGetAccount1`.</span></span> <span data-ttu-id="93a25-331">遵循上述相同步驟，以將 Microsoft 登入變更為第二個 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-331">Follow the same steps above to change microsoft logins to the second Microsoft account.</span></span>

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a><span data-ttu-id="93a25-332">使用 Microsoft 帳戶登入，但顯示我的電子郵件已連結到另一個 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="93a25-332">Signing in with Microsoft account shows me my email is linked to another Microsoft account</span></span>
<span data-ttu-id="93a25-333">若您嘗試使用 Microsoft 帳戶，也就是電子郵件 `account1@outlook.com` 登入，且看到以下錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="93a25-333">If you tried to sign in with your Microsoft account, say, with email `account1@outlook.com` and you see an error like below:</span></span>
> <span data-ttu-id="93a25-334">_The account with email 'account1@outlook.com' is linked with another microsoft account._</span><span class="sxs-lookup"><span data-stu-id="93a25-334">_The account with email 'account1@outlook.com' is linked with another microsoft account._</span></span>
>
> <span data-ttu-id="93a25-335">_If you would like to update the linked Microsoft account you can do so from the account settings page. (電子郵件為 'account1@outlook.com' 的帳戶已與另一個 Microsoft 帳戶連結。若您想要更新已連結的 Microsoft 帳戶，可以從帳戶設定頁面執行此動作。)_</span><span class="sxs-lookup"><span data-stu-id="93a25-335">_If you would like to update the linked Microsoft account you can do so from the account settings page._</span></span>

<span data-ttu-id="93a25-336">**以上錯誤訊息代表什麼意思？**</span><span class="sxs-lookup"><span data-stu-id="93a25-336">**What does the error above mean?**</span></span>

<span data-ttu-id="93a25-337">在 nuget.org 建立帳戶時，通訊電子郵件地址會與該帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-337">When an account is created on nuget.org, there is a communication email address associated with that account.</span></span> <span data-ttu-id="93a25-338">這通常與關聯 Microsoft 帳戶使用的電子郵件地址相同。</span><span class="sxs-lookup"><span data-stu-id="93a25-338">This is usually same as the email address that is used for associated Microsoft account.</span></span> <span data-ttu-id="93a25-339">不過，您可以選擇指定其他電子郵件地址進行通訊。</span><span class="sxs-lookup"><span data-stu-id="93a25-339">However, you could choose to specify a different email address for communication.</span></span> <span data-ttu-id="93a25-340">所以，技術上來說，您可以擁有其他 Microsoft 帳戶 (亦即 `account2@outlook.com`)，且連結到通訊電子郵件地址為 `account1@outlook.com` 的 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-340">So, technically, you could have a different Microsoft account, say with `account2@outlook.com` that is linked to nuget.org account with communication email address as `account1@outlook.com`.</span></span>

<span data-ttu-id="93a25-341">因此，上方的錯誤訊息代表已經有通訊電子郵件地址為 `account1@outlook.com` 的現有 nuget.org 帳戶，但卻與電子郵件**不是** `account1@outlook.com` 的另一個 Microsoft 帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-341">So the error above means that there already exists nuget.org account with communication email address `account1@outlook.com` but is associated with another Microsoft account with email **that is not** `account1@outlook.com`.</span></span>

<span data-ttu-id="93a25-342">**如何找出哪一個 Microsoft 帳戶連結到此 nuget.org 帳戶？**</span><span class="sxs-lookup"><span data-stu-id="93a25-342">**How do I find which Microsoft account is linked to this nuget.org account?**</span></span>

<span data-ttu-id="93a25-343">您應使用[登入協助](#which-microsoft-account-is-linked-to-my-nugetorg-account)流程，找出哪一個 Microsoft 帳戶連結到電子郵件地址為 `account1@outlook.com` 的 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-343">You should use the [sign in assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) flow to figure out which Microsoft account is linked to the nuget.org account with the email address `account1@outlook.com`.</span></span>

<span data-ttu-id="93a25-344">**我想要使用我的 Microsoft 帳戶覆寫該帳戶**</span><span class="sxs-lookup"><span data-stu-id="93a25-344">**I want to override that account with my Microsoft account**</span></span>

<span data-ttu-id="93a25-345">請遵循[無法使用 Microsoft 登入，如何復原我的 nuget.org 帳戶](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)一節所述的步驟，將 Microsoft 帳戶與現有的 nuget.org 帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-345">Follow the steps in [Unable to use microsoft login, how do I recover my nuget.org account](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) section to associate your Microsoft account with the existing nuget.org account.</span></span>

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a><span data-ttu-id="93a25-346">無法使用 Microsoft 登入，如何復原我的 nuget.org 帳戶？</span><span class="sxs-lookup"><span data-stu-id="93a25-346">Unable to use microsoft login, how do I recover my nuget.org account?</span></span>

<span data-ttu-id="93a25-347">若您已嘗試使用[登入協助](#which-microsoft-account-is-linked-to-my-nugetorg-account)，且沒有與 nuget.org 帳戶建立關聯之 Microsoft 帳戶的存取權，請遵循下列步驟，以將新的 Microsoft 帳戶連結到 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-347">If you tried using the [sign in assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) and you do not have access to the Microsoft account that is associated with your nuget.org account, please follow the steps below to link a new Microsoft account to your nuget.org account.</span></span>
1. <span data-ttu-id="93a25-348">**需求**:您需要 Microsoft 帳戶 (未與任何現有 nuget.org 帳戶建立關聯) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="93a25-348">**Requirement**: You will need an access to a Microsoft account(which is not associated with any existing nuget.org accounts).</span></span> <span data-ttu-id="93a25-349">如果沒有的話，您可以[建立](https://signup.live.com)帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-349">If you do not have one, you can [create](https://signup.live.com) one.</span></span>
2. <span data-ttu-id="93a25-350">請遵循[復原密碼登入的步驟](#how-to-recover-nugetorg-password-login)，若您擁有密碼登入，則略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-350">Follow the [steps to recover your password login](#how-to-recover-nugetorg-password-login), if you have the password login skip this step.</span></span>
3. <span data-ttu-id="93a25-351">以使用者名稱/密碼登入，[登入 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。</span><span class="sxs-lookup"><span data-stu-id="93a25-351">[Login to nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) using the username/password login.</span></span>
4. <span data-ttu-id="93a25-352">登入後，就會顯示出快顯對話方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="93a25-352">Once logged in, you will see the popup dialog show up like below.</span></span> <span data-ttu-id="93a25-353">此為密碼中止對話方塊。</span><span class="sxs-lookup"><span data-stu-id="93a25-353">This is the password discontinuation dialog box.</span></span>
5. <span data-ttu-id="93a25-354">**注意**：請忽略使用特定 Microsoft 帳戶登入的指示。</span><span class="sxs-lookup"><span data-stu-id="93a25-354">**NOTE**: Please ignore the instruction to login with the specified Microsoft account.</span></span> <span data-ttu-id="93a25-355">您現可將 nuget.org 帳戶連結到任何其他 Microsoft 登入。</span><span class="sxs-lookup"><span data-stu-id="93a25-355">You can now link your nuget.org account to any other Microsoft login.</span></span>
6. <span data-ttu-id="93a25-356">按一下 [使用 Microsoft 帳戶登入] 按鈕，然後使用您擁有其存取權的 Microsoft 帳戶登入，如步驟 1 所述。</span><span class="sxs-lookup"><span data-stu-id="93a25-356">Click on the button **Sign in with Microsoft** and login with the Microsoft account that you have an access to, as mentioned in step 1.</span></span>
7. <span data-ttu-id="93a25-357">您的帳戶現在會連結到新的 Microsoft 帳戶，且往後可以將其用來登入 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="93a25-357">Your account will now be linked to the new Microsoft account, which you can use to log into nuget.org going forward.</span></span>

    ![連結 MSA 對話方塊](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a><span data-ttu-id="93a25-359">如何將我的 nuget.org 帳戶轉換為組織？</span><span class="sxs-lookup"><span data-stu-id="93a25-359">How to transform my nuget.org account to an organization?</span></span>

<span data-ttu-id="93a25-360">若您想要將帳戶轉換為組織，且此帳戶已經與 Microsoft 帳戶登入建立關聯，那麼請遵循 [organizations on nuget org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org) (nuget org 上的組織) 一文中所提供的步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-360">If you want to transform your account to an organization, and this account is already associated with a Microsoft account login, please follow the steps given in the documentation for [organizations on nuget org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).</span></span>

<span data-ttu-id="93a25-361">不過，若您的 nuget.org 帳戶未與 Microsoft 帳戶建立關聯/連結，則可以遵循下列步驟將此帳戶轉換為組織。</span><span class="sxs-lookup"><span data-stu-id="93a25-361">If however, your nuget.org account is not associated/linked with a Microsoft account, you can follow the steps below to transform this account to an organization.</span></span>
1. <span data-ttu-id="93a25-362">**需求**:您必須先在 nuget.org 上建立個別帳戶，以作為組織帳戶上的系統管理員使用。</span><span class="sxs-lookup"><span data-stu-id="93a25-362">**Requirement**: You need to have an individual account first created on nuget.org to be used as an admin on the org account.</span></span> <span data-ttu-id="93a25-363">如果沒有的話，請[建立新的 nuget.org 帳戶](#how-to-create-a-nugetorg-account)</span><span class="sxs-lookup"><span data-stu-id="93a25-363">If you do not have one, please [create a new nuget.org account](#how-to-create-a-nugetorg-account)</span></span>
2. <span data-ttu-id="93a25-364">若您沒有可供使用的密碼登入，請遵循為 nuget.org 帳戶[復原密碼登入的步驟](#how-to-recover-nugetorg-password-login)，如果有的話，略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-364">Follow the [steps to recover your password login](#how-to-recover-nugetorg-password-login) for your nuget.org account if you do not have password login for it, if you do, skip this step.</span></span>
3. <span data-ttu-id="93a25-365">以使用者名稱/密碼登入，[登入 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。</span><span class="sxs-lookup"><span data-stu-id="93a25-365">[Login to nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) using the username/password login.</span></span>
4. <span data-ttu-id="93a25-366">登入後，就會顯示出快顯對話方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="93a25-366">Once logged in, you will see the popup dialog show up like below.</span></span> <span data-ttu-id="93a25-367">此為密碼中止對話方塊。</span><span class="sxs-lookup"><span data-stu-id="93a25-367">This is the password discontinuation dialog box.</span></span> 
    > [!Important]
    > <span data-ttu-id="93a25-368">忽略此對話方塊，**請勿**按一下 [使用Microsoft 帳戶登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93a25-368">Ignore this dialog box, **do not** click on the **Sign in with microsoft** button.</span></span>

5. <span data-ttu-id="93a25-369">移至 [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)。</span><span class="sxs-lookup"><span data-stu-id="93a25-369">Go to [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform).</span></span> <span data-ttu-id="93a25-370">這會使您無須連結到 Microsoft 帳戶，就能夠將 nuget.org 帳戶轉換為組織。</span><span class="sxs-lookup"><span data-stu-id="93a25-370">This will allow you to convert the nuget.org account to an org without linking to a Microsoft account.</span></span>
6. <span data-ttu-id="93a25-371">為您的個人 nuget.org 帳戶/在步驟 1 建立的帳戶，指定系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="93a25-371">Specify the admin username for your personal nuget.org account/the account you created in Step 1.</span></span>
7. <span data-ttu-id="93a25-372">請遵循指示以完成將此帳戶轉換為組織。</span><span class="sxs-lookup"><span data-stu-id="93a25-372">Follow the instructions to complete transformation of this account to an organization.</span></span>

    ![連結 MSA 對話方塊](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a><span data-ttu-id="93a25-374">具有非受控租用戶之 AAD 帳戶的 nuget.org 登入問題？</span><span class="sxs-lookup"><span data-stu-id="93a25-374">nuget.org login issues for AAD accounts with unmanaged tenant?</span></span>

<span data-ttu-id="93a25-375">若您使用電子郵件帳戶網域 (@yourdomain.com) 在登入流程中看到以下錯誤訊息，請參閱下列步驟來復原 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-375">If you see an error like below during your login flow with your email account domain(@yourdomain.com), see the steps below to recover your nuget.org account.</span></span>

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

<span data-ttu-id="93a25-376">**這項登入期間的非受控狀態是什麼？為什麼現在會發生這個問題？**</span><span class="sxs-lookup"><span data-stu-id="93a25-376">**What is this unmanaged state thing during login? And why is this happening now?**</span></span> 

<span data-ttu-id="93a25-377">看來您的帳戶之前註冊為個人 Microsoft 帳戶，且沒發生什麼問題，不過現在您的帳戶似乎已註冊為 Azure Active Directory (用來驗證 Microsoft 帳戶的識別服務) 中的「非受控」租用戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-377">Your account seems to be previously registered as a personal Microsoft account and it worked fine, however, now it seems like your account has been registered as an "Unmanaged" tenant in the Azure Active Directory (the identity service which we use to authenticate Microsoft accounts).</span></span> 

<span data-ttu-id="93a25-378">若您或組織中的某人 (電子郵件地址為 @yourdomain.com) 使用其中一項 AAD 整合服務註冊，或進行會為所使用 Microsoft 帳戶網域 (也就是 @yourdomain.com) 建立這類「非受控」租用戶的 [Azure Active Directory 自助式註冊](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)，就可能發生此情形。</span><span class="sxs-lookup"><span data-stu-id="93a25-378">This could have happened if you or someone from your organization(with @yourdomain.com email address) registered with one of the AAD integrated services or did a [self-service signup for Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), which creates such an "Unmanaged" tenant for the used Microsoft account domain(@yourdomain.com in your case).</span></span> 

<span data-ttu-id="93a25-379">**該如何復原我的帳戶？**</span><span class="sxs-lookup"><span data-stu-id="93a25-379">**What can I do to recover my account?**</span></span>

<span data-ttu-id="93a25-380">因為此帳戶在 Azure Active directory 中具有這類「非受控」租用戶帳戶，所以目前我們 (nuget.org) 無法予以驗證。</span><span class="sxs-lookup"><span data-stu-id="93a25-380">At this moment there is not a way for us (nuget.org) to authenticate accounts with such "Unmanaged" tenant accounts in Azure Active directory.</span></span> <span data-ttu-id="93a25-381">我們正在尋找更好的方法來驗證這類帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-381">We are looking in to a better way to authenticate such accounts.</span></span>

<span data-ttu-id="93a25-382">若您想要使用 Microsoft 帳戶 (@yourdomain.com) 登入 nuget.org，您 (或公司的系統管理員) 就必須使用電子郵件地址 "@yourdomain.com" 進行 DNS 驗證來驗證使用者，以宣告 AAD 的擁有權。</span><span class="sxs-lookup"><span data-stu-id="93a25-382">If you want to login to nuget.org with your Microsoft account(@yourdomain.com), you(or an administrator at your company) will need to claim the ownership of the AAD by doing a DNS validation to authenticate users with email address "@yourdomain.com".</span></span> <span data-ttu-id="93a25-383">請遵循由 Azure Active Directory 所記載[網域系統管理員接管](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)的步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-383">Please follow the steps for [domains admin takeover](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) documented by the Azure Active directory.</span></span> <span data-ttu-id="93a25-384">完成後，您的一般登入應開始正常運作。</span><span class="sxs-lookup"><span data-stu-id="93a25-384">Once this is done, your normal login should start working.</span></span>

<span data-ttu-id="93a25-385">**我不想要執行這些動作，可以復原我帳戶的其他方式為何？**</span><span class="sxs-lookup"><span data-stu-id="93a25-385">**I don’t want to do all that, what is the other way to recover my account?**</span></span>

<span data-ttu-id="93a25-386">您可以[建立](https://www.microsoft.com/en-us/account)新的 Microsoft 帳戶 (搭配**未**與 @yourdomain.com 建立關聯的電子郵件)</span><span class="sxs-lookup"><span data-stu-id="93a25-386">You can [create](https://www.microsoft.com/en-us/account) a new Microsoft account (with an email **not** associated with @yourdomain.com).</span></span> <span data-ttu-id="93a25-387">遵循[復原您的 nuget.org 帳戶](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)一節中提供的步驟。</span><span class="sxs-lookup"><span data-stu-id="93a25-387">Follow steps given in [recover your nuget.org account](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) section.</span></span>

### <a name="how-do-i-change-my-nugetorg-account-username"></a><span data-ttu-id="93a25-388">如何變更我的 nuget.org 帳戶使用者名稱？</span><span class="sxs-lookup"><span data-stu-id="93a25-388">How do I change my nuget.org account username?</span></span>

<span data-ttu-id="93a25-389">您不能進行變更。</span><span class="sxs-lookup"><span data-stu-id="93a25-389">You cannot.</span></span> <span data-ttu-id="93a25-390">因為原則的關係，我們目前不允許變更使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="93a25-390">As a matter of policy we do not allow the change of usernames as of yet.</span></span> <span data-ttu-id="93a25-391">唯一變更使用者名稱的方式為，以想要的使用者名稱建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-391">The only way to change your username is to create a new account with the desired username.</span></span> <span data-ttu-id="93a25-392">建議您在建立新帳戶之前，先將現有的帳戶刪除，否則您將無法重複使用註冊的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-392">We recommend you delete your existing account before you create a new one, otherwise you will not be able to reuse your registered Microsoft account.</span></span>
> [!Important]
> <span data-ttu-id="93a25-393">刪除使用者仍會**保留** `username`。</span><span class="sxs-lookup"><span data-stu-id="93a25-393">Deleting the user will still **reserve** the `username`.</span></span> <span data-ttu-id="93a25-394">您將無法再重複使用相同的使用者名稱，**這也包含大小寫的變更**。</span><span class="sxs-lookup"><span data-stu-id="93a25-394">You will not be able to reuse the same username again and **this includes the change of casings**.</span></span> <span data-ttu-id="93a25-395">例如，若您建立了使用者名稱為 `mycoolname` 的使用者，且想要將其變更為 `MyCoolName` (大小寫變更)，則在刪除使用者後，就不可能達成目的。</span><span class="sxs-lookup"><span data-stu-id="93a25-395">As an example if you created a user with username `mycoolname` and you want to change this to `MyCoolName`(casing changes), it will not be possible after deleting the user.</span></span>

<span data-ttu-id="93a25-396">請遵循[刪除 nuget.org 帳戶](#how-to-delete-my-nugetorg-account)一節中提供的步驟，並以正確的使用者名稱[註冊新帳戶](#how-to-create-a-new-nugetorg-account)。</span><span class="sxs-lookup"><span data-stu-id="93a25-396">Follow the steps given in [delete your nuget.org account](#how-to-delete-my-nugetorg-account) section and to [register a new account](#how-to-create-a-new-nugetorg-account) with correct username.</span></span>

### <a name="how-to-delete-my-nugetorg-account"></a><span data-ttu-id="93a25-397">如何刪除我的 nuget.org 帳戶？</span><span class="sxs-lookup"><span data-stu-id="93a25-397">How to delete my nuget.org account?</span></span>

<span data-ttu-id="93a25-398">請注意，若要刪除您的帳戶，建議轉換您為唯一擁有者的所有套件擁有權。</span><span class="sxs-lookup"><span data-stu-id="93a25-398">To delete your account, please note that we recommend that you transfer the ownership of any packages where you are the sole owner.</span></span> <span data-ttu-id="93a25-399">您可以深入了解如何[管理套件擁有者](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="93a25-399">You can read more about [managing package owners](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) on how to do it.</span></span> <span data-ttu-id="93a25-400">這也有助於我們加速處理您的要求。</span><span class="sxs-lookup"><span data-stu-id="93a25-400">This will also help us expedite your request.</span></span>

> [!Important]
> <span data-ttu-id="93a25-401">刪除使用者會導致以下情形：</span><span class="sxs-lookup"><span data-stu-id="93a25-401">Deleting the user will result in following:</span></span>
>  1. <span data-ttu-id="93a25-402">撤銷關聯的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="93a25-402">Revoke associated API key(s).</span></span> 
>  2. <span data-ttu-id="93a25-403">移除帳戶在所有子套件上的擁有者身分。</span><span class="sxs-lookup"><span data-stu-id="93a25-403">Remove the account as an owner for any child packages.</span></span>
>  3. <span data-ttu-id="93a25-404">解除所有先前既存識別碼前置詞保留與此帳戶的關聯。</span><span class="sxs-lookup"><span data-stu-id="93a25-404">Dissociate all previously existent ID prefix reservations with this account.</span></span>
>  4. <span data-ttu-id="93a25-405">移除帳戶在所有組織的成員身分。</span><span class="sxs-lookup"><span data-stu-id="93a25-405">Remove the account as a member of any organizations.</span></span>
>  5. <span data-ttu-id="93a25-406">您的使用者名稱將會保留，且只有擁有我們的權限才能予以重複使用。</span><span class="sxs-lookup"><span data-stu-id="93a25-406">Your username will be reserved and no one will be able to re-use it again without our permissions.</span></span>

<span data-ttu-id="93a25-407">請遵循下列步驟以繼續刪除帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a25-407">Follow the following steps to proceed with account deletion.</span></span>
1. <span data-ttu-id="93a25-408">使用您想要刪除的帳戶[登入 nuget.org](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="93a25-408">[Login to nuget.org](https://www.nuget.org/users/account/LogOn) with the account you wish to delete.</span></span>
2. <span data-ttu-id="93a25-409">按一下此 URL：[https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)，然後遵循這些步驟，以提交刪除帳戶的要求。</span><span class="sxs-lookup"><span data-stu-id="93a25-409">Click on this url: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) and follow the steps to submit the request for deleting the account.</span></span>

<span data-ttu-id="93a25-410">我們的客戶支援會處理此要求，並將帳戶刪除。</span><span class="sxs-lookup"><span data-stu-id="93a25-410">Our customer support will process this request and perform the account deletion.</span></span>
