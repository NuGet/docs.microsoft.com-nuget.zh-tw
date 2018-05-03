---
title: NuGet CLI 登命令
description: Nuget.exe 登命令參考
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="12ccd-103">符號命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="12ccd-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="12ccd-104">**適用於：**封裝建立&bullet;**支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="12ccd-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="12ccd-105">簽署憑證的第一個引數比對的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="12ccd-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="12ccd-106">從檔案或從安裝在憑證存放區提供主體名稱或指紋的憑證，您可以取得具有私密金鑰的憑證。</span><span class="sxs-lookup"><span data-stu-id="12ccd-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="12ccd-107">封裝簽章尚未支援在.NET Core Mono，或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="12ccd-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="12ccd-108">使用量</span><span class="sxs-lookup"><span data-stu-id="12ccd-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="12ccd-109">其中`<package(s)>`是一個或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="12ccd-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="12ccd-110">選項</span><span class="sxs-lookup"><span data-stu-id="12ccd-110">Options</span></span>

| <span data-ttu-id="12ccd-111">選項</span><span class="sxs-lookup"><span data-stu-id="12ccd-111">Option</span></span> | <span data-ttu-id="12ccd-112">描述</span><span class="sxs-lookup"><span data-stu-id="12ccd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12ccd-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="12ccd-113">CertificateFingerprint</span></span> | <span data-ttu-id="12ccd-114">指定用來搜尋憑證的本機憑證存放區的憑證的 sha-1 指紋。</span><span class="sxs-lookup"><span data-stu-id="12ccd-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="12ccd-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="12ccd-115">CertificatePassword</span></span> | <span data-ttu-id="12ccd-116">如有需要請指定憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="12ccd-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="12ccd-117">如果憑證是受密碼保護，但不提供任何密碼，此命令會提示輸入密碼在執行階段，除非-傳遞非互動式選項。</span><span class="sxs-lookup"><span data-stu-id="12ccd-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="12ccd-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="12ccd-118">CertificatePath</span></span> | <span data-ttu-id="12ccd-119">指定要用來簽署封裝的憑證的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="12ccd-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="12ccd-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="12ccd-120">CertificateStoreLocation</span></span> | <span data-ttu-id="12ccd-121">指定 X.509 憑證存放區用來搜尋憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="12ccd-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="12ccd-122">預設值為"CurrentUser"，目前使用者所使用的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="12ccd-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="12ccd-123">指定透過-CertificateSubjectName 或-CertificateFingerprint 選項憑證時，應該使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="12ccd-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="12ccd-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="12ccd-124">CertificateStoreName</span></span> | <span data-ttu-id="12ccd-125">指定要用於搜尋憑證的 X.509 憑證存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="12ccd-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="12ccd-126">預設為 「 我的 」，個人憑證的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="12ccd-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="12ccd-127">指定透過-CertificateSubjectName 或-CertificateFingerprint 選項憑證時，應該使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="12ccd-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="12ccd-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="12ccd-128">CertificateSubjectName</span></span> | <span data-ttu-id="12ccd-129">指定用來搜尋憑證的本機憑證存放區的憑證的主體名稱。</span><span class="sxs-lookup"><span data-stu-id="12ccd-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="12ccd-130">搜尋不區分大小寫字串比較，使用所提供的值，會發現所有憑證的主體名稱，包含該字串，不論其他主體的值。</span><span class="sxs-lookup"><span data-stu-id="12ccd-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="12ccd-131">-CertificateStoreName 和-CertificateStoreLocation 選項所指定的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="12ccd-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="12ccd-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="12ccd-132">ConfigFile</span></span> | <span data-ttu-id="12ccd-133">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="12ccd-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="12ccd-134">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="12ccd-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="12ccd-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="12ccd-135">ForceEnglishOutput</span></span> | <span data-ttu-id="12ccd-136">強制使用的非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="12ccd-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="12ccd-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="12ccd-137">HashAlgorithm</span></span> | <span data-ttu-id="12ccd-138">要用來簽署套件的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="12ccd-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="12ccd-139">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="12ccd-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="12ccd-140">說明</span><span class="sxs-lookup"><span data-stu-id="12ccd-140">Help</span></span> | <span data-ttu-id="12ccd-141">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="12ccd-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="12ccd-142">非互動式</span><span class="sxs-lookup"><span data-stu-id="12ccd-142">NonInteractive</span></span> | <span data-ttu-id="12ccd-143">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="12ccd-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="12ccd-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="12ccd-144">OutputDirectory</span></span> | <span data-ttu-id="12ccd-145">指定用來儲存已簽署的封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="12ccd-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="12ccd-146">依預設會覆寫的已簽署套件的原始封裝。</span><span class="sxs-lookup"><span data-stu-id="12ccd-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="12ccd-147">覆寫</span><span class="sxs-lookup"><span data-stu-id="12ccd-147">Overwrite</span></span> | <span data-ttu-id="12ccd-148">表示是否應該覆寫目前的簽章的參數。</span><span class="sxs-lookup"><span data-stu-id="12ccd-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="12ccd-149">如果已經有套件的簽章，則預設將會失敗命令。</span><span class="sxs-lookup"><span data-stu-id="12ccd-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="12ccd-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="12ccd-150">Timestamper</span></span> | <span data-ttu-id="12ccd-151">RFC 3161 時間戳記伺服器的 URL。</span><span class="sxs-lookup"><span data-stu-id="12ccd-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="12ccd-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="12ccd-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="12ccd-153">RFC 3161 時間戳記伺服器所使用的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="12ccd-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="12ccd-154">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="12ccd-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="12ccd-155">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="12ccd-155">Verbosity</span></span> | <span data-ttu-id="12ccd-156">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="12ccd-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="12ccd-157">範例</span><span class="sxs-lookup"><span data-stu-id="12ccd-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```