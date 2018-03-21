---
title: "UWP 專案的 NuGet project.json 檔案 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "描述如何使用 project.json 檔案來追蹤通用 Windows 平台 (UWP) 專案中的 NuGet 相依性。"
keywords: "NuGet 相依性, NuGet 和 UWP, UWP 和 project.json, NuGet project.json 檔案"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3ef3703b2be92f84d37866bce9934ebcfed3a9f7
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="projectjson-and-uwp"></a>project.json 和 UWP

> [!Important]
> 此內容已過時。 專案應使用 `packages.config` 或 PackageReference 格式。

本文件描述採用 NuGet 3+ 中功能的套件結構 (Visual Studio 2015 和更新版本)。 `.nuspec` 的 `minClientVersion` 屬性可以用來說明您需要這裡所述的功能，方法是將它設定為 3.1。

## <a name="adding-uwp-support-to-an-existing-package"></a>將 UWP 支援新增至現有套件

如果您有現有套件，而且想要新增 UWP 應用程式的支援，則不需要採用這裡所述的套件格式。 只有在您需要它所描述的功能，而且願意只與已更新為 NuGet 用戶端 3+ 版的用戶端合作時，才需要採用這種格式。

## <a name="i-already-target-netcore45"></a>我已經將目標設為 netcore45

如果您已經將目標設為 `netcore45`，而且不需要利用這裡的功能，則不需要採取任何動作。 UWP 應用程式可以使用 `netcore45` 套件。

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>我想要利用 Windows 10 特定 API

在此情況下，您需要將 `uap10.0` 目標架構 Moniker (TFM 或 TxM) 新增至套件。 在套件中建立新的資料夾，並將已編譯以使用 Windows 10 的組件新增至該資料夾。

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>我不需要 Windows 10 特定 API，但想要新的 .NET 功能或還沒有 netcore45

在此情況下，您需要將 `dotnet` TxM 新增至套件。 與其他 TxM 不同，`dotnet` 不表示為介面區或平台。 它會指出您的套件適用於相依性所作用的任何平台。 使用 `dotnet` TxM 建置套件時，在 `.nuspec` 中，您可能會有許多其他 TxM 特定相依性，因為您需要定義相依的 BCL 套件，例如 `System.Text`、`System.Xml` 等等。這些相依性作用的位置定義您套件的運作位置。

### <a name="how-do-i-find-out-my-dependencies"></a>如何找出我的相依性

有兩種方式可找出要列出的相依性：

1. 使用 [NuSpec 相依性產生器](https://github.com/onovotny/ReferenceGenerator)**協力廠商**工具。 此工具會將這個程序自動化，並在建置時使用相依套件更新 `.nuspec` 檔案。 它可透過 NuGet 套件 [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) 取得。

1. (較難方式) 使用 `ILDasm` 查看 `.dll`，以查看執行階段實際需要的組件。 然後判斷其各個所來自的 NuGet 套件。

如需協助建立支援 `dotnet` TxM 之套件的功能詳細資料，請參閱 [`project.json`](project-json.md) 主題。

> [!Important]
> 如果您的套件是要使用 PCL 專案，則強烈建議建立 `dotnet` 資料夾，以避免警告和潛在的相容性問題。

## <a name="directory-structure"></a>目錄結構

使用此格式的 NuGet 套件具有下列已知資料夾和行為：

| 資料夾 | 「行為」 |
| --- | --- |
| 組建 | 在此資料夾中包含 MSBuild 目標和屬性檔，會以不同的方式整合至專案，但沒有任何變更。 |
| 工具 | 未執行 `install.ps1` 和 `uninstall.ps1`。 `init.ps1` 會如常運作。 |
| 內容 | 內容不會自動複製至使用者的專案中。 更新的版本已規劃專案中的內容包含支援。 |
| Lib | 針對許多套件，`lib` 的運作方式都與在 NuGet 2.x 中相同，但具有擴充選項，可在其內使用名稱，以及在使用套件時選擇正確子資料夾的較佳邏輯。 不過，與 `ref` 搭配使用時，`lib` 資料夾所包含的組件會實作 `ref` 資料夾中組件所定義的介面區。 |
| 參考 | `ref` 為選用資料夾，其中包含定義公用介面 (公用類型和方法) 的 .NET 組件，讓應用程式對其進行編譯。 此資料夾中的組件可能沒有實作，它們只用來定義編譯器的介面區。 如果套件沒有 `ref` 資料夾，則 `lib` 既是參考組件也是實作組件。 |
| 執行階段 | `runtimes` 是選擇性資料夾，其中包含 OS 特定程式碼，例如 CPU 架構與 OS 特定或平台相依二進位檔。 |

## <a name="msbuild-targets-and-props-files-in-packages"></a>套件中的 MSBuild 目標和屬性檔

NuGet 套件可以包含 `.targets` 和 `.props` 檔案，而這些檔案匯入至套件安裝所在的任何 MSBuild 專案。 在 NuGet 2.x 中，做法是將 `<Import>` 陳述式插入 `.csproj` 檔案中，而在 NuGet 3.0 中，則沒有特定「專案安裝」動作。 相反地，套件還原程序會寫入兩個檔案 `[projectname].nuget.props` 和 `[projectname].NuGet.targets`。

MSBuild 知道要尋找這兩個檔案，並在專案建置程序即將開始和即將結束時自動予以匯入。 其提供的行為與 NuGet 2.x 非常類似，但有一個主要差異：「在此情況下不保證目標/屬性檔順序」。 不過，MSBuild 確實會提供方法，透過 `<Target>` 定義的 `BeforeTargets` 和 `AfterTargets` 屬性來排序目標 (請參閱[目標項目 (MSBuild)](/visualstudio/msbuild/target-element-msbuild))。

## <a name="lib-and-ref"></a>Lib 和 Ref

在 NuGet v3 中，`lib` 資料夾的行為沒有太大變更。 不過，所有組件都必須在 TxM 之後所命名的子資料夾內，而且無法再直接放在 `lib` 資料夾下方。 TxM 是假設套件中指定資產作用的平台名稱。 就邏輯而言，這些是目標架構 Moniker (TFM) 的延伸模組，例如 `net45`、`net46`、`netcore50` 和 `dnxcore50` 全部都是 TxM 範例 (請參閱[目標架構](../reference/target-frameworks.md))。 TxM 可以參照架構 (TFM) 以及其他平台特定介面區。 例如，UWP TxM (`uap10.0`) 代表 .NET 介面區，以及 UWP 應用程式的 Windows 介面區。

範例 lib 結構：

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` 資料夾包含在執行階段使用的組件。 針對大部分套件，您只需要 `lib` 下每個目標 TxM 的資料夾。

## <a name="ref"></a>參考

有時，在編譯期間應該使用不同的組件 (.NET 參考組件現在會執行此作業)。 在這些情況下，使用稱為 `ref` (「參考組件」的簡稱) 的最上層資料夾。

大部分套件作者不需要 `ref` 資料夾。 它適用於套件，而套件需要提供編譯和 IntelliSense 的一致介面區，但不同的 TxM 有不同的實作。 這個的最大使用案例是在 NuGet 上傳遞 .NET Core 時所產生的 `System.*` 套件。 這些套件有透過一組一致的參考組件統一的各種實作。

透過機械方式，將 `ref` 資料夾中所含的組件傳遞至編譯器的參考組件。 針對已使用 csc.exe 的人員，這些是傳遞給 [C# /reference 選項](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)參數的組件。

`ref` 資料夾的結構與 `lib` 相同，例如：

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

在此範例中，`ref` 目錄中的組件都會相同。

## <a name="runtimes"></a>執行階段

runtimes 資料夾包含在特定「執行階段」上執行所需的組件和原生程式庫，而執行階段一般是透過作業系統和 CPU 架構所定義。 這些執行階段是使用[執行階段識別碼 (RID)](/dotnet/core/rid-catalog) (例如 `win`、`win-x86`、`win7-x86`、`win8-64` 等等) 進行識別。

## <a name="native-helpers-to-use-platform-specific-apis"></a>使用平台專屬 API 的原生協助程式

下列範例示範具有數個平台之純受控 實作的套件，但在 Windows 8 上使用可呼叫 Windows 8 特定原生 API 的原生協助程式。

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

如果是上述套件，則會發生下列事項：

- 不在 Windows 8 時，會使用 `lib/net40/MyLibrary.dll` 組件。

- 在 Windows 8 上時，會使用 `runtimes/win8-<architecture>/lib/MyLibrary.dll`，並且將 `native/MyNativeHelper.dll` 複製至組建輸出。

在上述範例中，`lib/net40` 組件是純受控程式碼，而 runtimes 資料夾中的組件將會 p/叫用到原生協助程式組件，以呼叫 Windows 8 特有的 API。

只會挑選單一 `lib` 資料夾，因此如果有執行階段專用的資料夾，則會選擇該資料夾，而不選非執行階段專用的 `lib`。 原生資料夾是加總，如果已存在，則會將它複製至組建輸出。

## <a name="managed-wrapper"></a>受控包裝函式

另一種使用執行階段的方法是傳遞透過原生組件之純受控包裝函式的套件。 在此情況下，您可以建立套件，如下所示：

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

在此情況下，沒有與該資料夾相同的最上層 `lib` 資料夾，因為沒有此套件的實作未依賴對應原生組件。 在這兩種情況下，如果受控組件 `MyLibrary.dll` 完全相同，則可以將它放入最上層 `lib` 資料夾，但因為缺少原生組件並不會造成套件安裝失敗，所以如果它已安裝在不是 win-x86 或 win-x64 的平台上，則會使用最上層 lib，但不會複製任何原生組件。

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>編寫 NuGet 2 和 NuGet 3 的套件

如果您想要建立使用 `packages.config` 的專案以及使用 `project.json` 的套件可使用的套件，則下列項目適用：

- Ref 和執行階段只作用於 NuGet 3。 NuGet 2 會同時忽略它們。

- 您無法依賴 `install.ps1` 或 `uninstall.ps1` 運作。 使用 `packages.config` 時，會執行這些檔案，但在使用 `project.json` 時則會予以忽略。 因此，您的套件需要可用，而不需要執行。 `init.ps1` 仍在 NuGet 3 上執行。

- 目標和屬性安裝不同，因此請確定您的套件在這兩個用戶端上如預期運作。

- 在 NuGet 3 中，lib 的子目錄必須是 TxM。 您無法將二進位檔放到 `lib` 資料夾根目錄。

- 使用 NuGet 3，不會自動複製內容。 您套件的取用者可以自行複製檔案，或使用工作執行器這類工具將複製檔案自動化。

- 原始程式檔和組態檔轉換不是由 NuGet 3 所執行。

如果您支援 NuGet 2 和 3，則 `minClientVersion` 應該是您套件所處理之 NuGet 2 用戶端的最低版本。 如果是現有套件，則不需要進行變更。
