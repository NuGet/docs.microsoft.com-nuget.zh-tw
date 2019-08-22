---
title: 建立 NuGet 套件的概觀和工作流程
description: 建立和發行 NuGet 套件程序的概觀，以及程序之其他特定部分的連結。
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488850"
---
# <a name="package-creation-workflow"></a><span data-ttu-id="1b645-103">套件建立工作流程</span><span class="sxs-lookup"><span data-stu-id="1b645-103">Package creation workflow</span></span>

<span data-ttu-id="1b645-104">建立套件是以想要封裝並與其他人共用 (透過公用 nuget.org 資源庫或組織內的私用資源庫) 的已編譯程式碼 (一般是 .NET 組件) 開始。</span><span class="sxs-lookup"><span data-stu-id="1b645-104">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="1b645-105">套件也可以包含其他檔案 (例如，安裝套件時所顯示的讀我檔案)，而且可以包含特定專案檔的轉換。</span><span class="sxs-lookup"><span data-stu-id="1b645-105">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="1b645-106">套件也可以只用來拉回任意數目的其他相依性，而不包含任何其專屬的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1b645-106">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="1b645-107">這類套件是傳遞包含多個獨立套件之 SDK 的便利方式。</span><span class="sxs-lookup"><span data-stu-id="1b645-107">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="1b645-108">在其他情況下，套件可能只包含符號 (`.pdb`) 檔案，以協助偵錯。</span><span class="sxs-lookup"><span data-stu-id="1b645-108">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="1b645-109">當您建立供其他開發人員使用的套件時，請務必了解它們會與您的工作相依。</span><span class="sxs-lookup"><span data-stu-id="1b645-109">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="1b645-110">因此，建立並發行套件也表示承諾修正 Bug 以及進行其他更新，或在極少的情況下將套件設為開放原始碼，以讓其他人可以協助進行維護。</span><span class="sxs-lookup"><span data-stu-id="1b645-110">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="1b645-111">不論是哪種情況，建立套件一開始都是先決定其識別碼、版本號碼、授權、著作權資訊，以及任何其他必要內容。</span><span class="sxs-lookup"><span data-stu-id="1b645-111">Whatever the case, creating a package begins with deciding its identifier, version number, license, copyright information, and any other necessary content.</span></span> <span data-ttu-id="1b645-112">完成後，您可以使用 "pack" 命令將所有項目都放在一個 `.nupkg` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1b645-112">Once done, you can use the "pack" command to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="1b645-113">您可以將這個檔案發佈至 NuGet 摘要，像是 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="1b645-113">This file can be published to a NuGet feed, like nuget.org.</span></span>

> [!Tip]
> <span data-ttu-id="1b645-114">副檔名為 `.nupkg` 的 NuGet 套件就是 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b645-114">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="1b645-115">若要輕鬆地檢查任何套件的內容，請將副檔名變更為 `.zip`，並如常展開其內容。</span><span class="sxs-lookup"><span data-stu-id="1b645-115">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="1b645-116">只要確定先將副檔名變更回 `.nupkg`，再嘗試將它重新載入至主機。</span><span class="sxs-lookup"><span data-stu-id="1b645-116">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="1b645-117">若要學習並了解建立程序，請從[建立套件](../create-packages/creating-a-package.md)開始，其會引導您完成所有套件通用的核心程序。</span><span class="sxs-lookup"><span data-stu-id="1b645-117">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span>

<span data-ttu-id="1b645-118">在這裡，您可以考慮您套件的許多其他選項：</span><span class="sxs-lookup"><span data-stu-id="1b645-118">From there, you can consider a number of other options for your package:</span></span>

- <span data-ttu-id="1b645-119">[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)描述如何建立具有不同 .NET Frameworks 之多個變異的套件。</span><span class="sxs-lookup"><span data-stu-id="1b645-119">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
- <span data-ttu-id="1b645-120">[建立當地語系化套件](../create-packages/creating-localized-packages.md)描述如何建構具有多個語言資源的套件，以及如何使用個別的當地語系化附屬套件。</span><span class="sxs-lookup"><span data-stu-id="1b645-120">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
- <span data-ttu-id="1b645-121">[發行前套件](../create-packages/prerelease-packages.md)示範如何將 alpha、beta 和 rc 套件發行至感興趣的客戶。</span><span class="sxs-lookup"><span data-stu-id="1b645-121">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
- <span data-ttu-id="1b645-122">[原始程式檔和組態檔轉換](../create-packages/source-and-config-file-transformations.md)描述如何在新增至專案的檔案中執行兩個單向權杖取代，以及使用會在解除安裝套件時取消的設定來修改 `web.config` 和 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="1b645-122">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
- <span data-ttu-id="1b645-123">[符號套件](../create-packages/symbol-packages-snupkg.md)提供用於提供程式庫符號的指引，而符號允許取用者在偵錯時逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="1b645-123">[Symbol Packages](../create-packages/symbol-packages-snupkg.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
- <span data-ttu-id="1b645-124">[套件版本控制](../concepts/package-versioning.md)討論如何識別您相依性容許的確切版本 (從套件取用的其他套件)。</span><span class="sxs-lookup"><span data-stu-id="1b645-124">[Package versioning](../concepts/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
- <span data-ttu-id="1b645-125">[原生套件](../guides/native-packages.md)描述用於建立 C++ 取用者之套件的程序。</span><span class="sxs-lookup"><span data-stu-id="1b645-125">[Native Packages](../guides/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>
- <span data-ttu-id="1b645-126">[簽署套件](../create-packages/sign-a-package.md)描述用於在套件新增數位簽章的程序。</span><span class="sxs-lookup"><span data-stu-id="1b645-126">[Signing Packages](../create-packages/sign-a-package.md) describes the process for adding a digital signature to a package.</span></span>

<span data-ttu-id="1b645-127">當您準備好將套件發行至 nuget.org 時，請遵循[發行套件](../nuget-org/publish-a-package.md)中的簡單程序。</span><span class="sxs-lookup"><span data-stu-id="1b645-127">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="1b645-128">如果您想要使用私人摘要，而非 nuget.org，請參閱[裝載套件概觀](../hosting-packages/overview.md)</span><span class="sxs-lookup"><span data-stu-id="1b645-128">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>
