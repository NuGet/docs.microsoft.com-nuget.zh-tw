---
title: NuGet 2.6 版本資訊
description: Webmatrix 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.6.1 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551939"
---
# <a name="nuget-26-release-notes"></a><span data-ttu-id="8643a-103">NuGet 2.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="8643a-103">NuGet 2.6 Release Notes</span></span>

<span data-ttu-id="8643a-104">[NuGet 2.5 版本資訊](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix 版本資訊](../release-notes/nuget-2.6.1-for-webmatrix.md)</span><span class="sxs-lookup"><span data-stu-id="8643a-104">[NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md)</span></span>

<span data-ttu-id="8643a-105">NuGet 2.6 已於 2013 年 6 月 26 日發行。</span><span class="sxs-lookup"><span data-stu-id="8643a-105">NuGet 2.6 was released on June 26, 2013.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="8643a-106">在版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="8643a-106">Notable features in the release</span></span>

### <a name="support-for-visual-studio-2013"></a><span data-ttu-id="8643a-107">Visual Studio 2013 的支援</span><span class="sxs-lookup"><span data-stu-id="8643a-107">Support for Visual Studio 2013</span></span>

<span data-ttu-id="8643a-108">NuGet 2.6 是第一個版本所提供的 Visual Studio 2013 的支援。</span><span class="sxs-lookup"><span data-stu-id="8643a-108">NuGet 2.6 is the first release that provides support for Visual Studio 2013.</span></span> <span data-ttu-id="8643a-109">例如 Visual Studio 2012，NuGet 套件管理員延伸模組包含在每個版本的 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="8643a-109">And like Visual Studio 2012, the NuGet Package Manager extension is included in every edition of Visual Studio.</span></span>

<span data-ttu-id="8643a-110">為了提供可行的最佳支援 Visual Studio 2013 同時支援 Visual Studio 2010 和 Visual Studio 2012 和保留的延伸模組大小越小越好，我們會產生另外的延伸模組時的 Visual Studio 2013原始副檔名會繼續以 Visual Studio 2010 和 2012年為目標。</span><span class="sxs-lookup"><span data-stu-id="8643a-110">In order to provide the best possible support for Visual Studio 2013 while still supporting both Visual Studio 2010 and Visual Studio 2012, and keeping the extension sizes as small as possible, we are producing a separate extension for Visual Studio 2013 while the original extension continues to target both Visual Studio 2010 and 2012.</span></span>

<span data-ttu-id="8643a-111">從 NuGet 2.6 開始，我們將發佈兩個延伸模組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8643a-111">Starting with NuGet 2.6, we will publish two extensions as below:</span></span>

1. <span data-ttu-id="8643a-112">[NuGet 套件管理員](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（適用於 Visual Studio 2010 和 2012年）</span><span class="sxs-lookup"><span data-stu-id="8643a-112">[NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (applies to Visual Studio 2010 and 2012)</span></span>
1. [<span data-ttu-id="8643a-113">Visual Studio 2013 的 NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="8643a-113">NuGet Package Manager for Visual Studio 2013</span></span>](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

<span data-ttu-id="8643a-114">此分割中， [nuget.org](https://nuget.org)首頁的 「 安裝 NuGet"按鈕會帶您前往[安裝 NuGet](../install-nuget-client-tools.md)頁面上，您可以在其中找到安裝不同的 NuGet 用戶端的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8643a-114">With this split, the [nuget.org](https://nuget.org) home page's "Install NuGet" button takes you to the [installing NuGet](../install-nuget-client-tools.md) page, where you can find more information about installing the different NuGet clients.</span></span>

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a><span data-ttu-id="8643a-115">XDT Web.config 轉換的支援</span><span class="sxs-lookup"><span data-stu-id="8643a-115">XDT Web.config transformation support</span></span>

<span data-ttu-id="8643a-116">NuGet 用戶端的最高要求的功能之一就是支援更強大的 XML 轉換使用 XDT 轉換引擎會在 Visual Studio 組建組態轉換。</span><span class="sxs-lookup"><span data-stu-id="8643a-116">One of the most highly-requested features for the NuGet client has been to support more powerful XML transformations using the XDT transformation engine which is used in Visual Studio build configuration transformations.</span></span>

<span data-ttu-id="8643a-117">在 2013 年 4 月中，我們所做的有關 XDT 的 NuGet 支援的兩個大公告。</span><span class="sxs-lookup"><span data-stu-id="8643a-117">In April 2013, we made two big announcements regarding NuGet support for XDT.</span></span> <span data-ttu-id="8643a-118">第一是 XDT 程式庫本身正在被本身[NuGet 套件形式發行](https://nuget.org/packages/Microsoft.Web.Xdt)並[CodePlex 上的開放原始碼](http://xdt.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="8643a-118">The first was that the XDT library itself was being itself [released as a NuGet package](https://nuget.org/packages/Microsoft.Web.Xdt) and [open sourced on CodePlex](http://xdt.codeplex.com/).</span></span> <span data-ttu-id="8643a-119">此步驟中啟用 XDT 引擎，可供自由其他開放原始碼軟體，包括 NuGet 用戶端。</span><span class="sxs-lookup"><span data-stu-id="8643a-119">This step enabled the XDT engine to be used freely by other open-source software, including the NuGet client.</span></span> <span data-ttu-id="8643a-120">第二個宣告是要支援 NuGet 用戶端中的轉換使用 XDT 引擎的計劃。</span><span class="sxs-lookup"><span data-stu-id="8643a-120">The second announcement was the plan to support use of the XDT engine for transformations in the NuGet client.</span></span> <span data-ttu-id="8643a-121">NuGet 2.6 包含這項整合。</span><span class="sxs-lookup"><span data-stu-id="8643a-121">NuGet 2.6 includes this integration.</span></span>

#### <a name="how-it-works"></a><span data-ttu-id="8643a-122">它的運作方式</span><span class="sxs-lookup"><span data-stu-id="8643a-122">How it works</span></span>

<span data-ttu-id="8643a-123">若要充分利用 NuGet 的 XDT 支援，機制看起來類似[目前的組態轉換功能](../create-packages/source-and-config-file-transformations.md)。</span><span class="sxs-lookup"><span data-stu-id="8643a-123">To take advantage of NuGet’s XDT support, the mechanics look similar to those of the [current config transformation feature](../create-packages/source-and-config-file-transformations.md).</span></span>
<span data-ttu-id="8643a-124">轉換檔案新增至套件的內容資料夾。</span><span class="sxs-lookup"><span data-stu-id="8643a-124">Transformation files are added to the package’s content folder.</span></span> <span data-ttu-id="8643a-125">不過，雖然組態轉換會使用單一檔案的安裝和解除安裝，XDT 轉換就會啟用更細微的控制這兩個這些處理程序，使用下列檔案：</span><span class="sxs-lookup"><span data-stu-id="8643a-125">However, while config transformations use a single file for both installation and uninstallation, XDT transformations enable fine-grained control over both of these processes using the following files:</span></span>

- <span data-ttu-id="8643a-126">Web.config.install.xdt</span><span class="sxs-lookup"><span data-stu-id="8643a-126">Web.config.install.xdt</span></span>
- <span data-ttu-id="8643a-127">Web.config.uninstall.xdt</span><span class="sxs-lookup"><span data-stu-id="8643a-127">Web.config.uninstall.xdt</span></span>

<span data-ttu-id="8643a-128">此外，NuGet 會使用檔案後置字元來判斷哪些引擎來執行轉換，以便使用現有的 web.config.transforms 封裝將會繼續運作。</span><span class="sxs-lookup"><span data-stu-id="8643a-128">Additionally, NuGet uses the file suffix to determine which engine to run for transformations, so packages using the existing web.config.transforms will continue to work.</span></span> <span data-ttu-id="8643a-129">XDT 轉換也可以套用至任何 XML 檔案 (不只是 web.config)，讓您可以對其他應用程式中利用這，在您的專案。</span><span class="sxs-lookup"><span data-stu-id="8643a-129">XDT transformations can also be applied to any XML file (not just web.config), so you can leverage this for other applications in your project.</span></span>

#### <a name="what-you-can-do-with-xdt"></a><span data-ttu-id="8643a-130">您可以執行含有 XDT</span><span class="sxs-lookup"><span data-stu-id="8643a-130">What you can do with XDT</span></span>

<span data-ttu-id="8643a-131">其中一個 XDT 的最大優點是其[簡單但功能強大的語法](http://msdn.microsoft.com/library/dd465326.aspx)來操作 XML DOM 的結構</span><span class="sxs-lookup"><span data-stu-id="8643a-131">One of XDT’s greatest strengths is its [simple but powerful syntax](http://msdn.microsoft.com/library/dd465326.aspx) for manipulating the structure of an XML DOM.</span></span> <span data-ttu-id="8643a-132">而不是直接覆疊一個固定格式文件結構到另一個結構，XDT 會提供控制項，可比對各種不同的方式，從簡單的屬性名稱比對完整 XPath 支援的項目。</span><span class="sxs-lookup"><span data-stu-id="8643a-132">Rather than simply overlaying one fixed document structure onto another structure, XDT provides controls for matching elements in a variety of ways, from simple attribute name matching to full XPath support.</span></span> <span data-ttu-id="8643a-133">一旦找到相符的項目或項目集，XDT 提供一組豐富的函式操作項目，而不論其是指新增、 更新或移除屬性，將新的項目放在特定位置，或取代或移除整個元素和其子系。</span><span class="sxs-lookup"><span data-stu-id="8643a-133">Once a matching element or set of elements is found, XDT provides a rich set of functions for manipulating the elements, whether that means adding, updating, or removing attributes, placing a new element at a specific location, or replacing or removing the entire element and its children.</span></span>

### <a name="machine-wide-configuration"></a><span data-ttu-id="8643a-134">整部機器組態</span><span class="sxs-lookup"><span data-stu-id="8643a-134">Machine-Wide Configuration</span></span>

<span data-ttu-id="8643a-135">NuGet 的優點之一是，它會細分否則大型的可執行檔或程式庫的模組化元件都可以獨立整合，以及最重要的是維護與已建立版本的一組。</span><span class="sxs-lookup"><span data-stu-id="8643a-135">One of the great strengths of NuGet is that it breaks down an otherwise large executable or library into a set of modular components which can be integrated, and most importantly maintained and versioned independently.</span></span> <span data-ttu-id="8643a-136">其中一項副作用，不過，是傳統的產品或產品系列概念可能變得更分散。</span><span class="sxs-lookup"><span data-stu-id="8643a-136">One side effect of this, however, is that the conventional idea of a product or product family becomes potentially more fragmented.</span></span>
<span data-ttu-id="8643a-137">NuGet 的自訂套件來源功能提供的其中一種組織封裝，不過，自訂套件來源並不會自行探索。</span><span class="sxs-lookup"><span data-stu-id="8643a-137">NuGet’s custom package source feature provides one way of organizing packages; however, custom package sources are not discoverable on their own.</span></span>

<span data-ttu-id="8643a-138">NuGet 2.6 延伸來設定 NuGet 搜尋路徑 %programdata%/nuget/config 下的資料夾階層的邏輯。產品安裝程式可以加入自訂的 NuGet 組態檔，在此資料夾中註冊他們的產品的自訂套件來源。</span><span class="sxs-lookup"><span data-stu-id="8643a-138">NuGet 2.6 extends the logic for configuring NuGet by searching the folder hierarchy under the path %ProgramData%/NuGet/Config. Product installers can add custom NuGet configuration files under this folder to register a custom package source for their products.</span></span> <span data-ttu-id="8643a-139">此外，資料夾結構支援語意的產品、 版本和甚至是 SKU 的 IDE。</span><span class="sxs-lookup"><span data-stu-id="8643a-139">Additionally, the folder structure supports semantics for product, version, and even SKU of the IDE.</span></span> <span data-ttu-id="8643a-140">依下列順序 「 後進先 「 優先順序策略會套用這些目錄中的設定。</span><span class="sxs-lookup"><span data-stu-id="8643a-140">Settings from these directories are applied in the following order with a "last in wins" precedence strategy.</span></span>

1. <span data-ttu-id="8643a-141">%ProgramData%\NuGet\Config\*.config</span><span class="sxs-lookup"><span data-stu-id="8643a-141">%ProgramData%\NuGet\Config\*.config</span></span>
2. <span data-ttu-id="8643a-142">%ProgramData%\NuGet\Config\{IDE}\*.config</span><span class="sxs-lookup"><span data-stu-id="8643a-142">%ProgramData%\NuGet\Config\{IDE}\*.config</span></span>
3. <span data-ttu-id="8643a-143">%ProgramData%\NuGet\Config\{IDE}\{Version}\*.config</span><span class="sxs-lookup"><span data-stu-id="8643a-143">%ProgramData%\NuGet\Config\{IDE}\{Version}\*.config</span></span>
4. <span data-ttu-id="8643a-144">%ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config</span><span class="sxs-lookup"><span data-stu-id="8643a-144">%ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config</span></span>

<span data-ttu-id="8643a-145">在此清單中，以便在 Visual Studio 中，案例中，它會是"VisualStudio 」，是針對 IDE 中執行 NuGet，{IDE} 預留位置。</span><span class="sxs-lookup"><span data-stu-id="8643a-145">In this list, the {IDE} placeholder is specific to the IDE in which NuGet is running, so in the case of Visual Studio, it will be "VisualStudio".</span></span> <span data-ttu-id="8643a-146">{Version} 和 {SKU} 預留位置所提供的 IDE （例如："11.0"和"WDExpress"、"VWDExpress 」 和 「 專業 」，分別)。</span><span class="sxs-lookup"><span data-stu-id="8643a-146">The {Version} and {SKU} placeholders are provided by the IDE (e.g. "11.0" and "WDExpress", "VWDExpress" and "Pro", respectively).</span></span> <span data-ttu-id="8643a-147">資料夾可以則包含許多不同的 \*.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="8643a-147">The folder can then contain many different \*.config files.</span></span>
<span data-ttu-id="8643a-148">因此，ACME 元件公司，其產品安裝程式的過程中，新增將只會出現在 Visual Studio 2012 Professional 和 Ultimate 版本建立下列檔案路徑的自訂套件來源：</span><span class="sxs-lookup"><span data-stu-id="8643a-148">Therefore, the ACME component company can, as a part of their product installer, add a custom package source which will be visible only in the Professional and Ultimate versions of Visual Studio 2012 by creating the following file path:</span></span>

<span data-ttu-id="8643a-149">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span><span class="sxs-lookup"><span data-stu-id="8643a-149">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span></span>

<span data-ttu-id="8643a-150">雖然資料夾結構，並直接將整部電腦的套件來源新增至 NuGet 組態的軟體安裝程式 」 等方案，NuGet 組態對話方塊也已經更新，以便為套件來源的註冊其中一個特定使用者 （例如登錄 %appdata%/nuget/nuget.config 中） 或整部電腦。</span><span class="sxs-lookup"><span data-stu-id="8643a-150">While the folder structure makes it straightforward for programs like software installers to add machine-wide package sources to NuGet's configuration, the NuGet configuration dialog has also been updated to allow for the registration of package sources as either user-specific (e.g. registered in %AppData%/NuGet/NuGet.Config) or machine-wide.</span></span>

<span data-ttu-id="8643a-151">這項功能會利用 Visual Studio 2013，在安裝檔案的位置：</span><span class="sxs-lookup"><span data-stu-id="8643a-151">This feature is utilized by Visual Studio 2013, where a file is installed at:</span></span>

<span data-ttu-id="8643a-152">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span><span class="sxs-lookup"><span data-stu-id="8643a-152">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span></span>

<span data-ttu-id="8643a-153">在此檔案中，新的封裝來源，稱為 「.NET Framework 封裝 」 設定。</span><span class="sxs-lookup"><span data-stu-id="8643a-153">Within this file, a new package source called ".NET Framework Packages" is configured.</span></span>

![NuGet 組態檔機器的各種設定](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a><span data-ttu-id="8643a-155">內容化搜尋</span><span class="sxs-lookup"><span data-stu-id="8643a-155">Contextualizing Search</span></span>

<span data-ttu-id="8643a-156">因為 NuGet 資源庫所提供的套件數目持續迅速成長，改善搜尋會保持為曾經 NuGet 優先順序清單的頂端。</span><span class="sxs-lookup"><span data-stu-id="8643a-156">As the number of packages served by the NuGet gallery continues to grow at an exponential pace, improving search remains ever at the top of the NuGet priority list.</span></span> <span data-ttu-id="8643a-157">NuGet 的計劃的功能之一是搜尋的專案的內容相關式搜尋，也就是說，NuGet 會使用版本和 SKU 的 Visual Studio，您會使用和您要建置類型相關資訊作為準則來判斷潛在相關性結果。</span><span class="sxs-lookup"><span data-stu-id="8643a-157">One of the planned features for NuGet is contextual search, meaning that NuGet will use information about the version and SKU of Visual Studio that you are using and the type of project that you are building as criteria for determining the relevance of potential search results.</span></span>

<span data-ttu-id="8643a-158">從 NuGet 2.6 開始，安裝套件時，每次安裝的內容會記錄安裝作業資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="8643a-158">Starting with NuGet 2.6, each time a package is installed, the context for the installation is recorded as part of the installation operation data.</span></span>  <span data-ttu-id="8643a-159">搜尋也會傳送相同的內容資訊，這可讓 NuGet 資源庫，來提升搜尋結果的內容安裝趨勢。</span><span class="sxs-lookup"><span data-stu-id="8643a-159">Searches also send the same context information, which will allow the NuGet Gallery to boost search results by contextual installation trends.</span></span>  <span data-ttu-id="8643a-160">未來的更新至 NuGet 資源庫會啟用此內容相關的關聯性的提升。</span><span class="sxs-lookup"><span data-stu-id="8643a-160">A future update to the NuGet Gallery will enable this context-sensitive relevance boosting.</span></span>

### <a name="tracking-direct-installs-vs-dependency-installs"></a><span data-ttu-id="8643a-161">追蹤直接安裝 vs。相依性安裝</span><span class="sxs-lookup"><span data-stu-id="8643a-161">Tracking Direct Installs vs. Dependency Installs</span></span>

<span data-ttu-id="8643a-162">套件作者可以依賴越來越[封裝的統計資料](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)在 NuGet Gallery 上提供。</span><span class="sxs-lookup"><span data-stu-id="8643a-162">Package authors are relying more and more on the [Package Statistics](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) provided on the NuGet Gallery.</span></span>  <span data-ttu-id="8643a-163">其中一個重要的遺漏資料點的作者，提出的要求是直接的套件會安裝與相依性安裝之間的差異。</span><span class="sxs-lookup"><span data-stu-id="8643a-163">One significant missing data point that authors have asked for is a differentiation between direct package installs and dependency installs.</span></span>  <span data-ttu-id="8643a-164">到目前為止，NuGet 用戶端未傳送任何開發人員是否直接安裝套件，或如果在安裝符合相依性安裝作業的內容。</span><span class="sxs-lookup"><span data-stu-id="8643a-164">Until now, the NuGet client did not send any context around the installation operation for whether the developer directly installed the package or if it was installed to satisfy a dependency.</span></span>
<span data-ttu-id="8643a-165">從開始，使用 NuGet 2.6 中現在會將資料傳送為安裝操作。</span><span class="sxs-lookup"><span data-stu-id="8643a-165">Starting with NuGet 2.6, that data will now be sent for the installation operation.</span></span>  <span data-ttu-id="8643a-166">封裝在 NuGet Gallery 上的統計資料會公開為個別的安裝作業，該資料與 「-相依性"後置詞。</span><span class="sxs-lookup"><span data-stu-id="8643a-166">Package Statistics on the NuGet Gallery will expose that data as separate install operations, with a "-Dependency" suffix.</span></span>

* <span data-ttu-id="8643a-167">安裝</span><span class="sxs-lookup"><span data-stu-id="8643a-167">Install</span></span>
* <span data-ttu-id="8643a-168">安裝相依性</span><span class="sxs-lookup"><span data-stu-id="8643a-168">Install-Dependency</span></span>
* <span data-ttu-id="8643a-169">更新</span><span class="sxs-lookup"><span data-stu-id="8643a-169">Update</span></span>
* <span data-ttu-id="8643a-170">更新相依性</span><span class="sxs-lookup"><span data-stu-id="8643a-170">Update-Dependency</span></span>
* <span data-ttu-id="8643a-171">重新安裝</span><span class="sxs-lookup"><span data-stu-id="8643a-171">Reinstall</span></span>
* <span data-ttu-id="8643a-172">重新安裝相依性</span><span class="sxs-lookup"><span data-stu-id="8643a-172">Reinstall-Dependency</span></span>

<span data-ttu-id="8643a-173">除了不同的作業名稱，也會記錄相依的套件識別碼進行安裝。</span><span class="sxs-lookup"><span data-stu-id="8643a-173">In addition to the different operation name, the dependent package id is also recorded for the installation.</span></span>  <span data-ttu-id="8643a-174">在 NuGet Gallery 的未來更新會公開該報表，讓套件作者將全面了解如何開發人員要安裝其套件內的資料。</span><span class="sxs-lookup"><span data-stu-id="8643a-174">A future update to the NuGet Gallery will expose that data within reports, allowing package authors to fully understand how developers are installing their packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="8643a-175">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="8643a-175">Bug Fixes</span></span>

<span data-ttu-id="8643a-176">NuGet 2.6 也包含數個 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="8643a-176">NuGet 2.6 also includes several bug fixes.</span></span> <span data-ttu-id="8643a-177">如需完整的工作清單項目中已修正 NuGet 2.6，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="8643a-177">For a full list of work items fixed in NuGet 2.6, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>