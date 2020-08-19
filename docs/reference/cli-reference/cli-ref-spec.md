---
title: NuGet CLI 規格命令
description: nuget.exe 規格命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622560"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="ab377-103"> (NuGet CLI 的 spec 命令) </span><span class="sxs-lookup"><span data-stu-id="ab377-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="ab377-104">**適用物件：** 套件建立 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="ab377-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ab377-105">產生 `.nuspec` 新封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="ab377-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="ab377-106">如果在與專案檔相同的資料夾中執行 (`.csproj` ， `.vbproj`) 會建立 token 化檔案 `.fsproj` `spec` `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="ab377-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="ab377-107">如需詳細資訊，請參閱 [建立封裝](../../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="ab377-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ab377-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="ab377-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="ab377-109">其中 `<packageID>` 是要儲存在檔案中的選擇性封裝識別碼 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="ab377-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="ab377-110">選項。</span><span class="sxs-lookup"><span data-stu-id="ab377-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="ab377-111">指定要用於中繼資料之元件的路徑。</span><span class="sxs-lookup"><span data-stu-id="ab377-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="ab377-112">覆寫任何現有 `.nuspec` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ab377-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="ab377-113">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="ab377-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ab377-114">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="ab377-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ab377-115">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="ab377-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ab377-116">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="ab377-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ab377-117">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab377-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab377-118">範例</span><span class="sxs-lookup"><span data-stu-id="ab377-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
