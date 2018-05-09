---
title: 將命令加入 NuGet CLI
description: Nuget.exe 的參考加入命令
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a>加入命令 (NuGet CLI)

**適用於**： 封裝發行&bullet;**支援的版本，**: 3.3 +

將指定的封裝加入至階層式配置，其中的封裝識別碼和版本號碼會建立資料夾中的非 HTTP 封裝來源 （資料夾或 UNC 路徑）。 例如: 

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

當還原或更新對套件來源時，階層式配置會提供大幅提升效能。

若要擴充套件中的所有檔案到目的地封裝來源，使用`-Expand`切換。 這通常會導致其他子資料夾，例如出現在目的地`tools`和`lib`。

## <a name="usage"></a>使用量

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中`<packagePath>`是若要加入，封裝的路徑名稱和`<sourcePath>`指定要加入封裝的資料夾為基礎的封裝來源。 不支援 HTTP 的來源。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 要套用的 NuGet 設定檔案。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。|
| Expand | 加入封裝中的所有檔案，對套件來源。 |
| ForceEnglishOutput | *（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
