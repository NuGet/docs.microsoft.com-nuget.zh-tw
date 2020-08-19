---
title: NuGet CLI 規格命令
description: nuget.exe 規格命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622560"
---
# <a name="spec-command-nuget-cli"></a> (NuGet CLI 的 spec 命令) 

**適用物件：** 套件建立 &bullet; **支援的版本：** 全部

產生 `.nuspec` 新封裝的檔案。 如果在與專案檔相同的資料夾中執行 (`.csproj` ， `.vbproj`) 會建立 token 化檔案 `.fsproj` `spec` `.nuspec` 。 如需詳細資訊，請參閱 [建立封裝](../../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用方式

```cli
nuget spec [<packageID>] [options]
```

其中 `<packageID>` 是要儲存在檔案中的選擇性封裝識別碼 `.nuspec` 。

## <a name="options"></a>選項。

- **`-AssemblyPath`**

  指定要用於中繼資料之元件的路徑。

- **`-Force`**

  覆寫任何現有 `.nuspec` 的檔案。


- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。

另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
