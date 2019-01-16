---
title: NuGet CLI 信任簽署命令
description: Nuget.exe 信任簽署命令參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324704"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="cb1d4-103">受信任簽署命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cb1d4-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="cb1d4-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="cb1d4-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="cb1d4-105">取得或設定受信任的簽署人的 NuGet 組態。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="cb1d4-106">額外的使用量，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cb1d4-107">如需有關如何 nuget.config 結構描述的樣貌，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cb1d4-108">使用量</span><span class="sxs-lookup"><span data-stu-id="cb1d4-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="cb1d4-109">如果沒有任何`list|add|remove|sync`未指定，命令會預設為`list`。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="cb1d4-110">nuget 受信任簽署清單</span><span class="sxs-lookup"><span data-stu-id="cb1d4-110">nuget trusted-signers list</span></span>

<span data-ttu-id="cb1d4-111">列出組態中的所有受信任的簽署。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="cb1d4-112">此選項，將會包含所有憑證 （使用指紋和指紋演算法） 具有每個簽署者。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="cb1d4-113">如果憑證具有前面`[U]`，這表示憑證項目已`allowUntrustedRoot`設定為`true`。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="cb1d4-114">以下是此命令的輸出範例：</span><span class="sxs-lookup"><span data-stu-id="cb1d4-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="cb1d4-115">nuget 受信任簽署新增 [選項]</span><span class="sxs-lookup"><span data-stu-id="cb1d4-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="cb1d4-116">將具有指定名稱的受信任簽署者加入至組態中。此選項會有不同的手勢，來新增受信任的作者或存放庫。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="cb1d4-117">新增套件為基礎的選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="cb1d4-118">何處`<package(s)>`是一或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="cb1d4-119">選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-119">Option</span></span> | <span data-ttu-id="cb1d4-120">描述</span><span class="sxs-lookup"><span data-stu-id="cb1d4-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb1d4-121">作者</span><span class="sxs-lookup"><span data-stu-id="cb1d4-121">Author</span></span> | <span data-ttu-id="cb1d4-122">指定套件的作者簽章應該是受信任。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="cb1d4-123">儲存機制</span><span class="sxs-lookup"><span data-stu-id="cb1d4-123">Repository</span></span> | <span data-ttu-id="cb1d4-124">指定的存放庫簽章或副署的套件應該是受信任。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="cb1d4-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cb1d4-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="cb1d4-126">指定是否允許受信任簽署者的憑證鏈結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="cb1d4-127">Owners</span><span class="sxs-lookup"><span data-stu-id="cb1d4-127">Owners</span></span> | <span data-ttu-id="cb1d4-128">以分號分隔清單的受信任的擁有者，來進一步限制的儲存機制的信任。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="cb1d4-129">使用時，唯一有效`-Repository`選項。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="cb1d4-130">同時提供`-Author`和`-Repository`不支援在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="cb1d4-131">新增服務索引為基礎的選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cb1d4-132">_注意_：此選項只會將受信任的存放庫。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="cb1d4-133">選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-133">Option</span></span> | <span data-ttu-id="cb1d4-134">描述</span><span class="sxs-lookup"><span data-stu-id="cb1d4-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb1d4-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="cb1d4-135">ServiceIndex</span></span> | <span data-ttu-id="cb1d4-136">指定要信任的存放庫的 V3 服務索引。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="cb1d4-137">此存放庫，就必須支援的存放庫簽章的資源。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="cb1d4-138">如果未提供，此命令會尋找具有相同的套件來源`-Name`並從該處取得服務索引。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="cb1d4-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cb1d4-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="cb1d4-140">指定是否允許受信任簽署者的憑證鏈結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="cb1d4-141">Owners</span><span class="sxs-lookup"><span data-stu-id="cb1d4-141">Owners</span></span> | <span data-ttu-id="cb1d4-142">以分號分隔清單的受信任的擁有者，來進一步限制的儲存機制的信任。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="cb1d4-143">新增的憑證資訊為基礎的選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="cb1d4-144">_注意_：如果已經存在具有指定名稱的受信任簽署者，憑證項目會加入該簽章者。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="cb1d4-145">否則會建立受信任的作者與憑證項目從提供的憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="cb1d4-146">選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-146">Option</span></span> | <span data-ttu-id="cb1d4-147">描述</span><span class="sxs-lookup"><span data-stu-id="cb1d4-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb1d4-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="cb1d4-148">CertificateFingerprint</span></span> | <span data-ttu-id="cb1d4-149">指定已簽署的套件的憑證指紋必須經過簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="cb1d4-150">憑證指紋是憑證的雜湊。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="cb1d4-151">在指定的雜湊演算法，用來計算此雜湊應為`FingerprintAlgorithm`選項。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="cb1d4-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="cb1d4-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="cb1d4-153">指定用來計算憑證指紋的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="cb1d4-154">預設值為 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="cb1d4-155">支援的值為`SHA256`，`SHA384`和 `SHA512`</span><span class="sxs-lookup"><span data-stu-id="cb1d4-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="cb1d4-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="cb1d4-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="cb1d4-157">指定是否允許受信任簽署者的憑證鏈結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="cb1d4-158">nuget 受信任簽署 remove-名稱 <name></span><span class="sxs-lookup"><span data-stu-id="cb1d4-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="cb1d4-159">移除符合指定之名稱的任何受信任的簽署。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="cb1d4-160">nuget 受信任簽署同步-名稱 <name></span><span class="sxs-lookup"><span data-stu-id="cb1d4-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="cb1d4-161">要求目前受信任的存放庫中用來更新憑證的最新清單中受信任簽署者的現有憑證清單。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="cb1d4-162">_注意_：此動作會刪除目前的憑證清單，並取代從存放庫的最新清單。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="cb1d4-163">選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-163">Options</span></span>

| <span data-ttu-id="cb1d4-164">選項</span><span class="sxs-lookup"><span data-stu-id="cb1d4-164">Option</span></span> | <span data-ttu-id="cb1d4-165">描述</span><span class="sxs-lookup"><span data-stu-id="cb1d4-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb1d4-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cb1d4-166">ConfigFile</span></span> | <span data-ttu-id="cb1d4-167">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb1d4-168">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cb1d4-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cb1d4-169">ForceEnglishOutput</span></span> | <span data-ttu-id="cb1d4-170">會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cb1d4-171">說明</span><span class="sxs-lookup"><span data-stu-id="cb1d4-171">Help</span></span> | <span data-ttu-id="cb1d4-172">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="cb1d4-173">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="cb1d4-173">Verbosity</span></span> | <span data-ttu-id="cb1d4-174">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="cb1d4-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="cb1d4-175">範例</span><span class="sxs-lookup"><span data-stu-id="cb1d4-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
