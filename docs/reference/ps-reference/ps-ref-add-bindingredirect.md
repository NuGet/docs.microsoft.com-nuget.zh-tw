---
title: NuGet Add-BindingRedirect PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台中的 BindingRedirect PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623119"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>在 Visual Studio 中新增-BindingRedirect (封裝管理員主控台) 

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

`Add-BindingRedirect` 支援下列 [常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
