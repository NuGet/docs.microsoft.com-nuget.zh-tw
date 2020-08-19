---
title: NuGet CLI sign 命令
description: nuget.exe sign 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622768"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="e1ef6-103"> (NuGet CLI 的 sign 命令) </span><span class="sxs-lookup"><span data-stu-id="e1ef6-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="e1ef6-104">**適用物件：** 套件建立 &bullet; **支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="e1ef6-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="e1ef6-105">使用憑證簽署符合第一個引數的所有套件。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="e1ef6-106">具有私密金鑰的憑證可以透過提供主體名稱或指紋，從檔案或憑證存放區中安裝的憑證取得。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="e1ef6-107">在 .NET Core、Mono 或非 Windows 平臺上，尚未支援套件簽署。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="e1ef6-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="e1ef6-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="e1ef6-109">其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="e1ef6-110">選項。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="e1ef6-111">指定憑證的 SHA-1 指紋，用來搜尋憑證的本機憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="e1ef6-112">指定憑證密碼（如有需要）。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="e1ef6-113">如果憑證受到密碼保護，但未提供密碼，則命令會在執行時間提示輸入密碼，除非 `-NonInteractive` 已傳遞該選項。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="e1ef6-114">指定要用於簽署封裝之憑證的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="e1ef6-115">指定 x.509 憑證存放區用來搜尋憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="e1ef6-116">預設為 "CurrentUser"，這是目前使用者所使用的 x.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="e1ef6-117">透過或選項指定憑證時，應使用這個 `-CertificateSubjectName` 選項 `-CertificateFingerprint` 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="e1ef6-118">指定用來搜尋憑證的 x.509 憑證存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="e1ef6-119">預設值為 "My"，也就是個人憑證的 x.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="e1ef6-120">透過或選項指定憑證時，應使用這個 `-CertificateSubjectName` 選項 `-CertificateFingerprint` 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="e1ef6-121">指定憑證的主體名稱，用來搜尋憑證的本機憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="e1ef6-122">搜尋是使用提供的值進行不區分大小寫的字串比較，它會尋找所有具有該字串之主體名稱的憑證，而不考慮其他主體值。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="e1ef6-123">您可以使用和選項來指定憑證存放區 `-CertificateStoreName` `-CertificateStoreLocation` 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="e1ef6-124">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e1ef6-125">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="e1ef6-126">使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="e1ef6-127">用來簽署套件的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="e1ef6-128">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-128">Defaults to SHA256.</span></span> <span data-ttu-id="e1ef6-129">可能的值為 SHA256、SHA384 和 SHA512。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="e1ef6-130">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="e1ef6-131">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="e1ef6-132">指定要儲存已簽署之封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="e1ef6-133">依預設，已簽署的套件會覆寫原始封裝。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="e1ef6-134">切換以指出是否應該覆寫目前的簽章。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="e1ef6-135">根據預設，如果封裝已經有簽章，此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="e1ef6-136">RFC 3161 時間戳記伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="e1ef6-137">RFC 3161 時間戳記伺服器所使用的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="e1ef6-138">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="e1ef6-139">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="e1ef6-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="e1ef6-140">範例</span><span class="sxs-lookup"><span data-stu-id="e1ef6-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
