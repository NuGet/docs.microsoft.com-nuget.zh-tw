---
title: NuGet 1.5 版本資訊
description: NuGet 1.5 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383345"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 版本資訊

[Nuget 1.4 版本](../release-notes/nuget-1.4.md)資訊 | [nuget 1.6 版本](../release-notes/nuget-1.6.md)資訊

NuGet 1.5 已于2011年8月30日發行。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>具有預先安裝 NuGet 套件的專案範本
在建立新的 ASP.NET MVC 3 專案範本時，專案中所包含的 jQuery 腳本程式庫會藉由安裝 NuGet 套件，實際放在該處。

ASP.NET MVC 3 專案範本包含一組 NuGet 套件，會在叫用專案範本時一併安裝。 這項包含 NuGet 套件與專案範本的功能現在是 NuGet 的功能，_任何_專案範本現在都可以利用。

如需這項功能的詳細資訊，請閱讀此[功能開發人員提供的這篇 blog 文章](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>明確元件參考

已加入新的 `<references />` 專案，用來明確指定應參考封裝內的哪些元件。

例如，如果您新增下列內容：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然後只有 `xunit.dll` 和 `xunit.extensions.dll` 會從 `lib` 資料夾的適當[架構/設定檔子](../reference/nuspec.md#explicit-assembly-references)資料夾中參考，即使資料夾中有其他元件也一樣。

如果省略此元素，則會套用平常的行為，也就是參考 `lib` 資料夾中的每個元件。

__這項功能的用途為何？__

這項功能僅支援設計階段元件。 例如，當使用程式碼合約時，合約元件必須在其擴充的執行時間元件旁邊，以便 Visual Studio 可以找到它們，但合約元件不應實際由專案參考，也不能複製到 `bin` 資料夾中。

同樣地，此功能可用於單元測試架構（例如 XUnit），其工具元件必須位於執行時間元件旁，但從專案參考中排除。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>已新增在 nuspec 中排除檔案的能力
`.nuspec` 檔案中的 `<file>` 專案，可以用來包含特定檔案或使用萬用字元的一組檔案。 使用萬用字元時，沒有任何方法可以排除所包含檔案的特定子集。 例如，假設您想要資料夾內的所有文字檔（特定檔案除外）。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

請使用分號來指定多個檔案。

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

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>使用對話方塊移除套件時，會提示您移除相依性
卸載具有相依性的套件時，NuGet 會提示，允許移除套件的相依性及套件。

![移除相依封裝](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令改進
`Get-Package` 命令現在支援 `-ProjectName` 參數。 因此，命令

    Get-Package –ProjectName A

會列出所有安裝在專案 A 中的封裝。

### <a name="support-for-proxies-that-require-authentication"></a>支援需要驗證的 proxy
在需要驗證的 proxy 後方使用 NuGet 時，NuGet 現在會提示您提供 proxy 認證。 輸入認證可讓 NuGet 連接到遠端存放庫。

### <a name="support-for-repositories-that-require-authentication"></a>支援需要驗證的存放庫
NuGet 現在支援連接到需要基本或 NTLM 驗證的[私人存放庫](../hosting-packages/local-feeds.md)。

未來的版本將會加入摘要式驗證的支援。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 存放庫的效能改進
我們對 nuget.org 資源庫進行了幾項效能改善，讓套件清單和搜尋更快。

### <a name="solution-dialog-project-filtering"></a>方案對話方塊專案篩選
在 [方案層級] 對話方塊中，提示您要安裝的專案時，我們只會顯示與所選封裝相容的專案。

### <a name="package-release-notes"></a>套件版本資訊
NuGet 套件現在包含版本資訊的支援。 版本資訊只會在查看套件的_更新_時顯示，因此將它們新增至您的第一個版本並不合理。

![[更新] 索引標籤中的版本資訊](./media/manage-nuget-packages-release-notes.png)

若要將版本資訊新增至套件，請在 NuSpec 檔案中使用新的 `<releaseNotes />` 中繼資料元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & ltfiles/&gt; 改進
`.nuspec` 檔案現在允許空的 `<files />` 元素，這會指示 nuget.exe 不要在套件中包含任何檔案。

## <a name="bug-fixes"></a>Bug 修正
NuGet 1.5 總共已修正107個工作專案。 103的已標示為 bug。

如需 NuGet 1.5 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>錯誤修正值得注意：

* [問題 1273](http://nuget.codeplex.com/workitem/1273)：藉由依字母順序排序套件並移除額外的空白字元，讓 `packages.config` 更好的版本控制。
* [問題 844](http://nuget.codeplex.com/workitem/844)：現已正規化版本號碼，因此 `Install-Package 1.0` 在版本 `1.0.0`的封裝上運作。
* [問題 1060](http://nuget.codeplex.com/workitem/1060)：使用 nuget.exe 建立封裝時，`-Version` 旗標會覆寫 `<version />` 元素。
