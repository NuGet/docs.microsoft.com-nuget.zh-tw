---
title: 跨平台外掛程式的 NuGet
description: NuGet NuGet.exe、 dotnet.exe，msbuild.exe 和 Visual Studio 跨平台的外掛程式
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794182"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="5d7d1-103">跨平台外掛程式的 NuGet</span><span class="sxs-lookup"><span data-stu-id="5d7d1-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="5d7d1-104">已新增 nuget 4.8 + 跨平台的外掛程式支援。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="5d7d1-105">這是藉由建置新的外掛程式擴充性模型，必須符合一組嚴格的作業的規則，來達成與。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="5d7d1-106">外掛程式是獨立的可執行檔 (在.NET Core 世界 runnables)，NuGet 用戶端啟動個別的處理序。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="5d7d1-107">這是 true 寫入一次，隨處執行外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="5d7d1-108">它會使用所有的 NuGet 用戶端工具。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="5d7d1-109">增益集可以是 （NuGet.exe，MSBuild.exe 和 Visual Studio） 的.NET Framework 或.NET Core (dotnet.exe)。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="5d7d1-110">定義建立版本的通訊協定之間 NuGet 用戶端和外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="5d7d1-111">啟動交握期間的 2 個處理程序會交涉的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="5d7d1-112">若要涵蓋所有的 NuGet 用戶端工具案例，則需要.NET Framework 和.NET 核心外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="5d7d1-113">以下描述的用戶端/架構組合的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="5d7d1-114">用戶端工具</span><span class="sxs-lookup"><span data-stu-id="5d7d1-114">Client tool</span></span>  | <span data-ttu-id="5d7d1-115">架構</span><span class="sxs-lookup"><span data-stu-id="5d7d1-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="5d7d1-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d7d1-116">Visual Studio</span></span> | <span data-ttu-id="5d7d1-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d7d1-117">.NET Framework</span></span> |
| <span data-ttu-id="5d7d1-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="5d7d1-118">dotnet.exe</span></span> | <span data-ttu-id="5d7d1-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5d7d1-119">.NET Core</span></span> |
| <span data-ttu-id="5d7d1-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="5d7d1-120">NuGet.exe</span></span> | <span data-ttu-id="5d7d1-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d7d1-121">.NET Framework</span></span> |
| <span data-ttu-id="5d7d1-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="5d7d1-122">MSBuild.exe</span></span> | <span data-ttu-id="5d7d1-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d7d1-123">.NET Framework</span></span> |
| <span data-ttu-id="5d7d1-124">在 Mono 上的 NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="5d7d1-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="5d7d1-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d7d1-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="5d7d1-126">如何運作</span><span class="sxs-lookup"><span data-stu-id="5d7d1-126">How does it work</span></span>

<span data-ttu-id="5d7d1-127">高層級的工作流程可以如下所述：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="5d7d1-128">NuGet 會探索可用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="5d7d1-129">適用時，NuGet 會逐一依優先順序並開始逐一進行中的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="5d7d1-130">NuGet 會使用可以服務此要求的第一個外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="5d7d1-131">當您不再需要時，將會關閉增益集。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="5d7d1-132">一般外掛程式需求</span><span class="sxs-lookup"><span data-stu-id="5d7d1-132">General plugin requirements</span></span>

<span data-ttu-id="5d7d1-133">在目前的通訊協定版本*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="5d7d1-134">在此版本中，需求如下：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="5d7d1-135">有有效且信任 Authenticode 簽章的組件會在 Windows 和 Mono 執行。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="5d7d1-136">沒有任何特殊的信任需求尚未執行 Linux 和 Mac 上的組件。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="5d7d1-137">相關的問題</span><span class="sxs-lookup"><span data-stu-id="5d7d1-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="5d7d1-138">支援無狀態的 NuGet 用戶端工具的目前安全性內容下啟動。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="5d7d1-139">比方說，NuGet 用戶端工具不會執行提高權限或稍後所述的外掛程式通訊協定以外的其他初始化。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="5d7d1-140">除非另有明確指定，則為非互動式的。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="5d7d1-141">遵守交涉的外掛程式通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="5d7d1-142">在合理時間內回應所有的要求。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="5d7d1-143">接受任何進行中作業的取消要求。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="5d7d1-144">技術規格所述的下列規格中的更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="5d7d1-145">NuGet 封裝下載外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="5d7d1-146">跨平台驗證外掛程式的 NuGet</span><span class="sxs-lookup"><span data-stu-id="5d7d1-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="5d7d1-147">用戶端-外掛程式互動</span><span class="sxs-lookup"><span data-stu-id="5d7d1-147">Client - Plugin interaction</span></span>

<span data-ttu-id="5d7d1-148">NuGet 用戶端工具和外掛程式與 JSON 通訊標準資料流 （stdin、 stdout、 stderr） 中。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="5d7d1-149">所有的資料必須是 utf-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="5d7d1-150">外掛程式會啟動與引數"-外掛程式 」。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="5d7d1-151">如果使用者直接啟動可執行檔，而不需要這個引數的外掛程式，外掛程式可以提供資訊而非通訊協定交握正在等候訊息。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="5d7d1-152">通訊協定交握逾時是 5 秒。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="5d7d1-153">此外掛程式應該先完成中的設定為除了盡量。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="5d7d1-154">NuGet 用戶端工具會藉由 NuGet 來源的服務索引的傳入查詢的外掛程式支援的作業。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="5d7d1-155">外掛程式可用來檢查有支援的服務類型的服務索引。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="5d7d1-156">NuGet 用戶端工具和外掛程式之間的通訊是雙向。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="5d7d1-157">每個要求會有 5 秒的逾時。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="5d7d1-158">如果作業花費的時間應該在個別的程序應該傳送進度訊息，以防止要求逾時。在 1 分鐘的閒置時間後外掛程式會被視為閒置，並已關閉。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="5d7d1-159">安裝外掛程式和探索</span><span class="sxs-lookup"><span data-stu-id="5d7d1-159">Plugin installation and discovery</span></span>

<span data-ttu-id="5d7d1-160">透過慣例為基礎的目錄結構，並發現外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="5d7d1-161">CI/CD 案例和進階使用者可以使用環境變數覆寫行為。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="5d7d1-162">`NUGET_PLUGIN_PATHS` -定義將用於 NuGet 程序中，保留的優先順序的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="5d7d1-163">如果設定這個環境變數，它會覆寫慣例為基礎的探索。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="5d7d1-164">使用者位置]、 [中的 NuGet 首頁位置`%UserProfile%/.nuget/plugins`。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="5d7d1-165">此位置無法被覆寫。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-165">This location cannot be overriden.</span></span> <span data-ttu-id="5d7d1-166">不同的根目錄會用於.NET Core 和.NET Framework 的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="5d7d1-167">架構</span><span class="sxs-lookup"><span data-stu-id="5d7d1-167">Framework</span></span> | <span data-ttu-id="5d7d1-168">根探索位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="5d7d1-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5d7d1-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="5d7d1-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5d7d1-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="5d7d1-171">每個外掛程式應該安裝在它自己的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="5d7d1-172">外掛程式的進入點會與.dll 擴充功能適用於.NET Core 和.NET Framework 的.exe 副檔名之安裝資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="5d7d1-173">目前沒有任何使用者劇本，外掛程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="5d7d1-174">很簡單，只要將所需的檔案移至預先決定的位置。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="5d7d1-175">支援的作業</span><span class="sxs-lookup"><span data-stu-id="5d7d1-175">Supported operations</span></span>

<span data-ttu-id="5d7d1-176">以新的 「 外掛程式 」 通訊協定支援兩個作業。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="5d7d1-177">作業名稱</span><span class="sxs-lookup"><span data-stu-id="5d7d1-177">Operation name</span></span> | <span data-ttu-id="5d7d1-178">最小通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-178">Minimum protocol version</span></span> | <span data-ttu-id="5d7d1-179">最低 NuGet 用戶端版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="5d7d1-180">下載套件</span><span class="sxs-lookup"><span data-stu-id="5d7d1-180">Download Package</span></span> | <span data-ttu-id="5d7d1-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="5d7d1-181">1.0.0</span></span> | <span data-ttu-id="5d7d1-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="5d7d1-182">4.3.0</span></span> |
| [<span data-ttu-id="5d7d1-183">驗證</span><span class="sxs-lookup"><span data-stu-id="5d7d1-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="5d7d1-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5d7d1-184">2.0.0</span></span> | <span data-ttu-id="5d7d1-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="5d7d1-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="5d7d1-186">執行正確的執行階段下的外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="5d7d1-187">Dotnet.exe 案例中的 NuGet，外掛程式需要能夠在該特定的執行階段的 dotnet.exe 下執行。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="5d7d1-188">它是外掛程式提供者和取用者，以確定會使用相容的 dotnet.exe/plugin 組合上。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="5d7d1-189">可能的問題可能發生的使用者位置有更多的外掛程式時，例如，2.0 執行階段下的 dotnet.exe 便會嘗試使用 2.1 執行階段撰寫的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="5d7d1-190">快取的功能</span><span class="sxs-lookup"><span data-stu-id="5d7d1-190">Capabilities caching</span></span>

<span data-ttu-id="5d7d1-191">安全性驗證和具現化的外掛程式是成本高昂。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="5d7d1-192">不過平均 NuGet 使用者才可能會有的驗證外掛程式，會比驗證作業，方法會更頻繁地發生下載作業。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="5d7d1-193">若要改善體驗，NuGet 會快取指定之要求的作業宣告。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="5d7d1-194">此快取每個外掛程式與外掛程式索引鍵所外掛程式的路徑，而且此功能快取的到期日為 30 天。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="5d7d1-195">快取位於`%LocalAppData%/NuGet/plugins-cache`並將它覆寫環境變數`NUGET_PLUGINS_CACHE_PATH`。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="5d7d1-196">若要清除這[快取](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，可以執行 [區域變數] 命令搭配`plugins-cache`選項。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="5d7d1-197">`all` [區域變數] 選項也會立即刪除外掛程式快取。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="5d7d1-198">通訊協定訊息的索引</span><span class="sxs-lookup"><span data-stu-id="5d7d1-198">Protocol messages index</span></span>

<span data-ttu-id="5d7d1-199">通訊協定版本*1.0.0*訊息：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="5d7d1-200">關閉</span><span class="sxs-lookup"><span data-stu-id="5d7d1-200">Close</span></span>
    * <span data-ttu-id="5d7d1-201">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-202">要求將會包含任何承載</span><span class="sxs-lookup"><span data-stu-id="5d7d1-202">The request will contain no payload</span></span>
    * <span data-ttu-id="5d7d1-203">不需要回應。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-203">No response is expected.</span></span>  <span data-ttu-id="5d7d1-204">適當的回應是外掛程式處理序立即結束。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="5d7d1-205">將檔案複製在封裝中</span><span class="sxs-lookup"><span data-stu-id="5d7d1-205">Copy files in package</span></span>
    * <span data-ttu-id="5d7d1-206">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-207">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-207">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-208">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-208">the package ID and version</span></span>
        * <span data-ttu-id="5d7d1-209">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-209">the package source repository location</span></span>
        * <span data-ttu-id="5d7d1-210">目的地目錄路徑</span><span class="sxs-lookup"><span data-stu-id="5d7d1-210">destination directory path</span></span>
        * <span data-ttu-id="5d7d1-211">可列舉的封裝複製到目的地目錄路徑中的檔案</span><span class="sxs-lookup"><span data-stu-id="5d7d1-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="5d7d1-212">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-212">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-213">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-214">可列舉的完整路徑複製之檔案中的目的地目錄，如果作業成功</span><span class="sxs-lookup"><span data-stu-id="5d7d1-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="5d7d1-215">複製封裝檔案 (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="5d7d1-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="5d7d1-216">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-217">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-217">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-218">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-218">the package ID and version</span></span>
        * <span data-ttu-id="5d7d1-219">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-219">the package source repository location</span></span>
        * <span data-ttu-id="5d7d1-220">目的地檔案路徑</span><span class="sxs-lookup"><span data-stu-id="5d7d1-220">the destination file path</span></span>
    * <span data-ttu-id="5d7d1-221">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-221">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-222">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="5d7d1-223">取得認證</span><span class="sxs-lookup"><span data-stu-id="5d7d1-223">Get credentials</span></span>
    * <span data-ttu-id="5d7d1-224">要求方向： 外掛程式]-> [NuGet</span><span class="sxs-lookup"><span data-stu-id="5d7d1-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="5d7d1-225">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-225">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-226">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-226">the package source repository location</span></span>
        * <span data-ttu-id="5d7d1-227">從使用目前的認證套件來源存放庫取得 HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="5d7d1-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="5d7d1-228">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-228">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-229">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-230">使用者名稱，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-230">a username, if available</span></span>
        * <span data-ttu-id="5d7d1-231">密碼，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-231">a password, if available</span></span>

5.  <span data-ttu-id="5d7d1-232">取得封裝中的檔案</span><span class="sxs-lookup"><span data-stu-id="5d7d1-232">Get files in package</span></span>
    * <span data-ttu-id="5d7d1-233">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-234">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-234">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-235">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-235">the package ID and version</span></span>
        * <span data-ttu-id="5d7d1-236">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-236">the package source repository location</span></span>
    * <span data-ttu-id="5d7d1-237">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-237">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-238">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-239">可列舉的檔案路徑中的封裝，如果作業成功</span><span class="sxs-lookup"><span data-stu-id="5d7d1-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="5d7d1-240">取得作業的宣告</span><span class="sxs-lookup"><span data-stu-id="5d7d1-240">Get operation claims</span></span> 
    * <span data-ttu-id="5d7d1-241">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-242">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-242">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-243">服務 index.json，套件來源</span><span class="sxs-lookup"><span data-stu-id="5d7d1-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="5d7d1-244">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-244">the package source repository location</span></span>
    * <span data-ttu-id="5d7d1-245">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-245">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-246">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-247">可列舉的支援的作業 (例如： 套件下載) 如果作業成功。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="5d7d1-248">如果外掛程式不支援的套件來源，此外掛程式必須傳回空集合的支援的作業。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="5d7d1-249">此訊息已更新版本中*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="5d7d1-250">它是在用戶端，以保留回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="5d7d1-251">取得封裝雜湊</span><span class="sxs-lookup"><span data-stu-id="5d7d1-251">Get package hash</span></span>
    * <span data-ttu-id="5d7d1-252">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-253">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-253">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-254">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-254">the package ID and version</span></span>
        * <span data-ttu-id="5d7d1-255">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-255">the package source repository location</span></span>
        * <span data-ttu-id="5d7d1-256">雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="5d7d1-256">the hash algorithm</span></span>
    * <span data-ttu-id="5d7d1-257">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-257">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-258">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-259">封裝檔案的雜湊，使用要求的雜湊演算法，如果作業成功</span><span class="sxs-lookup"><span data-stu-id="5d7d1-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="5d7d1-260">取得封裝版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-260">Get package versions</span></span>
    * <span data-ttu-id="5d7d1-261">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-262">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-262">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-263">套件識別碼</span><span class="sxs-lookup"><span data-stu-id="5d7d1-263">the package ID</span></span>
        * <span data-ttu-id="5d7d1-264">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-264">the package source repository location</span></span>
    * <span data-ttu-id="5d7d1-265">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-265">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-266">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-267">可列舉的套件版本，如果作業成功</span><span class="sxs-lookup"><span data-stu-id="5d7d1-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="5d7d1-268">取得服務索引</span><span class="sxs-lookup"><span data-stu-id="5d7d1-268">Get service index</span></span>
    * <span data-ttu-id="5d7d1-269">要求方向： 外掛程式]-> [NuGet</span><span class="sxs-lookup"><span data-stu-id="5d7d1-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="5d7d1-270">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-270">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-271">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-271">the package source repository location</span></span>
    * <span data-ttu-id="5d7d1-272">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-272">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-273">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-274">服務索引，如果作業成功</span><span class="sxs-lookup"><span data-stu-id="5d7d1-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="5d7d1-275">交握</span><span class="sxs-lookup"><span data-stu-id="5d7d1-275">Handshake</span></span>
     * <span data-ttu-id="5d7d1-276">要求方向： NuGet <>-外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="5d7d1-277">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-277">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-278">目前的外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="5d7d1-279">支援的最低外掛程式通訊協定版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="5d7d1-280">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-280">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-281">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="5d7d1-282">如果作業成功交涉通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="5d7d1-283">失敗會導致終止的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="5d7d1-284">初始化</span><span class="sxs-lookup"><span data-stu-id="5d7d1-284">Initialize</span></span>
     * <span data-ttu-id="5d7d1-285">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5d7d1-286">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-286">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-287">NuGet 用戶端工具的版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="5d7d1-288">NuGet 用戶端工具有效語言。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="5d7d1-289">這會將考量 ForceEnglishOutput 設定中，如果使用。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="5d7d1-290">預設要求逾時，會取代預設的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="5d7d1-291">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-291">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-292">回應碼，用來表示作業的結果。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="5d7d1-293">失敗會導致終止的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="5d7d1-294">記錄檔</span><span class="sxs-lookup"><span data-stu-id="5d7d1-294">Log</span></span>
     * <span data-ttu-id="5d7d1-295">要求方向： 外掛程式]-> [NuGet</span><span class="sxs-lookup"><span data-stu-id="5d7d1-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="5d7d1-296">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-296">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-297">要求記錄層級</span><span class="sxs-lookup"><span data-stu-id="5d7d1-297">the log level for the request</span></span>
         * <span data-ttu-id="5d7d1-298">要記錄的訊息</span><span class="sxs-lookup"><span data-stu-id="5d7d1-298">a message to log</span></span>
     * <span data-ttu-id="5d7d1-299">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-299">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-300">回應碼，用來表示作業的結果。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="5d7d1-301">監視 NuGet 處理序結束</span><span class="sxs-lookup"><span data-stu-id="5d7d1-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="5d7d1-302">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5d7d1-303">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-303">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-304">NuGet 處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="5d7d1-304">the NuGet process ID</span></span>
     * <span data-ttu-id="5d7d1-305">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-305">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-306">回應碼，用來表示作業的結果。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="5d7d1-307">預先擷取的封裝</span><span class="sxs-lookup"><span data-stu-id="5d7d1-307">Prefetch package</span></span>
     * <span data-ttu-id="5d7d1-308">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5d7d1-309">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-309">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-310">套件識別碼和版本</span><span class="sxs-lookup"><span data-stu-id="5d7d1-310">the package ID and version</span></span>
         * <span data-ttu-id="5d7d1-311">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-311">the package source repository location</span></span>
     * <span data-ttu-id="5d7d1-312">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-312">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-313">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="5d7d1-314">設定認證</span><span class="sxs-lookup"><span data-stu-id="5d7d1-314">Set credentials</span></span>
     * <span data-ttu-id="5d7d1-315">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5d7d1-316">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-316">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-317">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-317">the package source repository location</span></span>
         * <span data-ttu-id="5d7d1-318">最後一個已知的套件來源使用者名稱，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="5d7d1-319">最後一個已知的封裝來源密碼，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="5d7d1-320">最後一個已知的 proxy 使用者名稱，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="5d7d1-321">最後一個已知的 proxy 密碼，如果有的話</span><span class="sxs-lookup"><span data-stu-id="5d7d1-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="5d7d1-322">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-322">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-323">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="5d7d1-324">設定記錄層級</span><span class="sxs-lookup"><span data-stu-id="5d7d1-324">Set log level</span></span>
     * <span data-ttu-id="5d7d1-325">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5d7d1-326">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-326">The request will contain:</span></span>
         * <span data-ttu-id="5d7d1-327">預設記錄層級</span><span class="sxs-lookup"><span data-stu-id="5d7d1-327">the default log level</span></span>
     * <span data-ttu-id="5d7d1-328">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-328">A response will contain:</span></span>
         * <span data-ttu-id="5d7d1-329">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="5d7d1-330">通訊協定版本*2.0.0*訊息</span><span class="sxs-lookup"><span data-stu-id="5d7d1-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="5d7d1-331">取得作業的宣告</span><span class="sxs-lookup"><span data-stu-id="5d7d1-331">Get Operation Claims</span></span>

* <span data-ttu-id="5d7d1-332">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5d7d1-333">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-333">The request will contain:</span></span>
        * <span data-ttu-id="5d7d1-334">服務 index.json，套件來源</span><span class="sxs-lookup"><span data-stu-id="5d7d1-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="5d7d1-335">套件來源存放庫位置</span><span class="sxs-lookup"><span data-stu-id="5d7d1-335">the package source repository location</span></span>
    * <span data-ttu-id="5d7d1-336">回應會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-336">A response will contain:</span></span>
        * <span data-ttu-id="5d7d1-337">回應碼，表示作業結果</span><span class="sxs-lookup"><span data-stu-id="5d7d1-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5d7d1-338">可列舉的支援的作業，如果作業成功。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="5d7d1-339">如果外掛程式不支援的套件來源，此外掛程式必須傳回空集合的支援的作業。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="5d7d1-340">如果服務索引和套件來源為 null 時，外掛程式可以回答與驗證。</span><span class="sxs-lookup"><span data-stu-id="5d7d1-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="5d7d1-341">取得驗證認證</span><span class="sxs-lookup"><span data-stu-id="5d7d1-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="5d7d1-342">要求方向： NuGet]-> [外掛程式</span><span class="sxs-lookup"><span data-stu-id="5d7d1-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="5d7d1-343">要求將會包含：</span><span class="sxs-lookup"><span data-stu-id="5d7d1-343">The request will contain:</span></span>
    * <span data-ttu-id="5d7d1-344">URI</span><span class="sxs-lookup"><span data-stu-id="5d7d1-344">Uri</span></span>
    * <span data-ttu-id="5d7d1-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="5d7d1-345">isRetry</span></span>
    * <span data-ttu-id="5d7d1-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5d7d1-346">NonInteractive</span></span>
    * <span data-ttu-id="5d7d1-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="5d7d1-347">CanShowDialog</span></span>
* <span data-ttu-id="5d7d1-348">回應會包含</span><span class="sxs-lookup"><span data-stu-id="5d7d1-348">A response will contain</span></span>
    * <span data-ttu-id="5d7d1-349">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="5d7d1-349">Username</span></span>
    * <span data-ttu-id="5d7d1-350">密碼</span><span class="sxs-lookup"><span data-stu-id="5d7d1-350">Password</span></span>
    * <span data-ttu-id="5d7d1-351">訊息</span><span class="sxs-lookup"><span data-stu-id="5d7d1-351">Message</span></span>
    * <span data-ttu-id="5d7d1-352">驗證類型清單</span><span class="sxs-lookup"><span data-stu-id="5d7d1-352">List of Auth Types</span></span>
    * <span data-ttu-id="5d7d1-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="5d7d1-353">MessageResponseCode</span></span>