---
title: NuGet 套件版本參考
description: 需指定版本號碼和範圍而定的 NuGet 套件，並安裝相依性的方式在其他套件的確切詳細資料。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549769"
---
# <a name="package-versioning"></a>套件版本控制

特定封裝一律被指使用其封裝識別碼和確切的版本號碼。 例如， [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 上有數個數十個特定套件可供使用，範圍從版本*4.1.10311*版本*6.1.3* （最新的穩定發行） 和各種不同的發行前版本*6.2.0-beta1*。

在建立封裝時，您可以指派包含發行前版本的選擇性文字尾碼的特定版本號碼。 當使用套件，相反地，您可以指定確切的版本號碼或可接受的版本範圍。

本主題內容：

- [版本的基本概念](#version-basics)包括發行前版本尾碼。
- [版本範圍和萬用字元](#version-ranges-and-wildcards)
- [正規化的版本號碼](#normalized-version-numbers)

## <a name="version-basics"></a>版本的基本概念

特定版本號碼的格式*Major.Minor.Patch [-後置詞]*，其中的元件具有下列意義：

- *主要*： 重大變更
- *次要*： 新功能，但具有回溯相容性
- *修補程式*： 只有具備回溯相容性 bug 修正
- *-後置詞*（選擇性）： 連字號後面接著用來表示發行前版本字串 (下列[語意版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。

**範例：**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 會拒絕任何缺少的確切版本號碼的封裝上傳。 必須指定版本`.nuspec`或用來建立封裝的專案檔。

### <a name="pre-release-versions"></a>發行前版本

就技術上而言，套件建立者可以使用任何字串做為尾碼來代表發行前版本，NuGet 任何這類版本視為發行前版本，並讓其他的解譯方式。 也就是說，NuGet 會顯示完整的版本字串中任何的 UI 與此有關，給取用者離開後置詞的意義的任何解譯。

話雖如此，封裝開發人員一般會遵循可辨識的命名慣例：

- `-alpha`: Alpha 版本，通常用來工作的進度和測試。
- `-beta`：搶鮮版 (Beta) 版本，通常是計劃發行的功能完整版本，但可能包含已知的 Bug。
- `-rc`：候選版，除非出現重大的 Bug，不然通常是準最終版本 (穩定版)。

> [!Note]
> NuGet 4.3.0 + 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，其支援發行前版本編號使用點標記法，如同*1.0.1-build.23*。 4.3.0 之前的 NuGet 版本不支援點標記法。 您可以使用的格式*1.0.1-build23*。

當解析套件參考和多個封裝版本只有不同後置詞，NuGet 首先，選擇沒有尾碼的版本，則適用於發行前版本以反向字母順序的優先順序。 例如，下列版本會選擇正確的順序顯示：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

NuGet 4.3.0 + 和 Visual Studio 2017 版本 15.3 +，NuGet 支援[Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html)。

在舊版的用戶端不支援的 SemVer v2.0.0 特定語意。 NuGet 會考慮將封裝版本為特定的 SemVer v2.0.0，如果下列陳述式：

- 發行前版本標籤是句點分隔，例如*1.0.0-alpha.1*
- 版本具有組建中繼資料，例如*1.0.0+githash*

對於 nuget.org，封裝被定義為 SemVer v2.0.0 封裝，如果下列陳述式為 true:

- 封裝自己的版本為 SemVer v2.0.0 相容，但不是 SemVer 1.0.0 版相容，如上面所定義。
- 中的任何套件的相依性版本範圍有的最小值或最大版本 SemVer v2.0.0 相容，但不是 SemVer 1.0.0 版相容的上述; 定義例如， *[1.0.0-alpha.1,)*。

如果您上傳至 nuget.org 的 SemVer v2.0.0 特定套件，套件會是看不到舊的用戶端，並可供 只有下列的 NuGet 用戶端：

- NuGet 4.3.0 +
- Visual Studio 2017 版本 15.3 +
- Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

第三方用戶端：

- JetBrains Rider
- Paket 版本 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本範圍和萬用字元

當參考的套件相依性，NuGet 會支援使用間隔標記法來指定版本範圍，彙總，如下所示：

| Notation | 套用的規則 | 描述 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 最小版本含 |
| (1.0,) | x > 1.0 | 最小版本獨佔 |
| [1.0] | x == 1.0 | 確切的版本相符 |
| (,1.0] | x ≤ 1.0 | 最高版本內含 |
| (,1.0) | x < 1.0 | 最高版本獨佔 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 確切的範圍內含 |
| (1.0,2.0) | 1.0 < x < 2.0 | 確切的範圍內獨佔 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合式內含最小值和專屬的最高版本 |
| (1.0)    | 無效 | 無效 |

使用 PackageReference 格式時，NuGet 也支援使用萬用字元標記法， \*、 為主要、 次要、 修補程式和數字的發行前版本後置詞部分。 不支援萬用字元`packages.config`格式。

> [!Note]
> 解析版本範圍時，不包含發行前版本。 發行前版本*都*包含時使用萬用字元 (\*)。 版本範圍 *[1.0,2.0]*，比方說，不包含 2.0 beta 版，但萬用字元標記法_2.0-*_ 沒有。 請參閱[發出 912](https://github.com/NuGet/Home/issues/912)進一步討論需發行前版本的萬用字元。

### <a name="examples"></a>範例

一定要在專案檔中指定的版本或版本範圍，如封裝相依性`packages.config`檔案，和`.nuspec`檔案。 不含版本或版本範圍，NuGet 2.8.x 和稍早選擇最新可用的套件版本時解析相依性，而 NuGet 3.x 和更新版本會選擇最低套件版本。 指定的版本或版本範圍可避免這種不確定性。

#### <a name="references-in-project-files-packagereference"></a>專案檔 (PackageReference) 中的參考

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

**在參考`packages.config`:**

在  `packages.config`，有列出每個相依性，且確切`version`還原套件時使用的屬性。 `allowedVersions`屬性僅更新作業期間用來限制可能會更新封裝版本。

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

**在參考`.nuspec`檔案**

`version`屬性中`<dependency>`項目描述範圍的版本可接受相依性。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a>正規化的版本號碼

> [!Note]
> 這是一項重大變更適用於 NuGet 3.4 及更新版本。

取得從存放庫的封裝，在安裝期間，重新安裝或還原作業，NuGet 3.4 + 會將版本號碼，如下所示：

- 前置的零會自版本號碼：

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 版本號碼的第四個部分中的零，則會予以忽略

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

這個正規化並不會影響套件本身; 中的版本號碼它會影響只如何 NuGet 會比對版本時解析相依性。

不過，NuGet 套件存放庫必須在與 NuGet 以避免套件版本重複相同的方式處理這些值。 因此包含版本的儲存機制*1.0*的封裝不應也裝載版本*1.0.0*為個別且不同的套件。
