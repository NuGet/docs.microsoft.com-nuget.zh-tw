---
title: NuGet 跨平臺外掛程式
description: 適用于 Nuget.exe、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平臺外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815313"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="1fbb4-103">NuGet 跨平臺外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="1fbb4-104">在 NuGet 4.8 + 中，已新增跨平臺外掛程式的支援。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="1fbb4-105">這是透過建立新的外掛程式擴充性模型來達成，必須符合一組嚴格的運算規則。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="1fbb4-106">外掛程式是獨立的可執行檔（在 .NET Core 世界中為 runnables），NuGet 用戶端會在個別的進程中啟動。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="1fbb4-107">這是真正的寫入一次，可在任何地方執行外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="1fbb4-108">它會與所有 NuGet 用戶端工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="1fbb4-109">外掛程式可以是 .NET Framework （Nuget.exe、Msbuild.exe 和 Visual Studio）或 .NET Core （dotnet .exe）。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="1fbb4-110">NuGet 用戶端和外掛程式之間已建立版本的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="1fbb4-111">在啟動信號交換期間，2個進程會協調通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="1fbb4-112">為了涵蓋所有 NuGet 用戶端工具案例，其中一項需要 .NET Framework 和 .NET Core 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="1fbb4-113">以下說明外掛程式的用戶端/架構組合。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="1fbb4-114">用戶端工具</span><span class="sxs-lookup"><span data-stu-id="1fbb4-114">Client tool</span></span>  | <span data-ttu-id="1fbb4-115">架構</span><span class="sxs-lookup"><span data-stu-id="1fbb4-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="1fbb4-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1fbb4-116">Visual Studio</span></span> | <span data-ttu-id="1fbb4-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1fbb4-117">.NET Framework</span></span> |
| <span data-ttu-id="1fbb4-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="1fbb4-118">dotnet.exe</span></span> | <span data-ttu-id="1fbb4-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1fbb4-119">.NET Core</span></span> |
| <span data-ttu-id="1fbb4-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1fbb4-120">NuGet.exe</span></span> | <span data-ttu-id="1fbb4-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1fbb4-121">.NET Framework</span></span> |
| <span data-ttu-id="1fbb4-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="1fbb4-122">MSBuild.exe</span></span> | <span data-ttu-id="1fbb4-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1fbb4-123">.NET Framework</span></span> |
| <span data-ttu-id="1fbb4-124">Mono 上的 Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1fbb4-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="1fbb4-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1fbb4-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="1fbb4-126">運作方式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-126">How does it work</span></span>

<span data-ttu-id="1fbb4-127">高階工作流程可以描述如下：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="1fbb4-128">NuGet 會探索可用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="1fbb4-129">當適用時，NuGet 會依優先順序逐一查看外掛程式，然後逐一啟動。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="1fbb4-130">NuGet 會使用可服務要求的第一個外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="1fbb4-131">外掛程式將會在不再需要時關閉。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="1fbb4-132">一般外掛程式需求</span><span class="sxs-lookup"><span data-stu-id="1fbb4-132">General plugin requirements</span></span>

<span data-ttu-id="1fbb4-133">目前的通訊協定版本是*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="1fbb4-134">在此版本底下，需求如下：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="1fbb4-135">擁有將在 Windows 和 Mono 上執行的有效、受信任的 Authenticode 簽章元件。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="1fbb4-136">尚未在 Linux 和 Mac 上執行元件的特殊信任需求。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="1fbb4-137">相關問題</span><span class="sxs-lookup"><span data-stu-id="1fbb4-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="1fbb4-138">支援 NuGet 用戶端工具的目前安全性內容下的無狀態啟動。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="1fbb4-139">例如，NuGet 用戶端工具不會在稍後所述的外掛程式通訊協定以外執行提高許可權或額外的初始化。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="1fbb4-140">除非明確指定，否則不是互動式的。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="1fbb4-141">遵循已協商的外掛程式通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="1fbb4-142">在合理的時間週期內回應所有要求。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="1fbb4-143">接受任何進行中作業的取消要求。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="1fbb4-144">下列規格將更詳細地說明技術規格：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="1fbb4-145">NuGet 套件下載外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="1fbb4-146">NuGet 跨平臺驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="1fbb4-147">用戶端-外掛程式的互動</span><span class="sxs-lookup"><span data-stu-id="1fbb4-147">Client - Plugin interaction</span></span>

<span data-ttu-id="1fbb4-148">NuGet 用戶端工具和外掛程式會透過標準資料流程（stdin、stdout、stderr）與 JSON 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="1fbb4-149">所有資料都必須以 UTF-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="1fbb4-150">外掛程式會以引數 "-外掛程式" 啟動。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="1fbb4-151">如果使用者直接啟動沒有此引數的外掛程式可執行檔，則外掛程式會提供資訊性訊息，而不是等候通訊協定交握。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="1fbb4-152">通訊協定交握時間為5秒。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="1fbb4-153">外掛程式應該盡可能以最少的數量完成中的設定。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="1fbb4-154">NuGet 用戶端工具會藉由傳遞 NuGet 來源的服務索引來查詢外掛程式支援的作業。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="1fbb4-155">外掛程式可以使用服務索引來檢查支援的服務類型是否存在。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="1fbb4-156">NuGet 用戶端工具和外掛程式之間的通訊是雙向的。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="1fbb4-157">每個要求的超時時間為5秒。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="1fbb4-158">如果作業應花費較長的時間，則個別的進程應傳送進度訊息，以防止要求超時。在閒置1分鐘後，外掛程式會被視為閒置並關閉。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="1fbb4-159">外掛程式安裝與探索</span><span class="sxs-lookup"><span data-stu-id="1fbb4-159">Plugin installation and discovery</span></span>

<span data-ttu-id="1fbb4-160">這些外掛程式會透過以慣例為基礎的目錄結構來探索。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="1fbb4-161">CI/CD 案例和 power 使用者可以使用環境變數來覆寫行為。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="1fbb4-162">請注意， `NUGET_NETCORE_PLUGIN_PATHS`和僅適用于 5.3 + 版本的 NuGet 工具和更新版本。 `NUGET_NETFX_PLUGIN_PATHS`</span><span class="sxs-lookup"><span data-stu-id="1fbb4-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="1fbb4-163">`NUGET_NETFX_PLUGIN_PATHS`-定義以 .NET Framework 為基礎的工具（Nuget.exe/Msbuild.exe/Visual Studio）將使用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="1fbb4-164">優先于`NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="1fbb4-165">（僅限 NuGet 5.3 版 +）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="1fbb4-166">`NUGET_NETCORE_PLUGIN_PATHS`-定義將由 .NET Core 工具（dotnet）使用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="1fbb4-167">優先于`NUGET_PLUGIN_PATHS`。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="1fbb4-168">（僅限 NuGet 5.3 版 +）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="1fbb4-169">`NUGET_PLUGIN_PATHS`-定義將用於該 NuGet 進程的外掛程式，保留優先順序。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="1fbb4-170">如果設定此環境變數，則會覆寫以慣例為基礎的探索。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="1fbb4-171">如果指定了其中一個架構特定的變數，則會忽略。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="1fbb4-172">使用者位置，是中`%UserProfile%/.nuget/plugins`的 NuGet 首頁位置。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="1fbb4-173">無法覆寫此位置。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-173">This location cannot be overriden.</span></span> <span data-ttu-id="1fbb4-174">.NET Core 和 .NET Framework 外掛程式將會使用不同的根目錄。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="1fbb4-175">架構</span><span class="sxs-lookup"><span data-stu-id="1fbb4-175">Framework</span></span> | <span data-ttu-id="1fbb4-176">根探索位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="1fbb4-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1fbb4-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="1fbb4-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1fbb4-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="1fbb4-179">每個外掛程式都應該安裝在自己的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="1fbb4-180">外掛程式進入點會是已安裝之資料夾的名稱，以及適用于 .NET Core 的 .dll 副檔名，而 .NET Framework 的 .exe 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="1fbb4-181">目前沒有安裝外掛程式的使用者案例。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="1fbb4-182">就像是將所需的檔案移到預先決定的位置一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="1fbb4-183">支援的作業</span><span class="sxs-lookup"><span data-stu-id="1fbb4-183">Supported operations</span></span>

<span data-ttu-id="1fbb4-184">新的外掛程式通訊協定支援兩個作業。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="1fbb4-185">作業名稱</span><span class="sxs-lookup"><span data-stu-id="1fbb4-185">Operation name</span></span> | <span data-ttu-id="1fbb4-186">最低通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-186">Minimum protocol version</span></span> | <span data-ttu-id="1fbb4-187">最低 NuGet 用戶端版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="1fbb4-188">下載套件</span><span class="sxs-lookup"><span data-stu-id="1fbb4-188">Download Package</span></span> | <span data-ttu-id="1fbb4-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1fbb4-189">1.0.0</span></span> | <span data-ttu-id="1fbb4-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="1fbb4-190">4.3.0</span></span> |
| [<span data-ttu-id="1fbb4-191">驗證</span><span class="sxs-lookup"><span data-stu-id="1fbb4-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="1fbb4-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="1fbb4-192">2.0.0</span></span> | <span data-ttu-id="1fbb4-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="1fbb4-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="1fbb4-194">在正確的執行時間下執行外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="1fbb4-195">在 dotnet 的 NuGet 案例中，外掛程式必須能夠在 dotnet 的特定執行時間下執行。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="1fbb4-196">它位於外掛程式提供者和取用者上，以確保使用相容的 dotnet .exe/外掛程式組合。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="1fbb4-197">使用者位置外掛程式可能會發生問題，例如，2.0 執行時間下的 dotnet 嘗試使用針對2.1 執行時間所撰寫的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="1fbb4-198">功能快取</span><span class="sxs-lookup"><span data-stu-id="1fbb4-198">Capabilities caching</span></span>

<span data-ttu-id="1fbb4-199">外掛程式的安全性驗證和具現化成本很高。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="1fbb4-200">下載作業的執行頻率比驗證作業更頻繁，但平均 NuGet 使用者只可能有驗證外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="1fbb4-201">為了改善此體驗，NuGet 會快取指定要求的作業宣告。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="1fbb4-202">此快取是每個外掛程式，其中外掛程式的索引鍵為外掛程式路徑，而此功能快取的到期時間為30天。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="1fbb4-203">快取位於中`%LocalAppData%/NuGet/plugins-cache` ，並使用環境變數`NUGET_PLUGINS_CACHE_PATH`來覆寫。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="1fbb4-204">若要清除[此快](../../consume-packages/managing-the-global-packages-and-cache-folders.md)取，可以使用`plugins-cache`選項來執行 [區域變數] 命令。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="1fbb4-205">[ `all`區域變數] 選項現在也會刪除外掛程式快取。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="1fbb4-206">通訊協定訊息索引</span><span class="sxs-lookup"><span data-stu-id="1fbb4-206">Protocol messages index</span></span>

<span data-ttu-id="1fbb4-207">通訊協定*1.0.0*版訊息：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="1fbb4-208">關閉</span><span class="sxs-lookup"><span data-stu-id="1fbb4-208">Close</span></span>
    * <span data-ttu-id="1fbb4-209">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-210">要求不會包含任何承載</span><span class="sxs-lookup"><span data-stu-id="1fbb4-210">The request will contain no payload</span></span>
    * <span data-ttu-id="1fbb4-211">不需要回應。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-211">No response is expected.</span></span>  <span data-ttu-id="1fbb4-212">適當的回應是讓外掛程式進程立即結束。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="1fbb4-213">複製封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="1fbb4-213">Copy files in package</span></span>
    * <span data-ttu-id="1fbb4-214">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-215">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-215">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-216">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-216">the package ID and version</span></span>
        * <span data-ttu-id="1fbb4-217">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-217">the package source repository location</span></span>
        * <span data-ttu-id="1fbb4-218">目的地目錄路徑</span><span class="sxs-lookup"><span data-stu-id="1fbb4-218">destination directory path</span></span>
        * <span data-ttu-id="1fbb4-219">封裝中要複製到目的地目錄路徑之檔案的可列舉</span><span class="sxs-lookup"><span data-stu-id="1fbb4-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="1fbb4-220">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-220">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-221">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-222">如果作業成功，則為目的地目錄中複製之檔案的完整路徑列舉</span><span class="sxs-lookup"><span data-stu-id="1fbb4-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="1fbb4-223">複製套件檔案（. nupkg）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="1fbb4-224">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-225">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-225">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-226">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-226">the package ID and version</span></span>
        * <span data-ttu-id="1fbb4-227">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-227">the package source repository location</span></span>
        * <span data-ttu-id="1fbb4-228">目的檔案路徑</span><span class="sxs-lookup"><span data-stu-id="1fbb4-228">the destination file path</span></span>
    * <span data-ttu-id="1fbb4-229">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-229">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-230">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="1fbb4-231">取得認證</span><span class="sxs-lookup"><span data-stu-id="1fbb4-231">Get credentials</span></span>
    * <span data-ttu-id="1fbb4-232">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="1fbb4-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1fbb4-233">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-233">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-234">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-234">the package source repository location</span></span>
        * <span data-ttu-id="1fbb4-235">使用目前認證從封裝來源存放庫取得的 HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="1fbb4-236">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-236">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-237">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-238">使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-238">a username, if available</span></span>
        * <span data-ttu-id="1fbb4-239">密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-239">a password, if available</span></span>

5.  <span data-ttu-id="1fbb4-240">取得封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="1fbb4-240">Get files in package</span></span>
    * <span data-ttu-id="1fbb4-241">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-242">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-242">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-243">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-243">the package ID and version</span></span>
        * <span data-ttu-id="1fbb4-244">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-244">the package source repository location</span></span>
    * <span data-ttu-id="1fbb4-245">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-245">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-246">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-247">如果作業成功，則為封裝中檔案路徑的可列舉</span><span class="sxs-lookup"><span data-stu-id="1fbb4-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="1fbb4-248">取得作業宣告</span><span class="sxs-lookup"><span data-stu-id="1fbb4-248">Get operation claims</span></span> 
    * <span data-ttu-id="1fbb4-249">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-250">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-250">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-251">封裝來源的服務索引. json</span><span class="sxs-lookup"><span data-stu-id="1fbb4-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="1fbb4-252">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-252">the package source repository location</span></span>
    * <span data-ttu-id="1fbb4-253">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-253">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-254">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-255">如果作業成功，則為支援的作業（例如：套件下載）的可列舉。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="1fbb4-256">如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="1fbb4-257">此訊息已在版本*2.0.0*中更新。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="1fbb4-258">它是在用戶端上，以保留回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="1fbb4-259">取得封裝雜湊</span><span class="sxs-lookup"><span data-stu-id="1fbb4-259">Get package hash</span></span>
    * <span data-ttu-id="1fbb4-260">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-261">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-261">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-262">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-262">the package ID and version</span></span>
        * <span data-ttu-id="1fbb4-263">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-263">the package source repository location</span></span>
        * <span data-ttu-id="1fbb4-264">雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="1fbb4-264">the hash algorithm</span></span>
    * <span data-ttu-id="1fbb4-265">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-265">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-266">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-267">如果作業成功，則使用要求的雜湊演算法來封裝檔案雜湊</span><span class="sxs-lookup"><span data-stu-id="1fbb4-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="1fbb4-268">取得套件版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-268">Get package versions</span></span>
    * <span data-ttu-id="1fbb4-269">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-270">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-270">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-271">套件識別碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-271">the package ID</span></span>
        * <span data-ttu-id="1fbb4-272">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-272">the package source repository location</span></span>
    * <span data-ttu-id="1fbb4-273">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-273">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-274">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-275">如果作業成功，則為封裝版本的可列舉</span><span class="sxs-lookup"><span data-stu-id="1fbb4-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="1fbb4-276">取得服務索引</span><span class="sxs-lookup"><span data-stu-id="1fbb4-276">Get service index</span></span>
    * <span data-ttu-id="1fbb4-277">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="1fbb4-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="1fbb4-278">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-278">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-279">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-279">the package source repository location</span></span>
    * <span data-ttu-id="1fbb4-280">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-280">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-281">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-282">作業成功時的服務索引</span><span class="sxs-lookup"><span data-stu-id="1fbb4-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="1fbb4-283">交握</span><span class="sxs-lookup"><span data-stu-id="1fbb4-283">Handshake</span></span>
     * <span data-ttu-id="1fbb4-284">要求方向：NuGet <-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="1fbb4-285">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-285">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-286">目前的外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="1fbb4-287">支援的最小外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="1fbb4-288">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-288">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-289">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="1fbb4-290">如果作業成功，則為已協商的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="1fbb4-291">失敗會導致外掛程式終止。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="1fbb4-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="1fbb4-292">Initialize</span></span>
     * <span data-ttu-id="1fbb4-293">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1fbb4-294">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-294">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-295">NuGet 用戶端工具版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="1fbb4-296">NuGet 用戶端工具有效語言。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="1fbb4-297">這會將 ForceEnglishOutput 設定納入考慮（如果使用的話）。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="1fbb4-298">預設的要求超時，會取代通訊協定的預設值。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="1fbb4-299">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-299">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-300">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="1fbb4-301">失敗會導致外掛程式終止。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="1fbb4-302">記錄檔</span><span class="sxs-lookup"><span data-stu-id="1fbb4-302">Log</span></span>
     * <span data-ttu-id="1fbb4-303">要求方向：外掛程式-> NuGet</span><span class="sxs-lookup"><span data-stu-id="1fbb4-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="1fbb4-304">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-304">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-305">要求的記錄層級</span><span class="sxs-lookup"><span data-stu-id="1fbb4-305">the log level for the request</span></span>
         * <span data-ttu-id="1fbb4-306">要記錄的訊息</span><span class="sxs-lookup"><span data-stu-id="1fbb4-306">a message to log</span></span>
     * <span data-ttu-id="1fbb4-307">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-307">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-308">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="1fbb4-309">監視 NuGet 進程結束</span><span class="sxs-lookup"><span data-stu-id="1fbb4-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="1fbb4-310">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1fbb4-311">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-311">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-312">NuGet 處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-312">the NuGet process ID</span></span>
     * <span data-ttu-id="1fbb4-313">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-313">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-314">表示作業結果的回應碼。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="1fbb4-315">預先提取套件</span><span class="sxs-lookup"><span data-stu-id="1fbb4-315">Prefetch package</span></span>
     * <span data-ttu-id="1fbb4-316">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1fbb4-317">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-317">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-318">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="1fbb4-318">the package ID and version</span></span>
         * <span data-ttu-id="1fbb4-319">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-319">the package source repository location</span></span>
     * <span data-ttu-id="1fbb4-320">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-320">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-321">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="1fbb4-322">設定認證</span><span class="sxs-lookup"><span data-stu-id="1fbb4-322">Set credentials</span></span>
     * <span data-ttu-id="1fbb4-323">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1fbb4-324">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-324">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-325">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-325">the package source repository location</span></span>
         * <span data-ttu-id="1fbb4-326">最後已知的套件來源使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="1fbb4-327">最後已知的套件來源密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="1fbb4-328">最後一個已知的 proxy 使用者名稱（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="1fbb4-329">最後一個已知的 proxy 密碼（如果有的話）</span><span class="sxs-lookup"><span data-stu-id="1fbb4-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="1fbb4-330">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-330">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-331">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="1fbb4-332">設定記錄層級</span><span class="sxs-lookup"><span data-stu-id="1fbb4-332">Set log level</span></span>
     * <span data-ttu-id="1fbb4-333">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="1fbb4-334">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-334">The request will contain:</span></span>
         * <span data-ttu-id="1fbb4-335">預設記錄層級</span><span class="sxs-lookup"><span data-stu-id="1fbb4-335">the default log level</span></span>
     * <span data-ttu-id="1fbb4-336">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-336">A response will contain:</span></span>
         * <span data-ttu-id="1fbb4-337">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="1fbb4-338">通訊協定版本*2.0.0*訊息</span><span class="sxs-lookup"><span data-stu-id="1fbb4-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="1fbb4-339">取得作業宣告</span><span class="sxs-lookup"><span data-stu-id="1fbb4-339">Get Operation Claims</span></span>

* <span data-ttu-id="1fbb4-340">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="1fbb4-341">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-341">The request will contain:</span></span>
        * <span data-ttu-id="1fbb4-342">封裝來源的服務索引. json</span><span class="sxs-lookup"><span data-stu-id="1fbb4-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="1fbb4-343">封裝來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="1fbb4-343">the package source repository location</span></span>
    * <span data-ttu-id="1fbb4-344">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-344">A response will contain:</span></span>
        * <span data-ttu-id="1fbb4-345">指出作業結果的回應碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="1fbb4-346">如果作業成功，則為支援的作業的可列舉。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="1fbb4-347">如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="1fbb4-348">如果服務索引和封裝來源為 null，則外掛程式可以使用驗證來回答。</span><span class="sxs-lookup"><span data-stu-id="1fbb4-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="1fbb4-349">取得驗證認證</span><span class="sxs-lookup"><span data-stu-id="1fbb4-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="1fbb4-350">要求方向：NuGet-> 外掛程式</span><span class="sxs-lookup"><span data-stu-id="1fbb4-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="1fbb4-351">要求將包含：</span><span class="sxs-lookup"><span data-stu-id="1fbb4-351">The request will contain:</span></span>
    * <span data-ttu-id="1fbb4-352">URI</span><span class="sxs-lookup"><span data-stu-id="1fbb4-352">Uri</span></span>
    * <span data-ttu-id="1fbb4-353">isRetry</span><span class="sxs-lookup"><span data-stu-id="1fbb4-353">isRetry</span></span>
    * <span data-ttu-id="1fbb4-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1fbb4-354">NonInteractive</span></span>
    * <span data-ttu-id="1fbb4-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="1fbb4-355">CanShowDialog</span></span>
* <span data-ttu-id="1fbb4-356">回應會包含</span><span class="sxs-lookup"><span data-stu-id="1fbb4-356">A response will contain</span></span>
    * <span data-ttu-id="1fbb4-357">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="1fbb4-357">Username</span></span>
    * <span data-ttu-id="1fbb4-358">密碼</span><span class="sxs-lookup"><span data-stu-id="1fbb4-358">Password</span></span>
    * <span data-ttu-id="1fbb4-359">訊息</span><span class="sxs-lookup"><span data-stu-id="1fbb4-359">Message</span></span>
    * <span data-ttu-id="1fbb4-360">驗證類型的清單</span><span class="sxs-lookup"><span data-stu-id="1fbb4-360">List of Auth Types</span></span>
    * <span data-ttu-id="1fbb4-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="1fbb4-361">MessageResponseCode</span></span>
