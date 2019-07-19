---
title: NuGet CLI 環境變數
description: Nuget.exe 環境變數的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327825"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境變數

您可以透過數個環境變數來設定 nuget.exe CLI 的行為, 這會影響整部電腦、使用者或進程層級上的 nuget.exe。 環境變數一律會覆寫檔案`NuGet.Config`中的任何設定, 讓組建伺服器能夠變更適當的設定, 而不需要修改任何檔案。

一般而言, 直接在命令列或 NuGet 設定檔中指定的選項具有優先順序, 但有一些例外狀況, 例如*FORCE_NUGET_EXE_INTERACTIVE*。 如果您發現 nuget.exe 在不同電腦之間的行為不同, 環境變數可能是原因。 例如, Azure Web Apps Kudu (在部署期間使用) 已將*NUGET_XMLDOC_MODE*設定為 [*略過*], 以加速封裝還原效能並節省磁碟空間。

NuGet CLI 會使用 MSBuild 來讀取專案檔案。 在 MSBuild 評估期間, 所有環境變數都可做為[屬性](/visualstudio/msbuild/msbuild-command-line-reference)。
[NuGet 套件和還原為 MSBuild 目標](../msbuild-targets.md#restore-properties)中記載的屬性清單, 也可以設定為環境變數。

| 變數 | 描述 | 備註 |
| --- | --- | --- |
| http_proxy | 用於 NuGet HTTP 作業的 HTTP proxy。 | 這會指定為`http://<username>:<password>@proxy.com`。 |
| no_proxy | 設定網域以略過使用 proxy。 | 指定為以逗號 (,) 分隔的網域。 |
| EnableNuGetPackageRestore | 如果在還原時封裝需要時, NuGet 應隱含授與同意, 則為的旗標。 | 指定的旗標會被視為*true*或*1*, 任何其他值會被視為未設定旗標。 |
| NUGET_EXE_NO_PROMPT | 防止 exe 提示輸入認證。 | 除了 null 或空字串以外的任何值都會被視為設定此旗標/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 用來強制互動模式的全域環境變數。 | 除了 null 或空字串以外的任何值都會被視為設定此旗標/true。 |
| NUGET_PACKAGES | 要用於*全域封裝*資料夾的路徑, 如[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾中所述。 | 指定為絕對路徑。 |
| NUGET_FALLBACK_PACKAGES | 全域回溯封裝資料夾。 | 以分號分隔的絕對資料夾路徑 (;)。 |
| NUGET_HTTP_CACHE_PATH | 要用於*HTTP*快取資料夾的路徑, 如[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾中所述。 | 指定為絕對路徑。 |
| NUGET_PERSIST_DG | 表示是否應該保存 dg 檔案 (從 MSBuild 收集的資料) 的旗標。 | 指定為*true*或*false* (預設值), 如果未設定 NUGET_PERSIST_DG_PATH, 將會儲存至臨時目錄 (在目前環境臨時目錄中的 NuGetScratch 資料夾)。 |
| NUGET_PERSIST_DG_PATH | 保存 dg 檔案的路徑。 | 指定為絕對路徑, 只有在*NUGET_PERSIST_DG*設定為 true 時, 才會使用此選項。 |
| NUGET_RESTORE_MSBUILD_ARGS | 設定其他 MSBuild 引數。 | 傳遞引數與傳遞給 msbuild.exe 的方式相同。 將專案屬性 Foo 從命令列設定為值列的範例是/p: Foo = Bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 設定 MSBuild 記錄詳細資訊。 | 預設值為*quiet* ("/v: q")。 可能的值*q [uiet]* 、 *m [inimal]* 、 *n [ormal]* 、 *d [etailed]* 和 *[診斷] [nostic]* 。 |
| NUGET_SHOW_STACK | 決定是否應該對使用者顯示完整的例外狀況 (包括堆疊追蹤)。 | 指定為*true*或*false* (預設值)。 |
| NUGET_XMLDOC_MODE | 決定如何處理元件 XML 檔檔案的解壓縮。 | 支援的模式為*skip* (不要解壓縮 XML 檔檔)、*壓縮*(將 xml 檔檔案儲存為 zip 封存) 或*none* (預設值, 將 xml 檔檔案視為一般檔案)。 |
| NUGET_CERT_REVOCATION_MODE | 決定在安裝或還原已簽署的套件時, 是否要檢查用來簽署封裝之憑證的撤銷狀態。 [未設定] 時, `online`預設為。| 可能值*上線*(預設值),*離線*。  與[NU3028](../errors-and-warnings/NU3028.md)相關 |

