---
title: NuGet 套件的多目標
description: 將目標設為單一 NuGet 套件內多個 .NET Framework 版本之各種方法的描述。
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: c59839240935e2a6c590dea3adf623313f79f02f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981141"
---
# <a name="supporting-multiple-net-framework-versions"></a>支援多個 .NET Framework 版本

*針對使用 NuGet 4.0+ 的 .NET Core 專案，請參閱 [NuGet 封裝和還原為 MSBuild 目標](../reference/msbuild-targets.md)，以取得跨目標的詳細資料。*

許多程式庫的目標都設為特定 .NET Framework 版本。 例如，您可能有一版的程式庫是 UWP 特有的，而另一個版本則利用 .NET Framework 4.6 中的功能。

為了完成此作業，使用[建立套件](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)中所述的慣例工作目錄方法時，NuGet 會支援將相同程式庫的多個版本放入單一套件中。

## <a name="framework-version-folder-structure"></a>架構版本資料夾結構

如果所建置的架構只包含一個版本的程式庫，或將目標設為多個架構，您一律會搭配使用不同的區分大小寫架構名稱與下列慣例，以在 `lib` 下建立子資料夾：

    lib\{framework name}[{version}]

如需所支援名稱的完整清單，請參閱[目標架構參考](../reference/target-frameworks.md#supported-frameworks)。

您的程式庫版本絕對不應該是架構特有的，而且會直接放在根 `lib` 資料夾中  (過去只有 `packages.config` 才支援此功能)。 如此會讓程式庫與任何目標架構相容，並且能夠安裝在任何位置，因而可能導致意外的執行階段錯誤。 使用 PackagesReference 格式時，已取代並忽略在根資料夾 (例如 `lib\abc.dll`) 或子資料夾 (例如 `lib\abc\abc.dll`) 中新增組件。

例如，下列資料夾結構支援架構特有的四種版本的組件：

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

若要在建置套件時輕鬆地包含所有這些檔案，請在 `.nuspec` 的 `<files>` 區段中使用遞迴 `**` 萬用字元：

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>架構特有資料夾

如果您有架構特有組件 (即目標設為 ARM、x86 和 x64 的不同組件)，則必須將它們放在 `runtimes` 資料夾的 `{platform}-{architecture}\lib\{framework}` 或 `{platform}-{architecture}\native` 子資料夾中。 例如，下列資料夾結構將放置原生以及目標設為 Windows 10 和 `uap10.0` 架構的 Managed DLL：

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

這些組件只有在執行階段中可用，因此若您也要提供對應的編譯階段組件，`AnyCPU` 必須位於 `/ref{tfm}` 資料夾中。 

請注意，NuGet 一律會從一個資料夾挑選這些編譯或執行階段資產，因此若有一些來自 `/ref` 的相容資產，則將忽略 `/lib` 以新增編譯階段組件。 同樣地，若有一些來自 `/runtime` 的相容資產，將也會針對執行階段忽略 `/lib`。

如需在 `.nuspec` 資訊清單中參考這些檔案的範例，請參閱[建立 UWP 套件](../guides/create-uwp-packages.md)。

此外，請參閱[使用 NuGet 封裝 Windows 市集應用程式](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>比對組件版本與專案中的目標架構

如果 NuGet 所安裝的套件具有多個組件版本，則會嘗試比對組件的架構名稱與專案的目標架構。

如果找不到相符項目，則 NuGet 會複製小於或等於專案目標架構 (如果可用) 的最高版本的組件。 如果找到不相容的組件，NuGet 會傳回適當的錯誤訊息。

例如，請考慮在套件中使用下列資料夾結構：

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

在目標設為 .NET Framework 4.6 的專案中安裝此套件時，NuGet 會在 `net45` 資料夾中安裝組件，因為這是小於或等於 4.6 的最高可用版本。

如果專案的目標設為 .NET Framework 4.6.1，則另一方面，NuGet 會安裝 `net461` 資料夾中的組件。

如果專案的目標設為 .NET Framework 4.0 和更早版本，NuGet 會擲回找不到相容組件的適當錯誤訊息。

## <a name="grouping-assemblies-by-framework-version"></a>依架構版本來群組組件

NuGet 只會複製套件中單一程式庫資料夾的組件。 例如，假設套件具有下列資料夾結構：

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

在目標設為 .NET Framework 4.5 的專案中安裝套件時，`MyAssembly.dll` (2.0 版) 是唯一安裝的組件。 未安裝 `MyAssembly.Core.dll` (v1.0)，因為它未列在 `net45` 資料夾中。 因為 `MyAssembly.Core.dll` 可能已合併至 2.0 版的 `MyAssembly.dll`，所以 NuGet 會以這種方式運作。

如果您想要為 .NET Framework 4.5 安裝 `MyAssembly.Core.dll`，請將複本放在 `net45` 資料夾中。

## <a name="grouping-assemblies-by-framework-profile"></a>依架構設定檔來群組組件

NuGet 也支援將目標設為特定架構設定檔，方法是將一個破折號和設定檔名稱附加到資料夾結尾。

    lib\{framework name}-{profile}

支援的設定檔如下所示：

- `client`：用戶端設定檔
- `full`：完整設定檔
- `wp`：Windows Phone
- `cf`：Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>判斷要使用的 NuGet 目標

封裝目標設為可攜式類別庫的程式庫時，可能很難判斷您應該在資料夾名稱和 `.nuspec` 檔案中使用的 NuGet 目標，特別是目標只設為 PCL 子集時。 下列外部資源將協助您進行下列作業：

- [.NET 中的架構設定檔](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [可攜式類別庫設定檔](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co)：列舉 PCL 設定檔和其對等 NuGet 目標的資料表
- [可攜式類別庫設定檔工具](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com)：用於判斷系統上可用之 PCL 設定檔的命令列工具

## <a name="content-files-and-powershell-scripts"></a>內容檔案和 PowerShell 指令碼

> [!Warning]
> 只有使用 `packages.config` 格式才能使用可變動的內容檔案和指令碼執行；可變動的內容檔案和指令碼執行已隨所有其他格式遭取代，而且不應該用於任何新套件。

使用 `packages.config`，可以在 `content` 和 `tools` 資料夾內使用相同的資料夾慣例，以依目標架構來群組內容檔案和 PowerShell 指令碼。 例如: 

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

如果架構資料夾空白，則 NuGet 不會新增組件參考或內容檔案，或執行該架構的 PowerShell 指令碼。

> [!Note]
> 因為 `init.ps1` 是在方案層級執行，並且與專案無關，所以必須直接將它放在 `tools` 資料夾下方。 如果放在架構資料夾下方，則會予以忽略。
