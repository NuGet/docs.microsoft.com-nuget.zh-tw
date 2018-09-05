---
title: NuGet CLI 推送命令
description: Nuget.exe 推送命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548339"
---
# <a name="push-command-nuget-cli"></a>推送命令 (NuGet CLI)

**適用於：** 封裝發行&bullet;**支援的版本：** 所有; 所需的 nuget.org 4.1.0 +

> [!Important]
> 若要將套件推送至 nuget.org，您必須使用 nuget.exe 4.1.0 版 + 中，它會實作所需[NuGet 通訊協定](../api/nuget-protocols.md)。

將套件推送至套件來源，並將其發佈。

NuGet 的預設組態的取得方式載入`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然後載入任何`Nuget.Config`或是`.nuget\Nuget.Config`檔案從磁碟機的根目錄開始和結束目前的目錄中 (請參閱[設定NuGet 行為](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用量

```cli
nuget push <packagePath> [options]
```

其中`<packagePath>`識別要推送至伺服器的封裝。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ApiKey | 目標存放庫的 API 金鑰。 如果不存在，則會使用組態檔中所指定。 |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| DisableBuffering | 停用緩衝處理時將推送至 http （s） 伺服器，以減少記憶體使用方式。 注意： 使用此選項時，整合式的 Windows 驗證可能無法運作。 |
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| NoSymbols | *（3.5 +)* 有符號套件時，它將不會推送至符號伺服器。 |
| 原始程式檔 | 指定伺服器 URL。 NuGet 會識別的 UNC 或本機資料夾的來源，並只會複製檔案而非發送它使用 HTTP。  此外，從開始 NuGet 3.4.2，這是必要參數除非`NuGet.Config`檔案會指定*DefaultPushSource*值 (請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md))。 |
| SymbolSource | *（3.5 +)* 指定符號伺服器 URL，當 nuget.smbsrc.net 推送至 nuget.org 時，會使用 |
| SymbolApiKey | *（3.5 +)* 指定 URL 中指定的 API 金鑰`-SymbolSource`。 |
| 等候逾時 | 指定的逾時 （秒），推送至伺服器。 預設值為 300 秒 （5 分鐘）。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
