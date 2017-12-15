---
title: "NuGet CLI 發送命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Nuget.exe 推送命令參考"
keywords: "nuget 推入參考，推入命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="4bbdf-104">推播命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4bbdf-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="4bbdf-105">**適用於：**封裝發行&bullet;**支援的版本：**所有; 所需的 nuget.org 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="4bbdf-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="4bbdf-106">若要推入至 nuget.org 的封裝，您必須使用 nuget.exe v4.1.0 +，它會實作所需[NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="4bbdf-107">將封裝的封裝來源以推入，並將其發佈。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="4bbdf-108">NuGet 的預設組態透過載入`%AppData%\NuGet\NuGet.Config`，然後載入任何`Nuget.Config`或`.nuget\Nuget.Config`檔案從磁碟機的根目錄開始和結束目前的目錄中 (請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="4bbdf-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="4bbdf-109">使用方式</span><span class="sxs-lookup"><span data-stu-id="4bbdf-109">Usage</span></span>

```
nuget push <packagePath> [options]
```

<span data-ttu-id="4bbdf-110">其中`<packagePath>`識別要推入至伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="4bbdf-111">選項</span><span class="sxs-lookup"><span data-stu-id="4bbdf-111">Options</span></span>

| <span data-ttu-id="4bbdf-112">選項</span><span class="sxs-lookup"><span data-stu-id="4bbdf-112">Option</span></span> | <span data-ttu-id="4bbdf-113">說明</span><span class="sxs-lookup"><span data-stu-id="4bbdf-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4bbdf-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="4bbdf-114">ApiKey</span></span> | <span data-ttu-id="4bbdf-115">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-115">The API key for the target repository.</span></span> <span data-ttu-id="4bbdf-116">如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4bbdf-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4bbdf-117">ConfigFile</span></span> | <span data-ttu-id="4bbdf-118">*（2.5 +)* NuGet 組態檔來套用。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-118">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="4bbdf-119">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4bbdf-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="4bbdf-120">DisableBuffering</span></span> | <span data-ttu-id="4bbdf-121">停用緩衝以減少記憶體使用方式的推入至 http （s） 伺服器時。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="4bbdf-122">注意： 使用此選項時，整合式的 Windows 驗證可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="4bbdf-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4bbdf-123">ForceEnglishOutput</span></span> | <span data-ttu-id="4bbdf-124">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4bbdf-125">說明</span><span class="sxs-lookup"><span data-stu-id="4bbdf-125">Help</span></span> | <span data-ttu-id="4bbdf-126">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="4bbdf-127">非互動式</span><span class="sxs-lookup"><span data-stu-id="4bbdf-127">NonInteractive</span></span> | <span data-ttu-id="4bbdf-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4bbdf-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="4bbdf-129">NoSymbols</span></span> | <span data-ttu-id="4bbdf-130">*（3.5 +)*如果符號封裝存在，它將不會發送至符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="4bbdf-131">來源</span><span class="sxs-lookup"><span data-stu-id="4bbdf-131">Source</span></span> | <span data-ttu-id="4bbdf-132">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-132">Specifies the server URL.</span></span> <span data-ttu-id="4bbdf-133">隨 NuGet 2.5 +，NuGet 會識別資料的 UNC 或本機資料夾的來源，並直接複製檔案而不是將它使用 HTTP 推送。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-133">With NuGet 2.5+, NuGet will identify a UNC or local folder source and simply copy the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="4bbdf-134">此外，從 NuGet 3.4.2 開始，這是必要參數除非`NuGet.Config`檔案會指定*DefaultPushSource*值 (請參閱[設定 NuGet 行為](../Consume-Packages/Configuring-NuGet-Behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="4bbdf-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="4bbdf-135">SymbolSource</span></span> | <span data-ttu-id="4bbdf-136">*（3.5 +)*指定符號伺服器 URL，當 nuget.smbsrc.net 推入至 nuget.org 時，會使用</span><span class="sxs-lookup"><span data-stu-id="4bbdf-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="4bbdf-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="4bbdf-137">SymbolApiKey</span></span> | <span data-ttu-id="4bbdf-138">*（3.5 +)*指定 URL 中指定的 API 金鑰`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="4bbdf-139">等候逾時</span><span class="sxs-lookup"><span data-stu-id="4bbdf-139">Timeout</span></span> | <span data-ttu-id="4bbdf-140">指定在逾時，以秒為單位，可用於推入到伺服器。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="4bbdf-141">預設值是 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="4bbdf-142">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4bbdf-142">Verbosity</span></span> | <span data-ttu-id="4bbdf-143">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="4bbdf-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="4bbdf-144">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4bbdf-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4bbdf-145">範例</span><span class="sxs-lookup"><span data-stu-id="4bbdf-145">Examples</span></span>

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
