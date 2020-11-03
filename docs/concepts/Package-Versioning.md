---
title: NuGet 套件版本參考
description: 為 NuGet 套件相依的其他套件指定版本號碼和範圍，以及相依性安裝方式的確切詳細資料。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4cb12f439d796d583f52d657225c39418d5a4836
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237357"
---
# <a name="package-versioning"></a>套件版本控制

您一律必須使用套件的套件識別碼與確切版本號碼來參考特定套件。 例如，nuget.org 上的 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) \(英文\) 有數十個特定套件可用，範圍從 *4.1.10311* 版到 *6.1.3* 版 (最新穩定版本) 與各種發行前版本 (像是 *6.2.0-beta1* )。

在建立套件時，您可以搭配選擇性的發行前版本文字尾碼來指派特定版本號碼。 另一方面，在取用套件時，您可以指定確切版本號碼或可接受的版本範圍。

本主題內容：

- [版本基本概念](#version-basics)包含發行前版本尾碼。
- [版本範圍](#version-ranges)
- [標準化版本號碼](#normalized-version-numbers)

## <a name="version-basics"></a>版本基本概念

特定版本號碼的格式為「主要.次要.修補程式[-尾碼]」，其中的元件具有下列意義：

- *主要* ：重大變更
- *次要* ：新功能，但與舊版相容
- *Patch* ：僅回溯相容的 bug 修正
- 「-尾碼」(選擇性)：後面接著字串的連字號，表示發行前版本 (遵循[語意化版本控制系統或 SemVer 1.0 慣例](https://semver.org/spec/v1.0.0.html))。

**範例：**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 會拒絕任何缺少確切版本號碼的套件上傳。 您必須在 `.nuspec` 中，或在用來建立套件的專案檔中指定版本。

### <a name="pre-release-versions"></a>發行前版本

就技術上而言，套件建立者可以使用任何字串作為尾碼來表示發行前版本，因為 NuGet 會將任何此類版本視為發行前版本，而且不會進行任何其他解讀。 也就是說，NuGet 會在牽涉到的任何 UI 中顯示完整版本字串，尾碼之意義的任何解讀，都保留給取用者。

話雖如此，套件開發人員通常會遵循公認的命名慣例：

- `-alpha`： Alpha 版本，通常用於進行中的工作和實驗。
- `-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。
- `-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。

> [!Note]
> NuGet 4.3.0+ 支援 [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html)，它支援使用點標記法的發行前版本號碼，如 *1.0.1-build.23* 。 4.3.0 之前的 NuGet 版本不支援點標記法。 您可以使用像 *1.0.1-build23* 的格式。

解析套件參考且多個套件版本只有尾碼不同時，NuGet 會先選擇不含尾碼的版本，然後再依相反字母順序套用發行前版本。 例如，系統會依照所示的順序選擇下列版本：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>語意化版本控制系統 2.0.0

使用 NuGet 4.3.0+ 與 Visual Studio 2017 15.3+ 版，NuGet 支援[語意化版本控制系統 2.0.0](https://semver.org/spec/v2.0.0.html)。

較舊的用戶端不支援 SemVer v2.0.0 的某些語意。 如果下列其中一個敘述成立，則 NuGet 會將套件版本視為 SemVer v2.0.0 特定：

- 發行前版本標籤是以點分隔的，例如 *1.0.0-alpha.1*
- 版本有組建中繼資料，例如 *1.0.0+githash*

針對 nuget.org，如果下列其中一個敘述立，則會將套件定義為 SemVer v2.0.0 套件：

- 套件本身的版本符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 的規範，如上面所定義。
- 套件的任何相依性版本範圍都有最小或最大版本，它們符合 SemVer v2.0.0 的規範，但不符合 SemVer v1.0.0 規範，如上面所定義；例如， *[1.0.0-alpha.1, )* 。

如果您將 SemVer v2.0.0 特定套件上傳到 nuget.org，則舊版用戶端看不到該套件，只有下列 NuGet 用戶端可以取得該套件：

- NuGet 4.3.0+
- Visual Studio 2017 15.3+ 版
- Visual Studio 2015 (含 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix))
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

協力廠商用戶端：

- JetBrains Rider
- Paket 5.0+ 版

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>版本範圍

在參考套件相依性時，NuGet 支援使用間隔標記法來指定版本範圍，摘要說明如下：

| 表示法 | 套用的規則 | Description |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 最小版本 (包含) |
| (1.0,) | x > 1.0 | 最小版本 (不包含) |
| [1.0] | x == 1.0 | 完全相符的版本 |
| (,1.0] | x ≤ 1.0 | 最大版本 (包含) |
| (,1.0) | x < 1.0 | 最大版本 (不包含) |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 完全相符的範圍 (包含) |
| (1.0,2.0) | 1.0 < x < 2.0 | 完全相符的範圍 (不包含) |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合包含最小且不包含最大版本 |
| (1.0)    | 無效 | 無效 |

使用 PackageReference 格式時，NuGet 也支援使用浮動標記法， \* 以用於數位的主要、次要、修補和預先發行尾碼部分。 格式不支援浮動版本 `packages.config` 。 當指定浮動版本時，規則會解析為符合版本描述的最高版本。 浮動版本和解決方法的範例如下。

> [!Note]
> PackageReference 中的版本範圍包含發行前版本。 根據設計，浮動版本不會解析發行前版本，除非選擇加入。 如需相關功能要求的狀態，請參閱[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) \(英文\)。

### <a name="examples"></a>範例

請一律針對專案檔、`packages.config` 檔案與 `.nuspec` 檔案中的套件相依性指定版本或版本範圍。 如果沒有版本或版本範圍，NuGet 2.8. x 和更早的版本會在解析相依性時選擇最新可用套件版本，而 NuGet 3.x 和更新版本會選擇最低套件版本。 指定版本或版本範圍可避免這種不確定性。

#### <a name="references-in-project-files-packagereference"></a>專案檔中的參考 (PackageReference)

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a>浮動版本解析 

| 版本 | 存在於伺服器上的版本 | 解決方法 | 原因 | 備忘稿 |
|----------|--------------|-------------|-------------|-------------|
| * | 1.1.0 <br> 1.1.1 <br> 1.2.0 <br> 1.3.0-Alpha  | 1.2.0 | 最高穩定版本。 |
| 1.1.* | 1.1.0 <br> 1.1.1 <br> 1.1.2-Alpha <br> 1.2.0-Alpha | 1.1.1 | 遵循指定模式的最高穩定版本。|
| * - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-Alpha <br> 1.3.0-Beta  | 1.3.0-Beta | 最高版本，包括不穩定版本。 | 適用于 Visual Studio 16.6 版、NuGet 5.6 版、.NET Core SDK 版本3.1.300 |
| 1.1. *-* | 1.1.0 <br> 1.1.1 <br> 1.1.2-Alpha <br> 1.1.2-Beta <br> 1.3.0-Beta  | 1.1.2-Beta | 採用模式並包含不穩定版本的最高版本。 | 適用于 Visual Studio 16.6 版、NuGet 5.6 版、.NET Core SDK 版本3.1.300 |

**`packages.config` 中的參考：**

在 `packages.config` 中，每個相依性都會隨還原套件時使用的確切 `version` 屬性一併列出。 只有在更新作業期間，才會使用 `allowedVersions` 屬性來限制套件可能更新的版本。

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**`.nuspec` 檔案中的參考**

`<dependency>` 元素中的 `version` 屬性描述相依性可接受的範圍版本。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>標準化版本號碼

> [!Note]
> 這是 NuGet 3.4 和更新版本的中斷性變更。

在安裝、重新安裝或還原作業期間從存放庫取得套件時，NuGet 3.4+ 會依照下列方式來對待版本號碼：

- 系統會將前置零從版本號碼移除：

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 系統會移除在版本號碼第四部分中的零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- 已移除 SemVer 2.0.0 組建中繼資料

        1.0.7+r3456 is treated as 1.0.7

`pack` 與 `restore` 作業會盡可能將版本標準化。 針對已建置的套件，此標準化不會影響套件本身的版本號碼；它只會影響 NuGet 在解析相依性時如何比對版本。

不過，NuGet 套件存放庫必須以與 NuGet 相同的方式來處理這些值，以防止套件版本重複。 因此，包含 *1.0* 版套件的存放庫，不應該也裝載 *1.0.0* 版，並作為個別且不同的套件。
