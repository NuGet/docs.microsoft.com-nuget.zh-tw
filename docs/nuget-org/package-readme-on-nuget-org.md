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
# <a name="package-readme-on-nugetorg"></a>NuGet.org 上的套件讀我檔案

將[讀我檔案包含在您的 NuGet 套件中](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)，讓您的套件詳細資料更豐富，並提供更豐富的資訊給您的使用者！

這可能是使用者在 NuGet.org 上查看套件詳細資料頁面時所看到的第一個元素，這是很好的印象。

> [!IMPORTANT]
> NuGet.org 只支援 [Markdown](https://daringfireball.net/projects/markdown/) 中的讀我檔案，以及來自一組有限網域的映射。 請參閱我們 [允許的影像網域](#allowed-domains-for-images-and-badges) 和 [支援的 Markdown 功能](#supported-markdown-features) ，以確保您的讀我檔案在 NuGet.org 上正確呈現。

## <a name="what-should-my-readme-include"></a>我的讀我檔案有哪些？

請考慮在讀我檔案中包含下列專案：
* 套件的功能和功能的簡介-它能解決哪些問題？
* 如何開始使用您的套件-是否有任何特定需求？
* 如果未包含在讀我檔案中，則連結至更完整的檔。
* 至少有幾個程式碼片段/範例或範例影像。
* 何處和如何離開意見反應，例如專案問題、Twitter、bug 追蹤程式或其他平臺的連結。
* 如何投稿（如果適用）。

請記住，高品質的讀我檔案可以有各式各樣的格式、圖形和大小！ 如果您在 NuGet.org 上已經有可用的套件，可能是因為您的儲存機制中已經有一個或其他檔檔，所以您的 `readme.md` NuGet.org 詳細資料頁面會有很大的補充。

## <a name="preview-your-readme"></a>預覽您的讀我檔案

若要在您的讀我檔案存留于 NuGet.org 前進行預覽，請使用 [NuGet.org 上的上傳套件入口網站](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) 上傳您的套件，並向下滾動至中繼資料預覽的「讀我檔案」一節。 您應該會看到類似下面的畫面：

![讀我檔案預覽](media\readme-upload-preview.PNG)

請考慮花時間複習和預覽您的讀我檔案，以瞭解 [影像合規性](#allowed-domains-for-images-and-badges) 和 [支援的格式](#supported-markdown-features) ，以確保能為可能的使用者提供絕佳的第一印象！ 若要更正封裝讀我檔案發行至 NuGet.org 之後的錯誤，您必須將更新的套件版本推送至修正程式。 確定一切的進展都能讓您省下更麻煩的道路。
## <a name="allowed-domains-for-images-and-badges"></a>允許的影像和徽章網域

基於安全性和隱私權的考慮，NuGet.org 會限制可將影像和徽章轉譯成受信任主機的網域。 

NuGet.org 允許轉譯來自下列受信任網域的所有影像，包括徽章：
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

如果您認為應該將另一個網域新增到允許清單中，請放心提出 [問題](https://github.com/NuGet/NuGetGallery/issues) ，我們的工程小組將會針對隱私權和安全性合規性進行審核。 系統將不會轉譯具有相對本機路徑的映射，以及從不支援的網域裝載的映射，而且將會在 [讀我檔案預覽] 和 [套件詳細資料] 頁面（只有套件擁有者可見）中產生警告。

## <a name="supported-markdown-features"></a>支援的 Markdown 功能
[Markdown](https://daringfireball.net/projects/markdown/) 是採用純文字格式語法的輕量型標記語言。 NuGet.org 讀我檔案透過[Markdig](https://github.com/lunet-io/markdig)剖析引擎支援符合[CommonMark](https://commonmark.org/)規範的 Markdown。

NuGet.org 目前支援下列 Markdown 功能：
* [標頭](https://spec.commonmark.org/0.29/#atx-headings)
* [影像](https://spec.commonmark.org/0.29/#images)
* [額外強調](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [清單](https://spec.commonmark.org/0.29/#lists)
* [連結](https://spec.commonmark.org/0.29/#links)
* [區塊引述](https://spec.commonmark.org/0.29/#block-quotes)
* [反斜線轉義](https://spec.commonmark.org/0.29/#backslash-escapes)
* [程式碼範圍](https://spec.commonmark.org/0.29/#code-spans)
* [工作清單](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [資料表](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emoji](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [自動連結](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

