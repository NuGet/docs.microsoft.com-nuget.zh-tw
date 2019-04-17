---
title: NuGet CLI 新增命令
description: Nuget.exe 的參考加入命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545830"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="7e4f9-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7e4f9-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="7e4f9-104">**適用於**： 封裝發行&bullet;**支援的版本**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7e4f9-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="7e4f9-105">將指定的封裝加入至階層的配置，其中會建立資料夾的套件識別碼和版本號碼的非 HTTP 套件來源 （資料夾或 UNC 路徑） 中。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="7e4f9-106">例如: </span><span class="sxs-lookup"><span data-stu-id="7e4f9-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="7e4f9-107">當還原或更新對套件來源時，階層式版面配置會提供大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="7e4f9-108">若要展開套件中的所有檔案到目的地套件來源，請使用`-Expand`切換。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="7e4f9-109">這通常不會出現在目的地，例如其他子資料夾中會造成`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="7e4f9-110">使用量</span><span class="sxs-lookup"><span data-stu-id="7e4f9-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="7e4f9-111">何處`<packagePath>`是要加入，封裝的路徑名稱和`<sourcePath>`指定要加入封裝的資料夾為基礎的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="7e4f9-112">不支援 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="7e4f9-113">選項</span><span class="sxs-lookup"><span data-stu-id="7e4f9-113">Options</span></span>

| <span data-ttu-id="7e4f9-114">選項</span><span class="sxs-lookup"><span data-stu-id="7e4f9-114">Option</span></span> | <span data-ttu-id="7e4f9-115">描述</span><span class="sxs-lookup"><span data-stu-id="7e4f9-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e4f9-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7e4f9-116">ConfigFile</span></span> | <span data-ttu-id="7e4f9-117">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7e4f9-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7e4f9-119">Expand</span><span class="sxs-lookup"><span data-stu-id="7e4f9-119">Expand</span></span> | <span data-ttu-id="7e4f9-120">將封裝中的所有檔案，加入套件來源。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="7e4f9-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7e4f9-121">ForceEnglishOutput</span></span> | <span data-ttu-id="7e4f9-122">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7e4f9-123">Help</span><span class="sxs-lookup"><span data-stu-id="7e4f9-123">Help</span></span> | <span data-ttu-id="7e4f9-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="7e4f9-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7e4f9-125">NonInteractive</span></span> | <span data-ttu-id="7e4f9-126">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7e4f9-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7e4f9-127">Verbosity</span></span> | <span data-ttu-id="7e4f9-128">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="7e4f9-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7e4f9-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7e4f9-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7e4f9-130">範例</span><span class="sxs-lookup"><span data-stu-id="7e4f9-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
