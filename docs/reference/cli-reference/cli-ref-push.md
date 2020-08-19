---
title: NuGet CLI push 命令
description: nuget.exe push 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622841"
---
# <a name="push-command-nuget-cli"></a> (NuGet CLI 的推送命令) 

**適用于：** 套件發行 &bullet; **支援的版本：** 全部; 4.1.0 + 需要 nuget.org

> [!Important]
> 若要將套件推送至 nuget.org，您必須使用 nuget.exe v 4.1.0 +，它會執行所需的 [nuget 通訊協定](../../api/nuget-protocols.md)。

將套件推送至封裝來源併發布。

NuGet 的預設設定是藉由載入 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ，然後 `Nuget.Config` `.nuget\Nuget.Config` 從磁片磁碟機的根目錄開始載入任何檔案，並在目前的目錄中結束 (查看 [常見的 NuGet](../../consume-packages/configuring-nuget-behavior.md) 設定) 

## <a name="usage"></a>使用方式

```cli
nuget push <packagePath> [options]
```

，其中會 `<packagePath>` 識別要推送至伺服器的封裝。

## <a name="options"></a>選項。

- **`-ApiKey`**

  目標儲存機制的 API 金鑰。 如果不存在，則會使用設定檔中指定的。

- **`-ConfigFile`**

  要套用的 NuGet 設定檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-DisableBuffering`**

  推送至 HTTP (s) server 時，會停用緩衝處理以減少記憶體使用量。 注意：使用此選項時，整合式 Windows 驗證可能無法運作。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用不因文化特性而異的文化特性，強制執行 nuget.exe。

- **`-?|-help`**

  顯示命令的說明資訊。

- **`-NonInteractive`**

  抑制使用者輸入或確認的提示。

- **`-NoServiceEndpoint`**

  不會附加 `api/v2/packages` 至來源 URL。

- **`-NoSymbols`**

  * (3.5 +) * 如果符號封裝存在，則不會將其推送至符號伺服器。

- **`-src|-Source`**

  指定伺服器 URL。 NuGet 會識別 UNC 或本機資料夾來源，只複製檔案，而不是使用 HTTP 推送。  此外，從 NuGet 3.4.2 開始，除非檔案 `NuGet.Config` 指定 *DefaultPushSource* 值 (請參閱設定 [nuget 行為](../../consume-packages/configuring-nuget-behavior.md)) ，否則此為必要參數。

- **`-SkipDuplicate`**

  * (5.1 +) * 如果套件和版本已經存在，請略過它，然後繼續進行推送中的下一個套件（如果有的話）。

- **`-SymbolSource`**

  * (3.5 +) * 指定符號伺服器 URL;nuget.smbsrc.net 會在推送至 nuget.org 時使用

- **`-SymbolApiKey`**

  * (3.5 +) * 指定中指定之 URL 的 API 金鑰 `-SymbolSource` 。

- **`-Timeout`**

  指定推送至伺服器的超時時間（以秒為單位）。 預設值是 300 秒 (5 分鐘)。

- **`-Verbosity [normal|quiet|detailed]`**

  指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。


另請參閱 [環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
