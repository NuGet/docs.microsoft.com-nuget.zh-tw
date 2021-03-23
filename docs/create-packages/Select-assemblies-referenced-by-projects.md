---
title: 選取專案所參考的組件
description: 讓套件中的部分組件可供編譯器使用，而所有組件在執行階段皆可用。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859027"
---
# <a name="select-assemblies-referenced-by-projects"></a>選取專案所參考的組件

明確的組件參考可讓部分組件用於 IntelliSense 及編譯，而所有組件在執行階段皆可用。 `PackageReference` 和 `packages.config` 的運作方式不同，因此套件作者必須費心建立套件，以便與這兩種專案類型相容。

> [!Note]
> 明確的組件參考與 .NET 組件有關。 它不是受控組件 P/叫用原生組件的散發方法。

## <a name="packagereference-support"></a>`PackageReference` 支援

當專案使用 `PackageReference` 來搭配套件且套件包含 `ref\<tfm>\` 目錄時，NuGet 會將那些組合分類為編譯時期資產，而 `lib\<tfm>\` 組件會分類為執行階段資產。 `ref\<tfm>\` 中的組件不會在執行階段使用。 這表示 `ref\<tfm>\` 中的任何組件必須要在 `lib\<tfm>\` 或相關 `runtime\` 目錄中有符合的組件，否則可能會發生執行階段錯誤。 由於 `ref\<tfm>\` 中的組件不會在執行階段使用，因此它們可以是[僅限中繼資料的組件](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)，以便縮減套件大小。

> [!Important]
> 如果套件包含 nuspec `<references>` 元素 (由 `packages.config` 使用，如下所示)，且在 `ref\<tfm>\` 中不包含組件，則 NuGet 會將 nuspec `<references>` 元素中列出的組件通告為編譯和執行階段資產。 這表示當參考的組件需要載入 `lib\<tfm>\` 目錄中任何其他組件時，會有執行階段例外狀況。

> [!Note]
> 如果套件包含 `runtime\` 目錄，則 NuGet 不能使用 `lib\` 目錄中的資產。

## <a name="packagesconfig-support"></a>`packages.config` 支援

使用 `packages.config` 管理 NuGet 套件的專案，通常會新增對 `lib\<tfm>\` 目錄中所有組件的參考。 已新增 `ref\` 目錄來支援 `PackageReference`，因此在使用 `packages.config` 時不會考慮它。 若要明確設定使用的專案參考的元件 `packages.config` ，封裝必須使用 nuspec 檔[ `<references>` 中的元素](../reference/nuspec.md#explicit-assembly-references)。 例如：

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` 專案使用稱為 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) 的處理序來將組件複製到 `bin\<configuration>\` 輸出目錄。 會複製您專案的組件，然後建置系統會查看所參考組件的組件資訊清單，然後複製這些組件並以遞迴方式針對所有組件重複執行。 這表示，如果 `lib\<tfm>\` 目錄中的任何組件未列在任何其他組件資訊清單中作為相依性 (如果在執行階段使用 `Assembly.Load`、MEF 或另一個相依性插入架構來載入組件)，則它可能不會複製到您專案的 `bin\<configuration>\` 輸出目錄，即使它在 `bin\<tfm>\` 中。

## <a name="example"></a>範例

我的套件會包含三個組件：`MyLib.dll`、`MyHelpers.dll` 和 `MyUtilities.dll`，它們以 .NET Framework 4.7.2 為目標。 `MyUtilities.dll` 包含的類別只為了供其他兩個組件使用，因此我不想要在 IntelliSense 中提供這些類別，或在編譯時期提供給使用我套件的專案。 我的 `nuspec` 檔案必須包含下列 XML 元素：

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

且套件中的檔案將為：

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
