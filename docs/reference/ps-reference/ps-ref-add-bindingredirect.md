---
title: NuGet BindingRedirect PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 BindingRedirect PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327455"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio 套件管理員主控台)

*僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*

檢查項目輸出路徑中的所有元件, 並在必要時將系結重新導向新增至應用程式或 web 設定檔。 安裝套件時, 會自動執行此命令。

如需系結重新導向和其使用原因的詳細資訊, 請參閱 .NET 檔中的重新導向[元件版本](/dotnet/framework/configure-apps/redirect-assembly-versions)。

## <a name="syntax"></a>語法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ProjectName | 具備要加入系結重新導向的專案。 -專案名稱參數本身是選擇性的。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Add-BindingRedirect`支援下列[常用的 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216):Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```