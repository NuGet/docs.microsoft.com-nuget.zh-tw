---
title: NuGet CLI push 命令
description: nuget.exe push 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622841"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="cad25-103"> (NuGet CLI 的推送命令) </span><span class="sxs-lookup"><span data-stu-id="cad25-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="cad25-104">**適用于：** 套件發行 &bullet; **支援的版本：** 全部; 4.1.0 + 需要 nuget.org</span><span class="sxs-lookup"><span data-stu-id="cad25-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="cad25-105">若要將套件推送至 nuget.org，您必須使用 nuget.exe v 4.1.0 +，它會執行所需的 [nuget 通訊協定](../../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="cad25-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="cad25-106">將套件推送至封裝來源併發布。</span><span class="sxs-lookup"><span data-stu-id="cad25-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="cad25-107">NuGet 的預設設定是藉由載入 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ，然後 `Nuget.Config` `.nuget\Nuget.Config` 從磁片磁碟機的根目錄開始載入任何檔案，並在目前的目錄中結束 (查看 [常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md) 設定) </span><span class="sxs-lookup"><span data-stu-id="cad25-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="cad25-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="cad25-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="cad25-109">，其中會 `<packagePath>` 識別要推送至伺服器的封裝。</span><span class="sxs-lookup"><span data-stu-id="cad25-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="cad25-110">選項。</span><span class="sxs-lookup"><span data-stu-id="cad25-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="cad25-111">目標儲存機制的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="cad25-111">The API key for the target repository.</span></span> <span data-ttu-id="cad25-112">如果不存在，則會使用設定檔中指定的。</span><span class="sxs-lookup"><span data-stu-id="cad25-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cad25-113">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="cad25-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cad25-114">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="cad25-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="cad25-115">推送至 HTTP (s) server 時，會停用緩衝處理以減少記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="cad25-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="cad25-116">注意：使用此選項時，整合式 Windows 驗證可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="cad25-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cad25-117">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="cad25-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cad25-118">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="cad25-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cad25-119">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="cad25-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="cad25-120">不會附加 `api/v2/packages` 至來源 URL。</span><span class="sxs-lookup"><span data-stu-id="cad25-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="cad25-121">\* (3.5 +) \* 如果符號封裝存在，則不會將其推送至符號伺服器。</span><span class="sxs-lookup"><span data-stu-id="cad25-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="cad25-122">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="cad25-122">Specifies the server URL.</span></span> <span data-ttu-id="cad25-123">NuGet 會識別 UNC 或本機資料夾來源，只複製檔案，而不是使用 HTTP 推送。</span><span class="sxs-lookup"><span data-stu-id="cad25-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="cad25-124">此外，從 NuGet 3.4.2 開始，除非檔案 `NuGet.Config` 指定 *DefaultPushSource* 值 (請參閱設定 [nuget 行為](../../consume-packages/configuring-nuget-behavior.md)) ，否則此為必要參數。</span><span class="sxs-lookup"><span data-stu-id="cad25-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="cad25-125">\* (5.1 +) \* 如果套件和版本已經存在，請略過它，然後繼續進行推送中的下一個套件（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="cad25-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="cad25-126">\* (3.5 +) \* 指定符號伺服器 URL;nuget.smbsrc.net 會在推送至 nuget.org 時使用</span><span class="sxs-lookup"><span data-stu-id="cad25-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="cad25-127">\* (3.5 +) \* 指定中指定之 URL 的 API 金鑰 `-SymbolSource` 。</span><span class="sxs-lookup"><span data-stu-id="cad25-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="cad25-128">指定推送至伺服器的超時時間（以秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="cad25-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cad25-129">預設值是 300 秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="cad25-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cad25-130">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="cad25-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="cad25-131">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cad25-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cad25-132">範例</span><span class="sxs-lookup"><span data-stu-id="cad25-132">Examples</span></span>

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
