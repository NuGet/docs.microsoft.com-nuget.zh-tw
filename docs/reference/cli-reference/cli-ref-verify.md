---
title: NuGet CLI 驗證命令
description: Nuget.exe verify 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327495"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**適用于:** 套件耗&bullet;用量**支援的版本:** 4.6 +

驗證套件。

在 .NET Core、Mono 或非 Windows 平臺上, 尚未支援已簽署套件的驗證。

## <a name="usage"></a>使用量

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中`<package(s)>`是一或多`.nupkg`個檔案。

## <a name="nuget-verify--all"></a>nuget 驗證-全部

指定所有可能的驗證都應該在封裝上執行。

## <a name="nuget-verify--signatures"></a>nuget 驗證-簽章

指定應該執行封裝簽章驗證。

## <a name="options-for-verify--signatures"></a>「驗證-簽章」的選項

| 選項 | 說明 |
| --- | --- |
| CertificateFingerprint | 指定憑證的一個或多個 SHA-256 憑證指紋, 其簽署的套件必須經過簽署。 憑證 SHA-256 指紋是憑證的 SHA-256 雜湊。 多個輸入應以分號分隔。 |

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| ForceEnglishOutput | 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

## <a name="examples"></a>範例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```