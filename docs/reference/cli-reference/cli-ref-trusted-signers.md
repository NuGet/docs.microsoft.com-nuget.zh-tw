---
title: NuGet CLI 受信任-簽署者命令
description: nuget.exe 受信任簽署者命令的參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9dd3fe3786c824c4a0a1cb252aa50cfc4458a483
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859417"
---
# <a name="trusted-signers-command-nuget-cli"></a>受信任的簽署者命令 (NuGet CLI) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 4.9.1 +

取得或設定受信任的簽署者為 NuGet 設定。 如需其他使用方式，請參閱 [一般 NuGet](../../consume-packages/configuring-nuget-behavior.md)設定。 如需 nuget.config 架構外觀的詳細資訊，請參閱 [NuGet 設定檔參考](../nuget-config-file.md)。

## <a name="usage"></a>使用方式

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

如果 `list|add|remove|sync` 未指定任何，則命令會預設為 `list` 。

## <a name="nuget-trusted-signers-list"></a>nuget 受信任-簽署者清單

列出設定中所有受信任的簽署者。 此選項會包含所有憑證 (指紋和指紋演算法，) 每位簽署者都有。 如果憑證前面有 `[U]` ，則表示該憑證專案已 `allowUntrustedRoot` 設定為 `true` 。

以下是此命令的輸出範例：

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget 受信任-簽署者新增 [選項]

將具有指定名稱的受信任簽署者新增至設定。此選項有不同的手勢可新增信任的作者或存放庫。

## <a name="options-for-add-based-on-a-package"></a>以套件為基礎的新增選項

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。

- **`-Author`**

  指定要信任的封裝 () 的作者簽章。

- **`-AllowUntrustedRoot`**

  指定是否應允許受信任簽署者的憑證連結至不受信任的根。

- **`-Owners`**

  以分號分隔的受信任擁有者清單，以進一步限制存放庫的信任。 只有在使用選項時才有效 `-Repository` 。

- **`-Repository`**

  指定要信任的封裝 () 的存放庫簽章或副署。

`-Author`不支援同時提供和 `-Repository` 。

## <a name="options-for-add-based-on-a-service-index"></a>根據服務索引新增的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：此選項只會新增信任的存放庫。 

- **`-AllowUntrustedRoot`**

  指定是否應允許受信任簽署者的憑證連結至不受信任的根。

- **`-Owners`**

  以分號分隔的受信任擁有者清單，以進一步限制存放庫的信任。

- **`-ServiceIndex`**

  指定要信任之存放庫的 V3 服務索引。 此存放庫必須支援存放庫簽章資源。 如果未提供，則命令會尋找具有相同的套件來源 `-Name` ，並從該處取得服務索引。

## <a name="options-for-add-based-on-the-certificate-information"></a>根據憑證資訊新增的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：如果已有具有指定名稱的受信任簽署者存在，則憑證專案將會新增至該簽署人。 否則，將會使用指定憑證資訊的憑證專案來建立信任的作者。


- **`-AllowUntrustedRoot`**

  指定是否應允許受信任簽署者的憑證連結至不受信任的根。

- **`-CertificateFingerprint`**

  指定憑證的憑證指紋，簽署的套件必須用來簽署。 憑證指紋是憑證的雜湊。 用來計算此雜湊的雜湊演算法應該在選項中指定 `FingerprintAlgorithm` 。

- **`-FingerprintAlgorithm`**

  指定用來計算憑證指紋的雜湊演算法。 預設值為 `SHA256`。 支援的值為 `SHA256` 、 `SHA384` 和 `SHA512` 。

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 受信任-簽署者移除名稱 \<name\>

移除任何符合指定名稱的受信任簽署者。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 受信任-簽署者同步-名稱 \<name\>

要求目前受信任存放庫中使用的最新憑證清單，以更新受信任簽署者中的現有憑證清單。

_注意_：此手勢將會刪除目前的憑證清單，並將其取代為存放庫中的最新清單。

## <a name="options"></a>選項

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-Name`**

  受信任簽署者的名稱。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。


## <a name="examples"></a>範例

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
