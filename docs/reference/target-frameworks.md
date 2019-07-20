---
title: NuGet 的目標 Framework 參考
description: NuGet 目標 Framework 參考會識別並隔離套件的 Framework 相依元件。
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ea9f699b202d7f32648f0ccfeac3ceb1ca325b7e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342436"
---
# <a name="target-frameworks"></a>目標 Framework

NuGet 在各種位置使用目標 Framework 參考，具體識別並隔離套件的 Framework 相依元件：

- [專案](../create-packages/multiple-target-frameworks-project-file.md)檔:針對 SDK 樣式的專案, *.csproj*包含目標 framework 參考。
- [nuspec 資訊清單](../reference/nuspec.md):封裝可以根據專案的目標架構, 指出要包含在專案中的不同套件。
- [. nupkg 資料夾名稱](../create-packages/creating-a-package.md#from-a-convention-based-working-directory):封裝`lib`資料夾內的資料夾可以根據目標 framework 命名, 其中每一個都包含 dll 和適用于該架構的其他內容。
- [封裝 .config](../reference/packages-config.md):相依`targetframework`性的屬性會指定要安裝之封裝的變體。

> [!Note]
> 計算下列表格的 NuGet 用戶端原始程式碼位在下列位置：
> - 支援的架構名稱:[FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - 架構優先順序和對應:[DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>支援的架構

Framework 通常是簡短的目標 Framework Moniker 或 TFM 的參考對象。 在 .NET Standard 中, 這也會一般化為*TxM* , 以允許單一參考多個架構。

NuGet 用戶端支援下表中的 Framework 。 對等項目會顯示在 [] 括弧內。 請注意，某些工具，例如 `dotnet`，可能會在某些檔案中使用標準的 TFM 變化。 例如，`dotnet pack` 在 `.nuspec` 檔案中使用 `.NETCoreApp2.0`，而非 `netcoreapp2.0`。 各種 NuGet 用戶端工具會正確處理這些變化，但直接編輯檔案時，您應該一律使用標準的 TFM。

| 名稱 | 縮寫 | TFM/TxM |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Windows Store) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|視窗 | win | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (Windows 10 平台不支援) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
通用 Windows 平台 | uap | uap [uap10.0] |
| | | uap10.0 |
| | | uap 10.0 (其中 10.0. xxxxx 是取用應用程式的目標平臺最小版本) |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET Core 應用程式 | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
| | | netcoreapp2.2 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>已被取代的架構

下列架構已被取代。 以這些架構為目標的套件應該移轉至所指出的取代項目。

| 已被取代的架構 | Replacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>優先順序

有一些 Framework 彼此相關且相容，但未必相等：

| 架構 | 可使用 |
| -- | --- |
| uap (通用 Windows 平台) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | |

## <a name="net-standard"></a>NET Standard

[.NET Standard](/dotnet/standard/net-standard)可簡化二進位相容架構之間的參考, 讓單一目標架構能夠參考其他專案的組合。 (背景請參閱 [.NET 入門](/dotnet/articles/standard/index)。)

[NuGet 取得最接近的 Framework 工具](https://aka.ms/s2m3th)會模擬 NuGet 使用的方法，從以專案 Framework 為基礎之套件中的許多可用 Framework 資產中選取一個 Framework。

NuGet 3.3 和更舊版本中應該使用 moniker 的 `dotnet` 系列，v3.4 及更新版本應使用 `netstandard` Moniker 語法。

## <a name="portable-class-libraries"></a>可攜式類別庫

> [!Warning]
> **不建議使用 PCL**。 儘管支援 PCL，但套件作者應改支援 netstandard。 .NET 平臺標準是 Pcl 的演進, 並使用未系結至靜態程式庫 (例如*便攜-a + b + c)* 的單一名字標記, 來代表跨平臺的二進位可攜性。

若要定義參考多個子目標 Framework 的目標 Framework，會使用 `portable` 關鍵字 作為參考之 Framework 清單的首碼。 避免以人為方式包含不會直接編譯的額外 Framework ，因為它會導致這些 Framework 出現非預期的副作用。

協力廠商定義的其他 Framework ，提供可以這種方式存取之其他環境的相容性。 此外，還有縮寫的設定檔編號，可用來參考這些相關 Framework 的組合，如 `Profile#`，但不建議以這種方法使用這些編號，因為這會降低資料夾和 `.nuspec` 的可讀性。

| 設定檔 # | 架構 | 完整名稱 | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

此外，以 Xamarin 為目標的 NuGet 套件可以使用其他 Xamarin 定義的 Framework。 請參閱 [Manually Creating NuGet Packages for Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/) (手動建立適用於 Xamarin 的 NuGet 套件)。

| 名稱 | 描述 | .NET Standard |
| --- | --- | ---
| monoandroid | Android 作業系統的 Mono 支援 | netstandard1.4 |
| monotouch | iOS 的 Mono 支援 | netstandard1.4 |
| monomac | OSX 的 Mono 支援 | netstandard1.4 |
| xamarinios | 支援 Xamarin for iOS | netstandard1.4 |
| xamarinmac | 支援 Xamarin for Mac | netstandard1.4 |
| xamarinpsthree | 支援 Playstation 3 上的 Xamarin | netstandard1.4 |
| xamarinpsfour | 支援 Playstation 4 上的 Xamarin | netstandard1.4 |
| xamarinpsvita | 支援 PS Vita 上的 Xamarin | netstandard1.4 |
| xamarinwatchos | Xamarin for Watch OS | netstandard1.4 |
| xamarintvos | Xamarin for TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin for XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin for XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary 建立的工具可以列出支援的 PCL，您可以在他的文章中找到這項工具：[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (.NET 中的 Framework 設定檔)。
