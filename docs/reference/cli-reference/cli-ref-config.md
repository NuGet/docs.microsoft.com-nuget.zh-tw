---
title: NuGet CLI config 命令
description: Nuget.exe config 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433311"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="22e5f-103">config 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="22e5f-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="22e5f-104">**適用于:** 所有&bullet; **支援的版本**: 全部</span><span class="sxs-lookup"><span data-stu-id="22e5f-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="22e5f-105">取得或設定 NuGet 設定值。</span><span class="sxs-lookup"><span data-stu-id="22e5f-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="22e5f-106">如需其他用法, 請參閱[一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="22e5f-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="22e5f-107">如需可允許金鑰名稱的詳細資訊, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="22e5f-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="22e5f-108">使用量</span><span class="sxs-lookup"><span data-stu-id="22e5f-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="22e5f-109">其中`<name>` , `<value>`並指定要在設定中設定的機碼值組。</span><span class="sxs-lookup"><span data-stu-id="22e5f-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="22e5f-110">您可以指定所需數量的配對。</span><span class="sxs-lookup"><span data-stu-id="22e5f-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="22e5f-111">若要移除值, 請指定名稱和`=`正負號, 但沒有值。</span><span class="sxs-lookup"><span data-stu-id="22e5f-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="22e5f-112">如需允許的金鑰名稱, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="22e5f-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="22e5f-113">在 NuGet 3.4 + 中`<value>` , 可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="22e5f-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="22e5f-114">選項</span><span class="sxs-lookup"><span data-stu-id="22e5f-114">Options</span></span>

| <span data-ttu-id="22e5f-115">選項</span><span class="sxs-lookup"><span data-stu-id="22e5f-115">Option</span></span> | <span data-ttu-id="22e5f-116">說明</span><span class="sxs-lookup"><span data-stu-id="22e5f-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22e5f-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="22e5f-117">AsPath</span></span> | <span data-ttu-id="22e5f-118">傳回設定值做為路徑, 並在使用`-Set`時予以忽略。</span><span class="sxs-lookup"><span data-stu-id="22e5f-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="22e5f-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="22e5f-119">ConfigFile</span></span> | <span data-ttu-id="22e5f-120">要修改的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="22e5f-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="22e5f-121">如果未指定, 則會使用預設檔案-`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.config/NuGet/NuGet.Config` (Mac/Linux) 或`~/.nuget/NuGet/NuGet.Config` (依 OS 散發而有所不同)。</span><span class="sxs-lookup"><span data-stu-id="22e5f-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="22e5f-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="22e5f-122">ForceEnglishOutput</span></span> | <span data-ttu-id="22e5f-123">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="22e5f-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="22e5f-124">Help</span><span class="sxs-lookup"><span data-stu-id="22e5f-124">Help</span></span> | <span data-ttu-id="22e5f-125">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="22e5f-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="22e5f-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="22e5f-126">NonInteractive</span></span> | <span data-ttu-id="22e5f-127">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="22e5f-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="22e5f-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="22e5f-128">Verbosity</span></span> | <span data-ttu-id="22e5f-129">指定輸出中顯示的詳細資料量: [*一般*] 、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="22e5f-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="22e5f-130">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="22e5f-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="22e5f-131">範例</span><span class="sxs-lookup"><span data-stu-id="22e5f-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
