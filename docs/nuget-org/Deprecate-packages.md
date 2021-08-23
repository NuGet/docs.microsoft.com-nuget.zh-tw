---
title: Nuget.org 上的淘汰套件
description: 淘汰封裝程式和用戶端如何顯示此資訊的詳細說明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726960"
---
# <a name="deprecating-packages"></a>淘汰套件

如果您不再維護套件，或是想要鼓勵封裝的取用者移至另一個套件，您可以取代封裝。 

套件淘汰不同于 **取消列出** 您的套件，如下所述：
* **取消列出** 套件會防止探索，因為它會在搜尋結果中隱藏。 
* **淘汰** 封裝可讓您的套件現有取用者瞭解它們是否已在其專案中安裝或使用。 它也可讓他們知道取代的原因，以及您 (套件發行者) 所指定的替代套件。 淘汰封裝未取消列出套件。 

做為發行者，您可以選擇取消列出和取代套件。

## <a name="deprecation-workflow"></a>淘汰工作流程
1. 若要取代套件，請移至 [ **管理封裝** ] **並選取 [** 取代]：

    ![移至取代套件選項](media/deprecation-select-option.png)

2. 選取您要取代的版本。 如果您想要取代所有版本，請選擇 [ **選取所有版本** ] 選項。

    ![選取要取代的套件版本](media/deprecation-select-version.png)

3. 選擇取代的原因。 如果不再保留封裝，請選擇 **舊版** 選項。 如果特定版本有重大 bug，請選擇 [ **有重大 bug** ] 選項。 基於任何其他原因，請選取 [ **其他**]。 您一律可以指定替代的建議套件 (和版本) 以及自訂訊息給擁有者。 

    ![選取替代套件建議和自訂訊息的原因](media/deprecation-save.png)

> [!Note]
> 自訂訊息只會顯示在 nuget.org，但不會顯示在用戶端上。 目前， `dotnet.exe` 和 NuGet 封裝管理員的用戶端並不會顯示自訂訊息。

## <a name="client-experience-for-deprecated-packages"></a>已淘汰套件的用戶端體驗
一旦套件淘汰之後，其取用者會以下列方式收到通知， (視使用) 的用戶端而定。

### <a name="visual-studio"></a>Visual Studio 
*從 Visual Studio 2019 16.3 版開始提供*

Visual Studio 警告有關索引標籤上已淘汰之套件的使用方式 `Installed` 。它會顯示封裝的警告和其取代資訊 (包括已淘汰的原因，以及改用替代套件（如果有) 的話）。

   ![套件管理員 Visual Studio 已安裝] 索引標籤上的已淘汰套件](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*從 .NET SDK 3.0 開始提供*

如果您使用 dotnet.exe，您可以 `dotnet list package --deprecated` 在方案或專案資料夾上執行命令，以取得已淘汰的套件清單以及取代的資訊：

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>將熱門程度轉移至較新的套件

已淘汰舊版套件的封裝作者可以選擇將其「熱門程度」轉移至較新的套件，以提升較新套件的搜尋排名。 這可協助客戶探索較新的封裝，而不是已淘汰的套件。

例如，假設我有兩個套件：

* 我已淘汰的舊版套件， `Contoso.Legacy` 含3000000下載
* 我最新的套件， `Contoso.Latest` 5 個下載

NuGet，則會優先使用較高下載/熱門的搜尋結果。 在指定搜尋查詢 "Contoso" 的情況下，我被取代的套件 `Contoso.Legacy` 可能會排名 `Contoso.Latest` 在搜尋結果中的最新套件。

為了解決這個問題，我可以申請將被取代的舊版封裝的熱門程度轉移至最新的套件。 這會導致 `Contoso.Latest` 搜尋結果中的排名較高，而 `Contoso.Legacy` 排名較低。 只有套件的內部熱門分數會受到影響，每個套件的實際下載計數不會受到影響。

> [!Note]
> 熱門轉移可讓取用者更難找到舊版套件。

請參閱下表，以瞭解熱門轉移對查詢 "Contoso" 的搜尋排名有何影響的具體概念：

| 搜尋排名    | 熱門轉移之前        | 熱門轉移之後         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso. Legacy、3M 下載*    | *Contoso. 最新版本，5次下載*     |
| 2                 | Contoso. 掃描器、2M 下載     | Contoso. 掃描器、2M 下載     |
| 3                 | Contoso. Core、1.5 M 下載     | Contoso. Core、1.5 M 下載     |
| 4                 | Contoso. UI、1M 下載          | Contoso. UI、1M 下載          |
| ...               | ...                               | ...                               |
| 20                | *Contoso. 最新版本，5次下載*     | *Contoso. Legacy、3M 下載*    |

### <a name="popularity-transfer-application-process"></a>熱門傳輸應用程式流程

1. 查看 [熱門轉移需求](#popularity-transfer-requirements)。
2. [account@nuget.org](mailto:account@nuget.org)使用已被取代的套件傳送的電子郵件，其最受歡迎的套件應該轉移，以及應接收熱門傳輸的穩定套件 () 清單。

提交應用程式之後，我們會通知您應用程式的接受或拒絕 (有造成拒絕) 的條件。 我們可能需要詢問額外的識別問題以確認擁有者身分識別。

#### <a name="popularity-transfer-requirements"></a>熱門傳輸需求

* 舊版封裝和新封裝必須共用所有擁有者。
* 新的封裝必須清楚地與命名和函式中的舊版套件相關 (也就是演進或下一代) 。
* 舊版套件的所有版本都必須被取代，並指向接收傳送的新套件。
* 熱門轉移對 NuGet 使用者或惡化 NuGet 搜尋體驗而言，不一定會造成混淆。
* 新的套件必須具有穩定版本。
* 舊版封裝不能從另一個已被取代的套件接收熱門轉移。

### <a name="advanced-popularity-transfer-scenarios"></a>先進的熱門轉移案例

#### <a name="package-consolidations"></a>封裝合併

我可以改為使用單一新套件來轉移多個已淘汰套件的熱門程度。 例如，假設我有3個套件：

* 我第一個被取代的舊版套件， `Contoso.Legacy1`
* 第二個已淘汰的舊版套件， `Contoso.Legacy2`
* 我的新合併套件 `Contoso.Latest`

取代和之後 `Contoso.Legacy1` `Contoso.Legacy2` ，我可以申請將其熱門程度轉移至 `Contoso.Latest` 。

#### <a name="package-splits"></a>封裝分割

已淘汰的套件熱門程度可以轉移至最多5個較新的套件，並加以分割。 如果已被取代之套件的功能已在多個新套件中分割，這就很有用。 例如，假設我有3個套件：

* 我已淘汰的舊版套件， `Contoso.Legacy`
* 我的第一個新套件， `Contoso.Web`
* 我的第二個新套件， `Contoso.Cloud`

`Contoso.Legacy` 同時包含 web 和雲端功能，但我決定將該功能分隔成不同的封裝，以供下一代之用。 取代之後 `Contoso.Legacy` ，我可以申請將其熱門程度轉移到 `Contoso.Web` 和 `Contoso.Cloud` 。

> [!Warning]
> 轉移的熱門程度將會平均分散到所有新的套件。 如此一來，我們建議您將已淘汰套件的熱門程度轉移到最少的套件。

#### <a name="popularity-transfer-chains"></a>熱門傳輸鏈

如果已被取代的套件已從另一個已被取代的套件接收熱門程度，則無法轉移其熱門程度。 例如，假設我有3個套件：

* 我已淘汰的舊版套件， `Contoso.First`
* 我已淘汰的舊版套件， `Contoso.Second`
* 我的新套件 `Contoso.Latest`

如果將 `Contoso.First` 其熱門程度轉移至， `Contoso.Second,` 則 `Contoso.Second` 無法將其熱門程度轉移至 `Contoso.Latest` 。 相反地，我們建議您 `Contoso.First` `Contoso.Second` `Contoso.Latest` 根據 [套件合併](#package-consolidations) 案例，將和的熱門程度轉移至。
