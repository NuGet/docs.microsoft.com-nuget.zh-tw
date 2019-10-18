---
title: NuGet 跨平臺外掛程式
description: 適用于 Nuget.exe、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平臺外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380505"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="a6151-103">NuGet 跨平臺外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="a6151-104">在 NuGet 4.8 + 中，已新增跨平臺外掛程式的支援。</span><span class="sxs-lookup"><span data-stu-id="a6151-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="a6151-105">這是透過建立新的外掛程式擴充性模型來達成，必須符合一組嚴格的運算規則。</span><span class="sxs-lookup"><span data-stu-id="a6151-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="a6151-106">外掛程式是獨立的可執行檔（在 .NET Core 世界中為 runnables），NuGet 用戶端會在個別的進程中啟動。</span><span class="sxs-lookup"><span data-stu-id="a6151-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="a6151-107">這是真正的寫入一次，可在任何地方執行外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="a6151-108">它會與所有 NuGet 用戶端工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a6151-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="a6151-109">外掛程式可以是 .NET Framework （Nuget.exe、Msbuild.exe 和 Visual Studio）或 .NET Core （dotnet .exe）。</span><span class="sxs-lookup"><span data-stu-id="a6151-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="a6151-110">NuGet 用戶端和外掛程式之間已建立版本的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a6151-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="a6151-111">在啟動信號交換期間，2個進程會協調通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="a6151-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="a6151-112">為了涵蓋所有 NuGet 用戶端工具案例，其中一項需要 .NET Framework 和 .NET Core 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="a6151-113">以下說明外掛程式的用戶端/架構組合。</span><span class="sxs-lookup"><span data-stu-id="a6151-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="a6151-114">用戶端工具</span><span class="sxs-lookup"><span data-stu-id="a6151-114">Client tool</span></span>  | <span data-ttu-id="a6151-115">架構</span><span class="sxs-lookup"><span data-stu-id="a6151-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="a6151-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6151-116">Visual Studio</span></span> | <span data-ttu-id="a6151-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6151-117">.NET Framework</span></span> |
| <span data-ttu-id="a6151-118">dotnet .exe</span><span class="sxs-lookup"><span data-stu-id="a6151-118">dotnet.exe</span></span> | <span data-ttu-id="a6151-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a6151-119">.NET Core</span></span> |
| <span data-ttu-id="a6151-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a6151-120">NuGet.exe</span></span> | <span data-ttu-id="a6151-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6151-121">.NET Framework</span></span> |
| <span data-ttu-id="a6151-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="a6151-122">MSBuild.exe</span></span> | <span data-ttu-id="a6151-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6151-123">.NET Framework</span></span> |
| <span data-ttu-id="a6151-124">Mono 上的 Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a6151-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="a6151-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6151-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="a6151-126">運作方式</span><span class="sxs-lookup"><span data-stu-id="a6151-126">How does it work</span></span>

<span data-ttu-id="a6151-127">高階工作流程可以描述如下：</span><span class="sxs-lookup"><span data-stu-id="a6151-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="a6151-128">NuGet 會探索可用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="a6151-129">當適用時，NuGet 會依優先順序逐一查看外掛程式，然後逐一啟動。</span><span class="sxs-lookup"><span data-stu-id="a6151-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="a6151-130">NuGet 會使用可服務要求的第一個外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="a6151-131">外掛程式將會在不再需要時關閉。</span><span class="sxs-lookup"><span data-stu-id="a6151-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="a6151-132">一般外掛程式需求</span><span class="sxs-lookup"><span data-stu-id="a6151-132">General plugin requirements</span></span>

<span data-ttu-id="a6151-133">目前的通訊協定版本是*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="a6151-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="a6151-134">在此版本底下，需求如下：</span><span class="sxs-lookup"><span data-stu-id="a6151-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="a6151-135">擁有將在 Windows 和 Mono 上執行的有效、受信任的 Authenticode 簽章元件。</span><span class="sxs-lookup"><span data-stu-id="a6151-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="a6151-136">尚未在 Linux 和 Mac 上執行元件的特殊信任需求。</span><span class="sxs-lookup"><span data-stu-id="a6151-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="a6151-137">相關問題</span><span class="sxs-lookup"><span data-stu-id="a6151-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="a6151-138">支援 NuGet 用戶端工具的目前安全性內容下的無狀態啟動。</span><span class="sxs-lookup"><span data-stu-id="a6151-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="a6151-139">例如，NuGet 用戶端工具不會在稍後所述的外掛程式通訊協定以外執行提高許可權或額外的初始化。</span><span class="sxs-lookup"><span data-stu-id="a6151-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="a6151-140">除非明確指定，否則不是互動式的。</span><span class="sxs-lookup"><span data-stu-id="a6151-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="a6151-141">遵循已協商的外掛程式通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="a6151-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="a6151-142">在合理的時間週期內回應所有要求。</span><span class="sxs-lookup"><span data-stu-id="a6151-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="a6151-143">接受任何進行中作業的取消要求。</span><span class="sxs-lookup"><span data-stu-id="a6151-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="a6151-144">下列規格將更詳細地說明技術規格：</span><span class="sxs-lookup"><span data-stu-id="a6151-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="a6151-145">NuGet 套件下載外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="a6151-146">NuGet 跨平臺驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="a6151-147">用戶端-外掛程式的互動</span><span class="sxs-lookup"><span data-stu-id="a6151-147">Client - Plugin interaction</span></span>

<span data-ttu-id="a6151-148">NuGet 用戶端工具和外掛程式會透過標準資料流程（stdin、stdout、stderr）與 JSON 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a6151-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="a6151-149">所有資料都必須以 UTF-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="a6151-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="a6151-150">外掛程式會以引數 "-外掛程式" 啟動。</span><span class="sxs-lookup"><span data-stu-id="a6151-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="a6151-151">如果使用者直接啟動沒有此引數的外掛程式可執行檔，則外掛程式會提供資訊性訊息，而不是等候通訊協定交握。</span><span class="sxs-lookup"><span data-stu-id="a6151-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="a6151-152">通訊協定交握時間為5秒。</span><span class="sxs-lookup"><span data-stu-id="a6151-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="a6151-153">外掛程式應該盡可能以最少的數量完成中的設定。</span><span class="sxs-lookup"><span data-stu-id="a6151-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="a6151-154">NuGet 用戶端工具會藉由傳遞 NuGet 來源的服務索引來查詢外掛程式支援的作業。</span><span class="sxs-lookup"><span data-stu-id="a6151-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="a6151-155">外掛程式可以使用服務索引來檢查支援的服務類型是否存在。</span><span class="sxs-lookup"><span data-stu-id="a6151-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="a6151-156">NuGet 用戶端工具和外掛程式之間的通訊是雙向的。</span><span class="sxs-lookup"><span data-stu-id="a6151-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="a6151-157">每個要求的超時時間為5秒。</span><span class="sxs-lookup"><span data-stu-id="a6151-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="a6151-158">如果作業應花費較長的時間，則個別的進程應傳送進度訊息，以防止要求超時。在閒置1分鐘後，外掛程式會被視為閒置並關閉。</span><span class="sxs-lookup"><span data-stu-id="a6151-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="a6151-159">外掛程式安裝與探索</span><span class="sxs-lookup"><span data-stu-id="a6151-159">Plugin installation and discovery</span></span>

<span data-ttu-id="a6151-160">這些外掛程式會透過以慣例為基礎的目錄結構來探索。</span><span class="sxs-lookup"><span data-stu-id="a6151-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="a6151-161">CI/CD 案例和 power 使用者可以使用環境變數來覆寫行為。</span><span class="sxs-lookup"><span data-stu-id="a6151-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="a6151-162">使用環境變數時，只允許絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="a6151-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="a6151-163">請注意，`NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 僅適用于 5.3 + 版的 NuGet 工具和更新版本。</span><span class="sxs-lookup"><span data-stu-id="a6151-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="a6151-164">`NUGET_NETFX_PLUGIN_PATHS`-定義 .NET Framework 為基礎的工具（Nuget.exe/Msbuild.exe/Visual Studio）將使用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="a6151-165">優先于 `NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="a6151-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="a6151-166">（僅限 NuGet 5.3 版 +）</span><span class="sxs-lookup"><span data-stu-id="a6151-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="a6151-167">`NUGET_NETCORE_PLUGIN_PATHS`-定義將由 .NET Core 工具（dotnet）使用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="a6151-168">優先于 `NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="a6151-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="a6151-169">（僅限 NuGet 5.3 版 +）</span><span class="sxs-lookup"><span data-stu-id="a6151-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="a6151-170">`NUGET_PLUGIN_PATHS`-定義將用於該 NuGet 進程的外掛程式，並保留優先順序。</span><span class="sxs-lookup"><span data-stu-id="a6151-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="a6151-171">如果設定此環境變數，則會覆寫以慣例為基礎的探索。</span><span class="sxs-lookup"><span data-stu-id="a6151-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="a6151-172">如果指定了其中一個架構特定的變數，則會忽略。</span><span class="sxs-lookup"><span data-stu-id="a6151-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="a6151-173">使用者位置，`%UserProfile%/.nuget/plugins` 中的 NuGet 首頁位置。</span><span class="sxs-lookup"><span data-stu-id="a6151-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="a6151-174">無法覆寫此位置。</span><span class="sxs-lookup"><span data-stu-id="a6151-174">This location cannot be overriden.</span></span> <span data-ttu-id="a6151-175">.NET Core 和 .NET Framework 外掛程式將會使用不同的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a6151-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="a6151-176">架構</span><span class="sxs-lookup"><span data-stu-id="a6151-176">Framework</span></span> | <span data-ttu-id="a6151-177">根探索位置</span><span class="sxs-lookup"><span data-stu-id="a6151-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="a6151-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a6151-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="a6151-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6151-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="a6151-180">每個外掛程式都應該安裝在自己的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a6151-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="a6151-181">外掛程式進入點會是已安裝之資料夾的名稱，以及適用于 .NET Core 的 .dll 副檔名，而 .NET Framework 的 .exe 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="a6151-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="a6151-182">目前沒有安裝外掛程式的使用者案例。</span><span class="sxs-lookup"><span data-stu-id="a6151-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="a6151-183">就像是將所需的檔案移到預先決定的位置一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="a6151-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="a6151-184">支援的作業</span><span class="sxs-lookup"><span data-stu-id="a6151-184">Supported operations</span></span>

<span data-ttu-id="a6151-185">新的外掛程式通訊協定支援兩個作業。</span><span class="sxs-lookup"><span data-stu-id="a6151-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="a6151-186">作業名稱</span><span class="sxs-lookup"><span data-stu-id="a6151-186">Operation name</span></span> | <span data-ttu-id="a6151-187">最低通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="a6151-187">Minimum protocol version</span></span> | <span data-ttu-id="a6151-188">最低 NuGet 用戶端版本</span><span class="sxs-lookup"><span data-stu-id="a6151-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="a6151-189">下載套件</span><span class="sxs-lookup"><span data-stu-id="a6151-189">Download Package</span></span> | <span data-ttu-id="a6151-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a6151-190">1.0.0</span></span> | <span data-ttu-id="a6151-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="a6151-191">4.3.0</span></span> |
| [<span data-ttu-id="a6151-192">驗證</span><span class="sxs-lookup"><span data-stu-id="a6151-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="a6151-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="a6151-193">2.0.0</span></span> | <span data-ttu-id="a6151-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="a6151-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="a6151-195">在正確的執行時間下執行外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="a6151-196">在 dotnet 的 NuGet 案例中，外掛程式必須能夠在 dotnet 的特定執行時間下執行。</span><span class="sxs-lookup"><span data-stu-id="a6151-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="a6151-197">它位於外掛程式提供者和取用者上，以確保使用相容的 dotnet .exe/外掛程式組合。</span><span class="sxs-lookup"><span data-stu-id="a6151-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="a6151-198">使用者位置外掛程式可能會發生問題，例如，2.0 執行時間下的 dotnet 嘗試使用針對2.1 執行時間所撰寫的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="a6151-199">功能快取</span><span class="sxs-lookup"><span data-stu-id="a6151-199">Capabilities caching</span></span>

<span data-ttu-id="a6151-200">外掛程式的安全性驗證和具現化成本很高。</span><span class="sxs-lookup"><span data-stu-id="a6151-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="a6151-201">下載作業的執行頻率比驗證作業更頻繁，但平均 NuGet 使用者只可能有驗證外掛程式。</span><span class="sxs-lookup"><span data-stu-id="a6151-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="a6151-202">為了改善此體驗，NuGet 會快取指定要求的作業宣告。</span><span class="sxs-lookup"><span data-stu-id="a6151-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="a6151-203">此快取是每個外掛程式，其中外掛程式的索引鍵為外掛程式路徑，而此功能快取的到期時間為30天。</span><span class="sxs-lookup"><span data-stu-id="a6151-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="a6151-204">快取位於 `%LocalAppData%/NuGet/plugins-cache` 中，並以環境變數 `NUGET_PLUGINS_CACHE_PATH` 覆寫。</span><span class="sxs-lookup"><span data-stu-id="a6151-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="a6151-205">若要清除[此快](../../consume-packages/managing-the-global-packages-and-cache-folders.md)取，可以使用 `plugins-cache` 選項來執行 [區域變數] 命令。</span><span class="sxs-lookup"><span data-stu-id="a6151-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="a6151-206">[@No__t_0 區域變數] 選項現在也會刪除外掛程式快取。</span><span class="sxs-lookup"><span data-stu-id="a6151-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="a6151-207">通訊協定訊息索引</span><span class="sxs-lookup"><span data-stu-id="a6151-207">Protocol messages index</span></span>

<span data-ttu-id="a6151-208">通訊協定*1.0.0*版訊息：</span><span class="sxs-lookup"><span data-stu-id="a6151-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="a6151-209">關閉</span><span class="sxs-lookup"><span data-stu-id="a6151-209">Close</span></span>
    * <span data-ttu-id="a6151-210">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-211">要求不會包含任何承載</span><span class="sxs-lookup"><span data-stu-id="a6151-211">The request will contain no payload</span></span>
    * <span data-ttu-id="a6151-212">不需要回應。</span><span class="sxs-lookup"><span data-stu-id="a6151-212">No response is expected.</span></span>  <span data-ttu-id="a6151-213">適當的回應是讓外掛程式進程立即結束。</span><span class="sxs-lookup"><span data-stu-id="a6151-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="a6151-214">複製封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="a6151-214">Copy files in package</span></span>
    * <span data-ttu-id="a6151-215">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-216">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-216">The request will contain:</span></span>
        * <span data-ttu-id="a6151-217">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="a6151-217">the package ID and version</span></span>
        * <span data-ttu-id="a6151-218">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-218">the package source repository location</span></span>
        * <span data-ttu-id="a6151-219">目的地目錄路徑</span><span class="sxs-lookup"><span data-stu-id="a6151-219">destination directory path</span></span>
        * <span data-ttu-id="a6151-220">封裝中要複製到目的地目錄路徑之檔案的可列舉</span><span class="sxs-lookup"><span data-stu-id="a6151-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="a6151-221">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-221">A response will contain:</span></span>
        * <span data-ttu-id="a6151-222">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-223">如果作業成功，則為目的地目錄中複製之檔案的完整路徑列舉</span><span class="sxs-lookup"><span data-stu-id="a6151-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="a6151-224">複製套件檔案（. nupkg）</span><span class="sxs-lookup"><span data-stu-id="a6151-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="a6151-225">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-226">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-226">The request will contain:</span></span>
        * <span data-ttu-id="a6151-227">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="a6151-227">the package ID and version</span></span>
        * <span data-ttu-id="a6151-228">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-228">the package source repository location</span></span>
        * <span data-ttu-id="a6151-229">目的檔案路徑</span><span class="sxs-lookup"><span data-stu-id="a6151-229">the destination file path</span></span>
    * <span data-ttu-id="a6151-230">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-230">A response will contain:</span></span>
        * <span data-ttu-id="a6151-231">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="a6151-232">取得認證</span><span class="sxs-lookup"><span data-stu-id="a6151-232">Get credentials</span></span>
    * <span data-ttu-id="a6151-233">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="a6151-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="a6151-234">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-234">The request will contain:</span></span>
        * <span data-ttu-id="a6151-235">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-235">the package source repository location</span></span>
        * <span data-ttu-id="a6151-236">使用目前認證從封裝來源存放庫取得的 HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="a6151-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="a6151-237">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-237">A response will contain:</span></span>
        * <span data-ttu-id="a6151-238">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-239">使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-239">a username, if available</span></span>
        * <span data-ttu-id="a6151-240">密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-240">a password, if available</span></span>

5.  <span data-ttu-id="a6151-241">取得封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="a6151-241">Get files in package</span></span>
    * <span data-ttu-id="a6151-242">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-243">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-243">The request will contain:</span></span>
        * <span data-ttu-id="a6151-244">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="a6151-244">the package ID and version</span></span>
        * <span data-ttu-id="a6151-245">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-245">the package source repository location</span></span>
    * <span data-ttu-id="a6151-246">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-246">A response will contain:</span></span>
        * <span data-ttu-id="a6151-247">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-248">如果作業成功，則為封裝中檔案路徑的可列舉</span><span class="sxs-lookup"><span data-stu-id="a6151-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="a6151-249">取得作業宣告</span><span class="sxs-lookup"><span data-stu-id="a6151-249">Get operation claims</span></span> 
    * <span data-ttu-id="a6151-250">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-251">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-251">The request will contain:</span></span>
        * <span data-ttu-id="a6151-252">封裝來源的服務索引. json</span><span class="sxs-lookup"><span data-stu-id="a6151-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="a6151-253">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-253">the package source repository location</span></span>
    * <span data-ttu-id="a6151-254">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-254">A response will contain:</span></span>
        * <span data-ttu-id="a6151-255">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-256">如果作業成功，則為支援的作業（例如：套件下載）的可列舉。</span><span class="sxs-lookup"><span data-stu-id="a6151-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="a6151-257">如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。</span><span class="sxs-lookup"><span data-stu-id="a6151-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="a6151-258">此訊息已在版本*2.0.0*中更新。</span><span class="sxs-lookup"><span data-stu-id="a6151-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="a6151-259">它是在用戶端上，以保留回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="a6151-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="a6151-260">取得封裝雜湊</span><span class="sxs-lookup"><span data-stu-id="a6151-260">Get package hash</span></span>
    * <span data-ttu-id="a6151-261">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-262">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-262">The request will contain:</span></span>
        * <span data-ttu-id="a6151-263">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="a6151-263">the package ID and version</span></span>
        * <span data-ttu-id="a6151-264">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-264">the package source repository location</span></span>
        * <span data-ttu-id="a6151-265">雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="a6151-265">the hash algorithm</span></span>
    * <span data-ttu-id="a6151-266">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-266">A response will contain:</span></span>
        * <span data-ttu-id="a6151-267">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-268">如果作業成功，則使用要求的雜湊演算法來封裝檔案雜湊</span><span class="sxs-lookup"><span data-stu-id="a6151-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="a6151-269">取得套件版本</span><span class="sxs-lookup"><span data-stu-id="a6151-269">Get package versions</span></span>
    * <span data-ttu-id="a6151-270">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-271">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-271">The request will contain:</span></span>
        * <span data-ttu-id="a6151-272">套件識別碼</span><span class="sxs-lookup"><span data-stu-id="a6151-272">the package ID</span></span>
        * <span data-ttu-id="a6151-273">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-273">the package source repository location</span></span>
    * <span data-ttu-id="a6151-274">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-274">A response will contain:</span></span>
        * <span data-ttu-id="a6151-275">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-276">如果作業成功，則為封裝版本的可列舉</span><span class="sxs-lookup"><span data-stu-id="a6151-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="a6151-277">取得服務索引</span><span class="sxs-lookup"><span data-stu-id="a6151-277">Get service index</span></span>
    * <span data-ttu-id="a6151-278">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="a6151-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="a6151-279">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-279">The request will contain:</span></span>
        * <span data-ttu-id="a6151-280">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-280">the package source repository location</span></span>
    * <span data-ttu-id="a6151-281">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-281">A response will contain:</span></span>
        * <span data-ttu-id="a6151-282">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-283">作業成功時的服務索引</span><span class="sxs-lookup"><span data-stu-id="a6151-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="a6151-284">交握</span><span class="sxs-lookup"><span data-stu-id="a6151-284">Handshake</span></span>
     * <span data-ttu-id="a6151-285">要求方向： NuGet <-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="a6151-286">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-286">The request will contain:</span></span>
         * <span data-ttu-id="a6151-287">目前的外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="a6151-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="a6151-288">支援的最小外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="a6151-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="a6151-289">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-289">A response will contain:</span></span>
         * <span data-ttu-id="a6151-290">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="a6151-291">如果作業成功，則為已協商的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="a6151-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="a6151-292">失敗會導致外掛程式終止。</span><span class="sxs-lookup"><span data-stu-id="a6151-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="a6151-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="a6151-293">Initialize</span></span>
     * <span data-ttu-id="a6151-294">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a6151-295">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-295">The request will contain:</span></span>
         * <span data-ttu-id="a6151-296">NuGet 用戶端工具版本</span><span class="sxs-lookup"><span data-stu-id="a6151-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="a6151-297">NuGet 用戶端工具有效語言。</span><span class="sxs-lookup"><span data-stu-id="a6151-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="a6151-298">這會將 ForceEnglishOutput 設定納入考慮（如果使用的話）。</span><span class="sxs-lookup"><span data-stu-id="a6151-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="a6151-299">預設的要求超時，會取代通訊協定的預設值。</span><span class="sxs-lookup"><span data-stu-id="a6151-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="a6151-300">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-300">A response will contain:</span></span>
         * <span data-ttu-id="a6151-301">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="a6151-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="a6151-302">失敗會導致外掛程式終止。</span><span class="sxs-lookup"><span data-stu-id="a6151-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="a6151-303">記錄檔</span><span class="sxs-lookup"><span data-stu-id="a6151-303">Log</span></span>
     * <span data-ttu-id="a6151-304">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="a6151-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="a6151-305">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-305">The request will contain:</span></span>
         * <span data-ttu-id="a6151-306">要求的記錄層級</span><span class="sxs-lookup"><span data-stu-id="a6151-306">the log level for the request</span></span>
         * <span data-ttu-id="a6151-307">要記錄的訊息</span><span class="sxs-lookup"><span data-stu-id="a6151-307">a message to log</span></span>
     * <span data-ttu-id="a6151-308">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-308">A response will contain:</span></span>
         * <span data-ttu-id="a6151-309">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="a6151-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="a6151-310">監視 NuGet 進程結束</span><span class="sxs-lookup"><span data-stu-id="a6151-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="a6151-311">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a6151-312">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-312">The request will contain:</span></span>
         * <span data-ttu-id="a6151-313">NuGet 處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="a6151-313">the NuGet process ID</span></span>
     * <span data-ttu-id="a6151-314">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-314">A response will contain:</span></span>
         * <span data-ttu-id="a6151-315">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="a6151-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="a6151-316">預先提取套件</span><span class="sxs-lookup"><span data-stu-id="a6151-316">Prefetch package</span></span>
     * <span data-ttu-id="a6151-317">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a6151-318">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-318">The request will contain:</span></span>
         * <span data-ttu-id="a6151-319">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="a6151-319">the package ID and version</span></span>
         * <span data-ttu-id="a6151-320">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-320">the package source repository location</span></span>
     * <span data-ttu-id="a6151-321">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-321">A response will contain:</span></span>
         * <span data-ttu-id="a6151-322">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="a6151-323">設定認證</span><span class="sxs-lookup"><span data-stu-id="a6151-323">Set credentials</span></span>
     * <span data-ttu-id="a6151-324">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a6151-325">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-325">The request will contain:</span></span>
         * <span data-ttu-id="a6151-326">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-326">the package source repository location</span></span>
         * <span data-ttu-id="a6151-327">最後已知的套件來源使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="a6151-328">最後已知的套件來源密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="a6151-329">最後一個已知的 proxy 使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="a6151-330">最後一個已知的 proxy 密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="a6151-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="a6151-331">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-331">A response will contain:</span></span>
         * <span data-ttu-id="a6151-332">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="a6151-333">設定記錄層級</span><span class="sxs-lookup"><span data-stu-id="a6151-333">Set log level</span></span>
     * <span data-ttu-id="a6151-334">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a6151-335">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-335">The request will contain:</span></span>
         * <span data-ttu-id="a6151-336">預設記錄層級</span><span class="sxs-lookup"><span data-stu-id="a6151-336">the default log level</span></span>
     * <span data-ttu-id="a6151-337">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-337">A response will contain:</span></span>
         * <span data-ttu-id="a6151-338">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="a6151-339">通訊協定版本*2.0.0*訊息</span><span class="sxs-lookup"><span data-stu-id="a6151-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="a6151-340">取得作業宣告</span><span class="sxs-lookup"><span data-stu-id="a6151-340">Get Operation Claims</span></span>

* <span data-ttu-id="a6151-341">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a6151-342">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-342">The request will contain:</span></span>
        * <span data-ttu-id="a6151-343">封裝來源的服務索引. json</span><span class="sxs-lookup"><span data-stu-id="a6151-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="a6151-344">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="a6151-344">the package source repository location</span></span>
    * <span data-ttu-id="a6151-345">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-345">A response will contain:</span></span>
        * <span data-ttu-id="a6151-346">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="a6151-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a6151-347">如果作業成功，則為支援的作業的可列舉。</span><span class="sxs-lookup"><span data-stu-id="a6151-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="a6151-348">如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。</span><span class="sxs-lookup"><span data-stu-id="a6151-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="a6151-349">如果服務索引和封裝來源為 null，則外掛程式可以使用驗證來回答。</span><span class="sxs-lookup"><span data-stu-id="a6151-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="a6151-350">取得驗證認證</span><span class="sxs-lookup"><span data-stu-id="a6151-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="a6151-351">要求方向： NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="a6151-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="a6151-352">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="a6151-352">The request will contain:</span></span>
    * <span data-ttu-id="a6151-353">URI</span><span class="sxs-lookup"><span data-stu-id="a6151-353">Uri</span></span>
    * <span data-ttu-id="a6151-354">isRetry</span><span class="sxs-lookup"><span data-stu-id="a6151-354">isRetry</span></span>
    * <span data-ttu-id="a6151-355">非</span><span class="sxs-lookup"><span data-stu-id="a6151-355">NonInteractive</span></span>
    * <span data-ttu-id="a6151-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="a6151-356">CanShowDialog</span></span>
* <span data-ttu-id="a6151-357">回應會包含</span><span class="sxs-lookup"><span data-stu-id="a6151-357">A response will contain</span></span>
    * <span data-ttu-id="a6151-358">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="a6151-358">Username</span></span>
    * <span data-ttu-id="a6151-359">密碼</span><span class="sxs-lookup"><span data-stu-id="a6151-359">Password</span></span>
    * <span data-ttu-id="a6151-360">訊息</span><span class="sxs-lookup"><span data-stu-id="a6151-360">Message</span></span>
    * <span data-ttu-id="a6151-361">驗證類型的清單</span><span class="sxs-lookup"><span data-stu-id="a6151-361">List of Auth Types</span></span>
    * <span data-ttu-id="a6151-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="a6151-362">MessageResponseCode</span></span>
