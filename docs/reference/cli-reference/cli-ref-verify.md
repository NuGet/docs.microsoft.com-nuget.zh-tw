---
title: NuGet CLI 驗證命令
description: Nuget.exe verify 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327495"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="2c2b1-103">verify 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2c2b1-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="2c2b1-104">**適用于:** 套件耗&bullet;用量**支援的版本:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="2c2b1-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2c2b1-105">驗證套件。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-105">Verifies a package.</span></span>

<span data-ttu-id="2c2b1-106">在 .NET Core、Mono 或非 Windows 平臺上, 尚未支援已簽署套件的驗證。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="2c2b1-107">使用量</span><span class="sxs-lookup"><span data-stu-id="2c2b1-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="2c2b1-108">其中`<package(s)>`是一或多`.nupkg`個檔案。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="2c2b1-109">nuget 驗證-全部</span><span class="sxs-lookup"><span data-stu-id="2c2b1-109">nuget verify -All</span></span>

<span data-ttu-id="2c2b1-110">指定所有可能的驗證都應該在封裝上執行。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="2c2b1-111">nuget 驗證-簽章</span><span class="sxs-lookup"><span data-stu-id="2c2b1-111">nuget verify -Signatures</span></span>

<span data-ttu-id="2c2b1-112">指定應該執行封裝簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="2c2b1-113">「驗證-簽章」的選項</span><span class="sxs-lookup"><span data-stu-id="2c2b1-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="2c2b1-114">選項</span><span class="sxs-lookup"><span data-stu-id="2c2b1-114">Option</span></span> | <span data-ttu-id="2c2b1-115">說明</span><span class="sxs-lookup"><span data-stu-id="2c2b1-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c2b1-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="2c2b1-116">CertificateFingerprint</span></span> | <span data-ttu-id="2c2b1-117">指定憑證的一個或多個 SHA-256 憑證指紋, 其簽署的套件必須經過簽署。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="2c2b1-118">憑證 SHA-256 指紋是憑證的 SHA-256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="2c2b1-119">多個輸入應以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="2c2b1-120">選項</span><span class="sxs-lookup"><span data-stu-id="2c2b1-120">Options</span></span>

| <span data-ttu-id="2c2b1-121">選項</span><span class="sxs-lookup"><span data-stu-id="2c2b1-121">Option</span></span> | <span data-ttu-id="2c2b1-122">描述</span><span class="sxs-lookup"><span data-stu-id="2c2b1-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c2b1-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2c2b1-123">ConfigFile</span></span> | <span data-ttu-id="2c2b1-124">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2c2b1-125">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2c2b1-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2c2b1-126">ForceEnglishOutput</span></span> | <span data-ttu-id="2c2b1-127">強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2c2b1-128">Help</span><span class="sxs-lookup"><span data-stu-id="2c2b1-128">Help</span></span> | <span data-ttu-id="2c2b1-129">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="2c2b1-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2c2b1-130">Verbosity</span></span> | <span data-ttu-id="2c2b1-131">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="2c2b1-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="2c2b1-132">範例</span><span class="sxs-lookup"><span data-stu-id="2c2b1-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```