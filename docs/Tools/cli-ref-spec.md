---
title: "NuGet CLI 規格命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe 規格命令參考"
keywords: "nuget 規格的參考，規格命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>規格命令 (NuGet CLI)

**適用於：**封裝建立&bullet;**支援的版本：**所有

會產生`.nuspec`新套件的檔案。 如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。 如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用方式

```
nuget spec [<packageID>] [options]
```

其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| AssemblyPath | 指定要用於中繼資料組件的路徑。 |
| 強制 | 覆寫任何現有`.nuspec`檔案。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
