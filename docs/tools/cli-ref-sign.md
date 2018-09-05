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
# <a name="sign-command-nuget-cli"></a>sign 命令 (NuGet CLI)

**適用於：** 封裝建立&bullet;**支援的版本：** 4.6 +

會比對第一個引數，使用憑證的所有封裝。 從檔案或從安裝在憑證存放區提供主體名稱或指紋的憑證，就可以取得具有私密金鑰的憑證。

封裝簽章尚無法在.NET Core、 Mono，或在非 Windows 平台上。

## <a name="usage"></a>使用量

```cli
nuget sign <package(s)> [options]
```

何處`<package(s)>`是一或多個`.nupkg`檔案。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定用來搜尋憑證的本機憑證存放區的憑證的 sha-1 指紋。 |
| CertificatePassword | 如有需要請指定憑證的密碼。 如果憑證有密碼保護，但不提供任何密碼，此命令會提示輸入密碼在執行階段，除非-非互動式選項傳遞。 |
| CertificatePath | 指定要用來簽署封裝的憑證檔案路徑。 |
| CertificateStoreLocation | 指定 X.509 憑證存放區使用，若要搜尋的憑證名稱。 預設值為"CurrentUser"，目前使用者所使用的 X.509 憑證存放區。 指定的憑證，透過-CertificateSubjectName 或-CertificateFingerprint 選項時，應該使用此選項。 |
| CertificateStoreName | 指定要用來搜尋憑證的 X.509 憑證存放區的名稱。 預設值為"My"，個人憑證的 X.509 憑證存放區。 指定的憑證，透過-CertificateSubjectName 或-CertificateFingerprint 選項時，應該使用此選項。 |
| CertificateSubjectName | 指定用來搜尋憑證的本機憑證存放區的憑證的主體名稱。  搜尋是使用所提供的值，可以找出所有的憑證包含該字串，其他資料值的主體名稱不區分大小寫的字串比較。  -CertificateStoreName 和-CertificateStoreLocation 選項所指定的憑證存放區。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| HashAlgorithm | 要用來簽署封裝的雜湊演算法。 預設為 SHA256。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| OutputDirectory | 指定用來儲存已簽署的封裝的目錄。 依預設已簽署的封裝會覆寫原始封裝。 |
| 覆寫 | 表示如果應該覆寫目前的簽章的參數。 如果封裝已簽章，則預設將會失敗命令。 |
| Timestamper | RFC 3161 時間戳記伺服器 URL。 |
| TimestampHashAlgorithm | RFC 3161 時間戳記伺服器所使用的雜湊演算法。 預設為 SHA256。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

## <a name="examples"></a>範例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```