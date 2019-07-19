---
title: NuGet CLI 新增命令
description: Nuget.exe add 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327855"
---
# <a name="add-command-nuget-cli"></a>add 命令 (NuGet CLI)

**適用**于: 套件發佈&bullet; **支援的版本**:3.3+

將指定的封裝新增至階層式配置中的非 HTTP 封裝來源 (資料夾或 UNC 路徑), 其中會建立套件識別碼和版本號碼的資料夾。 例如：

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

針對套件來源還原或更新時, 階層式配置可提供明顯較佳的效能。

若要將封裝中的所有檔案展開至目的地封裝來源, 請使用`-Expand`參數。 這通常會導致目的地中出現額外的子資料夾, 例如`tools`和`lib`。

## <a name="usage"></a>使用量

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中`<packagePath>`是要新增之封裝的路徑名稱, 並`<sourcePath>`指定要新增封裝之以資料夾為基礎的封裝來源。 不支援 HTTP 來源。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| Expand | 將封裝中的所有檔案新增至封裝來源。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
