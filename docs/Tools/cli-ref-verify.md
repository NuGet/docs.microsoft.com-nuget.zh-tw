---
title: NuGet CLI 確認命令 |Microsoft 文件
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 的參考會確認命令
keywords: nuget 驗證參考，請確認命令
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="6b8be-104">確認命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6b8be-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="6b8be-105">**適用於：**封裝耗用量&bullet;**支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="6b8be-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="6b8be-106">驗證封裝。</span><span class="sxs-lookup"><span data-stu-id="6b8be-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="6b8be-107">使用量</span><span class="sxs-lookup"><span data-stu-id="6b8be-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="6b8be-108">其中`<package(s)>`是一個或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="6b8be-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="6b8be-109">選項</span><span class="sxs-lookup"><span data-stu-id="6b8be-109">Options</span></span>

| <span data-ttu-id="6b8be-110">選項</span><span class="sxs-lookup"><span data-stu-id="6b8be-110">Option</span></span> | <span data-ttu-id="6b8be-111">描述</span><span class="sxs-lookup"><span data-stu-id="6b8be-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b8be-112">全部</span><span class="sxs-lookup"><span data-stu-id="6b8be-112">All</span></span> | <span data-ttu-id="6b8be-113">指定所有的驗證可能要執行的封裝上。</span><span class="sxs-lookup"><span data-stu-id="6b8be-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="6b8be-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6b8be-114">CertificateFingerprint</span></span> | <span data-ttu-id="6b8be-115">指定一或多個 sha-256 憑證指紋的憑證 (s) 必須經過簽署的簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="6b8be-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="6b8be-116">使用 sha-256 憑證指紋是憑證的 sha-256 雜湊。</span><span class="sxs-lookup"><span data-stu-id="6b8be-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="6b8be-117">多個輸入應該是以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="6b8be-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="6b8be-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6b8be-118">ConfigFile</span></span> | <span data-ttu-id="6b8be-119">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="6b8be-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6b8be-120">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="6b8be-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6b8be-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6b8be-121">ForceEnglishOutput</span></span> | <span data-ttu-id="6b8be-122">強制使用的非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="6b8be-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6b8be-123">說明</span><span class="sxs-lookup"><span data-stu-id="6b8be-123">Help</span></span> | <span data-ttu-id="6b8be-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="6b8be-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="6b8be-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6b8be-125">NonInteractive</span></span> | <span data-ttu-id="6b8be-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="6b8be-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6b8be-127">簽章</span><span class="sxs-lookup"><span data-stu-id="6b8be-127">Signatures</span></span> | <span data-ttu-id="6b8be-128">指定要執行的封裝簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="6b8be-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="6b8be-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6b8be-129">Verbosity</span></span> | <span data-ttu-id="6b8be-130">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="6b8be-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6b8be-131">範例</span><span class="sxs-lookup"><span data-stu-id="6b8be-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```