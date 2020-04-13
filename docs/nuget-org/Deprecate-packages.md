---
title: 棄用nuget.org包
description: 有關棄用套件程序以及客戶端如何顯示此資訊的詳細說明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096876"
---
# <a name="deprecating-packages"></a>棄用包

如果您不再維護包,或者希望鼓勵包的消費者轉到其他包,則可以棄用包。 

包棄用不同於**取消列出**包,如下所述:
* **取消列出**包會阻止其發現,因為它隱藏在搜尋結果中。 
* **棄用**包可以讓包的現有消費者瞭解其是否在其專案中安裝或使用。 它還讓他們知道棄用的原因以及您指定的備用建議包(包發行者)。 棄用包不會取消列出包。 

作為發行者,您可以選擇取消列出包和棄用包。

## <a name="deprecation-workflow"></a>棄用工作流
1. 要棄用套件,請轉到 **"管理包"** 並選擇 **「棄用**」 :

    ![跳到棄用套件選項](media/deprecation-select-option.png)

2. 選擇要棄用的版本。 如果要棄用所有版本,**請選擇「選擇所有版本**」選項。

    ![選擇要棄用的套件版本](media/deprecation-select-version.png)

3. 選擇棄用的原因。 如果包不再維護,請選擇 **「舊版」** 選項。 如果特定版本存在嚴重錯誤,請選擇 **「具有嚴重錯誤」** 選項。 出於任何其他原因,請選擇 **"其他**"。 您始終可以指定備用建議的包(和版本)和給擁有者的自定義消息。 

    ![選擇備用套件建議與自訂訊息的原因](media/deprecation-save.png)

> [!Note]
> 自定義消息僅在nuget.org上顯示,但不顯示在用戶端。 目前,像和`dotnet.exe`NuGet 包管理器這樣的用戶端不顯示自訂訊息。

## <a name="client-experience-for-deprecated-packages"></a>棄用套件的客戶端體驗
一旦包被棄用,就會以下列方式通知其消費者(取決於所使用的用戶端)。

### <a name="visual-studio"></a>Visual Studio 
*可從 Visual Studio 2019 版本 16.3 開始*

Visual Studio`Installed`警告 選項卡上已棄用的包的使用。它將顯示包及其棄用資訊的警告(包括棄用的原因和備用包(如果存在)。如果存在, 則改為使用。

   ![在安裝的「視覺工作室」選項卡上的已棄用包,選項卡上已安裝的包管理器](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*可從 .NET SDK 3.0 開始*

如果使用 dotnet.exe,則可以在解決方案或專案`dotnet list package --deprecated`資料夾 上執行該指令,以取得有關棄用套件的清單以及棄用資訊:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
