---
title: NuGet CLI push 命令
description: Nuget.exe push 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327625"
---
# <a name="push-command-nuget-cli"></a>push 命令 (NuGet CLI)

**適用于:** 套件發佈&bullet; **支援的版本:** 全部; 4.1.0 + nuget.org 的必要項

> [!Important]
> 若要將套件推送至 nuget.org, 您必須使用 nuget.exe v 4.1.0 +, 其會執行所需的[nuget 通訊協定](../../api/nuget-protocols.md)。

將套件推送至套件來源併發布。

NuGet 的預設設定是藉由載入`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 來取得, 然後`Nuget.Config`從`.nuget\Nuget.Config`磁片磁碟機根目錄開始載入任何或檔案, 並在目前的目錄中結束 (請參閱[通用 NuGet)](../../consume-packages/configuring-nuget-behavior.md)設定)

## <a name="usage"></a>使用量

```cli
nuget push <packagePath> [options]
```

其中`<packagePath>`識別要推送至伺服器的封裝。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在, 則會使用設定檔中指定的檔案。 |
| ConfigFile | 要套用的 NuGet 設定檔。 如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。|
| DisableBuffering | 推送至 HTTP (s) 伺服器時停用緩衝處理以減少記憶體使用量。 注意: 使用此選項時, 整合式 Windows 驗證可能無法正常執行。 |
| ForceEnglishOutput | *(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。 |
| Help | 顯示命令的說明資訊。 |
| NonInteractive | 抑制使用者輸入或確認的提示。 |
| NoSymbols | *(3.5 +)* 如果符號封裝存在, 則不會將它推送至符號伺服器。 |
| Source | 指定伺服器 URL。 NuGet 會識別 UNC 或本機資料夾來源, 並直接在該處複製檔案, 而不是使用 HTTP 推送該檔案。  此外, 從 NuGet 3.4.2 開始, 除非檔案指定*DefaultPushSource*值, 否則`NuGet.Config`這是必要參數 (請參閱設定[NuGet 行為](../../consume-packages/configuring-nuget-behavior.md))。 |
| SkipDuplicate | *(5.1 +)* 如果套件和版本已存在, 請略過它, 並繼續推送中的下一個套件 (如果有的話)。 |
| SymbolSource | *(3.5 +)* 指定符號伺服器 URL;推送至 nuget.org 時, 會使用 nuget.smbsrc.net |
| SymbolApiKey | *(3.5 +)* 針對中`-SymbolSource`指定的 URL 指定 API 金鑰。 |
| 逾時 | 指定推送至伺服器的超時時間 (以秒為單位)。 預設值為300秒 (5 分鐘)。 |
| Verbosity | 指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

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
