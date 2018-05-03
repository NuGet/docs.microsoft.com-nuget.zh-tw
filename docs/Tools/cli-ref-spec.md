---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a>規格命令 (NuGet CLI)

**適用於：**封裝建立&bullet;**支援的版本：**所有

會產生`.nuspec`新套件的檔案。 如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。 如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用量

```cli
nuget spec [<packageID>] [options]
```

其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| AssemblyPath | 指定要用於中繼資料組件的路徑。 |
| 強制 | 覆寫任何現有`.nuspec`檔案。 |
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
