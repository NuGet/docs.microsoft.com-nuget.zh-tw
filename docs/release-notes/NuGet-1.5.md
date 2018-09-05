---
title: NuGet 1.5 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.5 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548721"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 版本資訊

[NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md) | [NuGet 1.6 版版本資訊](../release-notes/nuget-1.6.md)

於 2011 年 8 月 30 日發行 NuGet 1.5。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>使用預先安裝的 NuGet 套件的專案範本
當建立新的 ASP.NET MVC 3 專案範本，jQuery 指令碼程式庫專案中包含實際放在這裡安裝 NuGet 套件。

ASP.NET MVC 3 專案範本包含一組叫用的專案範本時就會安裝的 NuGet 套件。 這項功能包含 NuGet 套件，使用專案範本現在是 NuGet 的功能，_任何_專案範本現在可以利用。

如需進一步瞭解這項功能的詳細資訊，請閱讀本[功能的開發人員的部落格文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>明確的組件參考

已新增`<references />`用來明確指定的組件內的項目應參考的套件。

比方說，如果您加入下列內容：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

則只有`xunit.dll`並`xunit.extensions.dll`會參考從適當[framework/設定檔的子資料夾](../reference/nuspec.md#explicit-assembly-references)的`lib`即使在資料夾中有其他組件的資料夾。

如果省略這個項目，則很平常的行為，也就是參考中的每個組件適用於`lib`資料夾。

__這項功能的用途為何？__

此功能支援設計階段只有組件。 比方說，當使用程式碼合約，合約組件需要為它們擴大以便 Visual Studio 可以找到它們，但是合約組件，不應實際參考專案，並不會複製到執行階段組件旁邊`bin`資料夾。

同樣地，此功能可用來針對單元測試架構，例如 XUnit 需要旁的執行階段組件，但排除專案參考其工具組件。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>若要排除在.nuspec 檔案的新增的功能
`<file>`內的項目`.nuspec`檔案可以用來包含特定檔案或一組使用萬用字元的檔案。 當使用萬用字元，沒有任何方法可以排除特定子集包含的檔案。 例如，假設您想要一個以外的資料夾內的所有文字檔案。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

您可以使用分號來指定多個檔案。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

或使用萬用字元來排除一組檔案，例如所有的備份檔案

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>移除套件使用的對話方塊會提示您移除相依性
當 解除安裝封裝，以利用相依性，NuGet 會提示，可讓封裝以及封裝的相依性移除。

![移除相依的套件](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令的改進
`Get-Package`命令現在支援`-ProjectName`參數。 因此命令

    Get-Package –ProjectName A

會列出安裝在專案 a 中的所有封裝

### <a name="support-for-proxies-that-require-authentication"></a>Proxy 需要驗證的支援
當需要驗證的 proxy 後方使用 NuGet，NuGet 現在會在 proxy 認證提示。 輸入認證，可讓連線至遠端存放庫的 NuGet。

### <a name="support-for-repositories-that-require-authentication"></a>適用於需要驗證的存放庫的支援
NuGet 現在支援連接至[私用存放庫](../hosting-packages/local-feeds.md)需要基本或 NTLM 驗證。

針對摘要式驗證的支援會加入未來的版本。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 存放庫的效能改善
我們已對 nuget.org 資源庫，若要讓套件清單，並更快速搜尋的數個效能改良。

### <a name="solution-dialog-project-filtering"></a>方案對話方塊專案篩選
在方案層級對話方塊中，若要安裝哪些專案的提示時，我們只會顯示與所選套件相容的專案。

### <a name="package-release-notes"></a>套件版本資訊
NuGet 套件現已支援的版本資訊。 版本會資訊向上只讓檢視時_更新_是封裝，因此沒有任何意義，將它們加入您的第一個版本。

![在 [更新] 索引標籤內的版本資訊](./media/manage-nuget-packages-release-notes.png)

若要加入封裝的版本資訊，請使用 新`<releaseNotes />`NuSpec 檔案中的中繼資料元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt;改進
`.nuspec`檔現在可讓空`<files />`項目，它會告訴 nuget.exe 不到封裝中包含任何檔案。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.5 必須共 107 工作固定的項目。 這些 103 已標示為錯誤。

如需完整的工作清單項目中已修正 NuGet 1.5，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的錯誤修正：

* [問題 1273年](http://nuget.codeplex.com/workitem/1273)： 進行`packages.config`易記藉由依字母順序排序套件，並移除額外的空白字元的多個版本控制。
* [問題 844](http://nuget.codeplex.com/workitem/844)： 現在會正規化版本號碼，讓`Install-Package 1.0`作用於封裝版本`1.0.0`。
* [問題 1060年](http://nuget.codeplex.com/workitem/1060)： 當使用 nuget.exe，建立封裝`-Version`覆寫的旗標`<version />`項目。
