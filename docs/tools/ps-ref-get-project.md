---
title: NuGet Get 專案 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台的 GetProject PowerShell 命令的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio 套件管理員主控台)

*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

顯示預設值或指定的專案相關資訊。 `Get-Project` 特別是傳回專案的 Visual Studio DTE （開發工具環境） 物件參考。

## <a name="syntax"></a>語法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 名稱 | 指定要顯示，請將預設為 Package Manager Console 中選取的預設專案。 -Name 參數是選擇性本身。 |
| 全部 | 顯示方案; 中的每個專案的資訊專案的順序不具決定性。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Get-Project` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```