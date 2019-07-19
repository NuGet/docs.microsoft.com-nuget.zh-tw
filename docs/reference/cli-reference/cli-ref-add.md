---
title: NuGet CLI 新增命令
description: Nuget.exe add 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327855"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="40145-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="40145-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="40145-104">**適用**于: 套件發佈&bullet; **支援的版本**:3.3+</span><span class="sxs-lookup"><span data-stu-id="40145-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="40145-105">將指定的封裝新增至階層式配置中的非 HTTP 封裝來源 (資料夾或 UNC 路徑), 其中會建立套件識別碼和版本號碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="40145-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="40145-106">例如：</span><span class="sxs-lookup"><span data-stu-id="40145-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="40145-107">針對套件來源還原或更新時, 階層式配置可提供明顯較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="40145-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="40145-108">若要將封裝中的所有檔案展開至目的地封裝來源, 請使用`-Expand`參數。</span><span class="sxs-lookup"><span data-stu-id="40145-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="40145-109">這通常會導致目的地中出現額外的子資料夾, 例如`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="40145-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="40145-110">使用量</span><span class="sxs-lookup"><span data-stu-id="40145-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="40145-111">其中`<packagePath>`是要新增之封裝的路徑名稱, 並`<sourcePath>`指定要新增封裝之以資料夾為基礎的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="40145-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="40145-112">不支援 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="40145-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="40145-113">選項</span><span class="sxs-lookup"><span data-stu-id="40145-113">Options</span></span>

| <span data-ttu-id="40145-114">選項</span><span class="sxs-lookup"><span data-stu-id="40145-114">Option</span></span> | <span data-ttu-id="40145-115">說明</span><span class="sxs-lookup"><span data-stu-id="40145-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40145-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="40145-116">ConfigFile</span></span> | <span data-ttu-id="40145-117">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="40145-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="40145-118">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="40145-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="40145-119">Expand</span><span class="sxs-lookup"><span data-stu-id="40145-119">Expand</span></span> | <span data-ttu-id="40145-120">將封裝中的所有檔案新增至封裝來源。</span><span class="sxs-lookup"><span data-stu-id="40145-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="40145-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="40145-121">ForceEnglishOutput</span></span> | <span data-ttu-id="40145-122">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="40145-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="40145-123">Help</span><span class="sxs-lookup"><span data-stu-id="40145-123">Help</span></span> | <span data-ttu-id="40145-124">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="40145-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="40145-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="40145-125">NonInteractive</span></span> | <span data-ttu-id="40145-126">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="40145-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="40145-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="40145-127">Verbosity</span></span> | <span data-ttu-id="40145-128">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="40145-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="40145-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="40145-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="40145-130">範例</span><span class="sxs-lookup"><span data-stu-id="40145-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
