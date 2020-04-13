---
title: 設定 NuGet 套件類型
description: 描述套件類型以指出套件的預定用途。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230820"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="84ca0-103">設定 NuGet 套件類型</span><span class="sxs-lookup"><span data-stu-id="84ca0-103">Set a NuGet package type</span></span>

<span data-ttu-id="84ca0-104">使用 NuGet 3.5+，可以將套件標上特定「套件類型」\*\*，指出其預定用途。</span><span class="sxs-lookup"><span data-stu-id="84ca0-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="84ca0-105">未標示類型的套件 (包含使用舊版 NuGet 所建立的所有套件) 預設為 `Dependency` 類型。</span><span class="sxs-lookup"><span data-stu-id="84ca0-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="84ca0-106">`Dependency` 類型套件會將建置或執行階段資產新增至程式庫和應用程式，並且可以安裝至任何專案類型 (假設它們相容)。</span><span class="sxs-lookup"><span data-stu-id="84ca0-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="84ca0-107">`DotnetTool` 類型套件是 [dotnet CLI](/dotnet/articles/core/tools/index) 的延伸模組，而且是從命令列叫用的。</span><span class="sxs-lookup"><span data-stu-id="84ca0-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="84ca0-108">這類套件只能安裝在 .NET Core 專案中，而且不會影響還原作業。</span><span class="sxs-lookup"><span data-stu-id="84ca0-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="84ca0-109">[.NET Core 擴充性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文件提供所有這些專案延伸模組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="84ca0-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="84ca0-110">`Template`類型套件提供可用於建立檔案或專案(如應用、服務、工具或類別庫)[的自訂樣本](/dotnet/core/tools/custom-templates)。</span><span class="sxs-lookup"><span data-stu-id="84ca0-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="84ca0-111">自訂類型套件會使用任意類型識別碼，而其符合與套件識別碼相同的格式規則。</span><span class="sxs-lookup"><span data-stu-id="84ca0-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="84ca0-112">不過，Visual Studio 中的 NuGet 套件管理員無法辨識 `Dependency` 和 `DotnetTool` 以外的任何類型。</span><span class="sxs-lookup"><span data-stu-id="84ca0-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="84ca0-113">套件類型是設定在 `.nuspec` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="84ca0-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="84ca0-114">針對回溯相容性，最好「不要」\*\* 明確設定 `Dependency` 類型，而是在未指定類型時改為依賴採用此類型的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="84ca0-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="84ca0-115">`.nuspec`：指出 `<metadata>` 項目的 `packageTypes\packageType` 節點內的套件類型：</span><span class="sxs-lookup"><span data-stu-id="84ca0-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
