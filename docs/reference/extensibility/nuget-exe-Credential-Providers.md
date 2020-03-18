---
title: nuget.exe 認證提供者
description: nuget.exe 認證提供者會使用摘要進行驗證，並實作為遵循特定慣例的命令列可執行檔。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428720"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="da423-103">使用 nuget.exe 認證提供者驗證摘要</span><span class="sxs-lookup"><span data-stu-id="da423-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="da423-104">已針對 `nuget.exe` 特定的認證提供者加入版本 `3.3` 支援。</span><span class="sxs-lookup"><span data-stu-id="da423-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="da423-105">之後，在版本中 `4.8` 支援在所有命令列案例（`nuget.exe`、`dotnet.exe`、`msbuild.exe`）上工作的[認證提供者](NuGet-Cross-Platform-Authentication-Plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="da423-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="da423-106">如需有關 `nuget.exe` 的所有驗證方法的詳細資訊，請參閱[使用來自已驗證](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)摘要的套件</span><span class="sxs-lookup"><span data-stu-id="da423-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="da423-107">nuget.exe 認證提供者探索</span><span class="sxs-lookup"><span data-stu-id="da423-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="da423-108">nuget.exe 認證提供者可透過三種方式來使用：</span><span class="sxs-lookup"><span data-stu-id="da423-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="da423-109">**全域**：若要讓 `nuget.exe` 的所有實例都能使用認證提供者，請在目前使用者的設定檔下，將其新增至 `%LocalAppData%\NuGet\CredentialProviders`。</span><span class="sxs-lookup"><span data-stu-id="da423-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="da423-110">您可能需要建立 `CredentialProviders` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="da423-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="da423-111">認證提供者可以安裝在 `CredentialProviders` 資料夾的根目錄或子資料夾內。</span><span class="sxs-lookup"><span data-stu-id="da423-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="da423-112">如果認證提供者有多個檔案/元件，您可以使用子資料夾來保留提供者的組織。</span><span class="sxs-lookup"><span data-stu-id="da423-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="da423-113">**從環境變數**：認證提供者可以儲存在任何位置，並可透過將 `%NUGET_CREDENTIALPROVIDERS_PATH%` 環境變數設定為提供者位置，以供 `nuget.exe` 存取。</span><span class="sxs-lookup"><span data-stu-id="da423-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="da423-114">如果您有多個位置，此變數可以是以分號分隔的清單（例如，`path1;path2`）。</span><span class="sxs-lookup"><span data-stu-id="da423-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="da423-115">與**Nuget.exe 並存**： nuget.exe 認證提供者可以放在與 `nuget.exe`相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="da423-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="da423-116">載入認證提供者時，`nuget.exe` 會依序在上述位置搜尋任何名為 `credentialprovider*.exe`的檔案，然後依照找到的順序載入這些檔案。</span><span class="sxs-lookup"><span data-stu-id="da423-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="da423-117">如果同一個資料夾中有多個認證提供者，就會依字母順序載入。</span><span class="sxs-lookup"><span data-stu-id="da423-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="da423-118">建立 nuget.exe 認證提供者</span><span class="sxs-lookup"><span data-stu-id="da423-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="da423-119">認證提供者是一種命令列可執行檔，以 `CredentialProvider*.exe`的形式命名，以收集輸入、取得適當的認證，然後傳回適當的結束狀態碼和標準輸出。</span><span class="sxs-lookup"><span data-stu-id="da423-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="da423-120">提供者必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="da423-120">A provider must do the following:</span></span>

- <span data-ttu-id="da423-121">判斷它是否可以在起始認證之前，提供目標 URI 的認證。</span><span class="sxs-lookup"><span data-stu-id="da423-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="da423-122">如果不是，它應該會傳回狀態碼1，而不會有任何認證。</span><span class="sxs-lookup"><span data-stu-id="da423-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="da423-123">不修改 `Nuget.Config` （例如在該處設定認證）。</span><span class="sxs-lookup"><span data-stu-id="da423-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="da423-124">自行處理 HTTP proxy 設定，因為 NuGet 不會提供 proxy 資訊給外掛程式。</span><span class="sxs-lookup"><span data-stu-id="da423-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="da423-125">使用 UTF-8 編碼將 JSON 回應物件（如下所示）寫入至 stdout，以將認證或錯誤詳細資料傳回 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="da423-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="da423-126">選擇性地對 stderr 發出額外的追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="da423-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="da423-127">不應該將任何秘密寫入 stderr，因為在詳細資訊層級「正常」或「詳細」的情況下，NuGet 會將這類追蹤回應到主控台。</span><span class="sxs-lookup"><span data-stu-id="da423-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="da423-128">應該忽略未預期的參數，以提供與未來 NuGet 版本的向前相容性。</span><span class="sxs-lookup"><span data-stu-id="da423-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da423-129">輸入參數</span><span class="sxs-lookup"><span data-stu-id="da423-129">Input parameters</span></span>

| <span data-ttu-id="da423-130">參數/切換</span><span class="sxs-lookup"><span data-stu-id="da423-130">Parameter/Switch</span></span> |<span data-ttu-id="da423-131">描述</span><span class="sxs-lookup"><span data-stu-id="da423-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="da423-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="da423-132">Uri {value}</span></span> | <span data-ttu-id="da423-133">需要認證的套件來源 URI。</span><span class="sxs-lookup"><span data-stu-id="da423-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="da423-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="da423-134">NonInteractive</span></span> | <span data-ttu-id="da423-135">提供者不會發出互動式提示（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="da423-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="da423-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="da423-136">IsRetry</span></span> | <span data-ttu-id="da423-137">如果存在，表示此嘗試是先前嘗試失敗的重試。</span><span class="sxs-lookup"><span data-stu-id="da423-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="da423-138">提供者通常會使用此旗標來確保其略過任何現有的快取，並在可能的情況下提示您輸入新的認證</span><span class="sxs-lookup"><span data-stu-id="da423-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="da423-139">詳細資訊 {值}</span><span class="sxs-lookup"><span data-stu-id="da423-139">Verbosity {value}</span></span> | <span data-ttu-id="da423-140">如果有，則會出現下列其中一個值：「normal」、「quiet」或「詳細」。</span><span class="sxs-lookup"><span data-stu-id="da423-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="da423-141">如果未提供任何值，則預設為「正常」。</span><span class="sxs-lookup"><span data-stu-id="da423-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="da423-142">提供者應該使用此來表示要發出至標準錯誤資料流程的選擇性記錄層級。</span><span class="sxs-lookup"><span data-stu-id="da423-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="da423-143">結束代碼</span><span class="sxs-lookup"><span data-stu-id="da423-143">Exit codes</span></span>

| <span data-ttu-id="da423-144">程式碼</span><span class="sxs-lookup"><span data-stu-id="da423-144">Code</span></span> |<span data-ttu-id="da423-145">結果</span><span class="sxs-lookup"><span data-stu-id="da423-145">Result</span></span> | <span data-ttu-id="da423-146">描述</span><span class="sxs-lookup"><span data-stu-id="da423-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="da423-147">0</span><span class="sxs-lookup"><span data-stu-id="da423-147">0</span></span> | <span data-ttu-id="da423-148">成功</span><span class="sxs-lookup"><span data-stu-id="da423-148">Success</span></span> | <span data-ttu-id="da423-149">已成功取得認證，並已將其寫入至 stdout。</span><span class="sxs-lookup"><span data-stu-id="da423-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="da423-150">1</span><span class="sxs-lookup"><span data-stu-id="da423-150">1</span></span> | <span data-ttu-id="da423-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="da423-151">ProviderNotApplicable</span></span> | <span data-ttu-id="da423-152">目前的提供者未提供指定 URI 的認證。</span><span class="sxs-lookup"><span data-stu-id="da423-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="da423-153">2</span><span class="sxs-lookup"><span data-stu-id="da423-153">2</span></span> | <span data-ttu-id="da423-154">失敗</span><span class="sxs-lookup"><span data-stu-id="da423-154">Failure</span></span> | <span data-ttu-id="da423-155">提供者是指定 URI 的正確提供者，但無法提供認證。</span><span class="sxs-lookup"><span data-stu-id="da423-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="da423-156">在此情況下，nuget.exe 將不會重試驗證，而且將會失敗。</span><span class="sxs-lookup"><span data-stu-id="da423-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="da423-157">一般的範例是當使用者取消互動式登入時。</span><span class="sxs-lookup"><span data-stu-id="da423-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="da423-158">標準輸出</span><span class="sxs-lookup"><span data-stu-id="da423-158">Standard output</span></span>

| <span data-ttu-id="da423-159">屬性</span><span class="sxs-lookup"><span data-stu-id="da423-159">Property</span></span> |<span data-ttu-id="da423-160">注意事項</span><span class="sxs-lookup"><span data-stu-id="da423-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="da423-161">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="da423-161">Username</span></span> | <span data-ttu-id="da423-162">已驗證要求的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="da423-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="da423-163">Password</span><span class="sxs-lookup"><span data-stu-id="da423-163">Password</span></span> | <span data-ttu-id="da423-164">已驗證要求的密碼。</span><span class="sxs-lookup"><span data-stu-id="da423-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="da423-165">訊息</span><span class="sxs-lookup"><span data-stu-id="da423-165">Message</span></span> | <span data-ttu-id="da423-166">關於回應的選擇性詳細資料，僅用於顯示失敗案例中的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="da423-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="da423-167">範例 stdout：</span><span class="sxs-lookup"><span data-stu-id="da423-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="da423-168">針對認證提供者進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="da423-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="da423-169">目前，NuGet 並不提供對自訂認證提供者的多個直接支援，[問題 4598](https://github.com/NuGet/Home/issues/4598)正在追蹤此工作。</span><span class="sxs-lookup"><span data-stu-id="da423-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="da423-170">您也可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="da423-170">You can also do the following:</span></span>

- <span data-ttu-id="da423-171">使用 `-verbosity` 參數執行 nuget.exe，以檢查詳細輸出。</span><span class="sxs-lookup"><span data-stu-id="da423-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="da423-172">將 [調試訊息] 加入至適當位置中的 `stdout`。</span><span class="sxs-lookup"><span data-stu-id="da423-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="da423-173">請確定您使用的是 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="da423-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="da423-174">在啟動時使用此程式碼片段附加偵錯工具：</span><span class="sxs-lookup"><span data-stu-id="da423-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
