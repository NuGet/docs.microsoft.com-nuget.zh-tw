---
title: "NuGet CLI 組態命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 組態命令的參考"
keywords: "nuget 組態參考組態命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7cf7c06000904a617752567ed7612c0c48042db9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="973e9-104">組態命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="973e9-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="973e9-105">**適用於：**所有&bullet;**支援的版本，**： 所有</span><span class="sxs-lookup"><span data-stu-id="973e9-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="973e9-106">取得或設定 NuGet 組態值。</span><span class="sxs-lookup"><span data-stu-id="973e9-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="973e9-107">對於其他使用方式，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="973e9-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="973e9-108">如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="973e9-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="973e9-109">使用量</span><span class="sxs-lookup"><span data-stu-id="973e9-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="973e9-110">其中`<name>`和`<value>`指定要在組態中設定的索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="973e9-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="973e9-111">您可以視需要指定多組。</span><span class="sxs-lookup"><span data-stu-id="973e9-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="973e9-112">若要移除的值，指定名稱和`=`號但沒有值。</span><span class="sxs-lookup"><span data-stu-id="973e9-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="973e9-113">如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="973e9-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="973e9-114">在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="973e9-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="973e9-115">選項</span><span class="sxs-lookup"><span data-stu-id="973e9-115">Options</span></span>

| <span data-ttu-id="973e9-116">選項</span><span class="sxs-lookup"><span data-stu-id="973e9-116">Option</span></span> | <span data-ttu-id="973e9-117">描述</span><span class="sxs-lookup"><span data-stu-id="973e9-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="973e9-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="973e9-118">AsPath</span></span> | <span data-ttu-id="973e9-119">傳回組態值做為路徑，會忽略時`-Set`用。</span><span class="sxs-lookup"><span data-stu-id="973e9-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="973e9-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="973e9-120">ConfigFile</span></span> | <span data-ttu-id="973e9-121">要修改的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="973e9-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="973e9-122">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="973e9-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="973e9-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="973e9-123">ForceEnglishOutput</span></span> | <span data-ttu-id="973e9-124">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="973e9-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="973e9-125">說明</span><span class="sxs-lookup"><span data-stu-id="973e9-125">Help</span></span> | <span data-ttu-id="973e9-126">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="973e9-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="973e9-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="973e9-127">NonInteractive</span></span> | <span data-ttu-id="973e9-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="973e9-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="973e9-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="973e9-129">Verbosity</span></span> | <span data-ttu-id="973e9-130">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="973e9-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="973e9-131">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="973e9-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="973e9-132">範例</span><span class="sxs-lookup"><span data-stu-id="973e9-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
