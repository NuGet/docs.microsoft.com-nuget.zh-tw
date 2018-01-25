---
title: "NuGet 1.5 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.5。"
keywords: "NuGet 1.5 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 版本資訊

[NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md) | [NuGet 1.6 版本資訊](../release-notes/nuget-1.6.md)

NuGet 1.5 已於 2011 年 8 月 30 日發行。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>專案範本以預先安裝的 NuGet 套件
建立新的 ASP.NET MVC 3 專案範本時，包含在專案中的 jQuery 指令碼程式庫會實際放在該處安裝 NuGet 封裝。

ASP.NET MVC 3 專案範本包含一組叫用的專案範本時，取得安裝的 NuGet 封裝。 這項功能包含 NuGet 封裝的專案範本現在是 NuGet 的功能，_任何_專案範本現在可以充分利用。

如需有關這項功能的詳細資訊，請閱讀本[功能的開發人員部落格文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>明確的組件參考

加入新`<references />`用來明確指定組件內的項目應該要參考的封裝。

例如，如果您將加入下列：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然後只`xunit.dll`和`xunit.extensions.dll`會參考適當[framework/設定檔的子資料夾](../schema/nuspec.md#explicit-assembly-references)的`lib`即使資料夾中沒有其他組件的資料夾。

如果省略此元素，則很平常的行為，也就是參考中的每個組件適用於`lib`資料夾。

__這項功能的使用是？__

此功能支援設計階段只有組件。 比方說，當使用程式碼合約，合約組件必須為它們擴大，讓 Visual Studio 可以找到它們，但應該不實際專案所參考的合約組件，並不會複製到執行階段組件旁邊`bin`資料夾。

同樣地，此功能可用來針對單元測試架構，例如 XUnit 需要旁的執行階段組件，但排除專案參考其工具組件。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>若要排除在.nuspec 檔案新增的功能
`<file>`內的項目`.nuspec`檔案可以用來包含特定的檔案或一組使用萬用字元的檔案。 使用萬用字元時, 沒有任何方法可以排除的特定子集包含的檔案。 例如，假設您想要特定以外之資料夾中的所有文字檔案。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

使用分號來指定多個檔案。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

或使用萬用字元來排除一組檔案，例如所有備份檔案

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>移除封裝使用的對話方塊會提示您移除相依性
當正在解除安裝的封裝相依性，NuGet 會提示，可讓封裝的相依性，以及套件移除。

![移除相依的套件](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package`命令的改進
`Get-Package`命令現在支援`-ProjectName`參數。 因此命令

    Get-Package –ProjectName A

會列出所有專案 A.中安裝的封裝

### <a name="support-for-proxies-that-require-authentication"></a>Proxy 需要驗證的支援
當使用 NuGet 需要驗證的 proxy 後面時，NuGet 會現在會提示輸入 proxy 認證。 輸入認證，可讓連接至遠端儲存機制的 NuGet。

### <a name="support-for-repositories-that-require-authentication"></a>需要驗證的儲存機制的支援
NuGet 現在支援連接至[私用儲存機制](../hosting-packages/local-feeds.md)需要基本或 NTLM 驗證。

在未來版本將會加入摘要式驗證的支援。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 儲存機制的效能增強功能
我們已經 nuget.org 圖庫 列出及更快速搜尋套件的數個效能改良。

### <a name="solution-dialog-project-filtering"></a>方案對話方塊專案篩選
在方案層級對話方塊中，若要安裝哪些專案的提示時，我們只會顯示所選取封裝相容的專案。

### <a name="package-release-notes"></a>封裝的版本資訊
NuGet 封裝現在包含版本資訊的支援。 版本會資訊向上只顯示檢視時_更新_是封裝，因此不會更有意義，將它們加入您的第一次釋放。

![在 [更新] 索引標籤中的版本資訊](./media/manage-nuget-packages-release-notes.png)

若要加入封裝的版本資訊，請使用 新`<releaseNotes />`NuSpec 檔中的中繼資料元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt;改進
`.nuspec`檔現在可讓空白`<files />`元素，其會告知 nuget.exe 加入封裝中的任何檔案。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.5 有工作項目固定 107 總數。 這些 103 被標示為錯誤。

如需完整的工作清單項目固定在 NuGet 1.5，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修正：

* [問題 1273年](http://nuget.codeplex.com/workitem/1273)： 進行`packages.config`易記藉由依字母順序排序封裝，並移除多餘的空白字元的多個版本控制。
* [問題 844](http://nuget.codeplex.com/workitem/844)： 現在會正規化版本號碼以便`Install-Package 1.0`版封裝適用於`1.0.0`。
* [問題 1060年](http://nuget.codeplex.com/workitem/1060)： 使用 nuget.exe，建立封裝時`-Version`覆寫的旗標`<version />`項目。
