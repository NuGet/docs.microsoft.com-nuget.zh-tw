---
title: NuGet CLI 區域變數命令
description: nuget.exe 區域變數命令的參考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623054"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="be85d-103"> (NuGet CLI 的區域變數命令) </span><span class="sxs-lookup"><span data-stu-id="be85d-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="be85d-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="be85d-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="be85d-105">清除或列出本機 NuGet 資源，例如 *HTTP*快取、 *全域套件* 資料夾和 temp 資料夾。</span><span class="sxs-lookup"><span data-stu-id="be85d-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="be85d-106">`locals`命令也可以用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="be85d-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="be85d-107">如需詳細資訊，請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="be85d-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="be85d-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="be85d-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="be85d-109">其中 `<folder>` 是 `all` 、 `http-cache` 、 `packages-cache` \* (3.5 和較早的) \*、 `global-packages` `temp` \* (3.4 +) \*，以及 `plugins-cache` \* (4.8 +) \*。</span><span class="sxs-lookup"><span data-stu-id="be85d-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="be85d-110">選項。</span><span class="sxs-lookup"><span data-stu-id="be85d-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="be85d-111">清除指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="be85d-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="be85d-112">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="be85d-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="be85d-113">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="be85d-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="be85d-114">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="be85d-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="be85d-115">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="be85d-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="be85d-116">列出指定之資料夾的位置，或與 *所有*資料夾一起使用時的位置。</span><span class="sxs-lookup"><span data-stu-id="be85d-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="be85d-117">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="be85d-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="be85d-118">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="be85d-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="be85d-119">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="be85d-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="be85d-120">範例</span><span class="sxs-lookup"><span data-stu-id="be85d-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="be85d-121">如需其他範例，請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="be85d-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
