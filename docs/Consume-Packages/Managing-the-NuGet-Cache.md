---
title: "如何管理 NuGet 中的套件快取 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "如何管理存在電腦上的不同 NuGet 套件快取，安裝或還原套件時會使用這些快取。"
keywords: "NuGet 套件快取, 套件快取, NuGet 快取, 管理快取, 本機 NuGet 快取, 全域 NuGet 快取, NuGet locals 命令, 清除快取"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="b6b03-104">管理 NuGet 快取</span><span class="sxs-lookup"><span data-stu-id="b6b03-104">Managing the NuGet cache</span></span>

<span data-ttu-id="b6b03-105">NuGet 會管理數個本機快取，以免下載電腦上已有的套件，並提供離線支援。</span><span class="sxs-lookup"><span data-stu-id="b6b03-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="b6b03-106">NuGet 2.8+ 會自動切換回安裝或重新安裝套件時快取，不需要網路連線。</span><span class="sxs-lookup"><span data-stu-id="b6b03-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="b6b03-107">使用 [locals 命令](../tools/cli-ref-locals.md) 取得快取位置：</span><span class="sxs-lookup"><span data-stu-id="b6b03-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="b6b03-108">一般輸出如下：</span><span class="sxs-lookup"><span data-stu-id="b6b03-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="b6b03-109">如果遇到套件安裝問題，或想要確保安裝的是遠端資源庫的套件，請使用 `locals -clear` 選項：</span><span class="sxs-lookup"><span data-stu-id="b6b03-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="b6b03-110">請注意，目前僅支援從 NuGet 命令列管理快取，不支援在 Visual Studio 中或透過套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="b6b03-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="b6b03-111">此外，NuGet 3.6 和更新版本不支援管理 2.x 快取。</span><span class="sxs-lookup"><span data-stu-id="b6b03-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="b6b03-112">使用 `nuget locals` 時會發生下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="b6b03-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="b6b03-113">**本機資源清除失敗：無法刪除一或多個檔案**</span><span class="sxs-lookup"><span data-stu-id="b6b03-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="b6b03-114">**目錄不是空的**</span><span class="sxs-lookup"><span data-stu-id="b6b03-114">**The directory is not empty**</span></span>

<span data-ttu-id="b6b03-115">這些都表示您沒有刪除快取中檔案的權限，或另一個處理序正在使用快取中的一或多個檔案，檔案必須先關閉才能移除。</span><span class="sxs-lookup"><span data-stu-id="b6b03-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>