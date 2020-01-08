---
title: NuGet 註冊-TabExpansion PowerShell 參考
description: Visual Studio 的 NuGet 套件管理員主控台中的 TabExpansion PowerShell 命令參考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384450"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>TabExpansion （Visual Studio 中的套件管理員主控台）

*僅適用于在 Windows 上 Visual Studio 的[套件管理員主控台](../../consume-packages/install-use-packages-powershell.md)中。*

為指定命令的參數註冊 tab 鍵擴充，讓您在輸入命令時使用 Tab 鍵時，展開的值會顯示為有問題之參數的可用選項。 系統會覆寫命令的任何先前的擴充。

## <a name="syntax"></a>語法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>參數

| 參數 | 描述 |
| --- | --- |
| Name | 具備要對其註冊擴充的命令。 -Name 參數本身是選擇性的。 |
| 定義 | 具備物件，描述語法中的引數 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 其中 `<parameter>` 是要修改的參數名稱，而每個 `<value>` 提供特定的擴充。 只接受單引號和雙引號。 |

這些參數都不接受管線輸入或萬用字元。

## <a name="common-parameters"></a>一般參數

`Register-TabExpansion` 支援下列[常見的 PowerShell 參數](https://go.microsoft.com/fwlink/?LinkID=113216)： Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>範例

假設有一個包含三個專案的方案： EventManager、公用程式和 SpecialParser。 開發人員經常會在每個專案的不同時間使用 `Update-Package` 命令。 她發現，讓 `Update-Package` 命令為 `-ProjectName` 引數提供自動完成擴充，讓她不需要每次都輸入專案名稱。 

然後，下列命令會將這三個專案名稱註冊為 `-ProjectName` 參數的擴充：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開發人員接著可以輸入 `Update-Package -ProjectName `，按 Tab 鍵，並查看作為自動完成選項提供的擴充功能：

![使用 Register-TabExpansion 的範例](media/Register-TabExpansion-Example.png)
