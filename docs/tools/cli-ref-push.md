---
title: NuGet CLI 推送命令
description: Nuget.exe 推送命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974995"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="3bf20-103">推送命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3bf20-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="3bf20-104">**適用於：** 封裝發行&bullet;**支援的版本：** 所有; 所需的 nuget.org 4.1.0 +</span><span class="sxs-lookup"><span data-stu-id="3bf20-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="3bf20-105">若要將套件推送至 nuget.org，您必須使用 nuget.exe 4.1.0 版 + 中，它會實作所需[NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="3bf20-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="3bf20-106">將套件推送至套件來源，並將其發佈。</span><span class="sxs-lookup"><span data-stu-id="3bf20-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="3bf20-107">NuGet 的預設組態的取得方式載入`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然後載入任何`Nuget.Config`或是`.nuget\Nuget.Config`檔案從磁碟機的根目錄開始和結束目前的目錄中 (請參閱[設定NuGet 行為](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="3bf20-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="3bf20-108">使用量</span><span class="sxs-lookup"><span data-stu-id="3bf20-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="3bf20-109">其中`<packagePath>`識別要推送至伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="3bf20-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="3bf20-110">選項</span><span class="sxs-lookup"><span data-stu-id="3bf20-110">Options</span></span>

| <span data-ttu-id="3bf20-111">選項</span><span class="sxs-lookup"><span data-stu-id="3bf20-111">Option</span></span> | <span data-ttu-id="3bf20-112">描述</span><span class="sxs-lookup"><span data-stu-id="3bf20-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3bf20-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3bf20-113">ApiKey</span></span> | <span data-ttu-id="3bf20-114">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="3bf20-114">The API key for the target repository.</span></span> <span data-ttu-id="3bf20-115">如果不存在，則會使用組態檔中所指定。</span><span class="sxs-lookup"><span data-stu-id="3bf20-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3bf20-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3bf20-116">ConfigFile</span></span> | <span data-ttu-id="3bf20-117">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="3bf20-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3bf20-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="3bf20-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3bf20-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="3bf20-119">DisableBuffering</span></span> | <span data-ttu-id="3bf20-120">停用緩衝處理時將推送至 http （s） 伺服器，以減少記憶體使用方式。</span><span class="sxs-lookup"><span data-stu-id="3bf20-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="3bf20-121">注意： 使用此選項時，整合式的 Windows 驗證可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="3bf20-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="3bf20-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3bf20-122">ForceEnglishOutput</span></span> | <span data-ttu-id="3bf20-123">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="3bf20-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3bf20-124">Help</span><span class="sxs-lookup"><span data-stu-id="3bf20-124">Help</span></span> | <span data-ttu-id="3bf20-125">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bf20-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="3bf20-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3bf20-126">NonInteractive</span></span> | <span data-ttu-id="3bf20-127">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="3bf20-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3bf20-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="3bf20-128">NoSymbols</span></span> | <span data-ttu-id="3bf20-129">*（3.5 +)* 有符號套件時，它將不會推送至符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bf20-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="3bf20-130">Source</span><span class="sxs-lookup"><span data-stu-id="3bf20-130">Source</span></span> | <span data-ttu-id="3bf20-131">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="3bf20-131">Specifies the server URL.</span></span> <span data-ttu-id="3bf20-132">NuGet 會識別的 UNC 或本機資料夾的來源，並只會複製檔案而非發送它使用 HTTP。</span><span class="sxs-lookup"><span data-stu-id="3bf20-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="3bf20-133">此外，從開始 NuGet 3.4.2，這是必要參數除非`NuGet.Config`檔案會指定*DefaultPushSource*值 (請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="3bf20-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="3bf20-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="3bf20-134">SkipDuplicate</span></span> | <span data-ttu-id="3bf20-135">如果套件和版本已經存在，略過它並繼續進行下一個封裝，在推播，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="3bf20-135">If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="3bf20-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="3bf20-136">SymbolSource</span></span> | <span data-ttu-id="3bf20-137">*（3.5 +)* 指定符號伺服器 URL，當 nuget.smbsrc.net 推送至 nuget.org 時，會使用</span><span class="sxs-lookup"><span data-stu-id="3bf20-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="3bf20-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="3bf20-138">SymbolApiKey</span></span> | <span data-ttu-id="3bf20-139">*（3.5 +)* 指定 URL 中指定的 API 金鑰`-SymbolSource`。</span><span class="sxs-lookup"><span data-stu-id="3bf20-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="3bf20-140">逾時</span><span class="sxs-lookup"><span data-stu-id="3bf20-140">Timeout</span></span> | <span data-ttu-id="3bf20-141">指定的逾時 （秒），推送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bf20-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3bf20-142">預設值為 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="3bf20-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3bf20-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3bf20-143">Verbosity</span></span> | <span data-ttu-id="3bf20-144">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="3bf20-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3bf20-145">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3bf20-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3bf20-146">範例</span><span class="sxs-lookup"><span data-stu-id="3bf20-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
