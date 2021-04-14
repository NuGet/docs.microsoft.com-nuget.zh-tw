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
# <a name="troubleshooting-installed-packages"></a>針對已安裝的套件進行疑難排解

有時您可能會想要驗證特定封裝的安裝來源。 以下是您可以檢查的一些方式。

> [!Note]
> 某些套件來源支援稱為上游來源的概念。 例如， [Azure Artifacts 上游來源](/azure/devops/artifacts/concepts/upstream-sources)。 NuGet 用戶端不知道封裝是否來自上游來源。 因此，任何套件來源的記錄都會列出已設定的來源，而不是上游來源。

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` [全域封裝] 資料夾中的檔案

當封裝解壓縮至 *全域套件* 資料夾時， `.nupkg.metadata` 會寫入檔案。 從 NuGet 5.9.0 開始，NuGet 會新增套件來源。 請參閱下文，將 NuGet 版本對應至 Visual Studio 或 .NET SDK 版本。 例如：

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> 如果您的 *全域套件* 資料夾已在升級至具有 NuGet 5.9.0 的較新版本工具之前解壓縮封裝，則該檔案 `.nupkg.metadata` 將會是第1版，而且不會包含套件來源。 您可以 [清除 *全域套件* 資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) ，以確保所有套件都包含套件來源。

> [!Tip]
> NuGet 只會將檔案寫入 `.nupkg.metadata` 至 *全域套件* 資料夾。 使用 `packages.config` 的專案會使用 [方案套件] 資料夾，但不會建立檔案 `.nupkg.metadata` 。

## <a name="installed-package-log-message"></a>已安裝的套件記錄檔訊息

從 NuGet 5.9.0 開始，NuGet 會在還原訊息中輸出封裝來源，通知已安裝套件。 例如：

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> 此訊息是正常/資訊詳細資訊的輸出。 Visual Studio 和 `dotnet` CLI 預設為最基本的詳細資訊，因此預設不會顯示此訊息。 `msbuild`和 `nuget` CLI 工具預設為正常詳細程度，因此預設會顯示此訊息。

## <a name="http-log-message"></a>HTTP 記錄檔訊息

當套件無法在本機使用時（在 *全域套件* 資料夾、回溯資料夾或本機檔案來源中），NuGet 會從任何已設定的套件來源（透過 HTTP）下載。 HTTP 要求和回應會記錄在一般詳細資訊層級，而且您應該只會看到每個套件版本的單一要求和回應。 例如：

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

如果檔案是最近下載的，則可能會從 NuGet 的 *HTTP* 快取中取出

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

不同 NuGet HTTP 伺服器的執行方式，以及它是否正在執行 NuGet V2 或 V3 HTTP 通訊協定，可能會有不同的 URL 格式。

如果您 `nuget.config` 已定義多個 HTTP 來源，您會看到每個套件檔案的多個要求 `index.json` ，每個來源各一個。 但是套件的每個版本都只會有一個 `nupkg` 下載。

## <a name="package-signature-log-message"></a>封裝簽名記錄訊息

如果要下載的套件經過簽署，NuGet 將會驗證簽章，並在詳細的詳細資訊中記錄下列訊息：

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

系統會報告是否已從 HTTP 套件來源下載封裝，或從本機套件來源複製該封裝。 如果封裝已可在 [ *全域封裝* ] 資料夾或 [fallback] 資料夾中使用，則不會輸出。

> [!Important]
> 由於 [移除 VERISIGN CA NuGet 的信任](https://github.com/dotnet/announcements/issues/180) ，在特定的 NuGet 和 .net SDK 版本中，已停用特定平臺上已簽署的套件驗證。 因此，相同的套件可能會有 `PackageSignatureVerificationLog` 記錄檔，或可能遺失這些記錄檔，這取決於您正在執行還原的平臺，以及您所使用的 .net 或 NuGet 版本。

## <a name="nuget-version-map"></a>NuGet 版本對應

下列版本的 NuGet 有關于套件來源記錄的重要變更：

|NuGet 版本|Visual Studio 版本|.NET SDK 版本|
|---|---|---|
|NuGet 5.9。0|Visual Studio 2019 16.9。0|.NET 5 SDK 5.0.200|
