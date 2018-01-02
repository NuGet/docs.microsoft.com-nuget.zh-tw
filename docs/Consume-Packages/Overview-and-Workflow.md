---
title: "使用 NuGet 套件的概觀和工作流程 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "在專案中使用 NuGet 套件之程序的概觀，以及程序之其他特定部分的連結。"
keywords: "NuGet 套件使用, NuGet 使用概觀, NuGet 使用工作流程, 套件使用工作流程, 套件使用概觀"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>套件使用工作流程

在 nuget.org 與您組織可建立的私人套件庫之間，您可以找到數以萬計的高可用套件，以在您的應用程式和服務中使用。 但是，不論來源為何，使用套件都會遵循相同的一般工作流程，如下所示。 如需詳細資料，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)和[使用套件快速入門](../quickstart/use-a-package.md)。

![移至套件來源、尋找套件、將它安裝至專案，然後新增 using 陳述式和套件 API 呼叫的流程](media/Overview-01-GeneralFlow.png)

\* _但從命令列使用 `nuget install` 除外，在此情況下，需要手動編輯組態檔。請參閱 [install 命令參考](../tools/cli-ref-install.md)。_

NuGet 會記住每個已安裝套件的身分識別和版本號碼，並將其記錄在 `packages.config`、專案檔，或專案根目錄中的 `project.json` 檔案 (視專案類型和 NuGet 版本而定)。 使用 NuGet 4.0+，[將相依性儲存至專案檔](../consume-packages/package-references-in-project-files.md)是預設值 (但目標設為 Windows 10 RS1 的 UWP 專案除外)。 在任何情況下，您隨時都可以查看適當的檔案，以查看您專案的完整相依性清單。

> [!Tip]
> 最好一律檢查您要在軟體中使用之每個套件的授權。 在 nuget.org 上，您可以在每個套件的描述頁面右側找到 [授權資訊] 連結。 如果套件未指定授權條款，請使用套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。 Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。

安裝套件時，NuGet 通常會檢查是否已經可以從其快取中使用套件。 您可以從命令列手動清除此快取，如[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md)中述。

NuGet 也會確保套件所支援的目標架構與您的專案相容。 如果套件未包含相容的組件，則 NuGet 會提供錯誤訊息。 請參閱[解決不相容的套件錯誤](dependency-resolution.md#resolving-incompatible-package-errors)。

將專案程式碼新增至來源存放庫時，您通常不會包含 NuGet 套件。 如果人員稍後複製包含 Visual Studio Team Services 這類系統上組建代理程式的存放庫，則必須先還原必要套件，再執行組建置：

![複製存放庫並使用還原命令來還原 NuGet 套件的流程](media/Overview-02-RestoreFlow.png)

[套件還原](../consume-packages/package-restore.md)使用 `packages.config`、`project.json` 專案檔中的資訊來重新安裝所有相依性。 請注意，所含的程序會有些差異，如[相依性解析](../consume-packages/dependency-resolution.md)中所述。

偶爾需要重新安裝已包含在專案中的套件，這也可能會重新安裝相依性。 透過 NuGet 命令列或 NuGet 套件管理員主控台使用 `reinstall`，就可以輕鬆做到這項作業。 如需詳細資料，請參閱[重新安裝和更新套件](../consume-packages/reinstalling-and-updating-packages.md)。

最後，NuGet 的行為是透過 `Nuget.Config` 組態檔所驅動。 可以使用多個檔案來集中管理不同層級的特定設定，如[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)所述。

使用 NuGet 套件享受具生產力的程式碼！
