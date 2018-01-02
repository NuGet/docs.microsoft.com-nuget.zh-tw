---
title: "針對 Visual Studio 中的 NuGet 套件還原進行疑難排解 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Visual Studio 中常見的 NuGet 還原錯誤描述，以及如何針對這些錯誤進行疑難排解。"
keywords: "NuGet 套件還原, 還原套件, 進行疑難排解, 疑難排解"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>針對 Visual Studio 中的套件還原錯誤進行疑難排解

> [!Note]
> 此頁面會著重於在 Visual Studio 中還原套件時常見的錯誤及其解決步驟。 如欲了解如何還原套件，請參閱[套件還原](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore)。

根據預設，在 Visual Studio 中建置專案會自動還原專案中參考的 NuGet 套件。 不過，如果 [工具] > [選項] > [NuGet 套件管理員] > [套件還原] 設定中已停用套件還原，且電腦上沒有必要的套件，建置就會失敗。 在這些案例中您可能會看到下列錯誤：

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

若要啟用 [套件還原]，請開啟 [工具] > [選項] > [NuGet 套件管理員]，選取 [允許 NuGet 下載遺漏的套件] 和 [在 Visual Studio 建置期間自動檢查遺漏的套件] 選項：

![在工具/選項中啟用 NuGet 套件還原](../Consume-Packages/media/restore-01-autorestoreoptions.png)

