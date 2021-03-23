---
title: 如何使用 NuGet 封裝 UI 控制項
description: 如何建立包含 UWP 或 WPF 控制項的 NuGet 套件，包含 Visual Studio 和 Blend 設計工具的必要中繼資料和支援檔案。
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 7660203ec44db75b7764767b519c9ff10dd1122e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859079"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>建立 UI 控制項作為 NuGet 套件

自 Visual Studio 2017 開始，您可利用 NuGet 套件所傳遞的 UWP 和 WPF 控制項新增功能。 本指南會使用 [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage)，在 UWP 控制項內容中，逐步介紹這些功能。 除非另外提及，否則所述內容也適用於 WPF 控制項。

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2017
1. 了解如何[建立 UWP 套件](create-uwp-packages.md)

## <a name="generate-library-layout"></a>產生程式庫配置

> [!Note]
> 這僅適用於 UWP 控制項。

設定 `GenerateLibraryLayout` 屬性可確保專案建置輸出以可供封裝的配置來產生，而不需要 nuspec 中的個別檔案項目。

從專案屬性中，移至 [建置] 索引標籤並選取 [產生程式庫配置] 核取方塊。 這將會修改專案檔，並將目前所選取的組建組態和平台的 `GenerateLibraryLayout` 旗標設定成 true。

或者，編輯專案檔，以將 `<GenerateLibraryLayout>true</GenerateLibraryLayout>` 新增至第一個無條件屬性群組。 這樣將會套用屬性，而不論組建組態和平台為何。

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>新增 XAML 控制項的工具箱/資產窗格支援

若要讓 XAML 控制項出現在 Visual Studio 的 XAML 設計工具工具箱中以及 Blend 的 [資產] 索引標籤中，請在套件專案的 `tools` 資料夾根中建立 `VisualStudioToolsManifest.xml` 檔案。 如果您不需要控制項出現在工具箱或 [資產] 窗格中，則不需要此檔案。

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

該檔案的結構如下：

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

其中：

- *your_package_file*：您控制檔案的名稱，例如 `ManagedPackage.winmd` ("ManagedPackage" 是用於此範例的任意名稱，沒有任何其他意義)。
- *vs_category*：Visual Studio 設計工具工具箱中控制項應該出現在其中的群組標籤。 需要有 `VSCategory`，控制項才會出現在工具箱中。
*ui_framework*： framework 的名稱，例如 ' WPF '，請注意 `UIFramework` Visual Studio 16.7 Preview 3 或更新版本上的 ToolboxItems 節點上需要屬性，控制項才會出現在 [工具箱] 中。
- *blend_category*：Blend 設計工具 [資產] 窗格中控制項應該出現在其中的群組標籤。 需要有 `BlendCategory`，控制項才會出現在 [資產] 中。
- *type_full_name_n*：每個控制項的完整名稱，包含命名空間 (例如 `ManagedPackage.MyCustomControl`)。 請注意，點格式適用於 Managed 和原生類型。

在更進階的情況下，您也可以在單一套件包含多個控制項組件時，於 `<FileList>` 內包含多個 `<File>` 項目。 如果您想要將您的控制項組織成不同的類別，則也可以在單一 `<File>` 內有多個 `<ToolboxItems>` 節點。

在下列範例中，`ManagedPackage.winmd` 中所實作的控制項會出現在 Visual Studio 和 Blend 的 [Managed Package] \(Managed 套件) 群組中，而且 “MyCustomControl” 會出現在該群組中。 所有這些名稱都是任意的。

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![在 Visual Studio 中出現的範例控制項](media/UWP-control-vs-toolbox.png)

![在 Blend 中出現的範例控制項](media/UWP-control-blend-assets.png)

> [!Note]
> 您必須明確指定想要在工具箱/[資產] 窗格中看到的每個控制項。 請確保以 `Namespace.ControlName` 格式指定它們。

## <a name="add-custom-icons-to-your-controls"></a>將自訂圖示新增至控制項

若要在工具箱/資產窗格中顯示自訂圖示，請將影像新增至專案或名為 “Namespace.ControlName.extension” 的對應 `design.dll` 專案，並將建置動作新增至 [內嵌資源]。 您也必須確定關聯的 `AssemblyInfo.cs` 指定 ProvideMetadata 屬性 - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`。 請參閱此[範例](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)。

支援的格式為 `.png`、`.jpg`、`.jpeg`、`.gif` 和 `.bmp`。 建議的格式為 16 x 16 像素的 BMP24。

![工具箱圖示範例](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

執行階段會更換粉紅色背景。 變更 Visual Studio 佈景主題時，圖示將會更換顏色，且應會出現背景顏色。 如需詳細資訊，請參考 [Visual Studio 的映像與圖示](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)。

在下列範例中，專案會包含名為 “ManagedPackage.MyCustomControl.png” 的影像檔。

![在專案中設定自訂圖示](media/UWP-control-custom-icon.png)

> [!Note]
> 對於原生控制項，您必須將圖示當成資源放至 `design.dll` 專案中。

## <a name="support-specific-windows-platform-versions"></a>支援特定的 Windows 平台版本

UWP 套件的 TargetPlatformVersion (TPV) 和 TargetPlatformMinVersion (TPMinV) 會定義可安裝應用程式之 OS 版本的上限和下限。 TPV 進一步指定用來建置應用程式的 SDK 版本。 撰寫 UWP 套件時，請留意這些屬性：在應用程式中所定義平台版本界限外部使用 API，會導致組建失敗，或應用程式在執行階段失敗。

例如，假設您已將控制項套件的 TPMinV 設定為 Windows 10 Anniversary Edition (10.0；組建 14393)，因此想要確保只有符合該下限的 UWP 專案會取用該套件。 若要允許 UWP 專案使用您的套件，您必須使用下列資料夾名稱來封裝控制項：

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

NuGet 會自動檢查取用專案的 TPMinV。如果低於 Windows 10 Anniversary Edition (10.0；組建 14393)，將無法安裝

若為 WPF，假設想要讓 WPF 控制項套件供目標為 .NET Framework v4.6.1 或更高版本的專案取用。 若要強制這麼做，必須使用以下資料夾名稱來封裝控制項：

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a>新增設計階段支援

若要設定在屬性偵測器中顯示控制項屬性、新增自訂裝飾項等等，請適當地將 `design.dll` 檔案放在目標平台的 `lib\uap10.0.14393\Design` 資料夾內。 此外，為了確保 [[編輯範本] > [編輯複本]](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)功能正常運作，您必須在 `<your_assembly_name>\Themes` 資料夾中包含 `Generic.xaml` 及其合併的任何資源目錄 (同樣使用您實際的組件名稱)。  (此檔案不會影響控制項的執行時間行為。 ) 資料夾結構會如下所示：

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

對於 WPF，請從範例中想要讓 WPF 控制項套件供目標為 .NET Framework v4.6.1 或更高版本的專案取用之處，繼續進行範例：

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> 控制屬性預設會顯示在屬性偵測器的 [其他] 類別下方。

## <a name="use-strings-and-resources"></a>使用字串和資源

您可以在套件中內嵌控制項或取用 UWP 專案可使用的字串資源 (`.resw`)，並將 `.resw` 檔案的 [建置動作] 屬性設定為 [PRIResource]。

如需範例，請參閱 ExtensionSDKasNuGetPackage 範例中的 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)。

> [!Note]
> 這僅適用於 UWP 控制項。

## <a name="see-also"></a>另請參閱

- [建立 UWP 套件](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 範例](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage)