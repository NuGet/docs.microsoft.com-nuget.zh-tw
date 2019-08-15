---
title: NuGet 套件版本參考
description: 有關為 NuGet 套件相依的其他套件指定版本號碼和範圍的確切詳細資料, 以及安裝相依性的方式。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020002"
---
# <a name="package-versioning"></a>套件版本控制

特定套件一律會使用其套件識別碼和確切的版本號碼來參考。 例如, nuget.org 上的[Entity Framework](https://www.nuget.org/packages/EntityFramework/)有數個特定的套件可用, 範圍從版本*4.1.10311*到版本*之 ef6.1.3* (最新的穩定版本) 和各種發行前版本 (例如*6.2.0-Beta1)* .

建立封裝時, 您可以使用選擇性的發行前文字尾碼來指派特定版本號碼。 另一方面, 使用封裝時, 您可以指定確切的版本號碼或可接受的版本範圍。

本主題內容：

- [版本基本概念](#version-basics), 包括發行前版本的尾碼。
- [版本範圍和萬用字元](#version-ranges-and-wildcards)
- [正規化版本號碼](#normalized-version-numbers)

## <a name="version-basics"></a>版本基本概念

特定版本號碼的格式為 *[主要. 次要修補程式 [-尾碼]]* , 其中元件具有下列意義:

- *主要*:重大變更
- *次要*:新功能，但具回溯相容性
- *修補程式*:僅具有回溯相容的錯誤 (Bug) 修正
- *-尾碼*(選擇性): 連字號後面接著字串, 表示發行前版本 (遵循[語義版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。

**典型**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 會拒絕任何缺少確切版本號碼的套件上傳。 您必須在用來建立封裝`.nuspec`的或專案檔中指定版本。

### <a name="pre-release-versions"></a>發行前版本

就技術上而言, 套件建立者可以使用任何字串做為後置詞來表示發行前版本, 因為 NuGet 會將任何此類版本視為預先發行版本, 而且不會進行任何其他轉譯。 也就是說, NuGet 會在牽涉到的任何 UI 中顯示完整的版本字串, 並將後置詞意義的任何解釋, 保留給取用者。

話雖如此, 封裝開發人員通常會遵循公認的命名慣例:

- `-alpha`：Alpha 版本, 通常用於進行中的工作和實驗。
- `-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的錯誤 (Bug)。
- `-rc`：候選版，除非出現重大的錯誤 (Bug)，不然通常是準最終版本 (穩定版)。

> [!Note]
> NuGet 4.3.0 + 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), 其支援具有點標記法的發行前版本號碼, 如同*1.0.1-build. 23*。 4\.3.0 之前的 NuGet 版本不支援點標記法。 您可以使用像是*1.0.1-build23*的表單。

解析套件參考和多個套件版本只有尾碼不同時, NuGet 會先選擇不含尾碼的版本, 然後再以相反的字母順序套用至發行前版本。 例如, 下列版本會依照所示的正確順序來選擇:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>語義版本控制2.0。0

使用 NuGet 4.3.0 + 和 Visual Studio 2017 版本 15.3 +, NuGet 支援[語義版本設定 2.0.0](http://semver.org/spec/v2.0.0.html)。

較舊的用戶端不支援 SemVer v 2.0.0 的某些語義。 如果下列其中一個陳述成立, NuGet 會將套件版本視為 SemVer v 2.0.0 特定:

- 發行前版本標籤是以點分隔的, 例如*1.0.0-Alpha。 1*
- 版本具有組建中繼資料, 例如*1.0.0 + githash*

針對 nuget.org, 如果下列其中一個陳述為 true, 則會將套件定義為 SemVer v 2.0.0 套件:

- 套件本身的版本為 SemVer v 2.0.0 相容, 但不符合 SemVer 1.0.0 版, 如上面所定義。
- 套件的任何相依性版本範圍都有最小或最大版本, 其為 SemVer v 2.0.0 相容, 但不符合 SemVer 1.0.0 標準, 定義于上方;例如, *[1.0.0-Alpha. 1,)* ]。

如果您將 SemVer v 2.0.0 特定封裝上傳到 nuget.org, 舊版用戶端就看不到套件, 而且只有下列 NuGet 用戶端可以使用:

- NuGet 4.3.0 +
- Visual Studio 2017 版本 15.3 +
- Visual Studio 2015 搭配[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore .exe (.NET SDK 2.0.0 +)

協力廠商用戶端:

- JetBrains 附件
- Paket 5.0 版 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本範圍和萬用字元

在參考套件相依性時, NuGet 支援使用間隔標記法來指定版本範圍, 摘要如下:

| Notation | 套用的規則 | 描述 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 最小版本 (含) |
| (1.0,) | x > 1.0 | 最低版本, 獨佔 |
| [1.0] | x == 1.0 | 完全相符的版本 |
| (,1.0] | x ≤ 1.0 | 最大版本 (含) |
| (,1.0) | x < 1.0 | 最大版本, 獨佔 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 確切範圍 (含) |
| (1.0,2.0) | 1.0 < x < 2.0 | 精確範圍, 獨佔 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合內含的最小和最大排除版本 |
| (1.0)    | 無效 | 無效 |

使用 PackageReference 格式時, NuGet 也支援使用萬用字元標記法, \*用於數位的主要、次要、修補和預先發行尾碼部分。 `packages.config`格式不支援萬用字元。

> [!Note]
> PackageReference 中的版本範圍包含發行前版本。 根據設計, 浮動版本不會解析發行前版本, 除非加入宣告。 如需相關功能要求的狀態, 請參閱[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)。

### <a name="examples"></a>範例

請一律針對專案檔、 `packages.config`檔案和`.nuspec`檔案中的封裝相依性指定版本或版本範圍。 如果沒有版本或版本範圍, NuGet 2.8. x 和更早的版本會在解析相依性時選擇最新可用的套件版本, 而 NuGet 3.x 和更新版本會選擇最低的套件版本。 指定版本或版本範圍可避免這種不確定性。

#### <a name="references-in-project-files-packagereference"></a>專案檔中的參考 (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**中的`packages.config`參考:**

在`packages.config`中, 每個相依性都會與`version`還原套件時使用的確切屬性一併列出。 只有在更新作業期間, 才會使用屬性來限制封裝可能更新的版本。`allowedVersions`

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

**檔案中`.nuspec`的參考**

元素中的`version`屬性會描述相依性可接受的範圍版本。 `<dependency>`

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

## <a name="normalized-version-numbers"></a>正規化版本號碼

> [!Note]
> 這是 NuGet 3.4 和更新版本的重大變更。

在安裝、重新安裝或還原作業期間從存放庫取得套件時, NuGet 3.4 + 會依照下列方式來對待版本號碼:

- 開頭的零會從版本號碼中移除:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 在版本號碼的第四個部分中, 會省略零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`和`restore`作業會盡可能將版本正規化。 針對已建立的封裝, 此正規化不會影響封裝本身的版本號碼;它只會影響 NuGet 在解析相依性時如何符合版本。

不過, NuGet 套件存放庫必須以與 NuGet 相同的方式來處理這些值, 以防止封裝版本重複。 因此, 包含*1.0*版套件的存放庫, 也不應該將*1.0.0*版裝載為不同的套件。
