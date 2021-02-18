---
title: NuGet CLI 受信任-簽署者命令
description: nuget.exe 受信任簽署者命令的參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 4b6a1c3b6eb0fefd9a78c78233f974eb0db19e93
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101364"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="a21cf-103">受信任的簽署者命令 (NuGet CLI) </span><span class="sxs-lookup"><span data-stu-id="a21cf-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="a21cf-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="a21cf-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="a21cf-105">取得或設定受信任的簽署者為 NuGet 設定。</span><span class="sxs-lookup"><span data-stu-id="a21cf-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="a21cf-106">如需其他使用方式，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。</span><span class="sxs-lookup"><span data-stu-id="a21cf-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a21cf-107">如需 nuget.config 架構外觀的詳細資訊，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="a21cf-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a21cf-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="a21cf-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="a21cf-109">如果 `list|add|remove|sync` 未指定任何，則命令會預設為 `list` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="a21cf-110">nuget 受信任-簽署者清單</span><span class="sxs-lookup"><span data-stu-id="a21cf-110">nuget trusted-signers list</span></span>

<span data-ttu-id="a21cf-111">列出設定中所有受信任的簽署者。</span><span class="sxs-lookup"><span data-stu-id="a21cf-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="a21cf-112">此選項會包含所有憑證 (指紋和指紋演算法，) 每位簽署者都有。</span><span class="sxs-lookup"><span data-stu-id="a21cf-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="a21cf-113">如果憑證前面有 `[U]` ，則表示該憑證專案已 `allowUntrustedRoot` 設定為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="a21cf-114">以下是此命令的輸出範例：</span><span class="sxs-lookup"><span data-stu-id="a21cf-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="a21cf-115">nuget 受信任-簽署者新增 [選項]</span><span class="sxs-lookup"><span data-stu-id="a21cf-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="a21cf-116">將具有指定名稱的受信任簽署者新增至設定。此選項有不同的手勢可新增信任的作者或存放庫。</span><span class="sxs-lookup"><span data-stu-id="a21cf-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="a21cf-117">以套件為基礎的新增選項</span><span class="sxs-lookup"><span data-stu-id="a21cf-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="a21cf-118">其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="a21cf-119">指定要信任的封裝 () 的作者簽章。</span><span class="sxs-lookup"><span data-stu-id="a21cf-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a21cf-120">指定是否應允許受信任簽署者的憑證連結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="a21cf-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="a21cf-121">以分號分隔的受信任擁有者清單，以進一步限制存放庫的信任。</span><span class="sxs-lookup"><span data-stu-id="a21cf-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="a21cf-122">只有在使用選項時才有效 `-Repository` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="a21cf-123">指定要信任的封裝 () 的存放庫簽章或副署。</span><span class="sxs-lookup"><span data-stu-id="a21cf-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="a21cf-124">`-Author`不支援同時提供和 `-Repository` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="a21cf-125">根據服務索引新增的選項</span><span class="sxs-lookup"><span data-stu-id="a21cf-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="a21cf-126">_注意_：此選項只會新增信任的存放庫。</span><span class="sxs-lookup"><span data-stu-id="a21cf-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a21cf-127">指定是否應允許受信任簽署者的憑證連結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="a21cf-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="a21cf-128">以分號分隔的受信任擁有者清單，以進一步限制存放庫的信任。</span><span class="sxs-lookup"><span data-stu-id="a21cf-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="a21cf-129">指定要信任之存放庫的 V3 服務索引。</span><span class="sxs-lookup"><span data-stu-id="a21cf-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="a21cf-130">此存放庫必須支援存放庫簽章資源。</span><span class="sxs-lookup"><span data-stu-id="a21cf-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="a21cf-131">如果未提供，則命令會尋找具有相同的套件來源 `-Name` ，並從該處取得服務索引。</span><span class="sxs-lookup"><span data-stu-id="a21cf-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="a21cf-132">根據憑證資訊新增的選項</span><span class="sxs-lookup"><span data-stu-id="a21cf-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="a21cf-133">_注意_：如果已有具有指定名稱的受信任簽署者存在，則憑證專案將會新增至該簽署人。</span><span class="sxs-lookup"><span data-stu-id="a21cf-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="a21cf-134">否則，將會使用指定憑證資訊的憑證專案來建立信任的作者。</span><span class="sxs-lookup"><span data-stu-id="a21cf-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="a21cf-135">指定是否應允許受信任簽署者的憑證連結至不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="a21cf-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a21cf-136">指定憑證的憑證指紋，簽署的套件必須用來簽署。</span><span class="sxs-lookup"><span data-stu-id="a21cf-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="a21cf-137">憑證指紋是憑證的雜湊。</span><span class="sxs-lookup"><span data-stu-id="a21cf-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="a21cf-138">用來計算此雜湊的雜湊演算法應該在選項中指定 `FingerprintAlgorithm` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="a21cf-139">指定用來計算憑證指紋的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="a21cf-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="a21cf-140">預設值為 `SHA256`。</span><span class="sxs-lookup"><span data-stu-id="a21cf-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="a21cf-141">支援的值為 `SHA256` 、 `SHA384` 和 `SHA512` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="a21cf-142">nuget 受信任-簽署者移除名稱 \<name\></span><span class="sxs-lookup"><span data-stu-id="a21cf-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="a21cf-143">移除任何符合指定名稱的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="a21cf-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="a21cf-144">nuget 受信任-簽署者同步-名稱 \<name\></span><span class="sxs-lookup"><span data-stu-id="a21cf-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="a21cf-145">要求目前受信任存放庫中使用的最新憑證清單，以更新受信任簽署者中的現有憑證清單。</span><span class="sxs-lookup"><span data-stu-id="a21cf-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="a21cf-146">_注意_：此手勢將會刪除目前的憑證清單，並將其取代為存放庫中的最新清單。</span><span class="sxs-lookup"><span data-stu-id="a21cf-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="a21cf-147">選項</span><span class="sxs-lookup"><span data-stu-id="a21cf-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a21cf-148">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a21cf-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a21cf-149">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a21cf-150">使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a21cf-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a21cf-151">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="a21cf-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="a21cf-152">受信任簽署者的名稱。</span><span class="sxs-lookup"><span data-stu-id="a21cf-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a21cf-153">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="a21cf-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a21cf-154">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="a21cf-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="a21cf-155">範例</span><span class="sxs-lookup"><span data-stu-id="a21cf-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
