---
title: NuGet CLI 新增命令
description: nuget.exe add 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776086"
---
# <a name="add-command-nuget-cli"></a> (NuGet CLI 新增命令) 

**適用于**：套件發行 &bullet; **支援的版本**： 3.3 +

將指定的封裝新增至非 HTTP 套件來源 (資料夾或 UNC 路徑) 以階層配置的方式，也就是針對封裝識別碼和版本號碼建立資料夾。 例如：

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

針對套件來源還原或更新時，階層配置可提供明顯較佳的效能。

若要將封裝中的所有檔案展開至目的地套件來源，請使用 `-Expand` 參數。 這通常會導致目的地中出現額外的子資料夾，例如 `tools` 和 `lib` 。

## <a name="usage"></a>使用方式

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中 `<packagePath>` 是要加入之封裝的路徑名稱，並 `<sourcePath>` 指定將加入封裝的資料夾型封裝來源。 不支援 HTTP 來源。

## <a name="options"></a>選項。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Expand`**

  將封裝中的所有檔案新增至套件來源。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。
使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-src|-Source`**

   指定要將 nupkg 新增至其中的 [封裝來源]，也就是資料夾或 UNC 共用。 不支援 Http 來源。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
