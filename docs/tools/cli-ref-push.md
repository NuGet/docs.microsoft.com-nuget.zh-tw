---
title: NuGet CLI 推入命令
description: Nuget.exe 推送命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817187"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="f9183-103">推播命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f9183-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="f9183-104">**適用於：** 封裝發行&bullet;**支援的版本：** 所有; 所需的 nuget.org 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="f9183-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="f9183-105">若要推入至 nuget.org 的封裝，您必須使用 nuget.exe v4.1.0 +，它會實作所需[NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="f9183-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="f9183-106">將封裝的封裝來源以推入，並將其發佈。</span><span class="sxs-lookup"><span data-stu-id="f9183-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="f9183-107">NuGet 的預設組態透過載入`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然後載入任何`Nuget.Config`或`.nuget\Nuget.Config`檔案從磁碟機的根目錄開始和結束目前的目錄中 (請參閱[設定NuGet 行為](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="f9183-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="f9183-108">使用量</span><span class="sxs-lookup"><span data-stu-id="f9183-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="f9183-109">其中`<packagePath>`識別要推入至伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="f9183-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="f9183-110">選項</span><span class="sxs-lookup"><span data-stu-id="f9183-110">Options</span></span>

| <span data-ttu-id="f9183-111">選項</span><span class="sxs-lookup"><span data-stu-id="f9183-111">Option</span></span> | <span data-ttu-id="f9183-112">描述</span><span class="sxs-lookup"><span data-stu-id="f9183-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9183-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="f9183-113">ApiKey</span></span> | <span data-ttu-id="f9183-114">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f9183-114">The API key for the target repository.</span></span> <span data-ttu-id="f9183-115">如果不存在，則會使用組態檔中所指定。</span><span class="sxs-lookup"><span data-stu-id="f9183-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f9183-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f9183-116">ConfigFile</span></span> | <span data-ttu-id="f9183-117">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="f9183-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f9183-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="f9183-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f9183-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="f9183-119">DisableBuffering</span></span> | <span data-ttu-id="f9183-120">停用緩衝以減少記憶體使用方式的推入至 http （s） 伺服器時。</span><span class="sxs-lookup"><span data-stu-id="f9183-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="f9183-121">注意： 使用此選項時，整合式的 Windows 驗證可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="f9183-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="f9183-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f9183-122">ForceEnglishOutput</span></span> | <span data-ttu-id="f9183-123">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="f9183-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f9183-124">說明</span><span class="sxs-lookup"><span data-stu-id="f9183-124">Help</span></span> | <span data-ttu-id="f9183-125">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="f9183-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="f9183-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f9183-126">NonInteractive</span></span> | <span data-ttu-id="f9183-127">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="f9183-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f9183-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="f9183-128">NoSymbols</span></span> | <span data-ttu-id="f9183-129">*（3.5 +)* 如果符號封裝存在，它將不會發送至符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="f9183-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="f9183-130">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="f9183-130">Source</span></span> | <span data-ttu-id="f9183-131">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="f9183-131">Specifies the server URL.</span></span> <span data-ttu-id="f9183-132">NuGet 識別的 UNC 或本機資料夾的來源，並只會複製檔案而不是將它使用 HTTP 推送。</span><span class="sxs-lookup"><span data-stu-id="f9183-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="f9183-133">此外，從 NuGet 3.4.2 開始，這是必要參數除非`NuGet.Config`檔案會指定*DefaultPushSource*值 (請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="f9183-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="f9183-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="f9183-134">SymbolSource</span></span> | <span data-ttu-id="f9183-135">*（3.5 +)* 指定符號伺服器 URL，當 nuget.smbsrc.net 推入至 nuget.org 時，會使用</span><span class="sxs-lookup"><span data-stu-id="f9183-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="f9183-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="f9183-136">SymbolApiKey</span></span> | <span data-ttu-id="f9183-137">*（3.5 +)* 指定 URL 中指定的 API 金鑰`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="f9183-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="f9183-138">等候逾時</span><span class="sxs-lookup"><span data-stu-id="f9183-138">Timeout</span></span> | <span data-ttu-id="f9183-139">指定在逾時，以秒為單位，可用於推入到伺服器。</span><span class="sxs-lookup"><span data-stu-id="f9183-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="f9183-140">預設值是 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="f9183-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="f9183-141">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f9183-141">Verbosity</span></span> | <span data-ttu-id="f9183-142">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="f9183-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f9183-143">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f9183-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f9183-144">範例</span><span class="sxs-lookup"><span data-stu-id="f9183-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
