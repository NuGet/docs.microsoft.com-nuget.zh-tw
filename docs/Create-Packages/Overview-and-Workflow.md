---
title: 建立 NuGet 套件的概觀和工作流程 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 建立和發行 NuGet 套件程序的概觀，以及程序之其他特定部分的連結。
keywords: NuGet 套件建立, NuGet 建立概觀, NuGet 建立工作流程, 套件建立工作流程, 套件建立概觀。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: df08e15c2632a88ea7cc3333d64f4844c78c278d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="package-creation-workflow"></a><span data-ttu-id="9dd0b-104">套件建立工作流程</span><span class="sxs-lookup"><span data-stu-id="9dd0b-104">Package creation workflow</span></span>

<span data-ttu-id="9dd0b-105">建立套件是以想要封裝並與其他人共用 (透過公用 nuget.org 資源庫或組織內的私用資源庫) 的已編譯程式碼 (一般是 .NET 組件) 開始。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-105">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="9dd0b-106">套件也可以包含其他檔案 (例如，安裝套件時所顯示的讀我檔案)，而且可以包含特定專案檔的轉換。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-106">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="9dd0b-107">套件也可以只用來拉回任意數目的其他相依性，而不包含任何其專屬的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-107">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="9dd0b-108">這類套件是傳遞包含多個獨立套件之 SDK 的便利方式。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-108">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="9dd0b-109">在其他情況下，套件可能只包含符號 (`.pdb`) 檔案，以協助偵錯。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-109">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="9dd0b-110">當您建立供其他開發人員使用的套件時，請務必了解它們會與您的工作相依。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-110">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="9dd0b-111">因此，建立並發行套件也表示承諾修正 Bug 以及進行其他更新，或在極少的情況下將套件設為開放原始碼，以讓其他人可以協助進行維護。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-111">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="9dd0b-112">不管是哪種情況，建立套件都是從決定要封裝的組件和其他檔案開始。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-112">Whatever the case, creating a package begins with deciding which assemblies and other files to package.</span></span> <span data-ttu-id="9dd0b-113">您接著會建立資訊清單檔案 (稱為 `.nuspec` 檔案)，以描述套件的內容以及其識別碼、版本號碼、著作權資訊、MSBuild pros 和 targets 等等。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-113">You then create a manifest file, referred to as a `.nuspec` file, to describe the package's contents along with its identifier, version number, copyright information, MSBuild props and targets, and much more.</span></span>

<span data-ttu-id="9dd0b-114">當您在適當的資料夾中準備好所有必要檔案並建立適當的 `.nuspec` 檔案時，則會使用 `nuget pack` 命令 (或 [MSBuild 封裝目標](../reference/msbuild-targets.md)) 以將所有項目都放入 `.nupkg` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-114">When you've prepared all the necessary files in the appropriate folders and have created the appropriate `.nuspec` file, you then use the `nuget pack` command (or the [MSBuild pack target](../reference/msbuild-targets.md)) to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="9dd0b-115">您準備好將套件部署至可讓其他開發人員使用它的主機。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-115">You're then ready to deploy the package to whatever host makes it available to other developers.</span></span>

> [!Tip]
> <span data-ttu-id="9dd0b-116">副檔名為 `.nupkg` 的 NuGet 套件就是 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-116">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="9dd0b-117">若要輕鬆地檢查任何套件的內容，請將副檔名變更為 `.zip`，並如常展開其內容。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-117">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="9dd0b-118">只要確定先將副檔名變更回 `.nupkg`，再嘗試將它重新載入至主機。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-118">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="9dd0b-119">若要學習並了解建立程序，請從[建立套件](../create-packages/creating-a-package.md)開始，其會引導您完成所有套件通用的核心程序。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-119">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span>

<span data-ttu-id="9dd0b-120">在這裡，您可以考慮您套件的許多其他選項：</span><span class="sxs-lookup"><span data-stu-id="9dd0b-120">From there, you can consider a number of other options for your package:</span></span>

- <span data-ttu-id="9dd0b-121">[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)描述如何建立具有不同 .NET Frameworks 之多個變異的套件。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-121">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
- <span data-ttu-id="9dd0b-122">[建立當地語系化套件](../create-packages/creating-localized-packages.md)描述如何建構具有多個語言資源的套件，以及如何使用個別的當地語系化附屬套件。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-122">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
- <span data-ttu-id="9dd0b-123">[發行前套件](../create-packages/prerelease-packages.md)示範如何將 alpha、beta 和 rc 套件發行至感興趣的客戶。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-123">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
- <span data-ttu-id="9dd0b-124">[原始程式檔和組態檔轉換](../create-packages/source-and-config-file-transformations.md)描述如何在新增至專案的檔案中執行兩個單向權杖取代，以及使用會在解除安裝套件時取消的設定來修改 `web.config` 和 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-124">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
- <span data-ttu-id="9dd0b-125">[符號套件](../create-packages/symbol-packages.md)提供用於提供程式庫符號的指引，而符號允許取用者在偵錯時逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-125">[Symbol Packages](../create-packages/symbol-packages.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
- <span data-ttu-id="9dd0b-126">[套件版本控制](../reference/package-versioning.md)討論如何識別您相依性容許的確切版本 (從套件取用的其他套件)。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-126">[Package versioning](../reference/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
- <span data-ttu-id="9dd0b-127">[原生套件](../create-packages/native-packages.md)描述用於建立 C++ 取用者之套件的程序。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-127">[Native Packages](../create-packages/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>
- <span data-ttu-id="9dd0b-128">[簽署套件](../create-packages/sign-a-package.md)描述用於在套件新增數位簽章的程序。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-128">[Signing Packages](../create-packages/sign-a-package.md) describes the process for adding a digital signature to a package.</span></span>

<span data-ttu-id="9dd0b-129">當您準備好將套件發行至 nuget.org 時，請遵循[發行套件](../create-packages/publish-a-package.md)中的簡單程序。</span><span class="sxs-lookup"><span data-stu-id="9dd0b-129">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="9dd0b-130">如果您想要使用私人摘要，而非 nuget.org，請參閱[裝載套件概觀](../hosting-packages/overview.md)</span><span class="sxs-lookup"><span data-stu-id="9dd0b-130">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>
