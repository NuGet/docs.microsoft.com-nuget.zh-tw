---
title: 設定 NuGet 套件類型
description: 描述套件類型以指出套件的預定用途。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774358"
---
# <a name="set-a-nuget-package-type"></a>設定 NuGet 套件類型

使用 NuGet 3.5+，可以將套件標上特定「套件類型」，指出其預定用途。 未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。

- `Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。

- `DotnetTool` 類型套件是 [dotnet CLI](/dotnet/articles/core/tools/index) 的延伸模組，而且是從命令列叫用的。 這類套件只能安裝在 .NET Core 專案中，而且不會影響還原作業。 [.NET Core 擴充性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文件提供所有這些專案延伸模組的詳細資料。

- `Template` 型別套件提供 [自訂範本](/dotnet/core/tools/custom-templates) ，可用來建立應用程式、服務、工具或類別庫等檔案或專案。

- 自訂類型套件會使用任意類型識別碼，而其符合與套件識別碼相同的格式規則。 不過，Visual Studio 中的 NuGet 套件管理員無法辨識 `Dependency` 和 `DotnetTool` 以外的任何類型。

套件類型是設定在 `.nuspec` 檔案中。 針對回溯相容性，最好「不要」明確設定 `Dependency` 類型，而是在未指定類型時改為依賴採用此類型的 NuGet。

- `.nuspec`：指出 `<metadata>` 項目的 `packageTypes\packageType` 節點內的套件類型：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
