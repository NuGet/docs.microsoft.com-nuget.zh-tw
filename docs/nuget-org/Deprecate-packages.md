---
title: Nuget.org 上的淘汰套件
description: 淘汰封裝程式的詳細描述，以及用戶端如何顯示此資訊
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248894"
---
# <a name="deprecating-packages"></a>淘汰套件

如果您不再維護封裝，或想要鼓勵套件的取用者移至另一個套件，您可以取代套件。 

套件取代與**取消列出**您的套件不同，如下所述：
* **取消列出**套件會防止其探索，因為它會隱藏在搜尋結果中。 
* **淘汰**封裝可讓您的套件現有取用者瞭解其是否已在其專案中安裝或使用。 它也會讓他們知道取代的原因，以及您所指定的替代建議套件（封裝發行者）。 淘汰封裝不會取消列出套件。 

身為發行者，您可以選擇取消列出和取代套件。

## <a name="deprecation-workflow"></a>淘汰工作流程
1. 若要取代封裝，請移至 [**管理套件**]，**然後選取 [** 淘汰]：

    ![移至取代封裝選項](media/deprecation-select-option.png)

2. 選取您想要取代的版本。 如果您想要取代所有版本，請選擇 [**選取所有版本**] 選項。

    ![選取要取代的套件版本](media/deprecation-select-version.png)

3. 選擇取代的原因。 如果不再維護封裝，請選擇 [**舊版**] 選項。 如果特定版本有重大錯誤，請選擇 [**有重大錯誤**] 選項。 基於任何其他原因，請選取 [**其他**]。 您一律可以為擁有者指定替代的建議套件（和版本）和自訂訊息。 

    ![選取原因替代套件建議和自訂訊息](media/deprecation-save.png)

> [!Note]
> 自訂訊息只會顯示在 nuget.org 上，但不會顯示在用戶端上。 目前， `dotnet.exe`和 NuGet 套件管理員之類的用戶端不會顯示自訂訊息。

## <a name="client-experience-for-deprecated-packages"></a>已淘汰套件的用戶端體驗
一旦套件已淘汰，其取用者會以下列方式收到通知（視使用的用戶端而定）。

### <a name="visual-studio"></a>Visual Studio 
*從 Visual Studio 2019 版本16.3 開始提供*

Visual Studio 警告索引標籤上`Installed`已淘汰的套件使用方式。它會將您導向封裝及其取代資訊（包括已淘汰的原因，以及要改用的替代封裝，如果有的話）。

   ![套件管理員 Visual Studio 已安裝 索引標籤上的已淘汰套件](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*從 .NET SDK 3.0 開始提供*

如果您使用 dotnet，您可以在方案或專案資料夾`dotnet list package --deprecated`上執行命令，以取得已淘汰的套件清單以及取代資訊：

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
