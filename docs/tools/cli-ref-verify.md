---
title: NuGet CLI 確認命令
description: Nuget.exe 的參考會確認命令
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462848"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**適用於：** 封裝耗用量&bullet;**支援的版本：** 4.6 +

驗證封裝。

驗證簽署的封裝尚未支援在.NET Core Mono，或在非 Windows 平台上。

## <a name="usage"></a>使用量

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中`<package(s)>`是一個或多個`.nupkg`檔案。

## <a name="nuget-verify--all"></a>驗證 nuget-所有

指定所有的驗證可能要執行的封裝上。

## <a name="nuget-verify--signatures"></a>驗證 nuget-簽章

指定要執行的封裝簽章驗證。

## <a name="options-for-verify--signatures"></a>「 驗證的簽章 」 的選項

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定一或多個 sha-256 憑證指紋的憑證 (s) 必須經過簽署的簽署的封裝。 使用 sha-256 憑證指紋是憑證的 sha-256 雜湊。 多個輸入應該是以分號分隔。 |

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| ForceEnglishOutput | 強制使用的非變異的英文文化特性來執行 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

## <a name="examples"></a>範例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```