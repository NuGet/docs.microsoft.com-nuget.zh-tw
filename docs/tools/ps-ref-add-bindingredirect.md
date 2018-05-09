---
title: NuGet 加入 BindingRedirect PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台新增 BindingRedirect PowerShell 命令的參考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>新增 BindingRedirect （在 Visual Studio 中的封裝管理員主控台）

*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

會檢查專案的輸出路徑內的所有組件，並在需要時，將繫結重新導向加入至應用程式或 web 組態檔。 安裝套件時，就會自動執行此命令。

如需繫結重新導向和使用的原因的詳細資訊，請參閱[重新導向組件版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文件中。

## <a name="syntax"></a>語法

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| ProjectName | （必要）要在其中加入繫結重新導向的專案。 -ProjectName 參數是選擇性的。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Add-BindingRedirect` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```