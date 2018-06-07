---
title: NuGet 的暫存器 TabExpansion PowerShell 參考
description: 在 Visual Studio 中的 NuGet 封裝管理員主控台中的暫存器 TabExpansion PowerShell 命令的參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818409"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>暫存器 TabExpansion （在 Visual Studio 中的封裝管理員主控台）

*只能在[NuGet Package Manager Console](package-manager-console.md) Windows 上的 Visual Studio 中。*

註冊 tab 鍵擴充參數指定的命令，使得索引標籤使用時輸入命令時，擴充的值會顯示為可用的選項有問題的參數。 會覆寫任何先前的展開命令。

## <a name="syntax"></a>語法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 名稱 | （必要）要用來註冊擴充的命令。 -Name 參數是選擇性的。 |
| 定義 | （必要）物件，描述語法中的引數`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的參數和每個名稱`<value>`提供特定的擴充。 接受單引號與雙引號引號。 |

這些參數接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Register-TabExpansion` 支援下列[一般 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

請考慮包含三個專案名稱 EventManager、 公用程式及 SpecialParser 的方案。 開發人員經常使用`Update-Package`命令在不同的時間，與每個這些專案。 她發現方便`Update-Package`命令提供的自動完成擴充功能`-ProjectName`引數，因此她不需要每次出專案名稱輸入。 

下列命令，然後註冊這些三個專案的名稱為擴充的`-ProjectName`參數：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開發人員可以再輸入`Update-Package -ProjectName `、 按 tab 鍵，並請參閱，以自動完成選項的展開：

![使用暫存器 TabExpansion 的範例](media/Register-TabExpansion-Example.png)
