---
title: NuGet 2.9-RC 版本資訊
description: NuGet 2.9 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780314"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="43c1a-103">NuGet 2.9-RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="43c1a-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="43c1a-104">[NuGet 2.8.7 版本](../release-notes/nuget-2.8.7.md)  |  資訊[NuGet 3.0 Preview 版本](../release-notes/nuget-3.0-preview.md)資訊</span><span class="sxs-lookup"><span data-stu-id="43c1a-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="43c1a-105">NuGet 2.9 已于2015年9月10日發行為 Visual Studio 2012 和2013的 2.8.7 VSIX 更新。</span><span class="sxs-lookup"><span data-stu-id="43c1a-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="43c1a-106">此版本中的更新</span><span class="sxs-lookup"><span data-stu-id="43c1a-106">Updates in this release</span></span>

* <span data-ttu-id="43c1a-107">現在如果其包含的檔案格式不正確，則會略過處理套件 `.nuspec` - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="43c1a-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="43c1a-108">修正了 \r\n for Unix/Linux 案例的 multipartwebrequest 處理- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="43c1a-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="43c1a-109">修正 Visual Studio 2013 社區版本- [1180](https://github.com/NuGet/Home/issues/1180)中的組建事件整合</span><span class="sxs-lookup"><span data-stu-id="43c1a-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="43c1a-110">您可以在 GitHub 的[2.8.8 里程碑](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)中找到此版本的完整修正清單</span><span class="sxs-lookup"><span data-stu-id="43c1a-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
