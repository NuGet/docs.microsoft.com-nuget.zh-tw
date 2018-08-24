---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794147"
---
# <a name="spec-command-nuget-cli"></a>規格的命令 (NuGet CLI)

**適用於：** 封裝建立&bullet;**支援的版本：** 所有

會產生`.nuspec`新封裝的檔案。 如果在專案檔相同的資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。 如需詳細資訊，請參閱[建立套件](../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用量

```cli
nuget spec [<packageID>] [options]
```

何處`<packageID>`是選擇性的套件識別碼儲存在`.nuspec`檔案。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AssemblyPath | 指定要用於中繼資料的組件的路徑。 |
| 強制 | 覆寫任何現有`.nuspec`檔案。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
