---
title: 安全軟體供應鏈的最佳作法
description: 使用 NuGet & GitHub 保護軟體供應鏈安全的最佳做法。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 125579832db2ac32217d24f6fc6fc1b555f54350
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101423"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a><span data-ttu-id="7de08-103">安全軟體供應鏈的最佳作法</span><span class="sxs-lookup"><span data-stu-id="7de08-103">Best practices for a secure software supply chain</span></span>

<span data-ttu-id="7de08-104">開放原始碼隨處都有。</span><span class="sxs-lookup"><span data-stu-id="7de08-104">Open Source is everywhere.</span></span> <span data-ttu-id="7de08-105">它是在許多專屬的程式碼基底和社區專案中。</span><span class="sxs-lookup"><span data-stu-id="7de08-105">It is in many proprietary codebases and community projects.</span></span> <span data-ttu-id="7de08-106">對於組織和個人來說，今天的問題不是您是或不是使用開放原始碼，而是您使用的開放原始碼程式碼，還有多少。</span><span class="sxs-lookup"><span data-stu-id="7de08-106">For organizations and individuals, the question today is not whether you are or are not using open-source code, but what open-source code you are using, and how much.</span></span>

<span data-ttu-id="7de08-107">如果您不知道軟體供應鏈的內容，其中一個相依性的上游弱點可能是嚴重問題，讓您和您的客戶遭受潛在的危害。</span><span class="sxs-lookup"><span data-stu-id="7de08-107">If you're not aware of what is in your software supply chain, an upstream vulnerability in one of your dependencies can be fatal, making you, and your customers, vulnerable to a potential compromise.</span></span> <span data-ttu-id="7de08-108">在本檔中，我們將深入探討「軟體供應鏈」的意義、其重要性，以及如何使用最佳做法來協助保護您的專案供應鏈。</span><span class="sxs-lookup"><span data-stu-id="7de08-108">In this document, we will dive deeper into what the term “software supply chain” means, why it matters, and how you can help secure your project’s supply chain with best practices.</span></span>

![Octoverse 2020-開放原始碼的狀態](media/opensource-percent.png)

## <a name="dependencies"></a><span data-ttu-id="7de08-110">相依性</span><span class="sxs-lookup"><span data-stu-id="7de08-110">Dependencies</span></span> 

<span data-ttu-id="7de08-111">「軟體供應鏈」一詞是用來參考您的軟體及其來源的所有專案。</span><span class="sxs-lookup"><span data-stu-id="7de08-111">The term software supply chain is used to refer to everything that goes into your software and where it comes from.</span></span> <span data-ttu-id="7de08-112">它是您的軟體供應鏈相依的相依性和屬性。</span><span class="sxs-lookup"><span data-stu-id="7de08-112">It is the dependencies and properties of your dependencies that your software supply chain depends on.</span></span> <span data-ttu-id="7de08-113">相依性是您的軟體需要執行的相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-113">A dependency is what your software needs to run.</span></span> <span data-ttu-id="7de08-114">它可以是程式碼、二進位檔或其他元件，以及它們的來源，例如存放庫或封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="7de08-114">It can be code, binaries, or other components, and where they come from, such as a repository or package manager.</span></span>

<span data-ttu-id="7de08-115">它包括撰寫程式碼的人員、發表者、如何檢查安全性問題、已知弱點、支援的版本、授權資訊，以及任何在程式的任何時間點的內容。</span><span class="sxs-lookup"><span data-stu-id="7de08-115">It includes who wrote the code, when it was contributed, how it was reviewed for security issues, known vulnerabilities, supported versions, license information, and just about anything that touches it at any point of the process.</span></span>

<span data-ttu-id="7de08-116">您的供應鏈也會將堆疊的其他部分包含在單一應用程式之外，例如您的組建和封裝腳本，或執行應用程式所依賴之基礎結構的軟體。</span><span class="sxs-lookup"><span data-stu-id="7de08-116">Your supply chain also encompasses other parts of your stack beyond a single application, such as your build and packaging scripts or the software that runs the infrastructure your application relies on.</span></span>

## <a name="vulnerabilities"></a><span data-ttu-id="7de08-117">弱點</span><span class="sxs-lookup"><span data-stu-id="7de08-117">Vulnerabilities</span></span>

<span data-ttu-id="7de08-118">現今的軟體相依性很普遍。</span><span class="sxs-lookup"><span data-stu-id="7de08-118">Today, software dependencies are pervasive.</span></span> <span data-ttu-id="7de08-119">針對您不需要自行撰寫的功能，您的專案使用數百個開放原始碼相依性，是很常見的情況。</span><span class="sxs-lookup"><span data-stu-id="7de08-119">It is quite common for your projects to use hundreds of open-source dependencies for functionality that you did not have to write yourself.</span></span> <span data-ttu-id="7de08-120">這可能表示您大部分的應用程式都是由您未撰寫的程式碼所組成。</span><span class="sxs-lookup"><span data-stu-id="7de08-120">This may mean that most of your application consists of code that you did not author.</span></span> 

![Octoverse 2020-相依性的狀態](media/dependencies.png)

<span data-ttu-id="7de08-122">協力廠商或開放原始碼相依性中可能的弱點，是您無法控制與您撰寫的程式碼緊密相關的相依性，這可能會在您的供應鏈中產生潛在的安全性風險。</span><span class="sxs-lookup"><span data-stu-id="7de08-122">Possible vulnerabilities in your third-party or open-source dependencies, are presumably dependencies you cannot control as tightly as the code you write, which can create potential security risks in your supply chain.</span></span>

<span data-ttu-id="7de08-123">如果其中一個相依性有弱點，您也可能會遇到弱點。</span><span class="sxs-lookup"><span data-stu-id="7de08-123">If one of these dependencies has a vulnerability, the chances are you have a vulnerability as well.</span></span> <span data-ttu-id="7de08-124">這可能會令人驚訝，因為您的其中一個相依性可能會變更，而您甚至不知道。</span><span class="sxs-lookup"><span data-stu-id="7de08-124">This can be scary as one of your dependencies may change without you even knowing.</span></span> <span data-ttu-id="7de08-125">即使存在於目前的相依性中，但不是可利用的弱點，也可以在未來進行攻擊。</span><span class="sxs-lookup"><span data-stu-id="7de08-125">Even if a vulnerability exists in a dependency today, but is not exploitable, it can be exploitable in the future.</span></span> 

<span data-ttu-id="7de08-126">能夠利用數千個開放原始碼開發人員和程式庫作者的工作，表示數以千計的陌生人可有效地參與您的生產程式碼。</span><span class="sxs-lookup"><span data-stu-id="7de08-126">Being able to leverage the work of thousands of open-source developers and library authors means that thousands of strangers can effectively contribute directly to your production code.</span></span> <span data-ttu-id="7de08-127">您的產品（透過軟體供應鏈）受未修補的弱點、無害錯誤或甚至惡意的惡意攻擊所影響。</span><span class="sxs-lookup"><span data-stu-id="7de08-127">Your product, through your software supply chain, is affected by unpatched vulnerabilities, innocent mistakes, or even malicious attacks against dependencies.</span></span>

## <a name="supply-chain-compromises"></a><span data-ttu-id="7de08-128">供應鏈的危害</span><span class="sxs-lookup"><span data-stu-id="7de08-128">Supply chain compromises</span></span>

<span data-ttu-id="7de08-129">供應鏈的傳統定義來自製造;這是建立和提供事物所需的程式鏈。</span><span class="sxs-lookup"><span data-stu-id="7de08-129">The traditional definition of a supply chain comes from manufacturing; it is the chain of processes required to make and supply something.</span></span> <span data-ttu-id="7de08-130">它包括規劃、材質供應、製造和零售。</span><span class="sxs-lookup"><span data-stu-id="7de08-130">It includes planning, supply of materials, manufacturing, and retail.</span></span> <span data-ttu-id="7de08-131">除了資料以外，軟體供應鏈也是很類似的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7de08-131">A software supply chain is similar, except instead of materials, it is code.</span></span> <span data-ttu-id="7de08-132">它不是製造，而是開發。</span><span class="sxs-lookup"><span data-stu-id="7de08-132">Instead of manufacturing, it is development.</span></span> <span data-ttu-id="7de08-133">程式碼是來自供應商、商業或開放原始碼，而不是從基礎深入探討，而一般而言，開放原始碼程式碼是來自存放庫。</span><span class="sxs-lookup"><span data-stu-id="7de08-133">Instead of digging ore from the ground, code is sourced from suppliers, commercial or open source, and, in general, the open-source code comes from repositories.</span></span> <span data-ttu-id="7de08-134">從存放庫新增程式碼表示您的產品會依賴該程式碼。</span><span class="sxs-lookup"><span data-stu-id="7de08-134">Adding code from a repository means your product takes a dependency on that code.</span></span>

<span data-ttu-id="7de08-135">在特意將惡意程式碼新增至相依性時，會使用該相依性的供應鏈將程式碼散發至其受害者，以提供軟體供應鏈攻擊的其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="7de08-135">One example of a software supply chain attack occurs when malicious code is purposefully added to a dependency, using the supply chain of that dependency to distribute the code to its victims.</span></span> <span data-ttu-id="7de08-136">供應鏈攻擊是真實的。</span><span class="sxs-lookup"><span data-stu-id="7de08-136">Supply chain attacks are real.</span></span> <span data-ttu-id="7de08-137">有許多方法可以攻擊供應鏈，包括直接插入惡意程式碼作為新的參與者、接管參與者的帳戶，而不會有其他人注意，或甚至是危及簽署金鑰來散發未正式參與的軟體。</span><span class="sxs-lookup"><span data-stu-id="7de08-137">There are many methods to attack a supply chain, from directly inserting malicious code as a new contributor, to taking over a contributor’s account without others noticing, or even compromising a signing key to distribute software that is not officially part of the dependency.</span></span>

<span data-ttu-id="7de08-138">軟體供應鏈攻擊本身並不是最終的目標，而是讓攻擊者插入惡意程式碼或提供後門以供日後存取的機會。</span><span class="sxs-lookup"><span data-stu-id="7de08-138">A software supply chain attack is in and of itself rarely the end goal, rather it is the beginning of an opportunity for an attacker to insert malware or provide a backdoor for future access.</span></span>

![Octoverse 2020-弱點生命週期的狀態](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a><span data-ttu-id="7de08-140">未修補的軟體</span><span class="sxs-lookup"><span data-stu-id="7de08-140">Unpatched software</span></span>

<span data-ttu-id="7de08-141">現今使用開放原始碼是很重要的，預計很快就會變慢。</span><span class="sxs-lookup"><span data-stu-id="7de08-141">The use of open source today is significant and is not expected to slow down anytime soon.</span></span> <span data-ttu-id="7de08-142">假設我們不打算停止使用開放原始碼軟體，提供連鎖安全性的威脅就是未修補的軟體。</span><span class="sxs-lookup"><span data-stu-id="7de08-142">Given that we are not going to stop using open-source software, the threat to supply chain security is unpatched software.</span></span> <span data-ttu-id="7de08-143">知道，您要如何解決專案相依性有弱點的風險？</span><span class="sxs-lookup"><span data-stu-id="7de08-143">Knowing that, how can you address the risk that a dependency of your project has a vulnerability?</span></span>

- <span data-ttu-id="7de08-144">**瞭解您環境中的內容。**</span><span class="sxs-lookup"><span data-stu-id="7de08-144">**Knowing what is in your environment.**</span></span> <span data-ttu-id="7de08-145">這需要探索您的相依性和任何可轉移的相依性，以瞭解這些相依性的風險，例如弱點或授許可權制。</span><span class="sxs-lookup"><span data-stu-id="7de08-145">This requires discovering your dependencies and any transitive dependencies to understand the risks of those dependencies such as vulnerabilities or licensing restrictions.</span></span>
- <span data-ttu-id="7de08-146">**管理您的相依性。**</span><span class="sxs-lookup"><span data-stu-id="7de08-146">**Manage your dependencies.**</span></span> <span data-ttu-id="7de08-147">探索到新的安全性弱點時，您必須判斷是否受到影響，如果是，則更新為可用的最新版本和安全性修補程式。</span><span class="sxs-lookup"><span data-stu-id="7de08-147">When a new security vulnerability is discovered, you must determine whether you are impacted, and if so, update to the latest version and security patch available.</span></span> <span data-ttu-id="7de08-148">這對於審核導入新相依性或定期審核較舊相依性的變更特別重要。</span><span class="sxs-lookup"><span data-stu-id="7de08-148">This is especially important to review changes that introduce new dependencies or regularly auditing older dependencies.</span></span>
- <span data-ttu-id="7de08-149">**監視您的供應鏈。**</span><span class="sxs-lookup"><span data-stu-id="7de08-149">**Monitor your supply chain.**</span></span> <span data-ttu-id="7de08-150">這是透過審核您已備妥的控制項來管理您的相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-150">This is by auditing the controls you have in place to manage your dependencies.</span></span> <span data-ttu-id="7de08-151">這可協助您針對相依性強制符合更嚴格的條件。</span><span class="sxs-lookup"><span data-stu-id="7de08-151">This will help you enforce more restrictive conditions to be met for your dependencies.</span></span>

![Octoverse 2020-諮詢的狀態](media/advisories.png)

<span data-ttu-id="7de08-153">我們將涵蓋 NuGet 和 GitHub 提供的各種工具和技術，您可以立即使用這些工具和技術來解決專案內的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="7de08-153">We will cover various tools and techniques that NuGet and GitHub provides, which you can use today to address potential risks inside your project.</span></span> 

## <a name="knowing-what-is-in-your-environment"></a><span data-ttu-id="7de08-154">瞭解您環境中的內容</span><span class="sxs-lookup"><span data-stu-id="7de08-154">Knowing what is in your environment</span></span>

### <a name="nuget-dependency-graph"></a><span data-ttu-id="7de08-155">NuGet 相依性圖形</span><span class="sxs-lookup"><span data-stu-id="7de08-155">NuGet dependency graph</span></span>

<span data-ttu-id="7de08-156">**📦 套件取用者**</span><span class="sxs-lookup"><span data-stu-id="7de08-156">**📦 Package Consumer**</span></span>

<span data-ttu-id="7de08-157">您可以直接查看個別的專案檔，以在專案中查看您的 NuGet 相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-157">You can view your NuGet dependencies in your project by looking directly at the respective project file.</span></span>

<span data-ttu-id="7de08-158">這通常會在下列兩個位置中找到：</span><span class="sxs-lookup"><span data-stu-id="7de08-158">This is typically found in one of two places:</span></span>

-   <span data-ttu-id="7de08-159">[`packages.config`](../reference/packages-config.md) –位於專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="7de08-159">[`packages.config`](../reference/packages-config.md) – Located in the project root.</span></span>
-   <span data-ttu-id="7de08-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) –位於專案檔中。</span><span class="sxs-lookup"><span data-stu-id="7de08-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Located in the project file.</span></span> 

<span data-ttu-id="7de08-161">根據您用來管理 NuGet 相依性的方法，您也可以使用 Visual Studio 直接在 [方案總管](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer) 或 [NuGet 封裝管理員](../consume-packages/install-use-packages-visual-studio.md)中查看相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-161">Depending on what method you use to manage your NuGet dependencies, you can also use Visual Studio to view your dependencies directly in [Solution Explorer](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer) or [NuGet Package Manager](../consume-packages/install-use-packages-visual-studio.md).</span></span>

<span data-ttu-id="7de08-162">在 CLI 環境中，您可以使用 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令來列出專案或解決方案的相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-162">For CLI environments, you can use the [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command to list out your project or solution’s dependencies.</span></span> 

<span data-ttu-id="7de08-163">如需管理 NuGet 相依性的詳細資訊， [請參閱下列檔](../consume-packages/overview-and-workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="7de08-163">For more information on managing NuGet dependencies, [see the following documentation](../consume-packages/overview-and-workflow.md).</span></span>

### <a name="github-dependency-graph"></a><span data-ttu-id="7de08-164">GitHub 相依性關係圖</span><span class="sxs-lookup"><span data-stu-id="7de08-164">GitHub dependency graph</span></span> 

<span data-ttu-id="7de08-165">**📦 套件取用者 | 📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-165">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-166">您可以使用 GitHub 的相依性圖形來查看您的專案相依的套件，以及相依于該套件的存放庫。</span><span class="sxs-lookup"><span data-stu-id="7de08-166">You can use GitHub’s dependency graph to see the packages your project depends on and the repositories that depend on it.</span></span> <span data-ttu-id="7de08-167">這可協助您查看其相依性中偵測到的任何弱點。</span><span class="sxs-lookup"><span data-stu-id="7de08-167">This can help you see any vulnerabilities detected in its dependencies.</span></span>

<span data-ttu-id="7de08-168">如需 GitHub 存放庫相依性的詳細資訊， [請參閱下列檔](https://github.co/dependency-graph)。</span><span class="sxs-lookup"><span data-stu-id="7de08-168">For more information on GitHub repository dependencies, [see the following documentation](https://github.co/dependency-graph).</span></span>

### <a name="dependency-versions"></a><span data-ttu-id="7de08-169">相依性版本</span><span class="sxs-lookup"><span data-stu-id="7de08-169">Dependency versions</span></span>

<span data-ttu-id="7de08-170">**📦 套件取用者 | 📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-170">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-171">為了確保安全的供應鏈相依性，您會想要確保所有相依性 & 工具都會定期更新為最新的穩定版本，因為它們通常會包含已知弱點的最新功能和安全性修補程式。</span><span class="sxs-lookup"><span data-stu-id="7de08-171">To ensure a secure supply chain of dependencies, you will want to ensure that all of your dependencies & tooling are regularly updated to the latest stable version as they will often include the latest functionality and security patches to known vulnerabilities.</span></span> <span data-ttu-id="7de08-172">您的相依性可以包含您依存的程式碼、您使用的二進位檔、使用的工具和其他元件。</span><span class="sxs-lookup"><span data-stu-id="7de08-172">Your dependencies can include code you depend on, binaries you consume, tooling you use, and other components.</span></span> <span data-ttu-id="7de08-173">這可能包括：</span><span class="sxs-lookup"><span data-stu-id="7de08-173">This may include:</span></span>

-   [<span data-ttu-id="7de08-174">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7de08-174">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)
-   [<span data-ttu-id="7de08-175">.NET SDK & 執行時間</span><span class="sxs-lookup"><span data-stu-id="7de08-175">.NET SDK & Runtime</span></span>](https://dotnet.microsoft.com/download)
-   [<span data-ttu-id="7de08-176">NuGet</span><span class="sxs-lookup"><span data-stu-id="7de08-176">NuGet</span></span>](https://www.nuget.org/downloads)
-   [<span data-ttu-id="7de08-177">NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="7de08-177">NuGet packages</span></span>](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a><span data-ttu-id="7de08-178">管理您的相依性</span><span class="sxs-lookup"><span data-stu-id="7de08-178">Manage your dependencies</span></span>

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a><span data-ttu-id="7de08-179">NuGet 已淘汰和易受攻擊的相依性</span><span class="sxs-lookup"><span data-stu-id="7de08-179">NuGet deprecated and vulnerable dependencies</span></span>

<span data-ttu-id="7de08-180">**📦 套件取用者 | 📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-180">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-181">您可以使用 [DOTNET CLI](/dotnet/core/tools/dotnet-list-package) 來列出您的專案或解決方案中可能存在的任何已知已淘汰或易受攻擊的相依性。</span><span class="sxs-lookup"><span data-stu-id="7de08-181">You can use the [dotnet CLI](/dotnet/core/tools/dotnet-list-package) to list any known deprecated or vulnerable dependencies you may have inside your project or solution.</span></span> <span data-ttu-id="7de08-182">您可以使用命令 `dotnet list package --deprecated` 或 `dotnet list package --vulnerable` 提供任何已知棄用功能或弱點的清單。</span><span class="sxs-lookup"><span data-stu-id="7de08-182">You can use the command `dotnet list package --deprecated` or `dotnet list package --vulnerable` to provide you a list of any known deprecations or vulnerabilities.</span></span>

### <a name="github-vulnerable-dependencies"></a><span data-ttu-id="7de08-183">GitHub 易受依存的相依性</span><span class="sxs-lookup"><span data-stu-id="7de08-183">GitHub vulnerable dependencies</span></span>

<span data-ttu-id="7de08-184">**📦 套件取用者 | 📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-184">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-185">如果您的專案是裝載在 GitHub 上，您可以利用 [Github 安全性](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) 找出專案中的安全性弱點和錯誤，Dependabot 會藉由開啟程式碼基底的提取要求來修正這些問題。</span><span class="sxs-lookup"><span data-stu-id="7de08-185">If your project is hosted on GitHub, you can leverage [GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) to find security vulnerabilities and errors in your project and Dependabot will fix them by opening up a pull request against your codebase.</span></span> 

<span data-ttu-id="7de08-186">在導入之前攔截易受攻擊的相依性，是「 [下移](https://en.wikipedia.org/wiki/Shift-left_testing) 」移動的一專案標。</span><span class="sxs-lookup"><span data-stu-id="7de08-186">Catching vulnerable dependencies before they are introduced is one goal of the [“Shift Left”](https://en.wikipedia.org/wiki/Shift-left_testing) movement.</span></span> <span data-ttu-id="7de08-187">可以取得相依性的相關資訊，例如其授權、可轉移的相依性，以及相依性的存留期，以協助您完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="7de08-187">Being able to have information about your dependencies such as their license, transitive dependencies, and the age of dependencies helps you do just that.</span></span>

<span data-ttu-id="7de08-188">如需有關 Dependabot 警示 & 安全性更新的詳細資訊， [請參閱下列檔](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="7de08-188">For more information about Dependabot alerts & security updates, [see the following documentation](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).</span></span>

### <a name="nuget-feeds"></a><span data-ttu-id="7de08-189">NuGet 摘要</span><span class="sxs-lookup"><span data-stu-id="7de08-189">NuGet feeds</span></span>

<span data-ttu-id="7de08-190">**📦 套件取用者**</span><span class="sxs-lookup"><span data-stu-id="7de08-190">**📦 Package Consumer**</span></span>

<span data-ttu-id="7de08-191">使用多個公用 & 私用 NuGet 來源摘要時，可以從任何饋送下載套件。</span><span class="sxs-lookup"><span data-stu-id="7de08-191">When using multiple public & private NuGet source feeds, a package can be downloaded from any of the feeds.</span></span> <span data-ttu-id="7de08-192">為了確保您的組建是可預測的，且不受已知的攻擊（例如相依性 [混淆](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)）的保護，請瞭解您的套件所) 的特定摘要 (是最佳作法。</span><span class="sxs-lookup"><span data-stu-id="7de08-192">To ensure your build is predictable and secure from known attacks such as [Dependency Confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), knowing what specific feed(s) your packages are coming from is a best practice.</span></span> <span data-ttu-id="7de08-193">您可以使用單一摘要或具有 upstreaming 功能的私人摘要來保護。</span><span class="sxs-lookup"><span data-stu-id="7de08-193">You can use a single feed or private feed with upstreaming capabilities for protection.</span></span>

<span data-ttu-id="7de08-194">如需保護套件摘要的詳細資訊，請參閱 [使用私用套件摘要時降低風險的三種方式](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)。</span><span class="sxs-lookup"><span data-stu-id="7de08-194">For more information to secure your package feeds, see [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).</span></span>

### <a name="client-trust-policies"></a><span data-ttu-id="7de08-195">用戶端信任原則</span><span class="sxs-lookup"><span data-stu-id="7de08-195">Client trust policies</span></span>

<span data-ttu-id="7de08-196">**📦 套件取用者**</span><span class="sxs-lookup"><span data-stu-id="7de08-196">**📦 Package Consumer**</span></span>

<span data-ttu-id="7de08-197">有一些您可以加入宣告的原則，您需要使用這些原則簽署封裝。</span><span class="sxs-lookup"><span data-stu-id="7de08-197">There are policies that you can opt-into in which you require the packages you use to be signed.</span></span> <span data-ttu-id="7de08-198">這可讓您信任套件作者，只要它是作者簽署的作者，或信任封裝（如果是由 NuGet.org 簽署的儲存機制的特定使用者或帳戶所擁有）。</span><span class="sxs-lookup"><span data-stu-id="7de08-198">This allows you to trust a package author, as long as it is author signed, or trust a package if it is owned by a specific user or account that is repository signed by NuGet.org.</span></span>

<span data-ttu-id="7de08-199">若要設定用戶端信任原則， [請參閱下列檔](../consume-packages/installing-signed-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="7de08-199">To configure client trust policies, [see the following documentation](../consume-packages/installing-signed-packages.md).</span></span>

### <a name="lock-files"></a><span data-ttu-id="7de08-200">鎖定檔案</span><span class="sxs-lookup"><span data-stu-id="7de08-200">Lock files</span></span>

<span data-ttu-id="7de08-201">**📦 套件取用者**</span><span class="sxs-lookup"><span data-stu-id="7de08-201">**📦 Package Consumer**</span></span>

<span data-ttu-id="7de08-202">鎖定檔案會儲存套件內容的雜湊。</span><span class="sxs-lookup"><span data-stu-id="7de08-202">Lock files store the hash of your package’s content.</span></span> <span data-ttu-id="7de08-203">如果您要安裝的套件內容雜湊符合鎖定檔案，則會確保封裝重複性。</span><span class="sxs-lookup"><span data-stu-id="7de08-203">If the content hash of a package you want to install matches with the lock file, it will ensure package repeatability.</span></span>

<span data-ttu-id="7de08-204">若要啟用鎖定檔案， [請參閱下列檔](../consume-packages/package-references-in-project-files#locking-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="7de08-204">To enable lock files, [see the following documentation](../consume-packages/package-references-in-project-files#locking-dependencies).</span></span>

## <a name="monitor-your-supply-chain"></a><span data-ttu-id="7de08-205">監視您的供應鏈</span><span class="sxs-lookup"><span data-stu-id="7de08-205">Monitor your supply chain</span></span>

### <a name="github-secret-scanning"></a><span data-ttu-id="7de08-206">GitHub 祕密掃描 (英文)</span><span class="sxs-lookup"><span data-stu-id="7de08-206">GitHub secret scanning</span></span>

<span data-ttu-id="7de08-207">**📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-207">**📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-208">GitHub 會掃描 NuGet API 金鑰的存放庫，以防止詐騙使用意外認可的秘密。</span><span class="sxs-lookup"><span data-stu-id="7de08-208">GitHub scans repositories for NuGet API keys to prevent fraudulent uses of secrets that were accidentally committed.</span></span> 

<span data-ttu-id="7de08-209">若要深入瞭解秘密掃描，請參閱 [關於秘密掃描](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)。</span><span class="sxs-lookup"><span data-stu-id="7de08-209">To learn more about secret scanning, see [About secret scanning](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).</span></span>

### <a name="author-package-signing"></a><span data-ttu-id="7de08-210">作者套件簽署</span><span class="sxs-lookup"><span data-stu-id="7de08-210">Author Package Signing</span></span>

<span data-ttu-id="7de08-211">**📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-211">**📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-212">[作者簽署](../reference/signed-packages-reference.md) 可讓套件作者在套件上標記其身分識別，並讓取用者確認其來自您的身分。</span><span class="sxs-lookup"><span data-stu-id="7de08-212">[Author signing](../reference/signed-packages-reference.md) allows a package author to stamp their identity on a package and for a consumer to verify it came from you.</span></span> <span data-ttu-id="7de08-213">這可保護您不受內容篡改的攻擊，並可作為套件來源和套件真實性的單一真實來源。</span><span class="sxs-lookup"><span data-stu-id="7de08-213">This protects you against content tampering and serves as a single source of truth about the origin of the package and the package authenticity.</span></span> <span data-ttu-id="7de08-214">結合用戶端信任原則時，您可以確認套件來自特定的作者。</span><span class="sxs-lookup"><span data-stu-id="7de08-214">When combined with client trust policies, you can verify a package came from a specific author.</span></span>

<span data-ttu-id="7de08-215">若要撰寫簽署套件，請參閱 [簽署封裝](../create-packages/sign-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="7de08-215">To author sign a package, see [Sign a package](../create-packages/sign-a-package.md).</span></span>

### <a name="two-factor-authentication-2fa"></a><span data-ttu-id="7de08-216">Two-Factor Authentication (2FA) </span><span class="sxs-lookup"><span data-stu-id="7de08-216">Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="7de08-217">**📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-217">**📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-218">啟用雙因素驗證 (2FA) 可以在 [登入您的 GitHub 帳戶](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) 或 [NuGet.org 公用套件存放庫](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)時，增加額外的安全性層級。</span><span class="sxs-lookup"><span data-stu-id="7de08-218">Enabling two-factor authentication (2FA) can add an extra layer of security when [logging into your GitHub account](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) or the [NuGet.org public package repository](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa).</span></span> <span data-ttu-id="7de08-219">建議您啟用雙重要素驗證來保護您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7de08-219">It is recommended that you enable two-factor authentication to protect your account.</span></span>

### <a name="package-id-prefix-reservation"></a><span data-ttu-id="7de08-220">套件識別碼首碼保留項目</span><span class="sxs-lookup"><span data-stu-id="7de08-220">Package ID prefix reservation</span></span> 

<span data-ttu-id="7de08-221">**📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-221">**📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-222">若要保護套件的身分識別，您可以保留套件識別碼前置詞與個別的命名空間，以便在您的套件識別碼前置詞正確地落在 [指定的準則](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)時，讓相符的擁有者產生關聯。</span><span class="sxs-lookup"><span data-stu-id="7de08-222">To protect the identity of your packages, you can reserve a package ID prefix with your respective namespace to associate a matching owner if your package ID prefix properly falls under the [specified criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).</span></span> 

<span data-ttu-id="7de08-223">若要瞭解如何保留識別碼首碼，請參閱 [套件識別碼前置詞保留](../nuget-org/id-prefix-reservation.md)。</span><span class="sxs-lookup"><span data-stu-id="7de08-223">To learn about reserving ID prefixes, see [Package ID prefix reservation](../nuget-org/id-prefix-reservation.md).</span></span>

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a><span data-ttu-id="7de08-224">淘汰和取消列出易受攻擊的套件</span><span class="sxs-lookup"><span data-stu-id="7de08-224">Deprecating and unlisting a vulnerable package</span></span>

<span data-ttu-id="7de08-225">**📦🖊 封裝作者**</span><span class="sxs-lookup"><span data-stu-id="7de08-225">**📦🖊 Package Author**</span></span>

<span data-ttu-id="7de08-226">若要在您注意到您所撰寫的封裝中有弱點時保護 .NET 封裝生態系統，最好取代並取消列出套件，讓使用者無法搜尋套件。</span><span class="sxs-lookup"><span data-stu-id="7de08-226">To protect the .NET package ecosystem when you are aware of a vulnerability in a package you have authored, do your best to deprecate and unlist the package so it is hidden from users searching for packages.</span></span> <span data-ttu-id="7de08-227">如果您使用已被取代且未列出的封裝，您應該避免使用封裝。</span><span class="sxs-lookup"><span data-stu-id="7de08-227">If you are consuming a package that is deprecated and unlisted, you should avoid using the package.</span></span>

<span data-ttu-id="7de08-228">若要瞭解如何取代和取消列出套件，請參閱下列有關 [淘汰](../nuget-org/deprecate-packages.md) 和 [取消列出套件](../nuget-org/policies/deleting-packages.md#unlisting-a-package)的檔。</span><span class="sxs-lookup"><span data-stu-id="7de08-228">To learn how to deprecate and unlist a package, see the following documentation on [deprecating](../nuget-org/deprecate-packages.md) and [unlisting packages](../nuget-org/policies/deleting-packages.md#unlisting-a-package).</span></span>

## <a name="summary"></a><span data-ttu-id="7de08-229">摘要</span><span class="sxs-lookup"><span data-stu-id="7de08-229">Summary</span></span>

<span data-ttu-id="7de08-230">您的軟體供應鏈是任何進入或影響程式碼的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7de08-230">Your software supply chain is anything that goes into or affects your code.</span></span> <span data-ttu-id="7de08-231">雖然供應鏈的危害是真實且越來越普及，但它們仍然很罕見;因此，您可以做的最重要的事，就是藉由 **瞭解您的相依性、管理您的** 相依性，以及 **監視您的供應鏈**，來保護您的供應鏈。</span><span class="sxs-lookup"><span data-stu-id="7de08-231">Even though supply chain compromises are real and growing in popularity, they are still rare; so the most important thing you can do is protect your supply chain by **being aware of your dependencies, managing your dependencies** and **monitoring your supply chain.**</span></span>

<span data-ttu-id="7de08-232">您已瞭解 NuGet 和 [GitHub](/learn/modules/maintain-secure-repository-github/) 提供的各種方法，現在可讓您更有效地查看、管理及監視您的供應鏈。</span><span class="sxs-lookup"><span data-stu-id="7de08-232">You learned about various methods that NuGet and [GitHub](/learn/modules/maintain-secure-repository-github/) provide that are available to you today to be more effective in viewing, managing, and monitoring your supply chain.</span></span>

<span data-ttu-id="7de08-233">如需保護世界軟體的相關資訊，請參閱 [Octoverse 2020 安全性報告的狀態](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)。</span><span class="sxs-lookup"><span data-stu-id="7de08-233">For more information about securing the world's software, see [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).</span></span>
