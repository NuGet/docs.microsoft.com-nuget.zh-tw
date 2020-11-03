---
title: NuGet Open-PackagePage PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Open-PackagePage PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238058"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Open-PackagePage (封裝管理員主控台

*3.0 + 中已淘汰;只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*

使用指定封裝的專案、授權或報告濫用 URL 來啟動預設瀏覽器。

## <a name="syntax"></a>語法

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | Description |
| --- | --- |
| Id | 所需封裝的封裝識別碼。 -Id 參數本身是選擇性的。 |
| 版本 | 封裝的版本，預設為最新版本。 |
| 來源 | 封裝來源，預設為來源下拉式清單中選取的來源。 |
| 授權 | 開啟瀏覽器並前往封裝的授權 URL。 如果未指定-License 或-ReportAbuse，瀏覽器會開啟套件的專案 URL。 |
| ReportAbuse | 開啟瀏覽器並前往封裝的檢舉不當使用 URL。 如果未指定-License 或-ReportAbuse，瀏覽器會開啟套件的專案 URL。 |
| PassThru | 顯示 URL;使用 with-WhatIf 來抑制開啟瀏覽器。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Open-PackagePage` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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