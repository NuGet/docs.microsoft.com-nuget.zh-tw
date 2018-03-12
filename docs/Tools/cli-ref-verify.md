---
title: "NuGet CLI 確認命令 |Microsoft 文件"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 的參考會確認命令"
keywords: "nuget 驗證參考，請確認命令"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a>確認命令 (NuGet CLI)

**適用於：**封裝耗用量&bullet;**支援的版本：** 4.6 +

驗證封裝。

## <a name="usage"></a>使用量

```cli
nuget verify <package(s)> [options]
```

其中`<package(s)>`是一個或多個`.nupkg`檔案。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| 全部 | 指定所有的驗證可能要執行的封裝上。 |
| CertificateFingerprint | 指定一或多個 sha-256 憑證指紋的憑證 (s) 必須經過簽署的簽署的封裝。 使用 sha-256 憑證指紋是憑證的 sha-256 雜湊。 多個輸入應該是以分號分隔。 |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | 強制使用的非變異的英文文化特性來執行 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 抑制使用者輸入或確認提示。 |
| 簽章 | 指定要執行的封裝簽章驗證。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

## <a name="examples"></a>範例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```