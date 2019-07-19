---
title: NuGet CLI push 命令
description: Nuget.exe push 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327625"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="02d63-103">push 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="02d63-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="02d63-104">**適用于:** 套件發佈&bullet; **支援的版本:** 全部; 4.1.0 + nuget.org 的必要項</span><span class="sxs-lookup"><span data-stu-id="02d63-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="02d63-105">若要將套件推送至 nuget.org, 您必須使用 nuget.exe v 4.1.0 +, 其會執行所需的[nuget 通訊協定](../../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="02d63-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="02d63-106">將套件推送至套件來源併發布。</span><span class="sxs-lookup"><span data-stu-id="02d63-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="02d63-107">NuGet 的預設設定是藉由載入`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 來取得, 然後`Nuget.Config`從`.nuget\Nuget.Config`磁片磁碟機根目錄開始載入任何或檔案, 並在目前的目錄中結束 (請參閱[通用 NuGet)](../../consume-packages/configuring-nuget-behavior.md)設定)</span><span class="sxs-lookup"><span data-stu-id="02d63-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="02d63-108">使用量</span><span class="sxs-lookup"><span data-stu-id="02d63-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="02d63-109">其中`<packagePath>`識別要推送至伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="02d63-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="02d63-110">選項</span><span class="sxs-lookup"><span data-stu-id="02d63-110">Options</span></span>

| <span data-ttu-id="02d63-111">選項</span><span class="sxs-lookup"><span data-stu-id="02d63-111">Option</span></span> | <span data-ttu-id="02d63-112">說明</span><span class="sxs-lookup"><span data-stu-id="02d63-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02d63-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="02d63-113">ApiKey</span></span> | <span data-ttu-id="02d63-114">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02d63-114">The API key for the target repository.</span></span> <span data-ttu-id="02d63-115">如果不存在, 則會使用設定檔中指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="02d63-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="02d63-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="02d63-116">ConfigFile</span></span> | <span data-ttu-id="02d63-117">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="02d63-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="02d63-118">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="02d63-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="02d63-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="02d63-119">DisableBuffering</span></span> | <span data-ttu-id="02d63-120">推送至 HTTP (s) 伺服器時停用緩衝處理以減少記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="02d63-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="02d63-121">注意: 使用此選項時, 整合式 Windows 驗證可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="02d63-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="02d63-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="02d63-122">ForceEnglishOutput</span></span> | <span data-ttu-id="02d63-123">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="02d63-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="02d63-124">Help</span><span class="sxs-lookup"><span data-stu-id="02d63-124">Help</span></span> | <span data-ttu-id="02d63-125">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="02d63-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="02d63-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="02d63-126">NonInteractive</span></span> | <span data-ttu-id="02d63-127">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="02d63-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="02d63-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="02d63-128">NoSymbols</span></span> | <span data-ttu-id="02d63-129">*(3.5 +)* 如果符號封裝存在, 則不會將它推送至符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="02d63-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="02d63-130">Source</span><span class="sxs-lookup"><span data-stu-id="02d63-130">Source</span></span> | <span data-ttu-id="02d63-131">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="02d63-131">Specifies the server URL.</span></span> <span data-ttu-id="02d63-132">NuGet 會識別 UNC 或本機資料夾來源, 並直接在該處複製檔案, 而不是使用 HTTP 推送該檔案。</span><span class="sxs-lookup"><span data-stu-id="02d63-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="02d63-133">此外, 從 NuGet 3.4.2 開始, 除非檔案指定*DefaultPushSource*值, 否則`NuGet.Config`這是必要參數 (請參閱設定[NuGet 行為](../../consume-packages/configuring-nuget-behavior.md))。</span><span class="sxs-lookup"><span data-stu-id="02d63-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="02d63-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="02d63-134">SkipDuplicate</span></span> | <span data-ttu-id="02d63-135">*(5.1 +)* 如果套件和版本已存在, 請略過它, 並繼續推送中的下一個套件 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="02d63-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="02d63-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="02d63-136">SymbolSource</span></span> | <span data-ttu-id="02d63-137">*(3.5 +)* 指定符號伺服器 URL;推送至 nuget.org 時, 會使用 nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="02d63-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="02d63-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="02d63-138">SymbolApiKey</span></span> | <span data-ttu-id="02d63-139">*(3.5 +)* 針對中`-SymbolSource`指定的 URL 指定 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02d63-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="02d63-140">逾時</span><span class="sxs-lookup"><span data-stu-id="02d63-140">Timeout</span></span> | <span data-ttu-id="02d63-141">指定推送至伺服器的超時時間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="02d63-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="02d63-142">預設值為300秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="02d63-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="02d63-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="02d63-143">Verbosity</span></span> | <span data-ttu-id="02d63-144">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="02d63-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="02d63-145">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="02d63-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="02d63-146">範例</span><span class="sxs-lookup"><span data-stu-id="02d63-146">Examples</span></span>

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
