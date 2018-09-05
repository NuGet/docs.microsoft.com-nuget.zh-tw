---
title: NuGet 註冊 TabExpansion PowerShell 參考
description: 在 NuGet 套件管理員主控台中，在 Visual Studio 中的暫存器 TabExpansion PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546601"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>註冊 TabExpansion （在 Visual Studio 中的套件管理員主控台）

*只能在[NuGet 套件管理員主控台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

註冊指定的命令參數的 tab 鍵擴充，這類輸入命令時使用索引標籤時，擴充的值會顯示為可用的選項，如有問題的參數。 會覆寫任何先前的展開命令。

## <a name="syntax"></a>語法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| 名稱 | （必要）要用來註冊擴充的命令。 -名稱是選擇性參數本身。 |
| 定義 | （必要）物件，描述語法中的引數`@{'<parameter>' = {'<value1>', '<value2>', ...}}`何處`<parameter>`是要修改的參數和每個名稱`<value>`提供特定的擴充。 接受單引號和雙引號。 |

這些參數都不接受管線輸入或萬用字元的字元。

## <a name="common-parameters"></a>一般參數

`Register-TabExpansion` 支援下列[常用 PowerShell 參數](http://go.microsoft.com/fwlink/?LinkID=113216)： 偵錯、 錯誤動作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

請考慮包含三個專案名稱 EventManager、 公用程式及 SpecialParser 的方案。 開發人員經常使用`Update-Package`命令在不同的時間，與每個這些專案。 她發現方便`Update-Package`命令提供自動完成擴充功能`-ProjectName`引數，因此她不需要每次輸入專案名稱。 

下列命令，然後將這三個專案名稱註冊為擴充的`-ProjectName`參數：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開發人員可以再輸入`Update-Package -ProjectName `、 按 Tab 鍵，並請參閱，以自動完成選項的展開：

![使用暫存器 TabExpansion 的範例](media/Register-TabExpansion-Example.png)
