---
title: NuGet CLI config 命令
description: nuget.exe config 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775963"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="9c17f-103"> (NuGet CLI 的設定命令) </span><span class="sxs-lookup"><span data-stu-id="9c17f-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="9c17f-104">**適用于：** 所有 &bullet; **支援的版本**：全部</span><span class="sxs-lookup"><span data-stu-id="9c17f-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="9c17f-105">取得或設定 NuGet 設定值。</span><span class="sxs-lookup"><span data-stu-id="9c17f-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="9c17f-106">如需其他使用方式，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="9c17f-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="9c17f-107">如需允許的金鑰名稱的詳細資訊，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="9c17f-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9c17f-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="9c17f-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="9c17f-109">其中 `<name>` 並 `<value>` 指定要在設定中設定的機碼值組。</span><span class="sxs-lookup"><span data-stu-id="9c17f-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="9c17f-110">您可以視需要指定任意數量的配對。</span><span class="sxs-lookup"><span data-stu-id="9c17f-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="9c17f-111">若要移除值，請指定名稱和 `=` 正負號，但不指定值。</span><span class="sxs-lookup"><span data-stu-id="9c17f-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="9c17f-112">如需允許的金鑰名稱，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="9c17f-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="9c17f-113">在 NuGet 3.4 + 中， `<value>` 可以使用 [環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="9c17f-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="9c17f-114">選項。</span><span class="sxs-lookup"><span data-stu-id="9c17f-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="9c17f-115">以路徑形式傳回設定值，使用時會忽略 `-Set` 。</span><span class="sxs-lookup"><span data-stu-id="9c17f-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="9c17f-116">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="9c17f-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9c17f-117">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="9c17f-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="9c17f-118">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="9c17f-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="9c17f-119">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="9c17f-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="9c17f-120">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="9c17f-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="9c17f-121">一個要在 config 中設定的索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="9c17f-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="9c17f-122">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="9c17f-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="9c17f-123">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9c17f-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="9c17f-124">範例</span><span class="sxs-lookup"><span data-stu-id="9c17f-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
