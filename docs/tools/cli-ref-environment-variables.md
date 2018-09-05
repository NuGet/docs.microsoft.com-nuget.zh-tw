---
title: NuGet CLI 環境變數
description: Nuget.exe 環境變數的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551734"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境變數

Nuget.exe CLI 的行為可以透過幾個環境變數，這會影響整個電腦的使用者，nuget.exe 或處理序層級的設定。 環境變數一律會覆寫中的任何設定`NuGet.Config`檔案，讓組建伺服器，以變更適當的設定，而不需修改任何檔案。

一般情況下，直接在命令列上或在 NuGet 組態檔中指定的選項的優先順序，但有少數的例外狀況的這類*FORCE_NUGET_EXE_INTERACTIVE*。 如果您發現該 nuget.exe，表現不同的電腦之間，環境變數可能是原因。 例如，Azure Web Apps Kudu （在部署期間使用） 具有*NUGET_XMLDOC_MODE*設為*略過*提升套件還原效能並節省磁碟空間。

| 變數 | 描述 | 備註 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 作業所使用的 http proxy。 | 這會指定為`http://<username>:<password>@proxy.com`。 |
| no_proxy | 設定使用 proxy 略過的網域。 | 指定為逗號 （，） 分隔的網域。 |
| EnableNuGetPackageRestore | 如果 NuGet 應以隱含方式授與同意，所還原的套件的旗標。 | 指定的旗標會被視為 *，則為 true*或是*1*，未設定任何其他視為旗標的值。 |
| NUGET_EXE_NO_PROMPT | 可防止提示輸入認證的 exe。 | 任何值，除了 null 或空字串會被視為此旗標集/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 若要強制互動模式的全域環境變數。 | 任何值，除了 null 或空字串會被視為此旗標集/true。 |
| NUGET_PACKAGES | 若要使用的路徑*全域套件*資料夾上所述[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定為絕對路徑。 |
| NUGET_FALLBACK_PACKAGES | 後援的全域套件資料夾。 | 以分號 （;） 分隔的絕對的資料夾路徑。 |
| NUGET_HTTP_CACHE_PATH | 若要使用的路徑*http 快取*資料夾上所述[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定為絕對路徑。 |
| NUGET_PERSIST_DG | 表示是否應該保存 dg 檔案 （從 MSBuild 所收集的資料） 的旗標。 | 指定為 *，則為 true*或是*false* （預設值），如果未設定 NUGET_PERSIST_DG_PATH 會儲存到暫存目錄 （NuGetScratch 資料夾在目前環境的暫存目錄中）。 |
| NUGET_PERSIST_DG_PATH | 保存通訊群組檔案的路徑。 | 指定為絕對路徑，此選項時才會使用*NUGET_PERSIST_DG*設為 true。 |
| NUGET_RESTORE_MSBUILD_ARGS | 設定額外的 MSBuild 引數。 | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 設定 MSBuild 記錄詳細資訊。 | 預設值是*安靜*("/ v: q")。 可能的值*q [uiet]*， *m [inimal]*， *n [ormal]*， *d [etailed]*，以及*diag [nostic]*。 |
| NUGET_SHOW_STACK | 判斷是否應該向使用者顯示完整的例外狀況 （包括堆疊追蹤）。 | 指定為*真*或是*false* （預設值）。 |
| NUGET_XMLDOC_MODE | 決定應該如何處理組件 XML 文件檔解壓縮。 | 支援的模式如下*略過*（不要擷取 XML 文件檔案），*壓縮*（儲存為 zip 封存的 XML 文件檔案） 或*none* （預設值，視為一般的 XML 文件檔案檔案）。 |
| NUGET_CERT_REVOCATION_MODE | 決定如何撤銷狀態檢查用來簽署封裝的憑證，簽署的套件會安裝或還原時，pefromed。 如果未設定，預設為`online`。| 可能的值*線上*（預設值），*離線*。  相關[NU3028](../reference/errors-and-warnings/NU3028.md) |
