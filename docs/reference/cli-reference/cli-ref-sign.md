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
# <a name="sign-command-nuget-cli"></a> (NuGet CLI 的 sign 命令) 

**適用物件：** 套件建立 &bullet; **支援的版本：** 4.6 +

使用憑證簽署符合第一個引數的所有套件。 具有私密金鑰的憑證可以透過提供主體名稱或指紋，從檔案或憑證存放區中安裝的憑證取得。

> [!Note]
> 在 .NET Core、Mono 或非 Windows 平臺上，尚未支援套件簽署。

## <a name="usage"></a>使用方式

```cli
nuget sign <package(s)> [options]
```

其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。

## <a name="options"></a>選項。

- **`-CertificateFingerprint`**

  指定憑證的 SHA-1 指紋，用來搜尋憑證的本機憑證存放區。

- **`-CertificatePassword`**

  指定憑證密碼（如有需要）。 如果憑證受到密碼保護，但未提供密碼，則命令會在執行時間提示輸入密碼，除非 `-NonInteractive` 已傳遞該選項。

- **`-CertificatePath`**

  指定要用於簽署封裝之憑證的檔案路徑。

- **`-CertificateStoreLocation`**

  指定 x.509 憑證存放區用來搜尋憑證的名稱。 預設為 "CurrentUser"，這是目前使用者所使用的 x.509 憑證存放區。 透過或選項指定憑證時，應使用這個 `-CertificateSubjectName` 選項 `-CertificateFingerprint` 。

- **`-CertificateStoreName`**

  指定用來搜尋憑證的 x.509 憑證存放區名稱。 預設值為 "My"，也就是個人憑證的 x.509 憑證存放區。 透過或選項指定憑證時，應使用這個 `-CertificateSubjectName` 選項 `-CertificateFingerprint` 。

- **`-CertificateSubjectName`**

  指定憑證的主體名稱，用來搜尋憑證的本機憑證存放區。  搜尋是使用提供的值進行不區分大小寫的字串比較，它會尋找所有具有該字串之主體名稱的憑證，而不考慮其他主體值。  您可以使用和選項來指定憑證存放區 `-CertificateStoreName` `-CertificateStoreLocation` 。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-HashAlgorithm`**

  用來簽署套件的雜湊演算法。 預設為 SHA256。 可能的值為 SHA256、SHA384 和 SHA512。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-OutputDirectory`**

  指定要儲存已簽署之封裝的目錄。 依預設，已簽署的套件會覆寫原始封裝。

- **`-Overwrite`**

  切換以指出是否應該覆寫目前的簽章。 根據預設，如果封裝已經有簽章，此命令將會失敗。

- **`-Timestamper`**

  RFC 3161 時間戳記伺服器的 URL。

- **`-TimestampHashAlgorithm`**

  RFC 3161 時間戳記伺服器所使用的雜湊演算法。 預設為 SHA256。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

## <a name="examples"></a>範例

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
