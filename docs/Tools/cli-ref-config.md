---
title: NuGet CLI 組態命令
description: Nuget.exe 組態命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="64fca-103">組態命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="64fca-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="64fca-104">**適用於：**所有&bullet;**支援的版本，**： 所有</span><span class="sxs-lookup"><span data-stu-id="64fca-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="64fca-105">取得或設定 NuGet 組態值。</span><span class="sxs-lookup"><span data-stu-id="64fca-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="64fca-106">對於其他使用方式，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="64fca-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="64fca-107">如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="64fca-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="64fca-108">使用量</span><span class="sxs-lookup"><span data-stu-id="64fca-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="64fca-109">其中`<name>`和`<value>`指定要在組態中設定的索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="64fca-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="64fca-110">您可以視需要指定多組。</span><span class="sxs-lookup"><span data-stu-id="64fca-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="64fca-111">若要移除的值，指定名稱和`=`號但沒有值。</span><span class="sxs-lookup"><span data-stu-id="64fca-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="64fca-112">如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="64fca-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="64fca-113">在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="64fca-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="64fca-114">選項</span><span class="sxs-lookup"><span data-stu-id="64fca-114">Options</span></span>

| <span data-ttu-id="64fca-115">選項</span><span class="sxs-lookup"><span data-stu-id="64fca-115">Option</span></span> | <span data-ttu-id="64fca-116">描述</span><span class="sxs-lookup"><span data-stu-id="64fca-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64fca-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="64fca-117">AsPath</span></span> | <span data-ttu-id="64fca-118">傳回組態值做為路徑，會忽略時`-Set`用。</span><span class="sxs-lookup"><span data-stu-id="64fca-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="64fca-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="64fca-119">ConfigFile</span></span> | <span data-ttu-id="64fca-120">要修改的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="64fca-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="64fca-121">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="64fca-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="64fca-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="64fca-122">ForceEnglishOutput</span></span> | <span data-ttu-id="64fca-123">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="64fca-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="64fca-124">說明</span><span class="sxs-lookup"><span data-stu-id="64fca-124">Help</span></span> | <span data-ttu-id="64fca-125">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="64fca-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="64fca-126">非互動式</span><span class="sxs-lookup"><span data-stu-id="64fca-126">NonInteractive</span></span> | <span data-ttu-id="64fca-127">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="64fca-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="64fca-128">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="64fca-128">Verbosity</span></span> | <span data-ttu-id="64fca-129">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="64fca-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="64fca-130">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="64fca-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="64fca-131">範例</span><span class="sxs-lookup"><span data-stu-id="64fca-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
