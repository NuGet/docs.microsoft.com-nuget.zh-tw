---
title: NuGet CLI git-config 命令
description: Nuget.exe git-config 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426066"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="f7c47-103">組態命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f7c47-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="f7c47-104">**適用於：** 所有&bullet;**支援的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="f7c47-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="f7c47-105">取得或設定 NuGet 組態值。</span><span class="sxs-lookup"><span data-stu-id="f7c47-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="f7c47-106">額外的使用量，請參閱 <<c0> [ 常見的 NuGet 組態](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c47-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f7c47-107">如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c47-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f7c47-108">使用量</span><span class="sxs-lookup"><span data-stu-id="f7c47-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="f7c47-109">何處`<name>`和`<value>`指定要在組態中設定的索引鍵 / 值組。</span><span class="sxs-lookup"><span data-stu-id="f7c47-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="f7c47-110">您可以指定多個組所需。</span><span class="sxs-lookup"><span data-stu-id="f7c47-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="f7c47-111">若要移除的值，指定名稱和`=`號但沒有值。</span><span class="sxs-lookup"><span data-stu-id="f7c47-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="f7c47-112">如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c47-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="f7c47-113">在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="f7c47-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="f7c47-114">選項</span><span class="sxs-lookup"><span data-stu-id="f7c47-114">Options</span></span>

| <span data-ttu-id="f7c47-115">選項</span><span class="sxs-lookup"><span data-stu-id="f7c47-115">Option</span></span> | <span data-ttu-id="f7c47-116">描述</span><span class="sxs-lookup"><span data-stu-id="f7c47-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7c47-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="f7c47-117">AsPath</span></span> | <span data-ttu-id="f7c47-118">傳回組態值做為路徑，會忽略時`-Set`用。</span><span class="sxs-lookup"><span data-stu-id="f7c47-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="f7c47-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f7c47-119">ConfigFile</span></span> | <span data-ttu-id="f7c47-120">要修改的 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="f7c47-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="f7c47-121">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f7c47-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f7c47-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f7c47-122">ForceEnglishOutput</span></span> | <span data-ttu-id="f7c47-123">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f7c47-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f7c47-124">Help</span><span class="sxs-lookup"><span data-stu-id="f7c47-124">Help</span></span> | <span data-ttu-id="f7c47-125">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="f7c47-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="f7c47-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f7c47-126">NonInteractive</span></span> | <span data-ttu-id="f7c47-127">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="f7c47-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f7c47-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f7c47-128">Verbosity</span></span> | <span data-ttu-id="f7c47-129">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="f7c47-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f7c47-130">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f7c47-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="f7c47-131">範例</span><span class="sxs-lookup"><span data-stu-id="f7c47-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
