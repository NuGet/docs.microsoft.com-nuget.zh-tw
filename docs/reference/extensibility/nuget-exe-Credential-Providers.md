---
title: nuget.exe 認證提供者
description: nuget.exe 認證提供者驗證摘要，並會實作為命令列可執行檔，請遵循特定的慣例。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550185"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="c2640-103">Nuget.exe 認證提供者使用的驗證摘要</span><span class="sxs-lookup"><span data-stu-id="c2640-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="c2640-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="c2640-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="c2640-105">當`nuget.exe`需要認證以驗證摘要，它們看起來如下：</span><span class="sxs-lookup"><span data-stu-id="c2640-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="c2640-106">中的認證會先尋找 NuGet`Nuget.Config`檔案。</span><span class="sxs-lookup"><span data-stu-id="c2640-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="c2640-107">NuGet 接著會使用外掛程式認證提供者，受限於下面所列的順序。</span><span class="sxs-lookup"><span data-stu-id="c2640-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="c2640-108">(範例中，而且[Visual Studio Team Services 認證提供者](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)</span><span class="sxs-lookup"><span data-stu-id="c2640-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="c2640-109">NuGet 接著會提示使用者輸入認證，在命令列上。</span><span class="sxs-lookup"><span data-stu-id="c2640-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="c2640-110">請注意，此處所述的認證提供者只能在運作`nuget.exe`而不是在 'dotnet restore' 或 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c2640-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="c2640-111">對於使用 Visual Studio 的認證提供者，請參閱[nuget.exe 認證提供者，適用於 Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="c2640-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="c2640-112">nuget.exe 認證提供者可以用於 3 種方式：</span><span class="sxs-lookup"><span data-stu-id="c2640-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="c2640-113">**全域**： 將認證提供者提供的所有執行個體`nuget.exe`目前的使用者設定檔之下執行，請將它新增至`%LocalAppData%\NuGet\CredentialProviders`。</span><span class="sxs-lookup"><span data-stu-id="c2640-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="c2640-114">您可能需要建立`CredentialProviders`資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2640-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="c2640-115">認證提供者可以安裝根目錄的`CredentialProviders`資料夾或子資料夾內。</span><span class="sxs-lookup"><span data-stu-id="c2640-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="c2640-116">如果認證提供者有多個檔案/組件，您可以使用子資料夾，將組織的提供者。</span><span class="sxs-lookup"><span data-stu-id="c2640-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="c2640-117">**從環境變數**： 認證提供者可以儲存在任何地方，並供`nuget.exe`藉由設定`%NUGET_CREDENTIALPROVIDERS_PATH%`環境變數，以提供者位置。</span><span class="sxs-lookup"><span data-stu-id="c2640-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="c2640-118">這個變數可以是以分號分隔的清單 (例如`path1;path2`) 如果您有多個位置。</span><span class="sxs-lookup"><span data-stu-id="c2640-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="c2640-119">**與 nuget.exe**: nuget.exe 認證提供者可以放在相同的資料夾`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="c2640-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="c2640-120">正在載入認證提供者，當`nuget.exe`搜尋上述的位置，讓任何名為檔案`credentialprovider*.exe`，然後將這些檔案在發現的順序。</span><span class="sxs-lookup"><span data-stu-id="c2640-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="c2640-121">如果多個認證提供者存在於相同的資料夾，它們是依字母順序排列的順序載入。</span><span class="sxs-lookup"><span data-stu-id="c2640-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="c2640-122">建立 nuget.exe 認證提供者</span><span class="sxs-lookup"><span data-stu-id="c2640-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="c2640-123">認證提供者是命令列可執行檔，在表單名為`CredentialProvider*.exe`，會收集輸入、 取得視需要的認證，則會傳回適當的結束狀態碼和標準輸出。</span><span class="sxs-lookup"><span data-stu-id="c2640-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="c2640-124">提供者必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="c2640-124">A provider must do the following:</span></span>

- <span data-ttu-id="c2640-125">判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。</span><span class="sxs-lookup"><span data-stu-id="c2640-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="c2640-126">如果沒有，它應該會傳回狀態碼為 1 以不含認證。</span><span class="sxs-lookup"><span data-stu-id="c2640-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="c2640-127">不會修改`Nuget.Config`（如那里設定認證）。</span><span class="sxs-lookup"><span data-stu-id="c2640-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="c2640-128">在它自己，做為 NuGet 上的控制代碼 HTTP proxy 設定不提供外掛程式的 proxy 資訊。</span><span class="sxs-lookup"><span data-stu-id="c2640-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="c2640-129">傳回認證或錯誤詳細資料，以`nuget.exe`藉由將寫入 stdout，使用 utf-8 編碼的 JSON 回應物件 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="c2640-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="c2640-130">選擇性地發出額外的追蹤記錄至 stderr。</span><span class="sxs-lookup"><span data-stu-id="c2640-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="c2640-131">沒有祕密應寫入到 stderr，因為 「 標準 」 或 「 詳細 」 的詳細資訊層級這類追蹤由 NuGet 回應到主控台。</span><span class="sxs-lookup"><span data-stu-id="c2640-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="c2640-132">未預期的參數應該予以忽略，提供往後相容性與未來版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="c2640-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c2640-133">輸入的參數</span><span class="sxs-lookup"><span data-stu-id="c2640-133">Input parameters</span></span>

| <span data-ttu-id="c2640-134">參數/切換</span><span class="sxs-lookup"><span data-stu-id="c2640-134">Parameter/Switch</span></span> |<span data-ttu-id="c2640-135">描述</span><span class="sxs-lookup"><span data-stu-id="c2640-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="c2640-136">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="c2640-136">Uri {value}</span></span> | <span data-ttu-id="c2640-137">封裝來源 URI 需要認證。</span><span class="sxs-lookup"><span data-stu-id="c2640-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="c2640-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c2640-138">NonInteractive</span></span> | <span data-ttu-id="c2640-139">如果有的話，提供者不會發出互動式提示。</span><span class="sxs-lookup"><span data-stu-id="c2640-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="c2640-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="c2640-140">IsRetry</span></span> | <span data-ttu-id="c2640-141">如果存在，表示這項嘗試是重試先前失敗的嘗試。</span><span class="sxs-lookup"><span data-stu-id="c2640-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="c2640-142">提供者通常會使用這個旗標，確保他們略過任何現有的快取，並提示您輸入新認證的話。</span><span class="sxs-lookup"><span data-stu-id="c2640-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="c2640-143">{Value} 的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c2640-143">Verbosity {value}</span></span> | <span data-ttu-id="c2640-144">如果有的話，下列值之一: 「 標準 」、 「 靜音 」 或 「 詳細 」。</span><span class="sxs-lookup"><span data-stu-id="c2640-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="c2640-145">如果未提供值，則會預設為 「 正常 」。</span><span class="sxs-lookup"><span data-stu-id="c2640-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="c2640-146">提供者應該以此做為選擇性的記錄層級表示會發送至標準錯誤資料流。</span><span class="sxs-lookup"><span data-stu-id="c2640-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="c2640-147">結束代碼</span><span class="sxs-lookup"><span data-stu-id="c2640-147">Exit codes</span></span>

| <span data-ttu-id="c2640-148">程式碼</span><span class="sxs-lookup"><span data-stu-id="c2640-148">Code</span></span> |<span data-ttu-id="c2640-149">結果</span><span class="sxs-lookup"><span data-stu-id="c2640-149">Result</span></span> | <span data-ttu-id="c2640-150">描述</span><span class="sxs-lookup"><span data-stu-id="c2640-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="c2640-151">0</span><span class="sxs-lookup"><span data-stu-id="c2640-151">0</span></span> | <span data-ttu-id="c2640-152">成功</span><span class="sxs-lookup"><span data-stu-id="c2640-152">Success</span></span> | <span data-ttu-id="c2640-153">已成功取得認證，而且已寫入至 stdout。</span><span class="sxs-lookup"><span data-stu-id="c2640-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="c2640-154">1</span><span class="sxs-lookup"><span data-stu-id="c2640-154">1</span></span> | <span data-ttu-id="c2640-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="c2640-155">ProviderNotApplicable</span></span> | <span data-ttu-id="c2640-156">目前的提供者不提供指定之 URI 的認證。</span><span class="sxs-lookup"><span data-stu-id="c2640-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="c2640-157">2</span><span class="sxs-lookup"><span data-stu-id="c2640-157">2</span></span> | <span data-ttu-id="c2640-158">失敗</span><span class="sxs-lookup"><span data-stu-id="c2640-158">Failure</span></span> | <span data-ttu-id="c2640-159">提供者是正確的提供者指定的 uri，但無法提供認證。</span><span class="sxs-lookup"><span data-stu-id="c2640-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="c2640-160">在此情況下，nuget.exe 會將不會重試驗證，而且會失敗。</span><span class="sxs-lookup"><span data-stu-id="c2640-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="c2640-161">當使用者取消互動式登入，就會是一個典型的例子。</span><span class="sxs-lookup"><span data-stu-id="c2640-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="c2640-162">標準輸出</span><span class="sxs-lookup"><span data-stu-id="c2640-162">Standard output</span></span>

| <span data-ttu-id="c2640-163">屬性</span><span class="sxs-lookup"><span data-stu-id="c2640-163">Property</span></span> |<span data-ttu-id="c2640-164">注意</span><span class="sxs-lookup"><span data-stu-id="c2640-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="c2640-165">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="c2640-165">Username</span></span> | <span data-ttu-id="c2640-166">已驗證要求的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c2640-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="c2640-167">密碼</span><span class="sxs-lookup"><span data-stu-id="c2640-167">Password</span></span> | <span data-ttu-id="c2640-168">已驗證要求的密碼。</span><span class="sxs-lookup"><span data-stu-id="c2640-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="c2640-169">訊息</span><span class="sxs-lookup"><span data-stu-id="c2640-169">Message</span></span> | <span data-ttu-id="c2640-170">選用的回應，只能用來在失敗情況下顯示其他詳細資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c2640-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="c2640-171">範例 stdout:</span><span class="sxs-lookup"><span data-stu-id="c2640-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="c2640-172">疑難排解認證提供者</span><span class="sxs-lookup"><span data-stu-id="c2640-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="c2640-173">目前，NuGet 不進行偵錯自訂認證提供者，提供更直接的支援[發出 4598](https://github.com/NuGet/Home/issues/4598)正在追蹤這項工作。</span><span class="sxs-lookup"><span data-stu-id="c2640-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="c2640-174">您也可以進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c2640-174">You can also do the following:</span></span>

- <span data-ttu-id="c2640-175">執行使用 nuget.exe`-verbosity`切換參數來檢查詳細的輸出。</span><span class="sxs-lookup"><span data-stu-id="c2640-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="c2640-176">新增偵錯訊息`stdout`適當位置。</span><span class="sxs-lookup"><span data-stu-id="c2640-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="c2640-177">請確定您使用 nuget.exe 3.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c2640-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="c2640-178">附加偵錯工具在啟動時，此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="c2640-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="c2640-179">進一步的說明，請[提交支援要求 nuget.org](https://www.nuget.org/policies/Contact)。</span><span class="sxs-lookup"><span data-stu-id="c2640-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
