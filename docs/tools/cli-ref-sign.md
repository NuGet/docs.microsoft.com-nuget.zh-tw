---
title: NuGet CLI 登命令
description: Nuget.exe 登命令參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546359"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="6c93a-103">sign 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6c93a-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="6c93a-104">**適用於：** 封裝建立&bullet;**支援的版本：** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="6c93a-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="6c93a-105">會比對第一個引數，使用憑證的所有封裝。</span><span class="sxs-lookup"><span data-stu-id="6c93a-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="6c93a-106">從檔案或從安裝在憑證存放區提供主體名稱或指紋的憑證，就可以取得具有私密金鑰的憑證。</span><span class="sxs-lookup"><span data-stu-id="6c93a-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="6c93a-107">封裝簽章尚無法在.NET Core、 Mono，或在非 Windows 平台上。</span><span class="sxs-lookup"><span data-stu-id="6c93a-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="6c93a-108">使用量</span><span class="sxs-lookup"><span data-stu-id="6c93a-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="6c93a-109">何處`<package(s)>`是一或多個`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="6c93a-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="6c93a-110">選項</span><span class="sxs-lookup"><span data-stu-id="6c93a-110">Options</span></span>

| <span data-ttu-id="6c93a-111">選項</span><span class="sxs-lookup"><span data-stu-id="6c93a-111">Option</span></span> | <span data-ttu-id="6c93a-112">描述</span><span class="sxs-lookup"><span data-stu-id="6c93a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c93a-113">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6c93a-113">CertificateFingerprint</span></span> | <span data-ttu-id="6c93a-114">指定用來搜尋憑證的本機憑證存放區的憑證的 sha-1 指紋。</span><span class="sxs-lookup"><span data-stu-id="6c93a-114">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="6c93a-115">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="6c93a-115">CertificatePassword</span></span> | <span data-ttu-id="6c93a-116">如有需要請指定憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="6c93a-116">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="6c93a-117">如果憑證有密碼保護，但不提供任何密碼，此命令會提示輸入密碼在執行階段，除非-非互動式選項傳遞。</span><span class="sxs-lookup"><span data-stu-id="6c93a-117">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="6c93a-118">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="6c93a-118">CertificatePath</span></span> | <span data-ttu-id="6c93a-119">指定要用來簽署封裝的憑證檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="6c93a-119">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="6c93a-120">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="6c93a-120">CertificateStoreLocation</span></span> | <span data-ttu-id="6c93a-121">指定 X.509 憑證存放區使用，若要搜尋的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="6c93a-121">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="6c93a-122">預設值為"CurrentUser"，目前使用者所使用的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="6c93a-122">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="6c93a-123">指定的憑證，透過-CertificateSubjectName 或-CertificateFingerprint 選項時，應該使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c93a-123">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="6c93a-124">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="6c93a-124">CertificateStoreName</span></span> | <span data-ttu-id="6c93a-125">指定要用來搜尋憑證的 X.509 憑證存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c93a-125">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="6c93a-126">預設值為"My"，個人憑證的 X.509 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="6c93a-126">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="6c93a-127">指定的憑證，透過-CertificateSubjectName 或-CertificateFingerprint 選項時，應該使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6c93a-127">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="6c93a-128">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="6c93a-128">CertificateSubjectName</span></span> | <span data-ttu-id="6c93a-129">指定用來搜尋憑證的本機憑證存放區的憑證的主體名稱。</span><span class="sxs-lookup"><span data-stu-id="6c93a-129">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="6c93a-130">搜尋是使用所提供的值，可以找出所有的憑證包含該字串，其他資料值的主體名稱不區分大小寫的字串比較。</span><span class="sxs-lookup"><span data-stu-id="6c93a-130">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="6c93a-131">-CertificateStoreName 和-CertificateStoreLocation 選項所指定的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="6c93a-131">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="6c93a-132">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6c93a-132">ConfigFile</span></span> | <span data-ttu-id="6c93a-133">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="6c93a-133">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6c93a-134">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="6c93a-134">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6c93a-135">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6c93a-135">ForceEnglishOutput</span></span> | <span data-ttu-id="6c93a-136">會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="6c93a-136">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6c93a-137">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="6c93a-137">HashAlgorithm</span></span> | <span data-ttu-id="6c93a-138">要用來簽署封裝的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="6c93a-138">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="6c93a-139">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="6c93a-139">Defaults to SHA256.</span></span> |
| <span data-ttu-id="6c93a-140">說明</span><span class="sxs-lookup"><span data-stu-id="6c93a-140">Help</span></span> | <span data-ttu-id="6c93a-141">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="6c93a-141">Displays help information for the command.</span></span> |
| <span data-ttu-id="6c93a-142">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6c93a-142">NonInteractive</span></span> | <span data-ttu-id="6c93a-143">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="6c93a-143">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6c93a-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="6c93a-144">OutputDirectory</span></span> | <span data-ttu-id="6c93a-145">指定用來儲存已簽署的封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="6c93a-145">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="6c93a-146">依預設已簽署的封裝會覆寫原始封裝。</span><span class="sxs-lookup"><span data-stu-id="6c93a-146">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="6c93a-147">覆寫</span><span class="sxs-lookup"><span data-stu-id="6c93a-147">Overwrite</span></span> | <span data-ttu-id="6c93a-148">表示如果應該覆寫目前的簽章的參數。</span><span class="sxs-lookup"><span data-stu-id="6c93a-148">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="6c93a-149">如果封裝已簽章，則預設將會失敗命令。</span><span class="sxs-lookup"><span data-stu-id="6c93a-149">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="6c93a-150">Timestamper</span><span class="sxs-lookup"><span data-stu-id="6c93a-150">Timestamper</span></span> | <span data-ttu-id="6c93a-151">RFC 3161 時間戳記伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="6c93a-151">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="6c93a-152">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="6c93a-152">TimestampHashAlgorithm</span></span> | <span data-ttu-id="6c93a-153">RFC 3161 時間戳記伺服器所使用的雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="6c93a-153">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="6c93a-154">預設為 SHA256。</span><span class="sxs-lookup"><span data-stu-id="6c93a-154">Defaults to SHA256.</span></span> |
| <span data-ttu-id="6c93a-155">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6c93a-155">Verbosity</span></span> | <span data-ttu-id="6c93a-156">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="6c93a-156">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6c93a-157">範例</span><span class="sxs-lookup"><span data-stu-id="6c93a-157">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```