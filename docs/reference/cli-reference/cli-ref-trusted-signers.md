---
title: NuGet CLI 受信任-簽署者命令
description: Nuget.exe 受信任的簽署者命令的參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610338"
---
# <a name="trusted-signers-command-nuget-cli"></a>受信任-簽署者命令（NuGet CLI）

**適用于：** 套件耗用量 &bullet;**支援的版本：** 4.9.1 +

取得或設定 NuGet 設定的受信任簽署者。 如需其他用法，請參閱[一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 如需有關 nuget.exe 架構外觀的詳細資訊，請參閱[nuget 設定檔參考](../nuget-config-file.md)。

## <a name="usage"></a>使用量

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

如果未指定任何 `list|add|remove|sync`，則此命令會預設為 `list`。

## <a name="nuget-trusted-signers-list"></a>nuget 受信任-簽署者清單

列出設定中所有受信任的簽署者。 此選項會包含每位簽署者具有的所有憑證（具有指紋和指紋演算法）。 如果憑證有前面的 `[U]`，則表示憑證專案已 `allowUntrustedRoot` 設定為 `true`。

以下是此命令的輸出範例：

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

## <a name="nuget-trusted-signers-add-options"></a>nuget 受信任-簽署者新增 [選項]

將具有指定名稱的受信任簽署者加入至設定。此選項會有不同的手勢來新增信任的作者或存放庫。

## <a name="options-for-add-based-on-a-package"></a>依據封裝新增的選項

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

其中 `<package(s)>` 是一或多個 `.nupkg` 檔案。

| 選項 | 描述 |
| --- | --- |
| 作者 | 指定封裝的作者簽章應該是受信任的。 |
| 儲存機制 | 指定應信任套件的存放庫簽章或副署。 |
| AllowUntrustedRoot | 指定信任的簽署者的憑證是否應允許鏈到不受信任的根。 |
| Owners | 信任的擁有者清單（以分號分隔），以進一步限制存放庫的信任。 只有在使用 [`-Repository`] 選項時才有效。 |

不支援同時提供 `-Author` 和 `-Repository`。

## <a name="options-for-add-based-on-a-service-index"></a>根據服務索引新增的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：此選項只會新增信任的存放庫。 

| 選項 | 描述 |
| --- | --- |
| ServiceIndex | 指定要信任之存放庫的 V3 服務索引。 此存放庫必須支援存放庫簽章資源。 如果未提供，此命令會尋找具有相同 `-Name` 的套件來源，並從該處取得服務索引。 |
| AllowUntrustedRoot | 指定信任的簽署者的憑證是否應允許鏈到不受信任的根。 |
| Owners | 信任的擁有者清單（以分號分隔），以進一步限制存放庫的信任。 |

## <a name="options-for-add-based-on-the-certificate-information"></a>根據憑證資訊新增的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：如果已存在具有指定名稱的受信任簽署者，則會將憑證專案新增至該簽署者。 否則，將會使用指定憑證資訊中的憑證專案來建立信任的作者。

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定憑證的憑證指紋，其簽署的套件必須以簽署。 憑證指紋是憑證的雜湊。 用於計算此雜湊的雜湊演算法應該在 [`FingerprintAlgorithm`] 選項中指定。 |
| FingerprintAlgorithm | 指定用來計算憑證指紋的雜湊演算法。 預設值為 `SHA256`。 支援的值為 `SHA256`、`SHA384` 和 `SHA512` |
| AllowUntrustedRoot | 指定信任的簽署者的憑證是否應允許鏈到不受信任的根。 |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 受信任-簽署者移除名稱 \<名稱\>

移除任何符合指定名稱的受信任簽署者。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 受信任-簽署者同步-名稱 \<名稱\>

要求目前信任的存放庫中所使用的最新憑證清單，以更新受信任簽署者中的現有憑證清單。

_注意_：此手勢會刪除目前的憑證清單，並將其取代為存放庫中的最新清單。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| 說明 | 顯示命令的說明資訊。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。 |

## <a name="examples"></a>範例

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
