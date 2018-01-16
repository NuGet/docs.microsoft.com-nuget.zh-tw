---
title: "NuGet CLI 組態命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Nuget.exe 組態命令的參考"
keywords: "nuget 組態參考組態命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="50bc1-104">組態命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="50bc1-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="50bc1-105">**適用於：**所有&bullet;**支援的版本，**： 所有</span><span class="sxs-lookup"><span data-stu-id="50bc1-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="50bc1-106">取得或設定 NuGet 組態值。</span><span class="sxs-lookup"><span data-stu-id="50bc1-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="50bc1-107">對於其他使用方式，請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="50bc1-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="50bc1-108">如需允許的索引鍵名稱的詳細資訊，請參閱[NuGet 組態檔參考](../Schema/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="50bc1-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="50bc1-109">使用量</span><span class="sxs-lookup"><span data-stu-id="50bc1-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="50bc1-110">其中`<name>`和`<value>`指定要在組態中設定的索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="50bc1-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="50bc1-111">您可以視需要指定多組。</span><span class="sxs-lookup"><span data-stu-id="50bc1-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="50bc1-112">若要移除的值，指定名稱和`=`號但沒有值。</span><span class="sxs-lookup"><span data-stu-id="50bc1-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="50bc1-113">如需允許的索引鍵名稱，請參閱[NuGet 組態檔參考](../Schema/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="50bc1-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="50bc1-114">在 NuGet 3.4 +`<value>`可以使用[環境變數](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="50bc1-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="50bc1-115">選項</span><span class="sxs-lookup"><span data-stu-id="50bc1-115">Options</span></span>

| <span data-ttu-id="50bc1-116">選項</span><span class="sxs-lookup"><span data-stu-id="50bc1-116">Option</span></span> | <span data-ttu-id="50bc1-117">描述</span><span class="sxs-lookup"><span data-stu-id="50bc1-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50bc1-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="50bc1-118">AsPath</span></span> | <span data-ttu-id="50bc1-119">傳回組態值做為路徑，會忽略時`-Set`用。</span><span class="sxs-lookup"><span data-stu-id="50bc1-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="50bc1-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="50bc1-120">ConfigFile</span></span> | <span data-ttu-id="50bc1-121">*（2.5 +)* NuGet 組態檔來修改。</span><span class="sxs-lookup"><span data-stu-id="50bc1-121">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="50bc1-122">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="50bc1-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="50bc1-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="50bc1-123">ForceEnglishOutput</span></span> | <span data-ttu-id="50bc1-124">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="50bc1-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="50bc1-125">說明</span><span class="sxs-lookup"><span data-stu-id="50bc1-125">Help</span></span> | <span data-ttu-id="50bc1-126">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="50bc1-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="50bc1-127">非互動式</span><span class="sxs-lookup"><span data-stu-id="50bc1-127">NonInteractive</span></span> | <span data-ttu-id="50bc1-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="50bc1-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="50bc1-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="50bc1-129">Verbosity</span></span> | <span data-ttu-id="50bc1-130">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="50bc1-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="50bc1-131">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="50bc1-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="50bc1-132">範例</span><span class="sxs-lookup"><span data-stu-id="50bc1-132">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
