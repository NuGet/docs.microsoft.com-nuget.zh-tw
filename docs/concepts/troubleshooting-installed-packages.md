---
title: 針對已安裝的套件進行疑難排解
description: 如何尋找用於個別套件的套件來源
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387546"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="d3b6d-103">針對已安裝的套件進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d3b6d-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="d3b6d-104">有時您可能會想要驗證特定封裝的安裝來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="d3b6d-105">以下是您可以檢查的一些方式。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="d3b6d-106">某些套件來源支援稱為上游來源的概念。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="d3b6d-107">例如， [Azure Artifacts 上游來源](/azure/devops/artifacts/concepts/upstream-sources)。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="d3b6d-108">NuGet 用戶端不知道封裝是否來自上游來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="d3b6d-109">因此，任何套件來源的記錄都會列出已設定的來源，而不是上游來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="d3b6d-110">`.nupkg.metadata` [全域封裝] 資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="d3b6d-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="d3b6d-111">當封裝解壓縮至 *全域套件* 資料夾時， `.nupkg.metadata` 會寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="d3b6d-112">從 NuGet 5.9.0 開始，NuGet 會新增套件來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="d3b6d-113">請參閱下文，將 NuGet 版本對應至 Visual Studio 或 .NET SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="d3b6d-114">例如：</span><span class="sxs-lookup"><span data-stu-id="d3b6d-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="d3b6d-115">如果您的 *全域套件* 資料夾已在升級至具有 NuGet 5.9.0 的較新版本工具之前解壓縮封裝，則該檔案 `.nupkg.metadata` 將會是第1版，而且不會包含套件來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="d3b6d-116">您可以 [清除 *全域套件* 資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) ，以確保所有套件都包含套件來源。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="d3b6d-117">NuGet 只會將檔案寫入 `.nupkg.metadata` 至 *全域套件* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="d3b6d-118">使用 `packages.config` 的專案會使用 [方案套件] 資料夾，但不會建立檔案 `.nupkg.metadata` 。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="d3b6d-119">已安裝的套件記錄檔訊息</span><span class="sxs-lookup"><span data-stu-id="d3b6d-119">Installed package log message</span></span>

<span data-ttu-id="d3b6d-120">從 NuGet 5.9.0 開始，NuGet 會在還原訊息中輸出封裝來源，通知已安裝套件。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="d3b6d-121">例如：</span><span class="sxs-lookup"><span data-stu-id="d3b6d-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="d3b6d-122">此訊息是正常/資訊詳細資訊的輸出。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="d3b6d-123">Visual Studio 和 `dotnet` CLI 預設為最基本的詳細資訊，因此預設不會顯示此訊息。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="d3b6d-124">`msbuild`和 `nuget` CLI 工具預設為正常詳細程度，因此預設會顯示此訊息。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="d3b6d-125">HTTP 記錄檔訊息</span><span class="sxs-lookup"><span data-stu-id="d3b6d-125">HTTP log message</span></span>

<span data-ttu-id="d3b6d-126">當套件無法在本機使用時（在 *全域套件* 資料夾、回溯資料夾或本機檔案來源中），NuGet 會從任何已設定的套件來源（透過 HTTP）下載。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="d3b6d-127">HTTP 要求和回應會記錄在一般詳細資訊層級，而且您應該只會看到每個套件版本的單一要求和回應。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="d3b6d-128">例如：</span><span class="sxs-lookup"><span data-stu-id="d3b6d-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="d3b6d-129">如果檔案是最近下載的，則可能會從 NuGet 的 *HTTP* 快取中取出</span><span class="sxs-lookup"><span data-stu-id="d3b6d-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="d3b6d-130">不同 NuGet HTTP 伺服器的執行方式，以及它是否正在執行 NuGet V2 或 V3 HTTP 通訊協定，可能會有不同的 URL 格式。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="d3b6d-131">如果您 `nuget.config` 已定義多個 HTTP 來源，您會看到每個套件檔案的多個要求 `index.json` ，每個來源各一個。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="d3b6d-132">但是套件的每個版本都只會有一個 `nupkg` 下載。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="d3b6d-133">封裝簽名記錄訊息</span><span class="sxs-lookup"><span data-stu-id="d3b6d-133">Package signature log message</span></span>

<span data-ttu-id="d3b6d-134">如果要下載的套件經過簽署，NuGet 將會驗證簽章，並在詳細的詳細資訊中記錄下列訊息：</span><span class="sxs-lookup"><span data-stu-id="d3b6d-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="d3b6d-135">系統會報告是否已從 HTTP 套件來源下載封裝，或從本機套件來源複製該封裝。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="d3b6d-136">如果封裝已可在 [ *全域封裝* ] 資料夾或 [fallback] 資料夾中使用，則不會輸出。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="d3b6d-137">由於 [移除 VERISIGN CA NuGet 的信任](https://github.com/dotnet/announcements/issues/180) ，在特定的 NuGet 和 .net SDK 版本中，已停用特定平臺上已簽署的套件驗證。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="d3b6d-138">因此，相同的套件可能會有 `PackageSignatureVerificationLog` 記錄檔，或可能遺失這些記錄檔，這取決於您正在執行還原的平臺，以及您所使用的 .net 或 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="d3b6d-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="d3b6d-139">NuGet 版本對應</span><span class="sxs-lookup"><span data-stu-id="d3b6d-139">NuGet Version Map</span></span>

<span data-ttu-id="d3b6d-140">下列版本的 NuGet 有關于套件來源記錄的重要變更：</span><span class="sxs-lookup"><span data-stu-id="d3b6d-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="d3b6d-141">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="d3b6d-141">NuGet Version</span></span>|<span data-ttu-id="d3b6d-142">Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="d3b6d-142">Visual Studio Version</span></span>|<span data-ttu-id="d3b6d-143">.NET SDK 版本</span><span class="sxs-lookup"><span data-stu-id="d3b6d-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="d3b6d-144">NuGet 5.9。0</span><span class="sxs-lookup"><span data-stu-id="d3b6d-144">NuGet 5.9.0</span></span>|<span data-ttu-id="d3b6d-145">Visual Studio 2019 16.9。0</span><span class="sxs-lookup"><span data-stu-id="d3b6d-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="d3b6d-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="d3b6d-146">.NET 5 SDK 5.0.200</span></span>|
