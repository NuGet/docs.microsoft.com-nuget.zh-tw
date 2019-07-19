---
title: NuGet CLI config 命令
description: Nuget.exe config 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327845"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="49da1-103">config 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="49da1-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="49da1-104">**適用于:** 所有&bullet; **支援的版本**: 全部</span><span class="sxs-lookup"><span data-stu-id="49da1-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="49da1-105">取得或設定 NuGet 設定值。</span><span class="sxs-lookup"><span data-stu-id="49da1-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="49da1-106">如需其他用法, 請參閱[一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="49da1-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="49da1-107">如需可允許金鑰名稱的詳細資訊, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="49da1-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="49da1-108">使用量</span><span class="sxs-lookup"><span data-stu-id="49da1-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="49da1-109">其中`<name>` , `<value>`並指定要在設定中設定的機碼值組。</span><span class="sxs-lookup"><span data-stu-id="49da1-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="49da1-110">您可以指定所需數量的配對。</span><span class="sxs-lookup"><span data-stu-id="49da1-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="49da1-111">若要移除值, 請指定名稱和`=`正負號, 但沒有值。</span><span class="sxs-lookup"><span data-stu-id="49da1-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="49da1-112">如需允許的金鑰名稱, 請參閱[NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="49da1-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="49da1-113">在 NuGet 3.4 + 中`<value>` , 可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="49da1-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="49da1-114">選項</span><span class="sxs-lookup"><span data-stu-id="49da1-114">Options</span></span>

| <span data-ttu-id="49da1-115">選項</span><span class="sxs-lookup"><span data-stu-id="49da1-115">Option</span></span> | <span data-ttu-id="49da1-116">說明</span><span class="sxs-lookup"><span data-stu-id="49da1-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49da1-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="49da1-117">AsPath</span></span> | <span data-ttu-id="49da1-118">傳回設定值做為路徑, 並在使用`-Set`時予以忽略。</span><span class="sxs-lookup"><span data-stu-id="49da1-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="49da1-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="49da1-119">ConfigFile</span></span> | <span data-ttu-id="49da1-120">要修改的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="49da1-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="49da1-121">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="49da1-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="49da1-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="49da1-122">ForceEnglishOutput</span></span> | <span data-ttu-id="49da1-123">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="49da1-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="49da1-124">Help</span><span class="sxs-lookup"><span data-stu-id="49da1-124">Help</span></span> | <span data-ttu-id="49da1-125">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="49da1-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="49da1-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="49da1-126">NonInteractive</span></span> | <span data-ttu-id="49da1-127">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="49da1-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="49da1-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="49da1-128">Verbosity</span></span> | <span data-ttu-id="49da1-129">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="49da1-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="49da1-130">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="49da1-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="49da1-131">範例</span><span class="sxs-lookup"><span data-stu-id="49da1-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
