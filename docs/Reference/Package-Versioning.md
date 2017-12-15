---
title: "NuGet 封裝版本參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "確切的指定版本號碼和範圍而定的 NuGet 封裝，並安裝相依性的方式在其他封裝的詳細資訊。"
keywords: "版本控制、 NuGet 封裝相依性、 NuGet 相依性版本、 NuGet 版本號碼、 NuGet 封裝版本、 版本範圍、 版本規格，正規化的版本號碼"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a>封裝版本控制

特定封裝永遠被指使用其封裝識別碼和確切的版本號碼。 例如， [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 上有數個數十種特定封裝可用，範圍從版本*4.1.10311*版本*6.1.3* （最新穩定發行） 和各種不同的發行前版本*6.2.0-beta1*。

在建立封裝時，您會指定特定版本號碼的選擇性發行前的文字尾碼。 當使用封裝，相反地，您可以指定確切的版本號碼或一個範圍的可接受的版本。

本主題內容：

- [版本的基本概念](#version-basics)包括發行前版本尾碼。
- [版本範圍與萬用字元](#version-ranges-and-wildcards)
- [正規化的版本號碼](#normalized-version-numbers)

## <a name="version-basics"></a>版本的基本概念

特定版本號碼的格式為*Major.Minor.Patch [-後置詞]*、 其中的元件具有以下意義：

- *主要*： 重大變更
- *次要*： 新的功能，但回溯相容性
- *修補程式*： 只有具備回溯相容性 bug 修正
- *-尾碼*（選擇性）： 連字號後面接著此項表示應發行前版本字串 (下列[語意化版本控制或 SemVer 1.0 慣例](http://semver.org/spec/v1.0.0.html))。

**範例：**
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> nuget.org 會拒絕任何缺少的確切的版本號碼的封裝上傳。 必須在指定的版本`.nuspec`或用來建立封裝的專案檔。

### <a name="pre-release-versions"></a>發行前版本

就技術上來說，封裝建立者可以使用任何字串做為尾碼來代表發行前版本，如 NuGet 視為發行前版本的任何這類的版本，並讓其他的解譯方式。 也就是說，NuGet 會顯示任何 UI 中的完整版本字串涉及時，取用者留下任何解譯的後置詞的意義。

話雖如此，封裝開發人員通常會依照可辨識的命名慣例：

- `-alpha`: Alpha 版本中，通常用於工作的進度和試驗。
- `-beta`: Beta 版本，通常是已規劃的版本中，接下來的完整功能，但是可能會包含已知的錯誤的其中一個。
- `-rc`： 發行候選版本，通常是最後一個潛在的版次 (stable) 除非重大的 bug 會出現。

> [!Note]
> NuGet 4.3.0+ 支援[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，可支援使用點標記法，發行前版本號碼中*1.0.1-build.23*。 與之前 4.3.0 的 NuGet 版本不支援點標記法。 您可以使用的表單*1.0.1-build23*。

解決時封裝會參照和多個封裝版本只有不同後置詞，NuGet 首先，選擇的版本不含尾碼，然後套用至發行前版本，以反向字母順序的優先順序。 例如，下列版本本來的順序顯示：

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a>2.0.0 的語意版本設定

使用 NuGet 4.3.0+ 和 Visual Studio 2017 15.3 + 版本，支援 NuGet[語意版本設定 2.0.0](http://semver.org/spec/v2.0.0.html)。

在舊版的用戶端不支援的 SemVer v2.0.0 特定語意。 NuGet 會考慮下列陳述式是否是 SemVer v2.0.0 特定的封裝版本：

- 發行前版本標籤是點分隔，例如*1.0.0-alpha.1*
- 版本有建置中繼資料，例如*1.0.0+githash*

對於 nuget.org，封裝定義為 SemVer v2.0.0 封裝如果為 true，下列陳述式：

- 封裝自己版本是 SemVer v2.0.0 相容，但相容、 不 SemVer v1.0.0 上方所定義。
- 所有封裝的相依性版本範圍有不相容 SemVer v2.0.0 但相容、 不 SemVer v1.0.0; 上述定義的最小值或最大版本例如， *[1.0.0-alpha.1,)*。

如果您要 nuget.org 傳 SemVer v2.0.0 特定封裝，封裝是看不到舊版的用戶端，並可供 只有下列 NuGet 用戶端：

- NuGet 4.3.0+
- Visual Studio 2017 15.3 + 版本 
- dotnet.exe (.NET SDK 2.0.0+)

第三方用戶端：

- JetBrains 騎兵
- Paket 5.0 + 版本

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本範圍與萬用字元

當參照的套件相依性，NuGet 會支援使用間隔標記法來指定版本範圍，彙總，如下所示：

| Notation | 套用的規則 | 說明 |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | 最小版本 （含） |
| (1.0,) | 1.0 < x | 最小版本，而獨佔式 |
| [1.0] | x = = 1.0 | 確切的版本相符項目 |
| (,1.0] | x ≤ 1.0 | 最大版本，（含） |
| (,1.0) | x < 1.0 | 最大版本，而獨佔式 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 確切的範圍內含 |
| (1.0,2.0) | 1.0 < x < 2.0 | 確切的範圍，獨占 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合含最小值和獨佔式最大版本 |
| (1.0)    | 無效 | 無效 |

當使用 PackageReference 或`project.json`封裝也支援使用萬用字元標記法參考格式，NuGet \*、 主要、 次要、 修補程式，和數字的發行前版本後置字元部分。 不支援萬用字元`packages.config`格式。

> [!Note]
> 解決版本範圍時，不會包含發行前版本。 發行前版本*是*包含時使用萬用字元 (\*)。 版本範圍*[1.0,2.0]*，比方說，不包括 2.0 beta 版，但萬用字元標記法_2.0-*_沒有。 請參閱[發出 912](https://github.com/NuGet/Home/issues/912)的進一步討論發行前版本萬用字元。

### <a name="examples"></a>範例

一律在專案檔中指定版本或封裝的相依性的版本範圍`packages.config`檔案，並`.nuspec`檔案。 不含版本或版本範圍，NuGet 2.8.x 稍早選擇最新可用的封裝版本時解析相依性，而 NuGet 3.x 及更新版本選擇最低的封裝版本。 指定的版本或版本範圍可避免此有助於減少不確定性。

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**在參考`packages.config`:**

在`packages.config`，每個相依性列為完全`version`還原封裝時所使用的屬性。 `allowedVersions`屬性只有在更新作業期間用來限制可能會更新封裝的版本。

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

`version`屬性`<dependency>`元素描述可接受的相依性範圍版本。

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
> 這是一項重大變更及更新版本的 NuGet 3.4。

取得從儲存機制的封裝，在安裝期間，重新安裝，或還原作業，NuGet 3.4 + 會將版本號碼，如下所示：

- 前置的零會從版本號碼：

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- 版本號碼的第四個部分中的零，則會予以忽略

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

這個正規化不會影響封裝本身; 中的版本號碼它會影響只如何 NuGet 符合版本解析相依性時。

不過，NuGet 封裝儲存機制必須與 NuGet 來避免封裝版本重複相同的方式處理這些值。 因此，包含版本的儲存機制*1.0*的封裝不應也裝載版本*1.0.0*個別且不同的套件。
