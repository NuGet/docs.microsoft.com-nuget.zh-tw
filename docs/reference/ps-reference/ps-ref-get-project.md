---
title: NuGet Get-Project PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台中的 GetProject PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238071"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Get-Project (封裝管理員主控台

*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*

顯示預設或指定專案的相關資訊。 `Get-Project` 特別針對專案的 Visual Studio DTE (開發工具環境) 物件，傳回對的引用。

## <a name="syntax"></a>語法

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| Name | 指定要顯示的專案，預設為在封裝管理員主控台中選取的預設專案。 -Name 參數本身是選擇性的。 |
| 全部 | 顯示方案中每個專案的資訊;專案的順序不具決定性。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Get-Project` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```