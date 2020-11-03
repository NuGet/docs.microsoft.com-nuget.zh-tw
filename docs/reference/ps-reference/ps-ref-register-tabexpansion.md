---
title: NuGet Register-TabExpansion PowerShell 參考
description: Visual Studio 中 NuGet 封裝管理員主控台的 Register-TabExpansion PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237149"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Visual Studio) 中的 Register-TabExpansion (封裝管理員主控台

*只能在 Windows 上 Visual Studio 的 [封裝管理員主控台](../../consume-packages/install-use-packages-powershell.md) 內使用。*

註冊指定命令之參數的索引標籤擴充，如此一來，當輸入命令時使用 Tab 鍵時，展開的值會顯示為有問題之參數的可用選項。 命令的任何先前的擴充都會遭到覆寫。

## <a name="syntax"></a>語法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| Name |  (需要) 註冊擴充的命令。 -Name 參數本身是選擇性的。 |
| 定義 |  (所需的) 物件描述語法中的引數， `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 其中 `<parameter>` 是要修改之參數的名稱，而每個都 `<value>` 提供特定的擴充。 單引號和雙引號都接受。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Register-TabExpansion` 支援下列 [常見的 PowerShell 參數](/powershell/module/microsoft.powershell.core/about/about_commonparameters)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

請考慮包含三個專案的方案 EventManager、公用程式和 SpecialParser。 開發人員經常會 `Update-Package` 在每個專案的不同時間使用命令。 她發現讓 `Update-Package` 命令提供自動完成擴充的 `-ProjectName` 引數很方便，因此她不需要每次都要輸入專案名稱。 

然後，下列命令會將這三個專案名稱註冊為參數的展開 `-ProjectName` ：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

然後，開發人員可以輸入 `Update-Package -ProjectName ` ，按下 tab 鍵，並查看以自動完成選項提供的擴充功能：

![使用 Register-TabExpansion 的範例](media/Register-TabExpansion-Example.png)