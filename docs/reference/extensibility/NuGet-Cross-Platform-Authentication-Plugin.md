---
title: NuGet 跨平台驗證外掛程式
description: NuGet NuGet.exe、 dotnet.exe，msbuild.exe 和 Visual Studio 跨平台驗證外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 1258ca4b30cb674c3832f12262940729438dd5b0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546630"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="e6fc1-103">NuGet 跨平台驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="e6fc1-104">在版本 4.8 + 中，所有的 NuGet 用戶端 (NuGet.exe，Visual Studio、 dotnet.exe 和 MSBuild.exe) 可以使用頂端的內建的驗證外掛程式[跨平台外掛程式的 NuGet](NuGet-Cross-Platform-Plugins.md)模型。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="e6fc1-105">Dotnet.exe 中的驗證</span><span class="sxs-lookup"><span data-stu-id="e6fc1-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="e6fc1-106">Visual Studio 和 NuGet.exe 所互動的預設值。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="e6fc1-107">NuGet.exe 會包含的交換器容易[非互動式](../../tools/nuget-exe-CLI-Reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-107">NuGet.exe contains a switch to make it [non interactive](../../tools/nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="e6fc1-108">此外 NuGet.exe 和 Visual Studio 外掛程式會提示使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="e6fc1-109">Dotnet.exe 中沒有任何提示，而且預設值為非互動式。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="e6fc1-110">Dotnet.exe 中的驗證機制是裝置流程。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="e6fc1-111">當還原或新增作業封鎖與使用者完成驗證將會提供如何在命令列的指示，以互動方式執行封裝作業。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="e6fc1-112">當使用者完成驗證作業會繼續。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="e6fc1-113">若要讓作業更具互動性，其中應傳入`--interactive`。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="e6fc1-114">目前只有明確`dotnet restore`和`dotnet add package`命令支援互動式切換。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="e6fc1-115">在沒有沒有互動式的交換器`dotnet build`和`dotnet publish`。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="e6fc1-116">在 MSBuild 中的驗證</span><span class="sxs-lookup"><span data-stu-id="e6fc1-116">Authentication in MSBuild</span></span>

<span data-ttu-id="e6fc1-117">類似於 dotnet.exe，MSBuild.exe 預設為非互動式 MSBuild.exe 驗證機制是裝置流程。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="e6fc1-118">若要允許暫停並等候驗證還原，呼叫還原與`msbuild /t:restore /p:NuGetInteractive="true"`。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-118">To allow the restore to pause and wait for authentication, call restore with `msbuild /t:restore /p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="e6fc1-119">建立跨平台驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="e6fc1-120">範例實作可在[MSCredProvider 外掛程式](https://github.com/Microsoft/mscredprovider)。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-120">A sample implementation can be found in [MSCredProvider plugin](https://github.com/Microsoft/mscredprovider).</span></span>

<span data-ttu-id="e6fc1-121">它是非常重要的外掛程式符合規定的 NuGet 用戶端工具的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="e6fc1-122">要驗證外掛程式的外掛程式版本所需的最小*2.0.0*。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="e6fc1-123">NuGet 會執行的外掛程式和查詢的交握，支援此作業的宣告。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="e6fc1-124">跨平台外掛程式 NuGet，請參閱[通訊協定訊息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)如需詳細資訊的特定訊息。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="e6fc1-125">NuGet 會將記錄層級設定，並提供 proxy 資訊，以適時的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="e6fc1-126">NuGet 登入主控台才可接受 NuGet 已設定為外掛程式的記錄層級之後。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="e6fc1-127">.NET framework 增益集的驗證行為</span><span class="sxs-lookup"><span data-stu-id="e6fc1-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="e6fc1-128">在.NET Framework，外掛程式可以提示使用者輸入，在對話方塊的表單中。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="e6fc1-129">.NET core 外掛程式驗證行為</span><span class="sxs-lookup"><span data-stu-id="e6fc1-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="e6fc1-130">在.NET Core，不會顯示一個對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="e6fc1-131">外掛程式應該使用裝置流程驗證。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="e6fc1-132">此外掛程式可以傳送給 NuGet 記錄訊息，指示給使用者。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="e6fc1-133">請注意，記錄至外掛程式設定的記錄層級之後。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="e6fc1-134">NuGet 不會從命令列的任何互動輸入。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="e6fc1-135">當用戶端呼叫以取得的驗證認證的外掛程式時，外掛程式必須符合使用者互動性參數，並採用對話方塊交換器。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="e6fc1-136">下表摘要說明此外掛程式的所有組合的行為方式。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="e6fc1-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="e6fc1-137">IsNonInteractive</span></span> | <span data-ttu-id="e6fc1-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="e6fc1-138">CanShowDialog</span></span> | <span data-ttu-id="e6fc1-139">外掛程式行為</span><span class="sxs-lookup"><span data-stu-id="e6fc1-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="e6fc1-140">true</span><span class="sxs-lookup"><span data-stu-id="e6fc1-140">true</span></span> | <span data-ttu-id="e6fc1-141">true</span><span class="sxs-lookup"><span data-stu-id="e6fc1-141">true</span></span> | <span data-ttu-id="e6fc1-142">IsNonInteractive 參數的優先順序高於對話方塊交換器。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="e6fc1-143">此外掛程式不是允許快顯對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="e6fc1-144">這種組合是唯一有效的.NET Framework 外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="e6fc1-145">true</span><span class="sxs-lookup"><span data-stu-id="e6fc1-145">true</span></span> | <span data-ttu-id="e6fc1-146">False</span><span class="sxs-lookup"><span data-stu-id="e6fc1-146">false</span></span> | <span data-ttu-id="e6fc1-147">IsNonInteractive 參數的優先順序高於對話方塊交換器。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="e6fc1-148">封鎖不允許此外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="e6fc1-149">這種組合是唯一有效的.NET Core 外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="e6fc1-150">False</span><span class="sxs-lookup"><span data-stu-id="e6fc1-150">false</span></span> | <span data-ttu-id="e6fc1-151">true</span><span class="sxs-lookup"><span data-stu-id="e6fc1-151">true</span></span> | <span data-ttu-id="e6fc1-152">此外掛程式應該會顯示一個對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-152">The plugin should show a dialog.</span></span> <span data-ttu-id="e6fc1-153">這種組合是唯一有效的.NET Framework 外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="e6fc1-154">False</span><span class="sxs-lookup"><span data-stu-id="e6fc1-154">false</span></span> | <span data-ttu-id="e6fc1-155">False</span><span class="sxs-lookup"><span data-stu-id="e6fc1-155">false</span></span> | <span data-ttu-id="e6fc1-156">此外掛程式可以應該不會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="e6fc1-157">此外掛程式應該使用裝置流程來驗證記錄透過記錄器指示訊息。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="e6fc1-158">這種組合是唯一有效的.NET Core 外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="e6fc1-159">請參閱下列規格之前撰寫的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6fc1-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="e6fc1-160">NuGet 封裝下載外掛程式</span><span class="sxs-lookup"><span data-stu-id="e6fc1-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="e6fc1-161">跨平台驗證外掛程式的 NuGet</span><span class="sxs-lookup"><span data-stu-id="e6fc1-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
