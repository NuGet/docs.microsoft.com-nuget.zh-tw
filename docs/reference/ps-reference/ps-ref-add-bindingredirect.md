---
title: NuGet Add-BindingRedirect PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Add-BindingRedirect PowerShell 命令參考。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777607"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Add-BindingRedirect (封裝管理員主控台

*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*

檢查項目輸出路徑內的所有元件，並在必要時將系結重新導向新增至應用程式或 web 設定檔。 此命令會在安裝套件時自動執行。

> [!NOTE]
> 這僅適用于使用 packages.config 檔案的案例。 如需詳細資訊，請參閱 [NuGet packages.config 檔案參考](~/reference/packages-config.md)。

如需系結重新導向及其使用原因的詳細資訊，請參閱 .NET 檔中的重新導向 [元件版本](/dotnet/framework/configure-apps/redirect-assembly-versions) 。

## <a name="syntax"></a>語法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ProjectName |  (需要) 要加入系結重新導向的專案。 -專案參數本身是選擇性的。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Add-BindingRedirect` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```