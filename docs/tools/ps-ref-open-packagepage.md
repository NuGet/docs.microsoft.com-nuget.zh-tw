---
title: NuGet 開啟 PackagePage PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中開啟 PackagePage PowerShell 命令的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio 套件管理員主控台)

*3.0 +; 中已被取代只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

啟動預設瀏覽器中使用專案、 授權或指定之封裝的報表濫用 URL。

## <a name="syntax"></a>語法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | 所要封裝之封裝 ID。 -Id 參數是選擇性的。 |
| 版本 | 預設為最新版本的封裝版本。 |
| 原始程式檔 | 封裝來源，將預設為 [來源] 下拉式清單中選取的來源。 |
| 使用權 | 瀏覽器開啟至封裝的授權 URL。 如果指定-授權都-ReportAbuse，瀏覽器會開啟封裝的專案 URL。 |
| ReportAbuse | 瀏覽器開啟至套件的報表濫用的 URL。 如果指定-授權都-ReportAbuse，瀏覽器會開啟封裝的專案 URL。 |
| PassThru | 顯示的 URL。您可以使用與-WhatIf 隱藏開啟瀏覽器。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Open-PackagePage` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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