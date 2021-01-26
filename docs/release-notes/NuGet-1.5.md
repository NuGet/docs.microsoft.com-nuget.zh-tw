---
title: NuGet 1.5 版本資訊
description: NuGet 1.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777098"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 版本資訊

[NuGet 1.4 版本](../release-notes/nuget-1.4.md)  |  資訊[NuGet 1.6 版本](../release-notes/nuget-1.6.md)資訊

NuGet 1.5 已于2011年8月30日發行。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>具有預先安裝 NuGet 套件的專案範本
建立新的 ASP.NET MVC 3 專案範本時，專案中包含的 jQuery 腳本程式庫實際上是藉由安裝 NuGet 套件來放置。

ASP.NET MVC 3 專案範本包含一組 NuGet 套件，可在叫用專案範本時一併安裝。 包含 NuGet 套件與專案範本的這項功能現在是 NuGet 的功能， _任何_ 專案範本現在都可以利用。

如需這項功能的詳細資訊，請閱讀此 [功能開發人員的這篇 blog 文章](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>明確的元件參考

加入新的專案 `<references />` ，用來明確指定應參考封裝內的哪些元件。

例如，如果您新增下列內容：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然後，只 `xunit.dll` 會 `xunit.extensions.dll` 從資料夾的適當 [架構/設定檔子](../reference/nuspec.md#explicit-assembly-references) 資料夾中參考和， `lib` 即使資料夾中有其他元件也一樣。

如果省略此元素，則會套用一般行為，也就是參考資料夾中的每個元件 `lib` 。

__這項功能的用途為何？__

這項功能僅支援設計階段元件。 例如，使用程式碼合約時，合約元件必須位於它們所擴充之執行時間元件的旁邊，以便 Visual Studio 可以找到它們，但是合約元件不應實際由專案參考，也不應該複製到 `bin` 資料夾。

同樣地，這項功能可用於單元測試架構（例如 XUnit），這類架構需要在執行時間元件旁邊找出其工具元件，但不能從專案參考中排除。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>已新增在 nuspec 中排除檔案的能力。
檔案 `<file>` 內的專案 `.nuspec` 可以用來包含特定檔案或使用萬用字元的檔案集合。 使用萬用字元時，不會有任何方法可以排除包含之檔案的特定子集。 例如，假設您想要一個資料夾中的所有文字檔，但有特定的檔案。

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

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>使用對話方塊來移除套件會提示移除相依性
卸載具有相依性的套件時，NuGet 會提示您允許移除套件的相依性和套件。

![移除相依封裝](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令改進
`Get-Package`命令現在支援 `-ProjectName` 參數。 命令

```
Get-Package –ProjectName A
```

會列出安裝在專案 A 中的所有套件。

### <a name="support-for-proxies-that-require-authentication"></a>支援需要驗證的 proxy
在需要驗證的 proxy 後方使用 NuGet 時，NuGet 現在會提示您輸入 proxy 認證。 輸入認證可讓 NuGet 連接至遠端存放庫。

### <a name="support-for-repositories-that-require-authentication"></a>支援需要驗證的儲存機制
NuGet 現在支援連接到需要基本或 NTLM 驗證的 [私人存放庫](../hosting-packages/local-feeds.md) 。

未來的版本將會新增摘要式驗證的支援。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 存放庫的效能改進
我們已對 nuget.org 資源庫進行數個效能改進，讓套件清單和搜尋更快。

### <a name="solution-dialog-project-filtering"></a>解決方案對話方塊專案篩選
在 [方案層級] 對話方塊中，當提示您要安裝哪些專案時，我們只會顯示與所選套件相容的專案。

### <a name="package-release-notes"></a>封裝版本資訊
NuGet 套件現在包含版本資訊的支援。 版本資訊只會在查看套件的 _更新_ 時顯示，因此將它們新增至您的第一個版本並不合理。

![[更新] 索引標籤中的版本資訊](./media/manage-nuget-packages-release-notes.png)

若要將版本資訊加入封裝，請在 NuSpec 檔中使用新的 `<releaseNotes />` 中繼資料元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>nuspec &ltfiles/ &gt; 改進
檔案 `.nuspec` 現在允許空的 `<files />` 元素，這會告知 nuget.exe 不包含封裝中的任何檔案。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.5 總共修正了107個工作專案。 這些標記為 bug 的103。

如需 NuGet 1.5 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>Bug 修正值得注意：

* [問題 1273](http://nuget.codeplex.com/workitem/1273)： `packages.config` 依字母順序排序封裝和移除額外的空白字元，讓版本控制更容易使用。
* [問題 844](http://nuget.codeplex.com/workitem/844)：現在已將版本號碼正規化，以便 `Install-Package 1.0` 在具有版本的套件上運作 `1.0.0` 。
* [問題 1060](http://nuget.codeplex.com/workitem/1060)：使用 nuget.exe 建立封裝時，旗標會 `-Version` 覆寫 `<version />` 元素。
