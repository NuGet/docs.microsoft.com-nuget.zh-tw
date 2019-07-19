---
title: NuGet CLI sign 命令
description: Nuget.exe sign 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327585"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="8ea38-103">sign 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8ea38-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="8ea38-104">**適用于:** 套件建立&bullet; **支援的版本:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="8ea38-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="8ea38-105">使用憑證簽署符合第一個引數的所有套件。</span><span class="sxs-lookup"><span data-stu-id="8ea38-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="8ea38-106">具有私密金鑰的憑證可以透過提供主體名稱或指紋, 從檔案或安裝在憑證存放區中的憑證取得。</span><span class="sxs-lookup"><span data-stu-id="8ea38-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="8ea38-107">在 .NET Core、Mono 或非 Windows 平臺上, 尚未支援套件簽署。</span><span class="sxs-lookup"><span data-stu-id="8ea38-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="8ea38-108">使用量</span><span class="sxs-lookup"><span data-stu-id="8ea38-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="8ea38-109">其中`<package(s)>`是一或多`.nupkg`個檔案。</span><span class="sxs-lookup"><span data-stu-id="8ea38-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="8ea38-110">選項</span><span class="sxs-lookup"><span data-stu-id="8ea38-110">Options</span></span>

| <span data-ttu-id="8ea38-111">選項</span><span class="sxs-lookup"><span data-stu-id="8ea38-111">Option</span></span> | <span data-ttu-id="8ea38-112">描述</span><span class="sxs-lookup"><span data-stu-id="8ea38-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ea38-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="8ea38-113">CertificateFingerprint</span></span> | <span data-ttu-id="8ea38-114">指定憑證的 SHA-1 指紋, 用來搜尋憑證的本機憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="8ea38-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="8ea38-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="8ea38-115">CertificatePassword</span></span> | <span data-ttu-id="8ea38-116">指定憑證密碼 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="8ea38-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="8ea38-117">如果憑證受密碼保護, 但未提供密碼, 除非傳遞-非互動式選項, 否則命令會在執行時間提示輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="8ea38-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="8ea38-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="8ea38-118">CertificatePath</span></span> | <span data-ttu-id="8ea38-119">指定要用來簽署封裝之憑證的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="8ea38-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="8ea38-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="8ea38-120">CertificateStoreLocation</span></span> | <span data-ttu-id="8ea38-121">指定用來搜尋憑證的 x.509 憑證存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="8ea38-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="8ea38-122">預設為 "CurrentUser", 這是目前使用者所使用的 x.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="8ea38-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="8ea38-123">當您透過-CertificateSubjectName 或-CertificateFingerprint 選項指定憑證時, 應該使用此選項。</span><span class="sxs-lookup"><span data-stu-id="8ea38-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="8ea38-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="8ea38-124">CertificateStoreName</span></span> | <span data-ttu-id="8ea38-125">指定要用來搜尋憑證的 x.509 憑證存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="8ea38-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="8ea38-126">預設為 "My", 個人憑證的 x.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="8ea38-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="8ea38-127">當您透過-CertificateSubjectName 或-CertificateFingerprint 選項指定憑證時, 應該使用此選項。</span><span class="sxs-lookup"><span data-stu-id="8ea38-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="8ea38-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="8ea38-128">CertificateSubjectName</span></span> | <span data-ttu-id="8ea38-129">指定用來搜尋憑證之本機憑證存放區的憑證主體名稱。</span><span class="sxs-lookup"><span data-stu-id="8ea38-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="8ea38-130">搜尋是使用提供的值時, 不區分大小寫的字串比較, 它會尋找具有包含該字串之主體名稱的所有憑證, 而不論其他主體值為何。</span><span class="sxs-lookup"><span data-stu-id="8ea38-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="8ea38-131">憑證存放區可以透過-CertificateStoreName 和-CertificateStoreLocation 選項來指定。</span><span class="sxs-lookup"><span data-stu-id="8ea38-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="8ea38-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8ea38-132">ConfigFile</span></span> | <span data-ttu-id="8ea38-133">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8ea38-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8ea38-134">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="8ea38-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8ea38-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8ea38-135">ForceEnglishOutput</span></span> | <span data-ttu-id="8ea38-136">強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="8ea38-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8ea38-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8ea38-137">HashAlgorithm</span></span> | <span data-ttu-id="8ea38-138">要用來簽署封裝的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="8ea38-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="8ea38-139">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="8ea38-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="8ea38-140">Help</span><span class="sxs-lookup"><span data-stu-id="8ea38-140">Help</span></span> | <span data-ttu-id="8ea38-141">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="8ea38-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="8ea38-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8ea38-142">NonInteractive</span></span> | <span data-ttu-id="8ea38-143">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="8ea38-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8ea38-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="8ea38-144">OutputDirectory</span></span> | <span data-ttu-id="8ea38-145">指定應儲存已簽署封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="8ea38-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="8ea38-146">根據預設, 已簽署的套件會覆寫原始的封裝。</span><span class="sxs-lookup"><span data-stu-id="8ea38-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="8ea38-147">覆寫</span><span class="sxs-lookup"><span data-stu-id="8ea38-147">Overwrite</span></span> | <span data-ttu-id="8ea38-148">切換以指出是否應該覆寫目前的簽章。</span><span class="sxs-lookup"><span data-stu-id="8ea38-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="8ea38-149">根據預設, 如果封裝已有簽章, 此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8ea38-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="8ea38-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="8ea38-150">Timestamper</span></span> | <span data-ttu-id="8ea38-151">RFC 3161 時間戳記伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="8ea38-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="8ea38-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8ea38-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="8ea38-153">RFC 3161 時間戳記伺服器所要使用的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="8ea38-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="8ea38-154">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="8ea38-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="8ea38-155">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8ea38-155">Verbosity</span></span> | <span data-ttu-id="8ea38-156">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="8ea38-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="8ea38-157">範例</span><span class="sxs-lookup"><span data-stu-id="8ea38-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```