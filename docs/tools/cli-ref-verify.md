---
title: NuGet CLI 確認命令
description: Nuget.exe 的參考會確認命令
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545209"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="789e7-103">verify 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="789e7-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="789e7-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="789e7-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="789e7-105">驗證封裝。</span><span class="sxs-lookup"><span data-stu-id="789e7-105">Verifies a package.</span></span>

<span data-ttu-id="789e7-106">驗證已簽署的套件尚未支援在.NET Core、 Mono，或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="789e7-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="789e7-107">使用量</span><span class="sxs-lookup"><span data-stu-id="789e7-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="789e7-108">何處`<package(s)>`是一或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="789e7-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="789e7-109">驗證 nuget-全部</span><span class="sxs-lookup"><span data-stu-id="789e7-109">nuget verify -All</span></span>

<span data-ttu-id="789e7-110">指定所有可能的驗證之後，應該對套件。</span><span class="sxs-lookup"><span data-stu-id="789e7-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="789e7-111">nuget 驗證-簽章</span><span class="sxs-lookup"><span data-stu-id="789e7-111">nuget verify -Signatures</span></span>

<span data-ttu-id="789e7-112">指定應該執行套件簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="789e7-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="789e7-113">針對 [驗證-簽章] 選項</span><span class="sxs-lookup"><span data-stu-id="789e7-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="789e7-114">選項</span><span class="sxs-lookup"><span data-stu-id="789e7-114">Option</span></span> | <span data-ttu-id="789e7-115">描述</span><span class="sxs-lookup"><span data-stu-id="789e7-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="789e7-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="789e7-116">CertificateFingerprint</span></span> | <span data-ttu-id="789e7-117">指定憑證 (s) 的已簽署的套件必須經過簽署的一或多個 SHA-256 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="789e7-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="789e7-118">使用 SHA-256 憑證指紋是憑證的 SHA-256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="789e7-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="789e7-119">多個輸入應該是以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="789e7-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="789e7-120">選項</span><span class="sxs-lookup"><span data-stu-id="789e7-120">Options</span></span>

| <span data-ttu-id="789e7-121">選項</span><span class="sxs-lookup"><span data-stu-id="789e7-121">Option</span></span> | <span data-ttu-id="789e7-122">描述</span><span class="sxs-lookup"><span data-stu-id="789e7-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="789e7-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="789e7-123">ConfigFile</span></span> | <span data-ttu-id="789e7-124">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="789e7-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="789e7-125">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="789e7-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="789e7-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="789e7-126">ForceEnglishOutput</span></span> | <span data-ttu-id="789e7-127">會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="789e7-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="789e7-128">說明</span><span class="sxs-lookup"><span data-stu-id="789e7-128">Help</span></span> | <span data-ttu-id="789e7-129">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="789e7-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="789e7-130">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="789e7-130">Verbosity</span></span> | <span data-ttu-id="789e7-131">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="789e7-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="789e7-132">範例</span><span class="sxs-lookup"><span data-stu-id="789e7-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```