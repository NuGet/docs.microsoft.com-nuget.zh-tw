---
title: NuGet CLI 環境變數
description: Nuget.exe 環境變數的參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817069"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境變數

Nuget.exe CLI 行為可以透過環境變數，其中會影響 nuget.exe 全電腦的使用者或處理序層級的數目來設定。 環境變數一律會覆寫中的任何設定`NuGet.Config`檔，讓建置伺服器變更適當的設定，而不需修改任何檔案。

一般情況下，直接在命令列上，或在 NuGet 組態檔中指定的選項的優先順序，但有少數的例外狀況的這類*FORCE_NUGET_EXE_INTERACTIVE*。 如果您發現該 nuget.exe 的行為方式會不同電腦之間，環境變數可能是原因。 例如，Azure Web 應用程式 Kudu （在部署期間使用） 具有*NUGET_XMLDOC_MODE*設*略過*來加速封裝還原效能，並節省磁碟空間。

| 變數 | 描述 | 備註 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 作業所使用的 http proxy。 | 這會指定為`http://<username>:<password>@proxy.com`。 |
| no_proxy | 設定網域以使用 proxy 略過。 | 指定為以逗號 （，） 分隔的網域。 |
| EnableNuGetPackageRestore | 如果 NuGet 應該以隱含方式授與同意，如果所需還原上套件的旗標。 | 指定的旗標會被視為*true*或*1*，未設定任何其他值視為旗標。 |
| NUGET_EXE_NO_PROMPT | 防止提示輸入認證的 exe。 | 任何值，除了 null 或空字串會被視為此旗標組/true。 |
| FORCE_NUGET_EXE_INTERACTIVE | 若要強制互動模式的全域環境變數。 | 任何值，除了 null 或空字串會被視為此旗標組/true。 |
| NUGET_PACKAGES | 路徑，供*全域封裝*資料夾述[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定為絕對路徑。 |
| NUGET_FALLBACK_PACKAGES | 全域後援封裝的資料夾。 | 絕對的資料夾路徑，並以分號 （;）。 |
| NUGET_HTTP_CACHE_PATH | 路徑，供*http 快取*資料夾述[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 | 指定為絕對路徑。 |
| NUGET_PERSIST_DG | 表示是否應該保存 dg 檔案 （從 MSBuild 收集資料） 的旗標。 | 指定為*true*或*false* （預設值），如果未設定 NUGET_PERSIST_DG_PATH 將儲存至暫存目錄 （NuGetScratch 資料夾在目前環境的暫存目錄中）。 |
| NUGET_PERSIST_DG_PATH | 保存 dg 檔案的路徑。 | 指定為絕對路徑，此選項使用的時，才會*NUGET_PERSIST_DG*設為 true。 |
| NUGET_RESTORE_MSBUILD_ARGS | 設定其他的 MSBuild 引數。 | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | 設定 MSBuild 記錄詳細資訊。 | 預設值是*安靜*("/ v: q")。 可能的值*q [uiet]*， *m [inimal]*， *n [ormal]*， *d [etailed]*，和*diag [nostic]*。 |
| NUGET_SHOW_STACK | 決定完整的例外狀況 （包括堆疊追蹤） 是否應該顯示給使用者。 | 指定為*true*或*false* （預設值）。 |
| NUGET_XMLDOC_MODE | 決定應該如何處理組件 XML 文件檔解壓縮。 | 支援的模式是*略過*（不要擷取 XML 文件檔），*壓縮*（的 zip 封存中儲存 XML 文件檔案） 或*無*（預設值，將 XML 文件的檔案都視為一般檔案）。 |
