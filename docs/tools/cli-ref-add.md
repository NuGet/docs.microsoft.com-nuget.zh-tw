---
title: 將命令加入 NuGet CLI
description: Nuget.exe 的參考加入命令
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="2349e-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2349e-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="2349e-104">**適用於**： 封裝發行&bullet;**支援的版本，**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="2349e-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="2349e-105">將指定的封裝加入至階層式配置，其中的封裝識別碼和版本號碼會建立資料夾中的非 HTTP 封裝來源 （資料夾或 UNC 路徑）。</span><span class="sxs-lookup"><span data-stu-id="2349e-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="2349e-106">例如: </span><span class="sxs-lookup"><span data-stu-id="2349e-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="2349e-107">當還原或更新對套件來源時，階層式配置會提供大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="2349e-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="2349e-108">若要擴充套件中的所有檔案到目的地封裝來源，使用`-Expand`切換。</span><span class="sxs-lookup"><span data-stu-id="2349e-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="2349e-109">這通常會導致其他子資料夾，例如出現在目的地`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="2349e-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="2349e-110">使用量</span><span class="sxs-lookup"><span data-stu-id="2349e-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="2349e-111">其中`<packagePath>`是若要加入，封裝的路徑名稱和`<sourcePath>`指定要加入封裝的資料夾為基礎的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="2349e-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="2349e-112">不支援 HTTP 的來源。</span><span class="sxs-lookup"><span data-stu-id="2349e-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="2349e-113">選項</span><span class="sxs-lookup"><span data-stu-id="2349e-113">Options</span></span>

| <span data-ttu-id="2349e-114">選項</span><span class="sxs-lookup"><span data-stu-id="2349e-114">Option</span></span> | <span data-ttu-id="2349e-115">描述</span><span class="sxs-lookup"><span data-stu-id="2349e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2349e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2349e-116">ConfigFile</span></span> | <span data-ttu-id="2349e-117">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="2349e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2349e-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="2349e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2349e-119">Expand</span><span class="sxs-lookup"><span data-stu-id="2349e-119">Expand</span></span> | <span data-ttu-id="2349e-120">加入封裝中的所有檔案，對套件來源。</span><span class="sxs-lookup"><span data-stu-id="2349e-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="2349e-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2349e-121">ForceEnglishOutput</span></span> | <span data-ttu-id="2349e-122">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="2349e-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2349e-123">說明</span><span class="sxs-lookup"><span data-stu-id="2349e-123">Help</span></span> | <span data-ttu-id="2349e-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="2349e-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="2349e-125">非互動式</span><span class="sxs-lookup"><span data-stu-id="2349e-125">NonInteractive</span></span> | <span data-ttu-id="2349e-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="2349e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2349e-127">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2349e-127">Verbosity</span></span> | <span data-ttu-id="2349e-128">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="2349e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2349e-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2349e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2349e-130">範例</span><span class="sxs-lookup"><span data-stu-id="2349e-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
