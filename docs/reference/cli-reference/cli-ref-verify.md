---
title: NuGet CLI 驗證命令
description: nuget.exe verify 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622599"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="ecb53-103">確認 (NuGet CLI 的命令) </span><span class="sxs-lookup"><span data-stu-id="ecb53-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="ecb53-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="ecb53-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="ecb53-105">驗證套件。</span><span class="sxs-lookup"><span data-stu-id="ecb53-105">Verifies a package.</span></span>

<span data-ttu-id="ecb53-106">.NET Core、Mono 或非 Windows 平臺上尚未支援已簽署套件的驗證。</span><span class="sxs-lookup"><span data-stu-id="ecb53-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="ecb53-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="ecb53-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="ecb53-108">其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="ecb53-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="ecb53-109">nuget 驗證-全部</span><span class="sxs-lookup"><span data-stu-id="ecb53-109">nuget verify -All</span></span>

<span data-ttu-id="ecb53-110">指定所有可能的驗證都應該在封裝 (s) 上執行。</span><span class="sxs-lookup"><span data-stu-id="ecb53-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="ecb53-111">nuget 驗證-簽章</span><span class="sxs-lookup"><span data-stu-id="ecb53-111">nuget verify -Signatures</span></span>

<span data-ttu-id="ecb53-112">指定應執行封裝簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="ecb53-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="ecb53-113">「驗證簽章」的選項</span><span class="sxs-lookup"><span data-stu-id="ecb53-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="ecb53-114">指定憑證 (s 的一或多個 256 SHA-1 憑證指紋，) 簽署的套件必須使用簽署。</span><span class="sxs-lookup"><span data-stu-id="ecb53-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="ecb53-115">憑證 256 SHA-1 指紋是憑證的 SHA-256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="ecb53-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="ecb53-116">多個輸入應以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="ecb53-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="ecb53-117">選項。</span><span class="sxs-lookup"><span data-stu-id="ecb53-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ecb53-118">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ecb53-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ecb53-119">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="ecb53-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ecb53-120">使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="ecb53-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ecb53-121">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="ecb53-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ecb53-122">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="ecb53-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ecb53-123">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="ecb53-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="ecb53-124">範例</span><span class="sxs-lookup"><span data-stu-id="ecb53-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```