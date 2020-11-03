---
title: NuGet CLI 驗證命令
description: nuget.exe verify 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238136"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="a7736-103">確認 (NuGet CLI 的命令) </span><span class="sxs-lookup"><span data-stu-id="a7736-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="a7736-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a7736-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a7736-105">驗證套件。</span><span class="sxs-lookup"><span data-stu-id="a7736-105">Verifies a package.</span></span>

<span data-ttu-id="a7736-106">Mono 下尚未支援已簽署套件的驗證。</span><span class="sxs-lookup"><span data-stu-id="a7736-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="a7736-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="a7736-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="a7736-108">其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="a7736-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="a7736-109">nuget 驗證-全部</span><span class="sxs-lookup"><span data-stu-id="a7736-109">nuget verify -All</span></span>

<span data-ttu-id="a7736-110">指定所有可能的驗證都應該在封裝 (s) 上執行。</span><span class="sxs-lookup"><span data-stu-id="a7736-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="a7736-111">nuget 驗證-簽章</span><span class="sxs-lookup"><span data-stu-id="a7736-111">nuget verify -Signatures</span></span>

<span data-ttu-id="a7736-112">指定應執行封裝簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="a7736-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="a7736-113">「驗證簽章」的選項</span><span class="sxs-lookup"><span data-stu-id="a7736-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a7736-114">指定憑證 (s 的一或多個 256 SHA-1 憑證指紋，) 簽署的套件必須使用簽署。</span><span class="sxs-lookup"><span data-stu-id="a7736-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="a7736-115">憑證 256 SHA-1 指紋是憑證的 SHA-256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="a7736-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="a7736-116">多個輸入應以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="a7736-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="a7736-117">選項</span><span class="sxs-lookup"><span data-stu-id="a7736-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a7736-118">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a7736-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a7736-119">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="a7736-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a7736-120">使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a7736-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a7736-121">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="a7736-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a7736-122">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="a7736-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a7736-123">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="a7736-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="a7736-124">範例</span><span class="sxs-lookup"><span data-stu-id="a7736-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```