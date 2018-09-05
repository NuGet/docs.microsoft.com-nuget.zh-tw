---
title: NuGet CLI 確認命令
description: Nuget.exe 的參考會確認命令
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545209"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**適用於：** 套件耗用量&bullet;**支援的版本：** 4.6 +

驗證封裝。

驗證已簽署的套件尚未支援在.NET Core、 Mono，或在非 Windows 平台上。

## <a name="usage"></a>使用量

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

何處`<package(s)>`是一或多個`.nupkg`檔案。

## <a name="nuget-verify--all"></a>驗證 nuget-全部

指定所有可能的驗證之後，應該對套件。

## <a name="nuget-verify--signatures"></a>nuget 驗證-簽章

指定應該執行套件簽章驗證。

## <a name="options-for-verify--signatures"></a>針對 [驗證-簽章] 選項

| 選項 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定憑證 (s) 的已簽署的套件必須經過簽署的一或多個 SHA-256 憑證的指紋。 使用 SHA-256 憑證指紋是憑證的 SHA-256 雜湊。 多個輸入應該是以分號分隔。 |

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

## <a name="examples"></a>範例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```