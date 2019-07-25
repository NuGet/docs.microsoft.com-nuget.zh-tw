---
title: NuGet project.json 封存內容
description: 從 NuGet 文件的其他區域所移除的各種 project.json 內容。
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 8d732e87f01c55bde87da0a2e382fd6d509886a3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317007"
---
# <a name="projectjson-archive"></a>project.json 封存

`project.json` 管理格式於 NuGet 3.x 引進並用於某些專案類型。 此格式已隨著 PackageReference 格式的引進而被取代，後者將相依性直接列在專案檔中。

也請參閱：

- [project.json 結構描述](project-json.md)
- [project.json 對套件作者的影響](project-json-impact.md)
- [project.json 和 UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>project.json 管理格式

原本在[套件還原](../what-is-nuget.md)中。 

在管理格式的清單中：

- [`project.json`](project-json.md)：(已過時)  這是一個 JSON 檔案，負責維護相關檔案 (`project.lock.json`) 中專案與整體套件關係圖的相依性清單。 此格式已由 PackageReference 所取代。

## <a name="nuget-restore-on-mono"></a>在 Mono 上的 nuget restore

原本在[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)中 

適用於 `project.json`。

## <a name="constraining-package-versions-with-restore"></a>使用還原限制套件版本

原本在[套件還原](../consume-packages/package-restore.md#constrain-package-versions-with-restore)中。 

- `project.json`：直接使用相依性的版本號碼來指定版本範圍。 例如：

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLI 命令

- `nuget install` 不適用於 `project.json`。
- `nuget restore`：針對使用 `project.json` 的專案，會視需要產生 `project.lock.json` 檔案和 `<project>.nuget.props` 檔案。 (兩個檔案都可以從原始檔控制省略)。`<projectPath>` 引數可以指向 `project.json` 檔案，且其行為就和指向 `packages.config` 或專案檔一樣。 根據套件資料夾的優先順序，使用 `project.json` 時會先搜尋 `%userprofile%\.nuget\packages`。
- `nuget update`：在 Mono 上，此命令無法與使用 `project.json` 的專案搭配使用。

## <a name="dependency-resolution-with-packagereference"></a>使用 PackageReference 的相依性解析

原本在[相依性解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中。 

PackageReference 的行為也適用於 `project.json`。 NuGet restore 將相依性關係圖寫入名為 `project.lock.json` 和 `project.json` 的檔案中。

## <a name="managing-dependency-assets"></a>管理相依性資產

原本在[相依性解析](../consume-packages/dependency-resolution.md#managing-dependency-assets)中。 

使用 `project.json` 格式時，您可以控制從相依性流入最上層專案的資產。 如需詳細資訊，請參閱 [project.json](project-json.md)。

## <a name="excluding-references"></a>排除參考

原本在[相依性解析](../consume-packages/dependency-resolution.md#excluding-references)中。 

- `project.json`：在套件 C 的相依性中新增 `"exclude" : "all"`：

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>解決不相容的套件錯誤

原本在[相依性解析](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)中。 

新增解決錯誤的方法：

- **不建議**：作為與套件作者合作時的暫時方案，目標設為 `netcore`、`netstandard` 和 `netcoreapp` 的專案可以將其他架構表示為相容，進而允許使用將目標設為這些其他架構的套件。 請參閱 [project.json 匯入](project-json.md#imports)和 [MSBuild 還原目標 PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback)。 這可能會造成非預期的行為，因此，同樣地，最好與套件作者合作處理更新，以解決套件不相容。

## <a name="target-frameworks"></a>目標 Framework

原本在[目標 Framework](../reference/target-frameworks.md) 中。 

- [project.json](project-json.md)：`frameworks` 節點會指定專案可以編譯的 Framework 版本。

## <a name="creating-a-package"></a>建立套件

原本在[建立套件](../create-packages/creating-a-package.md)中。 

### <a name="setting-a-package-type"></a>設定套件類型

使用 .NET Core 1.x 時，若安裝了 DotnetCliTool 套件，Visual Studio 會將套件放入 `project.json` `tools` 節點中，而不是 `dependencies` 節點。

套件類型是在 `project.json` 中設定的。

- `project.json`：指出 `packOptions.packageType` 屬性 JSON 內的套件類型：

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>新增 MSBuild 的目標與 props

原本在[使用 Visual Studio 2015 建立 .NET Standard NuGet 套件](../guides/create-net-standard-packages-vs2015.md)中。 

當使用 `project.json` 時，目標不會新增至專案，但可透過 `project.lock.json` 提供。

### <a name="package-versioning"></a>套件版本控制

原本在[套件版本控制](../reference/package-versioning.md)中。 

當使用 `project.json` 格式時，針對編號的主要、次要、修補和發行前版本後置詞部分，NuGet 也支援使用萬用字元標記法 (\*)。

### <a name="nugetconfig-reference"></a>NuGet.Config 參考

原本在 [NuGet.Config 參考](../reference/nuget-config-file.md)中。 

`globalPackagesFolder` 僅適用於 `project.json`。 (新增附註：也適用於 PackageReference。)

### <a name="nuspec-file-reference"></a>nuspec 檔案參考

原本在 [nuspec 參考](../reference/nuspec.md)中。 

使用 `<contentFiles>` 元素，而不是包含 `project.json` 的 `<files>`。

### <a name="package-manager-options-control"></a>套件管理員選項控制

原本在[套件管理員 UI 參考](../consume-packages/install-use-packages-visual-studio.md)中。 

使用 `project.json` 管理格式的專案只顯示 [顯示預覽視窗]  選項。

### <a name="visual-studio-templates"></a>Visual Studio 範本

原本在 [Visual Studio 範本中的 NuGet 套件](../visual-studio-extensibility/visual-studio-templates.md)中。 

最佳做法：範本不包含 `project.json` 檔案，而且不包含安裝 NuGet 套件時所新增的任何參考或內容。