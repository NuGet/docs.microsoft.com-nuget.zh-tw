---
title: NuGet.org 上的套件讀我檔案
description: 詳細說明如何轉譯 NuGet.org 上的讀我檔案，以及當您遇到問題時該怎麼辦。
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902242"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="8c9cf-103">NuGet.org 上的套件讀我檔案</span><span class="sxs-lookup"><span data-stu-id="8c9cf-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="8c9cf-104">將[讀我檔案包含在您的 NuGet 套件中](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)，讓您的套件詳細資料更豐富，並提供更豐富的資訊給您的使用者！</span><span class="sxs-lookup"><span data-stu-id="8c9cf-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="8c9cf-105">這可能是使用者在 NuGet.org 上查看套件詳細資料頁面時所看到的第一個元素，這是很好的印象。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9cf-106">NuGet.org 只支援 [Markdown](https://daringfireball.net/projects/markdown/) 中的讀我檔案，以及來自一組有限網域的映射。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="8c9cf-107">請參閱我們 [允許的影像網域](#allowed-domains-for-images-and-badges) 和 [支援的 Markdown 功能](#supported-markdown-features) ，以確保您的讀我檔案在 NuGet.org 上正確呈現。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="8c9cf-108">我的讀我檔案有哪些？</span><span class="sxs-lookup"><span data-stu-id="8c9cf-108">What should my readme include?</span></span>

<span data-ttu-id="8c9cf-109">請考慮在讀我檔案中包含下列專案：</span><span class="sxs-lookup"><span data-stu-id="8c9cf-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="8c9cf-110">套件的功能和功能的簡介-它能解決哪些問題？</span><span class="sxs-lookup"><span data-stu-id="8c9cf-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="8c9cf-111">如何開始使用您的套件-是否有任何特定需求？</span><span class="sxs-lookup"><span data-stu-id="8c9cf-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="8c9cf-112">如果未包含在讀我檔案中，則連結至更完整的檔。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="8c9cf-113">至少有幾個程式碼片段/範例或範例影像。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="8c9cf-114">何處和如何離開意見反應，例如專案問題、Twitter、bug 追蹤程式或其他平臺的連結。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="8c9cf-115">如何投稿（如果適用）。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="8c9cf-116">請記住，高品質的讀我檔案可以有各式各樣的格式、圖形和大小！</span><span class="sxs-lookup"><span data-stu-id="8c9cf-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="8c9cf-117">如果您在 NuGet.org 上已經有可用的套件，可能是因為您的儲存機制中已經有一個或其他檔檔，所以您的 `readme.md` NuGet.org 詳細資料頁面會有很大的補充。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="8c9cf-118">預覽您的讀我檔案</span><span class="sxs-lookup"><span data-stu-id="8c9cf-118">Preview your readme</span></span>

<span data-ttu-id="8c9cf-119">若要在您的讀我檔案存留于 NuGet.org 前進行預覽，請使用 [NuGet.org 上的上傳套件入口網站](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) 上傳您的套件，並向下滾動至中繼資料預覽的「讀我檔案」一節。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="8c9cf-120">您應該會看到類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="8c9cf-120">It should look something like this:</span></span>

![讀我檔案預覽](media\readme-upload-preview.PNG)

<span data-ttu-id="8c9cf-122">請考慮花時間複習和預覽您的讀我檔案，以瞭解 [影像合規性](#allowed-domains-for-images-and-badges) 和 [支援的格式](#supported-markdown-features) ，以確保能為可能的使用者提供絕佳的第一印象！</span><span class="sxs-lookup"><span data-stu-id="8c9cf-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="8c9cf-123">若要更正封裝讀我檔案發行至 NuGet.org 之後的錯誤，您必須將更新的套件版本推送至修正程式。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="8c9cf-124">確定一切的進展都能讓您省下更麻煩的道路。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="8c9cf-125">允許的影像和徽章網域</span><span class="sxs-lookup"><span data-stu-id="8c9cf-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="8c9cf-126">基於安全性和隱私權的考慮，NuGet.org 會限制可將影像和徽章轉譯成受信任主機的網域。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="8c9cf-127">NuGet.org 允許轉譯來自下列受信任網域的所有影像，包括徽章：</span><span class="sxs-lookup"><span data-stu-id="8c9cf-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="8c9cf-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-128">api.bintray.com</span></span>
* <span data-ttu-id="8c9cf-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-129">api.codacy.com</span></span>
* <span data-ttu-id="8c9cf-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-130">api.codeclimate.com</span></span>
* <span data-ttu-id="8c9cf-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-131">api.dependabot.com</span></span>
* <span data-ttu-id="8c9cf-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-132">api.travis-ci.com</span></span>
* <span data-ttu-id="8c9cf-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="8c9cf-133">api.travis-ci.org</span></span>
* <span data-ttu-id="8c9cf-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-134">app.fossa.io</span></span>
* <span data-ttu-id="8c9cf-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-135">badge.fury.io</span></span>
* <span data-ttu-id="8c9cf-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="8c9cf-136">badgen.net</span></span>
* <span data-ttu-id="8c9cf-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="8c9cf-137">badges.gitter.im</span></span>
* <span data-ttu-id="8c9cf-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-138">bettercodehub.com</span></span>
* <span data-ttu-id="8c9cf-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="8c9cf-139">buildstats.info</span></span>
* <span data-ttu-id="8c9cf-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="8c9cf-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-141">ci.appveyor.com</span></span>
* <span data-ttu-id="8c9cf-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-142">circleci.com</span></span>
* <span data-ttu-id="8c9cf-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-143">codecov.io</span></span>
* <span data-ttu-id="8c9cf-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-144">codefactor.io</span></span>
* <span data-ttu-id="8c9cf-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-145">coveralls.io</span></span>
* <span data-ttu-id="8c9cf-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-146">dev.azure.com</span></span>
* <span data-ttu-id="8c9cf-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="8c9cf-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="8c9cf-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-148">gitlab.com</span></span>
* <span data-ttu-id="8c9cf-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-149">img.shields.io</span></span>
* <span data-ttu-id="8c9cf-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-150">isitmaintained.com</span></span>
* <span data-ttu-id="8c9cf-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-151">opencollective.com</span></span>
* <span data-ttu-id="8c9cf-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-152">raw.github.com</span></span>
* <span data-ttu-id="8c9cf-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="8c9cf-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-154">snyk.io</span></span>
* <span data-ttu-id="8c9cf-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="8c9cf-155">sonarcloud.io</span></span>
* <span data-ttu-id="8c9cf-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="8c9cf-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="8c9cf-157">如果您認為應該將另一個網域新增到允許清單中，請放心提出 [問題](https://github.com/NuGet/NuGetGallery/issues) ，我們的工程小組將會針對隱私權和安全性合規性進行審核。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="8c9cf-158">系統將不會轉譯具有相對本機路徑的映射，以及從不支援的網域裝載的映射，而且將會在 [讀我檔案預覽] 和 [套件詳細資料] 頁面（只有套件擁有者可見）中產生警告。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="8c9cf-159">支援的 Markdown 功能</span><span class="sxs-lookup"><span data-stu-id="8c9cf-159">Supported Markdown features</span></span>
<span data-ttu-id="8c9cf-160">[Markdown](https://daringfireball.net/projects/markdown/) 是採用純文字格式語法的輕量型標記語言。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="8c9cf-161">NuGet.org 讀我檔案透過[Markdig](https://github.com/lunet-io/markdig)剖析引擎支援符合[CommonMark](https://commonmark.org/)規範的 Markdown。</span><span class="sxs-lookup"><span data-stu-id="8c9cf-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="8c9cf-162">NuGet.org 目前支援下列 Markdown 功能：</span><span class="sxs-lookup"><span data-stu-id="8c9cf-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="8c9cf-163">標頭</span><span class="sxs-lookup"><span data-stu-id="8c9cf-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="8c9cf-164">影像</span><span class="sxs-lookup"><span data-stu-id="8c9cf-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="8c9cf-165">額外強調</span><span class="sxs-lookup"><span data-stu-id="8c9cf-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="8c9cf-166">清單</span><span class="sxs-lookup"><span data-stu-id="8c9cf-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="8c9cf-167">連結</span><span class="sxs-lookup"><span data-stu-id="8c9cf-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="8c9cf-168">區塊引述</span><span class="sxs-lookup"><span data-stu-id="8c9cf-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="8c9cf-169">反斜線轉義</span><span class="sxs-lookup"><span data-stu-id="8c9cf-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="8c9cf-170">程式碼範圍</span><span class="sxs-lookup"><span data-stu-id="8c9cf-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="8c9cf-171">工作清單</span><span class="sxs-lookup"><span data-stu-id="8c9cf-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="8c9cf-172">資料表</span><span class="sxs-lookup"><span data-stu-id="8c9cf-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="8c9cf-173">Emoji</span><span class="sxs-lookup"><span data-stu-id="8c9cf-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="8c9cf-174">自動連結</span><span class="sxs-lookup"><span data-stu-id="8c9cf-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

