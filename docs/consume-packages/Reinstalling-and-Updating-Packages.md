---
title: 重新安裝和更新 NuGet 套件
description: 何時需要重新安裝和更新套件的詳細資料，與 Visual Studio 中的損毀套件參考相同。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237727"
---
# <a name="how-to-reinstall-and-update-packages"></a>如何重新安裝和更新套件

在[重新安裝套件的時機](#when-to-reinstall-a-package)下方所述的許多情況中，Visual Studio 專案內套件的參考可能損毀。 在這些情況下，解除安裝後重新安裝相同版本的套件，將會還原這些工作順序參考。 更新套件，只是表示安裝更新的版本，這通常會還原套件的工作順序。

在 Visual Studio 中，套件管理員主控台會提供許多彈性的選項來更新及重新安裝套件。

更新和重新安裝套件已完成，如下所示：

| 方法 | 更新 | 重新安裝 |
| --- | --- | --- |
| 套件管理員主控台 (如[使用 Update-Package](#using-update-package) 中所述) | `Update-Package` 命令 | `Update-Package -reinstall` 命令 |
| 套件管理員 UI | 在 [更新]  索引標籤上，選取一或多個套件，然後選取 [更新]  | 在 [已安裝]  索引標籤上，選取套件，並記錄其名稱，然後選取 [解除安裝]  。 切換至 [瀏覽]  索引標籤，並搜尋套件名稱，再選取它，然後選取 [安裝]  。 |
| nuget.exe CLI | `nuget update` 命令 | 針對所有套件，刪除套件資料夾，然後執行 `nuget install`。 針對單一套件，刪除套件資料夾，然後使用 `nuget install <id>` 重新安裝相同套件。 |

> [!NOTE]
> 若為 dotnet CLI，則不需要相同的程序。 在類似案例中，您可以[使用 dotnet CLI 還原套件](package-restore.md#restore-using-the-dotnet-cli)。

本文內容：

- [重新安裝套件的時機](#when-to-reinstall-a-package)
- [限制升級版本](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>重新安裝套件的時機

1. **套件還原之後參考損毀** ：如果您已開啟專案並還原 NuGet 套件，但仍看到損毀參考，請嘗試重新安裝所有這些套件。
1. **專案因已刪除檔案而中斷** ：NuGet 不會防止您移除已從套件新增的項目，因此很容易不慎修改從套件安裝的內容，並中斷您的專案。 若要還原專案，請重新安裝受影響的套件。
1. **套件更新中斷了專案** ：如果套件的更新會中斷專案，失敗的原因通常是也曾經更新的相依性套件所造成。 若要還原相依性的狀態，請重新安裝該特定套件。
1. **保護重設目標或升級** ：已對專案重設目標或升級時，以及套件因目標架構變更而需要重新安裝時，這可能十分好用。 在這類情況下，NuGet 會在專案重定目標之後立即顯示建置錯誤，而後續的建置警告可讓您知道可能需要重新安裝套件。 針對專案升級，NuGet 會在專案升級記錄中顯示錯誤。
1. **在開發套件期間重新安裝套件** ：套件作者通常需要重新安裝他們所開發以測試該行為之相同版本的套件。 `Install-Package` 命令未提供選項來強制重新安裝，因此請改用 `Update-Package -reinstall`。

## <a name="constraining-upgrade-versions"></a>限制升級版本

重新安裝或更新套件預設「一律」  會安裝套件來源中可用的最新版本。

不過，在使用 `packages.config` 管理格式的專案中，您可以特別限制版本範圍。 例如，如果您知道您的應用程式僅適用於 1.x 版的套件，而不是 2.0 和更新版本 (可能是套件 API 中的主要變更所造成)，則會想要限制 1.x 版的升級。 這可避免破壞應用程式的意外更新。

若要設定條件約束，請在文字編輯器中開啟 `packages.config`，並找到有問題的相依性，然後使用版本範圍新增 `allowedVersions` 屬性。 例如，若要限制 1.x 版的更新，請將 `allowedVersions` 設定為 `[1,2)`：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

在所有情況下，都請使用[套件版本控制](../concepts/package-versioning.md#version-ranges)中所述的標記法。

## <a name="using-update-package"></a>使用 Update-Package

請注意下面所述的  > [NuGet 套件管理員]  > [套件管理員主控台]  )。

```ps
Update-Package -Id <package_name> –reinstall
```

使用此命令，會比移除套件後嘗試使用相同的版本在 NuGet 資源庫中找到相同的套件更為簡單。 請注意，`-Id` 是選擇性參數。

沒有 `-reinstall` 的相同命令會將套件更新為較新版本 (適用時)。 如果專案中尚未安裝有問題的套件，則此命令會顯示錯誤；也就是說，`Update-Package` 不會直接安裝套件。

```ps
Update-Package <package_name>
```

`Update-Package` 預設會影響方案中的所有專案。 若要將動作限制為特定專案，請使用 `-ProjectName` 參數，並使用出現在方案總管中的專案名稱：

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

若要「更新」  專案中的所有套件 (或使用 `-reinstall` 重新安裝)，請使用 `-ProjectName`，而不指定任何特定套件：

```ps
Update-Package -ProjectName MyProject
```

若要更新方案中的所有套件，只需要使用 `Update-Package` 本身，而沒有其他引數或參數。 請小心使用此表單，因為它可能需要相當長的時間才能執行所有更新：

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

使用 [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) 來更新專案或解決方案中的套件，一律會更新為最新版本的套件 (發行前套件除外)。 如有需要，使用 `packages.config` 的專案可以限制下面[限制升級版本](#constraining-upgrade-versions)中所述的更新版本。

如需命令的完整詳細資料，請參閱 [Update-Package](../reference/ps-reference/ps-ref-update-package.md) 參考。

### <a name="considerations"></a>考量

重新安裝套件時，下列可能會受到影響：

1. **根據專案目標架構重設目標來重新安裝套件**
    - 在簡單的情況下，使用 `Update-Package –reinstall <package_name>` 重新安裝套件就能運作。 解除安裝針對舊目標架構所安裝的套件，並針對專案的目前目標架構安裝相同套件。
    - 在某些情況下，可能會有不支援新目標架構的套件。
        - 如果套件支援可攜式類別庫 (PCL)，並將專案的目標重設為套件不再支援的平台組合，則套件的參考會在重新安裝之後遺失。
        - 這可能會出現您直接使用的套件，或作為相依性而安裝的套件。 您使用的套件可能會直接支援新的目標架構，而其相依性則否。
        - 如果在重設應用程式的目標之後重新安裝套件導致組建或執行階段錯誤，您可能需要還原目標架構，或搜尋正確支援新目標架構的替代套件。

1. **專案重設目標或升級之後 packages.config 中所新增的 requireReinstallation 屬性**
    - 如果 NuGet 偵測到重設目標或升級專案已影響套件，則會將 `packages.config` 中的 `requireReinstallation="true"` 屬性新增至所有受影響的套件參考。 因此，Visual Studio 中的每個後續組建都會引發這些套件的組建警告，讓您可以記得重新安裝它們。

1. **使用相依性重新安裝套件**
    - `Update-Package –reinstall` 會重新安裝相同版本的原始套件，但除非提供特定版本條件約束，否則會安裝最新版本的相依性。 這可讓您視需要僅更新相依性，以修正問題。 不過，如果這會將相依性復原為舊版本，則您可以使用 `Update-Package <dependency_name>` 重新安裝該相依性，而不影響相依的套件。
    - `Update-Package –reinstall <packageName> -ignoreDependencies` 會重新安裝相同版本的原始套件，但不重新安裝相依性。 更新套件相依性可能導致中斷狀態時，請使用此項目

1. **在涉及相依的版本時重新安裝套件**
    - 如上所述，重新安裝套件時不會變更與其相依之任何其他已安裝套件的版本。 接著，重新安裝相依性可能會中斷相依的套件。
