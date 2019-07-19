---
title: NuGet 取得專案 PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 GetProject PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327355"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio 套件管理員主控台)

*僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*

顯示預設或指定專案的相關資訊。 `Get-Project`特別傳回專案的 Visual Studio DTE (開發工具環境) 物件的參照。

## <a name="syntax"></a>語法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 名稱 | 指定要顯示的專案, 預設為封裝管理員主控台中選取的預設專案。 -Name 參數本身是選擇性的。 |
| All | 顯示方案中每個專案的資訊;專案的順序不具決定性。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Get-Project`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```