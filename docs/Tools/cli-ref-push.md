---
title: "NuGet CLI 發送命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Nuget.exe 推送命令參考"
keywords: "nuget 推入參考，推入命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>推播命令 (NuGet CLI)

**適用於：**封裝發行&bullet;**支援的版本：**所有; 所需的 nuget.org 4.1.0+

> [!Important]
> 若要推入至 nuget.org 的封裝，您必須使用 nuget.exe v4.1.0 +，它會實作所需[NuGet 通訊協定](../api/nuget-protocols.md)。

將封裝的封裝來源以推入，並將其發佈。

NuGet 的預設組態透過載入`%AppData%\NuGet\NuGet.Config`，然後載入任何`Nuget.Config`或`.nuget\Nuget.Config`檔案從磁碟機的根目錄開始和結束目前的目錄中 (請參閱[設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用方式

```
nuget push <packagePath> [options]
```

其中`<packagePath>`識別要推入至伺服器的封裝。

## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| apiKey | 目標存放庫 API 金鑰。 如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。 |
| ConfigFile | *（2.5 +)* NuGet 組態檔來套用。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| DisableBuffering | 停用緩衝以減少記憶體使用方式的推入至 http （s） 伺服器時。 注意： 使用此選項時，整合式的 Windows 驗證可能無法運作。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| NoSymbols | *（3.5 +)*如果符號封裝存在，它將不會發送至符號伺服器。 |
| 來源 | 指定伺服器 URL。 隨 NuGet 2.5 +，NuGet 會識別資料的 UNC 或本機資料夾的來源，並直接複製檔案而不是將它使用 HTTP 推送。  此外，從 NuGet 3.4.2 開始，這是必要參數除非`NuGet.Config`檔案會指定*DefaultPushSource*值 (請參閱[設定 NuGet 行為](../Consume-Packages/Configuring-NuGet-Behavior.md))。 |
| SymbolSource | *（3.5 +)*指定符號伺服器 URL，當 nuget.smbsrc.net 推入至 nuget.org 時，會使用 |
| SymbolApiKey | *（3.5 +)*指定 URL 中指定的 API 金鑰`-SymbolSource`。 |
| 等候逾時 | 指定在逾時，以秒為單位，可用於推入到伺服器。 預設值是 300 秒 （5 分鐘）。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。 |

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
