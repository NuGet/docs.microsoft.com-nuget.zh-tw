---
title: NuGet 開放 PackagePage PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中開啟 PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547164"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio 套件管理員主控台)

*在 3.0 + 中; 已被取代只能在[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

會啟動預設瀏覽器中使用的專案、 授權或指定封裝的檢舉不當使用 URL。

## <a name="syntax"></a>語法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ID | 所需套件的套件識別碼。 -識別碼是選擇性參數本身。 |
| 版本 | 將預設為最新版本的封裝版本。 |
| 原始程式檔 | 封裝來源，將預設為來源下拉式清單中選取的來源。 |
| 使用權 | 瀏覽器開啟至套件的授權 URL。 如果-授權和-ReportAbuse 都未指定，則瀏覽器會開啟套件的專案 URL。 |
| ReportAbuse | 瀏覽器開啟至套件的檢舉不當使用 URL。 如果-授權和-ReportAbuse 都未指定，則瀏覽器會開啟套件的專案 URL。 |
| PassThru | 顯示的 URL;若要隱藏開啟瀏覽器使用-WhatIf。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Open-PackagePage` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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