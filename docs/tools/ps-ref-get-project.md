---
title: NuGet 專案 PowerShell 參考
description: 在 Visual Studio 中的 NuGet 套件管理員主控台的 GetProject PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842272"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio 套件管理員主控台)

*只能在[Package Manager Console](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

顯示預設值或指定的專案相關資訊。 `Get-Project` 特別是回到專案的 Visual Studio DTE （開發工具環境） 物件的參照。

## <a name="syntax"></a>語法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 名稱 | 指定專案，以顯示，請將預設為選取 套件管理員主控台中的預設專案。 -Name 參數是選擇性本身。 |
| All | 會顯示解決方案中每個專案的資訊專案的順序不具決定性。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Get-Project` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，詳細資訊、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```