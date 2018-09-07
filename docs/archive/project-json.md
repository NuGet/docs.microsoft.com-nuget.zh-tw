---
title: NuGet 的 project.json 檔案參考
description: 在某些專案類型中，project.json 會維護專案中所使用的 NuGet 套件清單。
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547780"
---
# <a name="projectjson-reference"></a>project.json 參考

*NuGet 3.x+*

`project.json` 檔案維護一份專案中使用的套件之清單，稱為套件管理格式。 它會取代 `packages.config`，但又被 NuGet 4.0+ 的 [PackageReference](../consume-packages/package-references-in-project-files.md) 所取代。

[`project.lock.json`](#projectlockjson) 檔案 (如下所述) 也用於採用 `project.json` 的專案。

`project.json` 有下列的基本結構，其中四個最上層物件每個都可以有任意數目的子物件：

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>相依性

以下列形式，列出您專案的 NuGet 套件相依性：

```json
"PackageID" : "version_constraint"
```

例如: 

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies` 區段是 [NuGet 套件管理員] 對話方塊將套件相依性新增到專案的位置。

套件識別碼對應至 nuget.org 上的套件識別碼，與套件管理員主控台中使用的識別碼相同：`Install-Package Microsoft.NETCore`。

還原套件時，`"5.0.0"` 的版本條件約束意味著 `>= 5.0.0`。 也就是說，如果伺服器上未提供 5.0.0，但有提供 5.0.1，則 NuGet 會安裝 5.0.1，而且會警告您有關此升級。 否則 NuGet 會在符合條件約束的伺服器上挑選最低的可能版本。

如需解析規則的詳細資料，請參閱[相依性解析](../consume-packages/dependency-resolution.md)。

### <a name="managing-dependency-assets"></a>管理相依性資產

相依性的哪些資產流入最上層專案，是藉由在相依性參考的 `include` 和 `exclude` 屬性指定以逗號分隔的標記集合來控制。 標記會列在下列資料表中：

| 包含/排除標記 | 目標的受影響資料夾 |
| --- | --- |
| contentFiles | 內容  |
| 執行階段 | 執行階段、資源和 FrameworkAssemblies  |
| compile | lib |
| build | 組建 (MSBuild props 和目標) |
| native | native |
| 無 | 無資料夾 |
| 全部 | 全部資料夾 |

以 `exclude` 指定的標記優先於以 `include` 指定的標記。 例如，`include="runtime, compile" exclude="compile"` 與 `include="runtime"` 相同。

例如，若要包含相依性的 `build` 和 `native` 資料夾，請使用下列命令：

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

若要排除相依性的 `content` 和 `build` 資料夾，請使用下列命令：

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>架構

列出專案執行所在的架構，例如 `net45`、`netcoreapp`、`netstandard`。

```json
"frameworks": {
    "netcore50": {}
    }
 ```

在 `frameworks` 區段中只允許單一項目。 (有一項例外就是使用已淘汰的 DNX 工具鏈建置之 ASP.NET 專案的 `project.json` 檔，它允許多個目標。)

## <a name="runtimes"></a>執行階段

列出您的應用程式執行所在的作業系統和架構，例如 `win10-arm`、`win8-x64`、`win8-x86`。

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

包含可在任何執行階段上執行之 PCL 的套件不需要指定執行階段。 任何相依性也必須都是如此，否則您必須指定執行階段。


## <a name="supports"></a>Supports

定義一組套件相依性檢查。 您可以定義您預期 PCL 或應用程式執行的位置。 定義沒有限制，因為您的程式碼可能能夠在其他位置執行。 但是，指定這些檢查可以讓 NuGet 確認在列出的 TxM 上符合所有相依性。 此值的範例有 `net46.app`、`uwp.10.0.app` 等等。

當您在可攜式類別庫目標對話方塊中選取一個項目時，應該會自動填入此區段。

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Imports

Imports 設計目的是為了讓使用 `dotnet` TxM 的套件能和未宣告 dotnet TxM 的套件一起運作。 如果您的專案使用 `dotnet` TxM，除非您將下列內容新增至 `project.json`，以讓非 `dotnet` 平台變成能與 `dotnet` 相容，否則您相依的所有套件也必須要有 `dotnet` TxM：

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

如果您使用 `dotnet` TxM，則 PCL 專案系統會根據支援的目標，新增適當的 `imports` 陳述式。

## <a name="differences-from-portable-apps-and-web-projects"></a>與可攜式應用程式和 Web 專案的差異

NuGet 所使用的 `project.json` 檔案，是在 ASP.NET Core 專案中找到的檔案子集。 在 ASP.NET Core 中，`project.json` 用於專案中繼資料、編譯資訊，以及相依性。 用於其他專案系統時，這三項會分成不同的檔案，且 `project.json` 會包含較少資訊。 值得注意的差異包括：

- 在 `frameworks` 區段只能有一個架構。

- 檔案不能包含您在 DNX `project.json` 檔案看到的相依性、編譯選項等等。 假設只能有單一架構，輸入特定架構的相依性便沒有意義。

- 編譯由 MSBuild 處理，所以編譯選項、前置處理器定義等都是屬於 MSBuild 專案檔，而非 `project.json`。

在 NuGet 3+ 中，開發人員不應該手動編輯 `project.json`，因為 Visual Studio 中的套件管理員 UI 會操作其內容。 話雖如此，您確實可以編輯檔案，但您必須建置專案以啟動套件還原，或以另一種方式叫用還原。 請參閱[套件還原](../consume-packages/package-restore.md)。


## <a name="projectlockjson"></a>project.lock.json

在使用 `project.json` 的專案中還原 NuGet 套件的過程，會產生 `project.lock.json` 檔。 它保留當 NuGet 逐步檢查套件的圖形時所產生的所有資訊快照集，並且包含您專案中所有套件的版本、內容和相依性。 在建置專案時，組建系統用這來從相關全域位置選擇套件，而不依賴專案本身的本機 packages 資料夾。 這會導致更快的組建效能，因為只需要讀取 `project.lock.json`，而不是許多個不同的 `.nuspec` 檔案。

`project.lock.json` 會在套件還原時自動產生，所以可以從原始檔控制中省略，方法是將它新增至 `.gitignore` 和 `.tfignore` 檔案 (請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。 不過，如果您將它包含在原始檔控制中，變更歷程記錄會顯示在一段時間解析的相依性變化。
