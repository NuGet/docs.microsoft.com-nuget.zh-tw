---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327565"
---
# <a name="spec-command-nuget-cli"></a>spec 命令 (NuGet CLI)

**適用于:** 套件建立&bullet; **支援的版本:** 全部

`.nuspec`為新封裝產生檔案。 如果在與專案檔相同的資料夾中執行 (`.csproj`、 `.vbproj`、 `.fsproj`), `spec`則會建立`.nuspec`已標記化的檔案。 如需其他資訊, 請參閱[建立封裝](../../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用量

```cli
nuget spec [<packageID>] [options]
```

其中`<packageID>`是要儲存`.nuspec`在檔案中的選擇性套件識別碼。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| AssemblyPath | 指定要用於中繼資料之元件的路徑。 |
| 使 | 覆寫任何`.nuspec`現有的檔案。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
