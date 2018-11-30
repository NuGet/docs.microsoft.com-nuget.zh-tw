---
title: 建立 NuGet 套件的概觀和工作流程
description: 建立和發行 NuGet 套件程序的概觀，以及程序之其他特定部分的連結。
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 6b41b23df115c45e830404afcf9defa23615bd7c
ms.sourcegitcommit: ce97dded7715f217ec44f6c8368ab0df19c38342
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2018
ms.locfileid: "52615752"
---
# <a name="package-creation-workflow"></a>套件建立工作流程

建立套件是以想要封裝並與其他人共用 (透過公用 nuget.org 資源庫或組織內的私用資源庫) 的已編譯程式碼 (一般是 .NET 組件) 開始。 套件也可以包含其他檔案 (例如，安裝套件時所顯示的讀我檔案)，而且可以包含特定專案檔的轉換。

套件也可以只用來拉回任意數目的其他相依性，而不包含任何其專屬的程式碼。 這類套件是傳遞包含多個獨立套件之 SDK 的便利方式。 在其他情況下，套件可能只包含符號 (`.pdb`) 檔案，以協助偵錯。

> [!Note]
> 當您建立供其他開發人員使用的套件時，請務必了解它們會與您的工作相依。 因此，建立並發行套件也表示承諾修正 Bug 以及進行其他更新，或在極少的情況下將套件設為開放原始碼，以讓其他人可以協助進行維護。

不管是哪種情況，建立套件都是從決定要封裝的組件和其他檔案開始。 您接著會建立資訊清單檔案 (稱為 `.nuspec` 檔案)，以描述套件的內容以及其識別碼、版本號碼、著作權資訊、MSBuild pros 和 targets 等等。

當您在適當的資料夾中準備好所有必要檔案並建立適當的 `.nuspec` 檔案時，則會使用 `nuget pack` 命令 (或 [MSBuild 封裝目標](../reference/msbuild-targets.md)) 以將所有項目都放入 `.nupkg` 檔案中。 您準備好將套件部署至可讓其他開發人員使用它的主機。

> [!Tip]
> 副檔名為 `.nupkg` 的 NuGet 套件就是 ZIP 檔案。 若要輕鬆地檢查任何套件的內容，請將副檔名變更為 `.zip`，並如常展開其內容。 只要確定先將副檔名變更回 `.nupkg`，再嘗試將它重新載入至主機。

若要學習並了解建立程序，請從[建立套件](../create-packages/creating-a-package.md)開始，其會引導您完成所有套件通用的核心程序。

在這裡，您可以考慮您套件的許多其他選項：

- [支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)描述如何建立具有不同 .NET Frameworks 之多個變異的套件。
- [建立當地語系化套件](../create-packages/creating-localized-packages.md)描述如何建構具有多個語言資源的套件，以及如何使用個別的當地語系化附屬套件。
- [發行前套件](../create-packages/prerelease-packages.md)示範如何將 alpha、beta 和 rc 套件發行至感興趣的客戶。
- [原始程式檔和組態檔轉換](../create-packages/source-and-config-file-transformations.md)描述如何在新增至專案的檔案中執行兩個單向權杖取代，以及使用會在解除安裝套件時取消的設定來修改 `web.config` 和 `app.config`。
- [符號套件](../create-packages/symbol-packages-snupkg.md)提供用於提供程式庫符號的指引，而符號允許取用者在偵錯時逐步執行程式碼。
- [套件版本控制](../reference/package-versioning.md)討論如何識別您相依性容許的確切版本 (從套件取用的其他套件)。
- [原生套件](../create-packages/native-packages.md)描述用於建立 C++ 取用者之套件的程序。
- [簽署套件](../create-packages/sign-a-package.md)描述用於在套件新增數位簽章的程序。

當您準備好將套件發行至 nuget.org 時，請遵循[發行套件](../create-packages/publish-a-package.md)中的簡單程序。

如果您想要使用私人摘要，而非 nuget.org，請參閱[裝載套件概觀](../hosting-packages/overview.md)
