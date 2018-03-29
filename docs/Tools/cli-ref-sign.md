---
title: NuGet CLI 登命令 |Microsoft 文件
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 登命令參考
keywords: nuget 符號參考登命令
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="254c3-104">符號命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="254c3-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="254c3-105">**適用於：**封裝建立&bullet;**支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="254c3-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="254c3-106">簽署憑證的第一個引數比對的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="254c3-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="254c3-107">從檔案或從安裝在憑證存放區提供主體名稱或指紋的憑證，您可以取得具有私密金鑰的憑證。</span><span class="sxs-lookup"><span data-stu-id="254c3-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="254c3-108">封裝簽章尚未支援單聲道下或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="254c3-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="254c3-109">使用量</span><span class="sxs-lookup"><span data-stu-id="254c3-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="254c3-110">其中`<package(s)>`是一個或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="254c3-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="254c3-111">選項</span><span class="sxs-lookup"><span data-stu-id="254c3-111">Options</span></span>

| <span data-ttu-id="254c3-112">選項</span><span class="sxs-lookup"><span data-stu-id="254c3-112">Option</span></span> | <span data-ttu-id="254c3-113">描述</span><span class="sxs-lookup"><span data-stu-id="254c3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="254c3-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="254c3-114">CertificateFingerprint</span></span> | <span data-ttu-id="254c3-115">指定用來搜尋憑證的本機憑證存放區的憑證的 sha-1 指紋。</span><span class="sxs-lookup"><span data-stu-id="254c3-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="254c3-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="254c3-116">CertificatePassword</span></span> | <span data-ttu-id="254c3-117">如有需要請指定憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="254c3-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="254c3-118">如果憑證是受密碼保護，但不提供任何密碼，此命令會提示輸入密碼在執行階段，除非-傳遞非互動式選項。</span><span class="sxs-lookup"><span data-stu-id="254c3-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="254c3-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="254c3-119">CertificatePath</span></span> | <span data-ttu-id="254c3-120">指定要用來簽署封裝的憑證的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="254c3-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="254c3-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="254c3-121">CertificateStoreLocation</span></span> | <span data-ttu-id="254c3-122">指定 X.509 憑證存放區用來搜尋憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="254c3-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="254c3-123">預設值為"CurrentUser"，目前使用者所使用的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="254c3-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="254c3-124">指定透過-CertificateSubjectName 或-CertificateFingerprint 選項憑證時，應該使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="254c3-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="254c3-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="254c3-125">CertificateStoreName</span></span> | <span data-ttu-id="254c3-126">指定要用於搜尋憑證的 X.509 憑證存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="254c3-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="254c3-127">預設為 「 我的 」，個人憑證的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="254c3-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="254c3-128">指定透過-CertificateSubjectName 或-CertificateFingerprint 選項憑證時，應該使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="254c3-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="254c3-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="254c3-129">CertificateSubjectName</span></span> | <span data-ttu-id="254c3-130">指定用來搜尋憑證的本機憑證存放區的憑證的主體名稱。</span><span class="sxs-lookup"><span data-stu-id="254c3-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="254c3-131">搜尋不區分大小寫字串比較，使用所提供的值，會發現所有憑證的主體名稱，包含該字串，不論其他主體的值。</span><span class="sxs-lookup"><span data-stu-id="254c3-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="254c3-132">-CertificateStoreName 和-CertificateStoreLocation 選項所指定的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="254c3-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="254c3-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="254c3-133">ConfigFile</span></span> | <span data-ttu-id="254c3-134">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="254c3-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="254c3-135">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="254c3-135">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="254c3-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="254c3-136">ForceEnglishOutput</span></span> | <span data-ttu-id="254c3-137">強制使用的非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="254c3-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="254c3-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="254c3-138">HashAlgorithm</span></span> | <span data-ttu-id="254c3-139">要用來簽署套件的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="254c3-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="254c3-140">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="254c3-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="254c3-141">說明</span><span class="sxs-lookup"><span data-stu-id="254c3-141">Help</span></span> | <span data-ttu-id="254c3-142">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="254c3-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="254c3-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="254c3-143">NonInteractive</span></span> | <span data-ttu-id="254c3-144">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="254c3-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="254c3-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="254c3-145">OutputDirectory</span></span> | <span data-ttu-id="254c3-146">指定用來儲存已簽署的封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="254c3-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="254c3-147">依預設會覆寫的已簽署套件的原始封裝。</span><span class="sxs-lookup"><span data-stu-id="254c3-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="254c3-148">覆寫</span><span class="sxs-lookup"><span data-stu-id="254c3-148">Overwrite</span></span> | <span data-ttu-id="254c3-149">表示是否應該覆寫目前的簽章的參數。</span><span class="sxs-lookup"><span data-stu-id="254c3-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="254c3-150">如果已經有套件的簽章，則預設將會失敗命令。</span><span class="sxs-lookup"><span data-stu-id="254c3-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="254c3-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="254c3-151">Timestamper</span></span> | <span data-ttu-id="254c3-152">RFC 3161 時間戳記伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="254c3-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="254c3-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="254c3-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="254c3-154">RFC 3161 時間戳記伺服器所使用的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="254c3-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="254c3-155">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="254c3-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="254c3-156">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="254c3-156">Verbosity</span></span> | <span data-ttu-id="254c3-157">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="254c3-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="254c3-158">範例</span><span class="sxs-lookup"><span data-stu-id="254c3-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```