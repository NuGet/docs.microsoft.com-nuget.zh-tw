---
title: NuGet 套件中的發行前版本
description: 建置發行前版本套件的指引
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 150fc61e51fe10622fe6b369b60dfc61a9ac916f
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432448"
---
# <a name="building-pre-release-packages"></a>建置發行前版本套件

每當您使用新的版本號碼發行更新的套件時，NuGet 會將它視為「最新的穩定版本」(如範例所示)，例如在 Visual Studio 的套件管理員 UI 中：

![顯示最新穩定版本的套件管理員 UI](media/Prerelease_01-LatestStable.png)

穩定版本是認為足夠可靠能在生產環境中使用的版本。 最新的穩定版本也是會安裝為套件更新或在套件還原期間安裝的版本 (受[重新安裝及更新套件](../consume-packages/reinstalling-and-updating-packages.md)中所述的條件約束)。

為支援軟體發行生命週期，NuGet 1.6 和更新版本允許散發發行前套件，它們的版本號碼包含語意版本尾碼，例如 `-alpha`、`-beta` 或 `-rc`。 如需詳細資訊，請參閱[套件版本控制](../reference/package-versioning.md#pre-release-versions)。

有兩種方式可以指定這類版本：

- `.nuspec` 檔案：`version` 項目中包含語意版本尾碼：

    ```xml
    <version>1.0.1-alpha</version>
    ```

- 組件屬性：從 Visual Studio 專案建置套件時 (`.csproj` 或 `.vbproj`)，使用 `AssemblyInformationalVersionAttribute` 指定版本：

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet 會挑選此值，而非不支援語意版本控制的 `AssemblyVersion` 屬性中指定的值。

當您準備好要發行穩定版本時，只要移除尾碼，套件就會優先於任何發行前版本。 請再次參考[套件版本控制](../reference/package-versioning.md#pre-release-versions)。

## <a name="installing-and-updating-pre-release-packages"></a>安裝和更新發行前版本套件

NuGet 使用套件時預設不包含發行前版本，但是您可以如下所示變更此行為：

- **Visual Studio 中的套件管理員 UI**：在 [管理 NuGet 套件] UI 中，選取 [包含發行前版本] 方塊：

    ![Visual Studio 中的 [包含發行前版本] 核取方塊](media/Prerelease_02-CheckPrerelease.png)

    設定或清除此方塊會重新整理套件管理員 UI，以及您可以安裝的可用版本清單。

- **套件管理員主控台**：使用 `-IncludePrerelease` 參數搭配 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 與 `Update-Package` 命令。 請參閱 [PowerShell 參考](../tools/powershell-reference.md)。

- **NuGet CLI**：使用 `-prerelease` 參數搭配 `install`、`update`、`delete` 與 `mirror` 命令。 請參閱 [NuGet CLI 參考](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>語意版本控制

[語意化版本控制系統或 SemVer 慣例](http://semver.org/spec/v1.0.0.html)描述如何利用版本號碼中的字串傳遞基礎程式碼的意涵。

在此慣例中，每個版本都有三個部分 `Major.Minor.Patch`，代表意義如下：

- `Major`：重大變更
- `Minor`：新功能，但具回溯相容性
- `Patch`：僅具有回溯相容的錯誤 (Bug) 修正

然後在發行前版本的修補程式編號後附加連字號和一個字串。 就技術層面而言，連字號後面可以使用「任何」字串，NuGet 會將套件視為發行前版本。 然後，NuGet 會在適用的 UI 中顯示完整的版本號碼，讓取用者自行解譯其意義。

請記住，通常遵循如下所示的可辨識命名慣例會比較好：

- `-alpha`：Alpha 版本，通常用於進行中的工作和實驗
- `-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的錯誤 (Bug)。
- `-rc`：候選版，除非出現重大的錯誤 (Bug)，不然通常是準最終版本 (穩定版)。

> [!Note]
> NuGet 4.3.0+ 支援[ v2.0.0](http://semver.org/spec/v2.0.0.html)，其支援使用點標記法的發行前版本號碼，如同 `1.0.1-build.23`。 4.3.0 之前的 NuGet 版本不支援點標記法。 在舊版的 NuGet 中，您可以使用類似 `1.0.1-build23` 的形式，但之前向來將這視為發行前版本。

但無論使用什麼樣的尾碼，NuGet 都會以反向字母順序給予它們優先權：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

如範例所示，不含任何尾碼的版本一律優先於發行前版本。 另請注意，如果您使用數值尾碼和可能使用兩位數 (或以上) 數字的發行前版本標籤，請和 beta01 及 beta05 一樣前面加零，以確保數字變大時正確排序。
