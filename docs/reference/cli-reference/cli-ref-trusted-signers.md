---
title: NuGet CLI 受信任-簽署者命令
description: Nuget.exe 受信任的簽署者命令的參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610338"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="21648-103">受信任-簽署者命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="21648-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="21648-104">**適用于：** 套件耗用量 &bullet;**支援的版本：** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="21648-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="21648-105">取得或設定 NuGet 設定的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="21648-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="21648-106">如需其他用法，請參閱[一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="21648-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="21648-107">如需有關 nuget.exe 架構外觀的詳細資訊，請參閱[nuget 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="21648-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="21648-108">使用量</span><span class="sxs-lookup"><span data-stu-id="21648-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="21648-109">如果未指定任何 `list|add|remove|sync`，則此命令會預設為 `list`。</span><span class="sxs-lookup"><span data-stu-id="21648-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="21648-110">nuget 受信任-簽署者清單</span><span class="sxs-lookup"><span data-stu-id="21648-110">nuget trusted-signers list</span></span>

<span data-ttu-id="21648-111">列出設定中所有受信任的簽署者。</span><span class="sxs-lookup"><span data-stu-id="21648-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="21648-112">此選項會包含每位簽署者具有的所有憑證（具有指紋和指紋演算法）。</span><span class="sxs-lookup"><span data-stu-id="21648-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="21648-113">如果憑證有前面的 `[U]`，則表示憑證專案已 `allowUntrustedRoot` 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="21648-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="21648-114">以下是此命令的輸出範例：</span><span class="sxs-lookup"><span data-stu-id="21648-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="21648-115">nuget 受信任-簽署者新增 [選項]</span><span class="sxs-lookup"><span data-stu-id="21648-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="21648-116">將具有指定名稱的受信任簽署者加入至設定。此選項會有不同的手勢來新增信任的作者或存放庫。</span><span class="sxs-lookup"><span data-stu-id="21648-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="21648-117">依據封裝新增的選項</span><span class="sxs-lookup"><span data-stu-id="21648-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="21648-118">其中 `<package(s)>` 是一或多個 `.nupkg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="21648-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="21648-119">選項</span><span class="sxs-lookup"><span data-stu-id="21648-119">Option</span></span> | <span data-ttu-id="21648-120">描述</span><span class="sxs-lookup"><span data-stu-id="21648-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21648-121">作者</span><span class="sxs-lookup"><span data-stu-id="21648-121">Author</span></span> | <span data-ttu-id="21648-122">指定封裝的作者簽章應該是受信任的。</span><span class="sxs-lookup"><span data-stu-id="21648-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="21648-123">儲存機制</span><span class="sxs-lookup"><span data-stu-id="21648-123">Repository</span></span> | <span data-ttu-id="21648-124">指定應信任套件的存放庫簽章或副署。</span><span class="sxs-lookup"><span data-stu-id="21648-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="21648-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="21648-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="21648-126">指定信任的簽署者的憑證是否應允許鏈到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="21648-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="21648-127">Owners</span><span class="sxs-lookup"><span data-stu-id="21648-127">Owners</span></span> | <span data-ttu-id="21648-128">信任的擁有者清單（以分號分隔），以進一步限制存放庫的信任。</span><span class="sxs-lookup"><span data-stu-id="21648-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="21648-129">只有在使用 [`-Repository`] 選項時才有效。</span><span class="sxs-lookup"><span data-stu-id="21648-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="21648-130">不支援同時提供 `-Author` 和 `-Repository`。</span><span class="sxs-lookup"><span data-stu-id="21648-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="21648-131">根據服務索引新增的選項</span><span class="sxs-lookup"><span data-stu-id="21648-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="21648-132">_注意_：此選項只會新增信任的存放庫。</span><span class="sxs-lookup"><span data-stu-id="21648-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="21648-133">選項</span><span class="sxs-lookup"><span data-stu-id="21648-133">Option</span></span> | <span data-ttu-id="21648-134">描述</span><span class="sxs-lookup"><span data-stu-id="21648-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21648-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="21648-135">ServiceIndex</span></span> | <span data-ttu-id="21648-136">指定要信任之存放庫的 V3 服務索引。</span><span class="sxs-lookup"><span data-stu-id="21648-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="21648-137">此存放庫必須支援存放庫簽章資源。</span><span class="sxs-lookup"><span data-stu-id="21648-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="21648-138">如果未提供，此命令會尋找具有相同 `-Name` 的套件來源，並從該處取得服務索引。</span><span class="sxs-lookup"><span data-stu-id="21648-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="21648-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="21648-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="21648-140">指定信任的簽署者的憑證是否應允許鏈到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="21648-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="21648-141">Owners</span><span class="sxs-lookup"><span data-stu-id="21648-141">Owners</span></span> | <span data-ttu-id="21648-142">信任的擁有者清單（以分號分隔），以進一步限制存放庫的信任。</span><span class="sxs-lookup"><span data-stu-id="21648-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="21648-143">根據憑證資訊新增的選項</span><span class="sxs-lookup"><span data-stu-id="21648-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="21648-144">_注意_：如果已存在具有指定名稱的受信任簽署者，則會將憑證專案新增至該簽署者。</span><span class="sxs-lookup"><span data-stu-id="21648-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="21648-145">否則，將會使用指定憑證資訊中的憑證專案來建立信任的作者。</span><span class="sxs-lookup"><span data-stu-id="21648-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="21648-146">選項</span><span class="sxs-lookup"><span data-stu-id="21648-146">Option</span></span> | <span data-ttu-id="21648-147">描述</span><span class="sxs-lookup"><span data-stu-id="21648-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21648-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="21648-148">CertificateFingerprint</span></span> | <span data-ttu-id="21648-149">指定憑證的憑證指紋，其簽署的套件必須以簽署。</span><span class="sxs-lookup"><span data-stu-id="21648-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="21648-150">憑證指紋是憑證的雜湊。</span><span class="sxs-lookup"><span data-stu-id="21648-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="21648-151">用於計算此雜湊的雜湊演算法應該在 [`FingerprintAlgorithm`] 選項中指定。</span><span class="sxs-lookup"><span data-stu-id="21648-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="21648-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="21648-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="21648-153">指定用來計算憑證指紋的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="21648-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="21648-154">預設值為 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="21648-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="21648-155">支援的值為 `SHA256`、`SHA384` 和 `SHA512`</span><span class="sxs-lookup"><span data-stu-id="21648-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="21648-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="21648-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="21648-157">指定信任的簽署者的憑證是否應允許鏈到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="21648-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="21648-158">nuget 受信任-簽署者移除名稱 \<名稱\></span><span class="sxs-lookup"><span data-stu-id="21648-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="21648-159">移除任何符合指定名稱的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="21648-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="21648-160">nuget 受信任-簽署者同步-名稱 \<名稱\></span><span class="sxs-lookup"><span data-stu-id="21648-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="21648-161">要求目前信任的存放庫中所使用的最新憑證清單，以更新受信任簽署者中的現有憑證清單。</span><span class="sxs-lookup"><span data-stu-id="21648-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="21648-162">_注意_：此手勢會刪除目前的憑證清單，並將其取代為存放庫中的最新清單。</span><span class="sxs-lookup"><span data-stu-id="21648-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="21648-163">選項</span><span class="sxs-lookup"><span data-stu-id="21648-163">Options</span></span>

| <span data-ttu-id="21648-164">選項</span><span class="sxs-lookup"><span data-stu-id="21648-164">Option</span></span> | <span data-ttu-id="21648-165">描述</span><span class="sxs-lookup"><span data-stu-id="21648-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21648-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="21648-166">ConfigFile</span></span> | <span data-ttu-id="21648-167">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="21648-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="21648-168">如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="21648-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="21648-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="21648-169">ForceEnglishOutput</span></span> | <span data-ttu-id="21648-170">強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="21648-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="21648-171">說明</span><span class="sxs-lookup"><span data-stu-id="21648-171">Help</span></span> | <span data-ttu-id="21648-172">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="21648-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="21648-173">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="21648-173">Verbosity</span></span> | <span data-ttu-id="21648-174">指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="21648-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="21648-175">範例</span><span class="sxs-lookup"><span data-stu-id="21648-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
