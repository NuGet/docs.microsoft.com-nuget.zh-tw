---
title: NuGet CLI 新增命令
description: Nuget.exe 的參考加入命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545830"
---
# <a name="add-command-nuget-cli"></a>add 命令 (NuGet CLI)

**適用於**： 封裝發行&bullet;**支援的版本**: 3.3 +

將指定的封裝加入至階層的配置，其中會建立資料夾的套件識別碼和版本號碼的非 HTTP 套件來源 （資料夾或 UNC 路徑） 中。 例如: 

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

當還原或更新對套件來源時，階層式版面配置會提供大幅提升效能。

若要展開套件中的所有檔案到目的地套件來源，請使用`-Expand`切換。 這通常不會出現在目的地，例如其他子資料夾中會造成`tools`和`lib`。

## <a name="usage"></a>使用量

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

何處`<packagePath>`是要加入，封裝的路徑名稱和`<sourcePath>`指定要加入封裝的資料夾為基礎的封裝來源。 不支援 HTTP 來源。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| Expand | 將封裝中的所有檔案，加入套件來源。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
