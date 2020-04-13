---
title: 設定本機 NuGet 摘要
description: 如何使用區域網路上的資料夾建立 NuGet 套件的本機摘要
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317597"
---
# <a name="local-feeds"></a><span data-ttu-id="5a30f-103">本機摘要</span><span class="sxs-lookup"><span data-stu-id="5a30f-103">Local feeds</span></span>

<span data-ttu-id="5a30f-104">本機的 NuGet 套件摘要只是您區域網路 (或只是您自己的電腦) 上放置套件的階層式資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="5a30f-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="5a30f-105">然後，這些摘要會和所有其他使用 CLI、套件管理員 UI 和套件管理員主控台的 NuGet 作業一起，作為套件來源。</span><span class="sxs-lookup"><span data-stu-id="5a30f-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="5a30f-106">若要啟用來源，請使用[套件管理員 UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) 或 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) 命令，將其路徑名稱 (例如 `\\myserver\packages`) 新增至來源清單。</span><span class="sxs-lookup"><span data-stu-id="5a30f-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="5a30f-107">NuGet 3.3+ 支援階層式資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="5a30f-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="5a30f-108">舊版的 NuGet 只使用包含套件的單一資料夾，此類資料夾的效能遠低於階層式結構。</span><span class="sxs-lookup"><span data-stu-id="5a30f-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="5a30f-109">初始化和維護階層式資料夾</span><span class="sxs-lookup"><span data-stu-id="5a30f-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="5a30f-110">階層式版本的資料夾樹狀目錄有下列的一般結構：</span><span class="sxs-lookup"><span data-stu-id="5a30f-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="5a30f-111">當您使用指令將套件複製到來源時,NuGet[`nuget add`](../reference/cli-reference/cli-ref-add.md)會自動建立此結構:</span><span class="sxs-lookup"><span data-stu-id="5a30f-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="5a30f-112">`nuget add` 命令一次使用一個套件，這在設定有多個套件的摘要時會很不方便。</span><span class="sxs-lookup"><span data-stu-id="5a30f-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="5a30f-113">在這種情況下,使用命令[`nuget init`](../reference/cli-reference/cli-ref-init.md)將資料夾中的所有包複製到源,就像單獨運行`nuget add`每個包一樣。</span><span class="sxs-lookup"><span data-stu-id="5a30f-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="5a30f-114">例如，下列命令會將所有的套件從 `c:\packages` 複製到 `\\myserver\packages` 的階層式樹狀結構：</span><span class="sxs-lookup"><span data-stu-id="5a30f-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="5a30f-115">與 `add` 命令一樣，`init` 會為每個套件識別碼建立一個資料夾，各自包含一個版本號碼資料夾，裡面是合適的套件。</span><span class="sxs-lookup"><span data-stu-id="5a30f-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
