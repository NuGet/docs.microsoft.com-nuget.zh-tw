---
title: NuGet CLI init 命令
description: nuget.exe init 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780067"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="b4783-103"> (NuGet CLI 的 init 命令) </span><span class="sxs-lookup"><span data-stu-id="b4783-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="b4783-104">**適用物件：** 套件建立 &bullet; **支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b4783-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="b4783-105">使用階層配置，將所有封裝從一般資料夾複製到目的資料夾，如 [新增命令](cli-ref-add.md)所述。</span><span class="sxs-lookup"><span data-stu-id="b4783-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="b4783-106">也就是說，使用 `init` 相當於在 `add` 資料夾中的每個封裝上使用命令。</span><span class="sxs-lookup"><span data-stu-id="b4783-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="b4783-107">如同 `add` ，目的地必須是本機資料夾或 UNC 路徑。不支援 HTTP 套件存放庫（例如 nuget.org 或私用伺服器）。</span><span class="sxs-lookup"><span data-stu-id="b4783-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="b4783-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="b4783-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="b4783-109">其中 `<source>` 是包含封裝的資料夾，以及 `<destination>` 要將封裝複製到其中的本機資料夾或 UNC 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="b4783-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="b4783-110">選項。</span><span class="sxs-lookup"><span data-stu-id="b4783-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b4783-111">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4783-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b4783-112">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="b4783-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="b4783-113">將每個新增至封裝來源的套件中的所有檔案加入。與 `-Expand` `add` 命令相同。</span><span class="sxs-lookup"><span data-stu-id="b4783-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b4783-114">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="b4783-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b4783-115">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="b4783-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b4783-116">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="b4783-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b4783-117">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="b4783-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="b4783-118">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b4783-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b4783-119">範例</span><span class="sxs-lookup"><span data-stu-id="b4783-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
