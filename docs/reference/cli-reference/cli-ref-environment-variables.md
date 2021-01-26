---
title: NuGet CLI 環境變數
description: nuget.exe 環境變數的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779386"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境變數

您可以透過許多環境變數來設定 nuget.exe CLI 的行為，這會影響整部電腦、使用者或進程層級上的 nuget.exe。 環境變數一律會覆寫檔案中的任何設定 `NuGet.Config` ，讓組建伺服器能夠在不修改任何檔案的情況下變更適當的設定。

一般情況下，直接在命令列或 NuGet 設定檔中指定的選項具有優先順序，但有一些例外狀況，例如 *FORCE_NUGET_EXE_INTERACTIVE*。 如果您發現 nuget.exe 在不同電腦之間的行為不同，可能是因為環境變數的原因。 例如，在部署期間使用的 Azure Web Apps Kudu () 將 *NUGET_XMLDOC_MODE* 設定為 *skip* ，以加速封裝還原效能並節省磁碟空間。

NuGet CLI 會使用 MSBuild 來讀取專案檔。 在 MSBuild 評估期間，所有環境變數都可做為 [屬性](/visualstudio/msbuild/msbuild-command-line-reference) 。
[NuGet 套件和還原為 MSBuild 目標](../msbuild-targets.md#restore-properties)中記載的屬性清單也可以設定為環境變數。

| 變數 | 描述 | 備註 |
| --- | --- | --- |
| HTTP_proxy | 用於 NuGet HTTP 作業的 HTTP proxy。 | 這會指定為 `http://<username>:<password>@proxy.com` 。 |
| no_proxy | 將網域設定為略過使用 proxy。 | 指定為以逗號分隔的網域 (，) 。 |
| EnableNuGetPackageRestore | 如果在還原時封裝需要時，以隱含方式授與 NuGet 的旗標。 | 指定的旗標被視為 *true* 或 *1*，任何其他值視為旗標未設定。 |
| NUGET_EXE_NO_PROMPT | 防止 exe 提示輸入認證。 | Null 或空字串以外的任何值都會被視為此旗標 set/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 強制互動模式的全域環境變數。 | Null 或空字串以外的任何值都會被視為此旗標 set/true。 |
| NUGET_PACKAGES | 要用於 *全域封裝* 資料夾的路徑，如 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾所述。 | 指定為絕對路徑。 |
| NUGET_FALLBACK_PACKAGES | 全域 fallback 封裝資料夾。 | 以分號分隔的絕對資料夾路徑 (; ) 。 |
| NUGET_HTTP_CACHE_PATH | 用於 *HTTP* 快取資料夾的路徑，如 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾所述。 | 指定為絕對路徑。 |
| NUGET_PERSIST_DG | 旗標，指出是否應該保存從 MSBuild) 收集的 dg 檔案 (資料。 | 指定為 *true* 或 *false* (預設) ，如果 NUGET_PERSIST_DG_PATH 未設定，將會儲存到目前環境 temp 目錄) 中 (NuGetScratch 資料夾的臨時目錄。 |
| NUGET_PERSIST_DG_PATH | 保存 dg 檔案的路徑。 | 指定為絕對路徑，只有在 *NUGET_PERSIST_DG* 設定為 true 時，才會使用此選項。 |
| NUGET_RESTORE_MSBUILD_ARGS | 設定其他 MSBuild 引數。 | 傳遞引數，與您傳遞它們給 msbuild.exe 的方式相同。 從命令列將專案屬性 Foo 設定為值列的範例為/p： Foo = Bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 設定 MSBuild 記錄詳細資訊。 | 預設值為 *quiet* ( "/v： q" ) 。 可能的值為 *q [uiet]*、 *m [inimal]*、 *n [ormal]*、 *d [etailed]* 和 *診斷 [nostic]*。 |
| NUGET_SHOW_STACK | 決定是否應該對使用者顯示完整的例外狀況 (包括堆疊追蹤) 。 | 指定為 *true* 或 *false* (預設) 。 |
| NUGET_XMLDOC_MODE | 決定如何處理元件 XML 檔檔案解壓縮。 | 支援的模式為 *skip* (不要將 xml 檔檔案解壓縮) 、將 (儲存 xml 檔檔案 *壓縮* 成 zip 封存) 或 *無* (預設，將 xml 檔檔案視為一般檔案) 。 |
| NUGET_CERT_REVOCATION_MODE | 決定在安裝或還原已簽署的套件時，如何執行用來簽署封裝之憑證的撤銷狀態檢查。 若未設定，則預設為 `online` 。| 可能的值在 *線上* (預設) （ *離線*）。  與[NU3028](../errors-and-warnings/NU3028.md)相關 |

