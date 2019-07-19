---
title: NuGet Open-PackagePage PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327375"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio 套件管理員主控台)

*已在 3.0 + 中淘汰;僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*

使用指定封裝的 [專案]、[授權] 或 [報表濫用 URL] 來啟動預設瀏覽器。

## <a name="syntax"></a>語法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | 所需套件的封裝識別碼。 -Id 參數本身是選擇性的。 |
| 版本 | 封裝的版本, 預設為最新版本。 |
| Source | 封裝來源, 預設為 [來源] 下拉式選單中選取的來源。 |
| 使用權 | 將瀏覽器開啟至套件的授權 URL。 如果未指定-License 或-ReportAbuse, 瀏覽器會開啟封裝的專案 URL。 |
| ReportAbuse | 將瀏覽器開啟至套件的報告濫用 URL。 如果未指定-License 或-ReportAbuse, 瀏覽器會開啟封裝的專案 URL。 |
| PassThru | 顯示 URL;使用 with-WhatIf 來隱藏開啟瀏覽器。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Open-PackagePage`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```