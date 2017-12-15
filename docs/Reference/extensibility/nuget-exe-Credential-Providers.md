---
title: "nuget.exe 認證提供者 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: "nuget.exe 認證提供者使用摘要驗證，而且會實作為命令列可執行檔，請遵循特定的慣例。"
keywords: "nuget.exe 認證提供者認證提供者 API，驗證使用的摘要，驗證組件庫"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="6be5e-104">搭配 nuget.exe 認證提供者使用的驗證摘要</span><span class="sxs-lookup"><span data-stu-id="6be5e-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="6be5e-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="6be5e-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="6be5e-106">當`nuget.exe`需要使用摘要驗證的認證會以下列方式尋找它們：</span><span class="sxs-lookup"><span data-stu-id="6be5e-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="6be5e-107">中的認證會先尋找 NuGet`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="6be5e-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="6be5e-108">NuGet 接著會使用外掛程式的認證提供者，受限於如下所示的順序。</span><span class="sxs-lookup"><span data-stu-id="6be5e-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="6be5e-109">(範例中，且[Visual Studio Team Services 認證提供者](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)</span><span class="sxs-lookup"><span data-stu-id="6be5e-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="6be5e-110">NuGet 接著會提示使用者提供認證，在命令列上。</span><span class="sxs-lookup"><span data-stu-id="6be5e-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="6be5e-111">請注意，此處所述的認證提供者只在工作`nuget.exe`而不是在 'dotnet restore' 或 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6be5e-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="6be5e-112">Visual Studio 中的認證提供者，請參閱[nuget.exe for Visual Studio 的認證提供者](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="6be5e-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="6be5e-113">nuget.exe 認證提供者可用以 3 種方式：</span><span class="sxs-lookup"><span data-stu-id="6be5e-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="6be5e-114">**全域**： 若要使用的所有執行個體的認證提供者`nuget.exe`執行目前的使用者設定檔 下，將它加入至`%LocalAppData%\NuGet\CredentialProviders`。</span><span class="sxs-lookup"><span data-stu-id="6be5e-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="6be5e-115">您可能需要建立`CredentialProviders`資料夾。</span><span class="sxs-lookup"><span data-stu-id="6be5e-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="6be5e-116">認證提供者可以安裝根目錄的`CredentialProviders`資料夾或子資料夾內。</span><span class="sxs-lookup"><span data-stu-id="6be5e-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="6be5e-117">如果認證提供者有多個檔案/組件，您可以使用子資料夾，將組織的提供者。</span><span class="sxs-lookup"><span data-stu-id="6be5e-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="6be5e-118">**環境變數從**： 認證提供者可以儲存在任何地方，並存取`nuget.exe`藉由設定`%NUGET_CREDENTIALPROVIDERS_PATH%`環境變數，以提供者位置。</span><span class="sxs-lookup"><span data-stu-id="6be5e-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="6be5e-119">這個變數可以是以分號分隔的清單 (例如， `path1;path2`) 如果您有多個位置。</span><span class="sxs-lookup"><span data-stu-id="6be5e-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="6be5e-120">**連同 nuget.exe**: nuget.exe 認證提供者可以放在相同的資料夾`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="6be5e-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="6be5e-121">認證提供者，在載入時`nuget.exe`搜尋上述的位置，讓任何名為檔案`credentialprovider*.exe`，接著會載入這些檔案在發現的順序。</span><span class="sxs-lookup"><span data-stu-id="6be5e-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="6be5e-122">如果多個認證提供者存在相同資料夾中，變更就會依字母順序排列的順序載入。</span><span class="sxs-lookup"><span data-stu-id="6be5e-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="6be5e-123">建立 nuget.exe 認證提供者</span><span class="sxs-lookup"><span data-stu-id="6be5e-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="6be5e-124">認證提供者是命令列可執行檔中以`CredentialProvider*.exe`，，會收集輸入取得適當的認證，然後傳回適當的結束狀態碼和標準輸出。</span><span class="sxs-lookup"><span data-stu-id="6be5e-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="6be5e-125">提供者必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="6be5e-125">A provider must do the following:</span></span>

- <span data-ttu-id="6be5e-126">判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。</span><span class="sxs-lookup"><span data-stu-id="6be5e-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="6be5e-127">如果沒有，則應該傳回狀態碼不含認證的 1。</span><span class="sxs-lookup"><span data-stu-id="6be5e-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="6be5e-128">不會修改`Nuget.Config`（如那里設定認證）。</span><span class="sxs-lookup"><span data-stu-id="6be5e-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="6be5e-129">控制代碼 HTTP proxy 設定，在其專屬且為 NuGet 不提供外掛程式的 proxy 資訊。</span><span class="sxs-lookup"><span data-stu-id="6be5e-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="6be5e-130">傳回認證或錯誤詳細資料給`nuget.exe`寫入 stdout、 使用 utf-8 編碼的 JSON 回應物件 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="6be5e-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="6be5e-131">選擇性地發出其他的追蹤記錄至 stderr。</span><span class="sxs-lookup"><span data-stu-id="6be5e-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="6be5e-132">密碼應該寫入至 stderr，因為在 「 標準 」 或 「 詳細 」 的詳細資訊層級這類追蹤所 nuget 傳到主控台。</span><span class="sxs-lookup"><span data-stu-id="6be5e-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="6be5e-133">應忽略非預期的參數，提供往後相容性，在未來版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="6be5e-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6be5e-134">輸入的參數</span><span class="sxs-lookup"><span data-stu-id="6be5e-134">Input parameters</span></span>

| <span data-ttu-id="6be5e-135">參數/切換</span><span class="sxs-lookup"><span data-stu-id="6be5e-135">Parameter/Switch</span></span> |<span data-ttu-id="6be5e-136">說明</span><span class="sxs-lookup"><span data-stu-id="6be5e-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="6be5e-137">Uri 的 {value}</span><span class="sxs-lookup"><span data-stu-id="6be5e-137">Uri {value}</span></span> | <span data-ttu-id="6be5e-138">封裝來源 URI 需要認證。</span><span class="sxs-lookup"><span data-stu-id="6be5e-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="6be5e-139">非互動式</span><span class="sxs-lookup"><span data-stu-id="6be5e-139">NonInteractive</span></span> | <span data-ttu-id="6be5e-140">如果有的話，提供者不會發出互動式提示。</span><span class="sxs-lookup"><span data-stu-id="6be5e-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="6be5e-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="6be5e-141">IsRetry</span></span> | <span data-ttu-id="6be5e-142">如果有的話，表示這項嘗試是先前的失敗嘗試的重試。</span><span class="sxs-lookup"><span data-stu-id="6be5e-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="6be5e-143">提供者通常使用這個旗標，以確保它們略過任何現有的快取，並盡可能提示您輸入新的認證。</span><span class="sxs-lookup"><span data-stu-id="6be5e-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="6be5e-144">詳細等級 {value}</span><span class="sxs-lookup"><span data-stu-id="6be5e-144">Verbosity {value}</span></span> | <span data-ttu-id="6be5e-145">如果有的話，下列值之一: 「 標準 」、 「 無訊息 」 或 「 詳細 」。</span><span class="sxs-lookup"><span data-stu-id="6be5e-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="6be5e-146">如果未提供值，預設為"normal"。</span><span class="sxs-lookup"><span data-stu-id="6be5e-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="6be5e-147">提供者應該使用這個選擇性記錄的層級的指示來發出至標準錯誤資料流。</span><span class="sxs-lookup"><span data-stu-id="6be5e-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="6be5e-148">結束代碼</span><span class="sxs-lookup"><span data-stu-id="6be5e-148">Exit codes</span></span>

| <span data-ttu-id="6be5e-149">程式碼</span><span class="sxs-lookup"><span data-stu-id="6be5e-149">Code</span></span> |<span data-ttu-id="6be5e-150">結果</span><span class="sxs-lookup"><span data-stu-id="6be5e-150">Result</span></span> | <span data-ttu-id="6be5e-151">說明</span><span class="sxs-lookup"><span data-stu-id="6be5e-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="6be5e-152">0</span><span class="sxs-lookup"><span data-stu-id="6be5e-152">0</span></span> | <span data-ttu-id="6be5e-153">成功</span><span class="sxs-lookup"><span data-stu-id="6be5e-153">Success</span></span> | <span data-ttu-id="6be5e-154">已成功取得認證，並已寫入至 stdout。</span><span class="sxs-lookup"><span data-stu-id="6be5e-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="6be5e-155">1</span><span class="sxs-lookup"><span data-stu-id="6be5e-155">1</span></span> | <span data-ttu-id="6be5e-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="6be5e-156">ProviderNotApplicable</span></span> | <span data-ttu-id="6be5e-157">目前的提供者不提供認證指定的 uri。</span><span class="sxs-lookup"><span data-stu-id="6be5e-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="6be5e-158">2</span><span class="sxs-lookup"><span data-stu-id="6be5e-158">2</span></span> | <span data-ttu-id="6be5e-159">失敗</span><span class="sxs-lookup"><span data-stu-id="6be5e-159">Failure</span></span> | <span data-ttu-id="6be5e-160">提供者是正確的提供者指定的 uri，但無法提供認證。</span><span class="sxs-lookup"><span data-stu-id="6be5e-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="6be5e-161">在此情況下，nuget.exe 將不會重試驗證，而且會失敗。</span><span class="sxs-lookup"><span data-stu-id="6be5e-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="6be5e-162">典型的範例是當使用者取消互動式登入。</span><span class="sxs-lookup"><span data-stu-id="6be5e-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="6be5e-163">標準輸出</span><span class="sxs-lookup"><span data-stu-id="6be5e-163">Standard output</span></span>

| <span data-ttu-id="6be5e-164">屬性</span><span class="sxs-lookup"><span data-stu-id="6be5e-164">Property</span></span> |<span data-ttu-id="6be5e-165">注意</span><span class="sxs-lookup"><span data-stu-id="6be5e-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="6be5e-166">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="6be5e-166">Username</span></span> | <span data-ttu-id="6be5e-167">已驗證要求的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6be5e-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="6be5e-168">密碼</span><span class="sxs-lookup"><span data-stu-id="6be5e-168">Password</span></span> | <span data-ttu-id="6be5e-169">已驗證要求的密碼。</span><span class="sxs-lookup"><span data-stu-id="6be5e-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="6be5e-170">訊息</span><span class="sxs-lookup"><span data-stu-id="6be5e-170">Message</span></span> | <span data-ttu-id="6be5e-171">選擇性回應，只能用來顯示其他詳細資料中的失敗情況相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6be5e-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="6be5e-172">範例 stdout:</span><span class="sxs-lookup"><span data-stu-id="6be5e-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="6be5e-173">疑難排解認證提供者</span><span class="sxs-lookup"><span data-stu-id="6be5e-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="6be5e-174">目前，NuGet 不直接支援的偵錯提供自訂認證提供者;[發出 4598](https://github.com/NuGet/Home/issues/4598)是否會追蹤這項工作。</span><span class="sxs-lookup"><span data-stu-id="6be5e-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="6be5e-175">您也可以進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6be5e-175">You can also do the following:</span></span>

- <span data-ttu-id="6be5e-176">執行與 nuget.exe`-verbosity`檢查詳細的輸出參數。</span><span class="sxs-lookup"><span data-stu-id="6be5e-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="6be5e-177">加入至偵錯訊息`stdout`適當位置。</span><span class="sxs-lookup"><span data-stu-id="6be5e-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="6be5e-178">請確定您使用 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6be5e-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="6be5e-179">附加偵錯工具在啟動時，此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="6be5e-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="6be5e-180">取得進一步的協助，[提交支援要求 nuget.org](https://www.nuget.org/policies/Contact)。</span><span class="sxs-lookup"><span data-stu-id="6be5e-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
