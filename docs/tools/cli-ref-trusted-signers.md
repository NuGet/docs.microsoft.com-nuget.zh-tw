---
title: NuGet CLI 信任簽署命令
description: Nuget.exe 信任簽署命令參考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324704"
---
# <a name="trusted-signers-command-nuget-cli"></a>受信任簽署命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 4.9.1+

取得或設定受信任的簽署人的 NuGet 組態。 額外的使用量，請參閱 <<c0> [ 設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)。 如需有關如何 nuget.config 結構描述的樣貌，請參閱[NuGet 組態檔參考](../reference/nuget-config-file.md)。

## <a name="usage"></a>使用量

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

如果沒有任何`list|add|remove|sync`未指定，命令會預設為`list`。

## <a name="nuget-trusted-signers-list"></a>nuget 受信任簽署清單

列出組態中的所有受信任的簽署。 此選項，將會包含所有憑證 （使用指紋和指紋演算法） 具有每個簽署者。 如果憑證具有前面`[U]`，這表示憑證項目已`allowUntrustedRoot`設定為`true`。

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

## <a name="nuget-trusted-signers-add-options"></a>nuget 受信任簽署新增 [選項]

將具有指定名稱的受信任簽署者加入至組態中。此選項會有不同的手勢，來新增受信任的作者或存放庫。

## <a name="options-for-add-based-on-a-package"></a>新增套件為基礎的選項

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

何處`<package(s)>`是一或多個`.nupkg`檔案。

| 選項 | 描述 |
| --- | --- |
| 作者 | 指定套件的作者簽章應該是受信任。 |
| 儲存機制 | 指定的存放庫簽章或副署的套件應該是受信任。 |
| AllowUntrustedRoot | 指定是否允許受信任簽署者的憑證鏈結至不受信任的根。 |
| Owners | 以分號分隔清單的受信任的擁有者，來進一步限制的儲存機制的信任。 使用時，唯一有效`-Repository`選項。 |

同時提供`-Author`和`-Repository`不支援在相同的時間。

## <a name="options-for-add-based-on-a-service-index"></a>新增服務索引為基礎的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：此選項只會將受信任的存放庫。 

| 選項 | 描述 |
| --- | --- |
| ServiceIndex | 指定要信任的存放庫的 V3 服務索引。 此存放庫，就必須支援的存放庫簽章的資源。 如果未提供，此命令會尋找具有相同的套件來源`-Name`並從該處取得服務索引。 |
| AllowUntrustedRoot | 指定是否允許受信任簽署者的憑證鏈結至不受信任的根。 |
| Owners | 以分號分隔清單的受信任的擁有者，來進一步限制的儲存機制的信任。 |

## <a name="options-for-add-based-on-the-certificate-information"></a>新增的憑證資訊為基礎的選項

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_：如果已經存在具有指定名稱的受信任簽署者，憑證項目會加入該簽章者。 否則會建立受信任的作者與憑證項目從提供的憑證資訊。

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定已簽署的套件的憑證指紋必須經過簽署的憑證。 憑證指紋是憑證的雜湊。 在指定的雜湊演算法，用來計算此雜湊應為`FingerprintAlgorithm`選項。 |
| FingerprintAlgorithm | 指定用來計算憑證指紋的雜湊演算法。 預設值為 `SHA256`。 支援的值為`SHA256`，`SHA384`和 `SHA512` |
| AllowUntrustedRoot | 指定是否允許受信任簽署者的憑證鏈結至不受信任的根。 |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 受信任簽署 remove-名稱 <name>

移除符合指定之名稱的任何受信任的簽署。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 受信任簽署同步-名稱 <name>

要求目前受信任的存放庫中用來更新憑證的最新清單中受信任簽署者的現有憑證清單。

_注意_：此動作會刪除目前的憑證清單，並取代從存放庫的最新清單。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

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
