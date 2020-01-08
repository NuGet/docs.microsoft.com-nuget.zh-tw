---
title: NuGet CLI sign 命令
description: Nuget.exe sign 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 746f7a421bd855b77716388b4af2fecbd5cf5a68
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676402"
---
# <a name="sign-command-nuget-cli"></a>sign 命令（NuGet CLI）

**適用于：** 套件建立 &bullet;**支援的版本：** 4.6 +

使用憑證簽署符合第一個引數的所有套件。 具有私密金鑰的憑證可以透過提供主體名稱或指紋，從檔案或安裝在憑證存放區中的憑證取得。

> [!Note]
> 在 .NET Core、Mono 或非 Windows 平臺上，尚未支援套件簽署。

## <a name="usage"></a>使用

```cli
nuget sign <package(s)> [options]
```

其中 `<package(s)>` 是一或多個 `.nupkg` 檔案。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定憑證的 SHA-1 指紋，用來搜尋憑證的本機憑證存放區。 |
| CertificatePassword | 指定憑證密碼（如有需要）。 如果憑證受密碼保護，但未提供密碼，除非傳遞-非互動式選項，否則命令會在執行時間提示輸入密碼。 |
| CertificatePath | 指定要用來簽署封裝之憑證的檔案路徑。 |
| CertificateStoreLocation | 指定用來搜尋憑證的 x.509 憑證存放區名稱。 預設為 "CurrentUser"，這是目前使用者所使用的 x.509 憑證存放區。 當您透過-CertificateSubjectName 或-CertificateFingerprint 選項指定憑證時，應該使用此選項。 |
| CertificateStoreName | 指定要用來搜尋憑證的 x.509 憑證存放區名稱。 預設為 "My"，個人憑證的 x.509 憑證存放區。 當您透過-CertificateSubjectName 或-CertificateFingerprint 選項指定憑證時，應該使用此選項。 |
| CertificateSubjectName | 指定用來搜尋憑證之本機憑證存放區的憑證主體名稱。  搜尋是使用提供的值時，不區分大小寫的字串比較，它會尋找具有包含該字串之主體名稱的所有憑證，而不論其他主體值為何。  憑證存放區可以透過-CertificateStoreName 和-CertificateStoreLocation 選項來指定。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| HashAlgorithm | 要用來簽署封裝的雜湊演算法。 預設為 SHA256。 |
| 說明 | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| OutputDirectory | 指定應儲存已簽署封裝的目錄。 根據預設，已簽署的套件會覆寫原始的封裝。 |
| 覆寫 | 切換以指出是否應該覆寫目前的簽章。 根據預設，如果封裝已有簽章，此命令將會失敗。 |
| Timestamper | RFC 3161 時間戳記伺服器的 URL。 |
| TimestampHashAlgorithm | RFC 3161 時間戳記伺服器所要使用的雜湊演算法。 預設為 SHA256。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |

## <a name="examples"></a>範例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
