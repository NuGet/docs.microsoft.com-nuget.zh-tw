---
title: NuGet CLI 驗證命令
description: nuget.exe verify 命令的參考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238136"
---
# <a name="verify-command-nuget-cli"></a>確認 (NuGet CLI 的命令) 

**適用物件：** 套件耗用量 &bullet; **支援的版本：** 4.6 +

驗證套件。

Mono 下尚未支援已簽署套件的驗證。

## <a name="usage"></a>使用方式

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中 `<package(s)>` 是一或多個檔案 `.nupkg` 。

## <a name="nuget-verify--all"></a>nuget 驗證-全部

指定所有可能的驗證都應該在封裝 (s) 上執行。

## <a name="nuget-verify--signatures"></a>nuget 驗證-簽章

指定應執行封裝簽章驗證。

## <a name="options-for-verify--signatures"></a>「驗證簽章」的選項

- **`-CertificateFingerprint`**

  指定憑證 (s 的一或多個 256 SHA-1 憑證指紋，) 簽署的套件必須使用簽署。 憑證 256 SHA-1 指紋是憑證的 SHA-256 雜湊。 多個輸入應以分號分隔。

## <a name="options"></a>選項

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

## <a name="examples"></a>範例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```