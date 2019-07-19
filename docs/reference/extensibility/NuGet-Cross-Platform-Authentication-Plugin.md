---
title: NuGet 跨平台驗證外掛程式
description: 適用于 Nuget.exe、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平臺驗證外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317284"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="72de6-103">NuGet 跨平台驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="72de6-104">在 4.8 + 版本中, 所有 NuGet 用戶端 (Nuget.exe、Visual Studio、dotnet 和 Msbuild.exe) 都可以使用建置於[NuGet 跨平臺外掛程式](NuGet-Cross-Platform-Plugins.md)模型之上的驗證外掛程式。</span><span class="sxs-lookup"><span data-stu-id="72de6-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="72de6-105">Dotnet 中的驗證</span><span class="sxs-lookup"><span data-stu-id="72de6-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="72de6-106">Visual Studio 和 Nuget.exe 預設是互動式的。</span><span class="sxs-lookup"><span data-stu-id="72de6-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="72de6-107">Nuget.exe 包含將它設為[非互動](../nuget-exe-CLI-Reference.md)的交換器。</span><span class="sxs-lookup"><span data-stu-id="72de6-107">NuGet.exe contains a switch to make it [non interactive](../nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="72de6-108">此外, Nuget.exe 和 Visual Studio 外掛程式會提示使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="72de6-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="72de6-109">在 dotnet 中, 不會出現提示, 而且預設值為非互動式。</span><span class="sxs-lookup"><span data-stu-id="72de6-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="72de6-110">Dotnet 中的驗證機制是裝置流程。</span><span class="sxs-lookup"><span data-stu-id="72de6-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="72de6-111">以互動方式執行「還原」或「新增封裝」作業時, 會在命令列上提供作業封鎖, 以及使用者如何完成驗證的指示。</span><span class="sxs-lookup"><span data-stu-id="72de6-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="72de6-112">當使用者完成驗證時, 作業將會繼續。</span><span class="sxs-lookup"><span data-stu-id="72de6-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="72de6-113">若要讓作業成為互動式作業, 應該`--interactive`傳遞一個。</span><span class="sxs-lookup"><span data-stu-id="72de6-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="72de6-114">目前只有明確`dotnet restore`和`dotnet add package`命令支援互動式交換器。</span><span class="sxs-lookup"><span data-stu-id="72de6-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="72de6-115">`dotnet build` 和`dotnet publish`上沒有互動開關。</span><span class="sxs-lookup"><span data-stu-id="72de6-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="72de6-116">MSBuild 中的驗證</span><span class="sxs-lookup"><span data-stu-id="72de6-116">Authentication in MSBuild</span></span>

<span data-ttu-id="72de6-117">如同 dotnet, Msbuild.exe 預設為非互動式, 而 Msbuild.exe 驗證機制是裝置流程。</span><span class="sxs-lookup"><span data-stu-id="72de6-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="72de6-118">若要讓還原暫停並等候驗證, 請使用`msbuild -t:restore -p:NuGetInteractive="true"`呼叫 restore。</span><span class="sxs-lookup"><span data-stu-id="72de6-118">To allow the restore to pause and wait for authentication, call restore with `msbuild -t:restore -p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="72de6-119">建立跨平臺驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="72de6-120">您可以在[Microsoft 認證提供者外掛程式](https://github.com/Microsoft/artifacts-credprovider)中找到範例執行。</span><span class="sxs-lookup"><span data-stu-id="72de6-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="72de6-121">外掛程式必須符合 NuGet 用戶端工具所設定的安全性需求, 這點非常重要。</span><span class="sxs-lookup"><span data-stu-id="72de6-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="72de6-122">外掛程式的最低必要版本為「驗證外掛程式」 ( *2.0.0*)。</span><span class="sxs-lookup"><span data-stu-id="72de6-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="72de6-123">NuGet 將會執行與外掛程式的交握, 並查詢支援的作業宣告。</span><span class="sxs-lookup"><span data-stu-id="72de6-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="72de6-124">如需特定訊息的詳細資訊, 請參閱 NuGet 跨平臺外掛程式[通訊協定訊息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)。</span><span class="sxs-lookup"><span data-stu-id="72de6-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="72de6-125">NuGet 會設定記錄層級, 並將 proxy 資訊提供給外掛程式 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="72de6-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="72de6-126">只有在 NuGet 已將記錄層級設定為外掛程式之後, 才可接受記錄至 NuGet 主控台。</span><span class="sxs-lookup"><span data-stu-id="72de6-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="72de6-127">.NET Framework 外掛程式驗證行為</span><span class="sxs-lookup"><span data-stu-id="72de6-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="72de6-128">在 .NET Framework 中, 允許外掛程式以對話方塊的形式提示使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="72de6-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="72de6-129">.NET Core 外掛程式驗證行為</span><span class="sxs-lookup"><span data-stu-id="72de6-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="72de6-130">在 .NET Core 中, 無法顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="72de6-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="72de6-131">外掛程式應該使用裝置流程來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="72de6-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="72de6-132">外掛程式可以透過指示將記錄訊息傳送至 NuGet, 並提供使用者的指示。</span><span class="sxs-lookup"><span data-stu-id="72de6-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="72de6-133">請注意, 在記錄層級設定為外掛程式之後, 才可以使用記錄。</span><span class="sxs-lookup"><span data-stu-id="72de6-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="72de6-134">NuGet 不會從命令列進行任何互動式輸入。</span><span class="sxs-lookup"><span data-stu-id="72de6-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="72de6-135">當用戶端呼叫具有取得驗證認證的外掛程式時, 外掛程式必須符合互動性交換器, 並遵循對話參數。</span><span class="sxs-lookup"><span data-stu-id="72de6-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="72de6-136">下表摘要說明外掛程式在所有組合中的行為方式。</span><span class="sxs-lookup"><span data-stu-id="72de6-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="72de6-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="72de6-137">IsNonInteractive</span></span> | <span data-ttu-id="72de6-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="72de6-138">CanShowDialog</span></span> | <span data-ttu-id="72de6-139">外掛程式行為</span><span class="sxs-lookup"><span data-stu-id="72de6-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="72de6-140">true</span><span class="sxs-lookup"><span data-stu-id="72de6-140">true</span></span> | <span data-ttu-id="72de6-141">true</span><span class="sxs-lookup"><span data-stu-id="72de6-141">true</span></span> | <span data-ttu-id="72de6-142">IsNonInteractive 參數的優先順序高於對話方塊參數。</span><span class="sxs-lookup"><span data-stu-id="72de6-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="72de6-143">不允許外掛程式彈出對話方塊。</span><span class="sxs-lookup"><span data-stu-id="72de6-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="72de6-144">此組合僅適用于 .NET Framework 外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="72de6-145">true</span><span class="sxs-lookup"><span data-stu-id="72de6-145">true</span></span> | <span data-ttu-id="72de6-146">False</span><span class="sxs-lookup"><span data-stu-id="72de6-146">false</span></span> | <span data-ttu-id="72de6-147">IsNonInteractive 參數的優先順序高於對話方塊參數。</span><span class="sxs-lookup"><span data-stu-id="72de6-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="72de6-148">不允許封鎖此外掛程式。</span><span class="sxs-lookup"><span data-stu-id="72de6-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="72de6-149">此組合僅適用于 .NET Core 外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="72de6-150">False</span><span class="sxs-lookup"><span data-stu-id="72de6-150">false</span></span> | <span data-ttu-id="72de6-151">true</span><span class="sxs-lookup"><span data-stu-id="72de6-151">true</span></span> | <span data-ttu-id="72de6-152">外掛程式應該會顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="72de6-152">The plugin should show a dialog.</span></span> <span data-ttu-id="72de6-153">此組合僅適用于 .NET Framework 外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="72de6-154">False</span><span class="sxs-lookup"><span data-stu-id="72de6-154">false</span></span> | <span data-ttu-id="72de6-155">False</span><span class="sxs-lookup"><span data-stu-id="72de6-155">false</span></span> | <span data-ttu-id="72de6-156">外掛程式應該/無法顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="72de6-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="72de6-157">外掛程式應該使用裝置流程, 透過記錄器記錄指示訊息來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="72de6-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="72de6-158">此組合僅適用于 .NET Core 外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="72de6-159">撰寫外掛程式之前, 請參閱下列規格。</span><span class="sxs-lookup"><span data-stu-id="72de6-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="72de6-160">NuGet 套件下載外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="72de6-161">NuGet 跨平臺驗證外掛程式</span><span class="sxs-lookup"><span data-stu-id="72de6-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
