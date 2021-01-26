---
title: NuGet CLI 新增命令
description: nuget.exe add 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776086"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="e5493-103"> (NuGet CLI 新增命令) </span><span class="sxs-lookup"><span data-stu-id="e5493-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="e5493-104">**適用于**：套件發行 &bullet; **支援的版本**： 3.3 +</span><span class="sxs-lookup"><span data-stu-id="e5493-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="e5493-105">將指定的封裝新增至非 HTTP 套件來源 (資料夾或 UNC 路徑) 以階層配置的方式，也就是針對封裝識別碼和版本號碼建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5493-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="e5493-106">例如：</span><span class="sxs-lookup"><span data-stu-id="e5493-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="e5493-107">針對套件來源還原或更新時，階層配置可提供明顯較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="e5493-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="e5493-108">若要將封裝中的所有檔案展開至目的地套件來源，請使用 `-Expand` 參數。</span><span class="sxs-lookup"><span data-stu-id="e5493-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="e5493-109">這通常會導致目的地中出現額外的子資料夾，例如 `tools` 和 `lib` 。</span><span class="sxs-lookup"><span data-stu-id="e5493-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="e5493-110">使用方式</span><span class="sxs-lookup"><span data-stu-id="e5493-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="e5493-111">其中 `<packagePath>` 是要加入之封裝的路徑名稱，並 `<sourcePath>` 指定將加入封裝的資料夾型封裝來源。</span><span class="sxs-lookup"><span data-stu-id="e5493-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="e5493-112">不支援 HTTP 來源。</span><span class="sxs-lookup"><span data-stu-id="e5493-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="e5493-113">選項。</span><span class="sxs-lookup"><span data-stu-id="e5493-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e5493-114">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="e5493-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e5493-115">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="e5493-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="e5493-116">將封裝中的所有檔案新增至套件來源。</span><span class="sxs-lookup"><span data-stu-id="e5493-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e5493-117">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="e5493-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="e5493-118">使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="e5493-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e5493-119">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="e5493-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e5493-120">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="e5493-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="e5493-121">指定要將 nupkg 新增至其中的 [封裝來源]，也就是資料夾或 UNC 共用。</span><span class="sxs-lookup"><span data-stu-id="e5493-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="e5493-122">不支援 Http 來源。</span><span class="sxs-lookup"><span data-stu-id="e5493-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e5493-123">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="e5493-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="e5493-124">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e5493-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e5493-125">範例</span><span class="sxs-lookup"><span data-stu-id="e5493-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
