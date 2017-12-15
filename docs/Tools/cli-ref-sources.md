---
title: "NuGet CLI 來源命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Nuget.exe 的參考資料來源的命令"
keywords: "nuget 的來源參考、 來源命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a>來源命令 (NuGet CLI)

**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有

管理清單的來源位於`%AppData%\NuGet\NuGet.Config`或指定的組態檔。

## <a name="usage"></a>使用方式

```
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>`是其中一個*清單、 加入、 移除、 啟用、 停用，*或*更新*，`<name>`是來源的名稱和`<source>`是來源的 URL。


## <a name="options"></a>選項

| 選項 | 說明 |
| --- | --- |
| ConfigFile | *（2.5 +)* NuGet 組態檔來套用。 如果未指定， *%AppData%\NuGet\NuGet.Config*用。 |
| ForceEnglishOutput | *（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。 |
| 格式 | 適用於`list`動作，而且可以是`Detailed`（預設值） 或`Short`。 |
| 說明 | 顯示說明命令的資訊。 |
| 非互動式 | 抑制使用者輸入或確認提示。 |
| 密碼 | 指定與來源進行驗證的密碼。 |
| StorePasswordInClearText | 表示將密碼儲存在未加密的文字，而不是將以加密的格式儲存的預設行為。 |
| 使用者名稱 | 指定的使用者名稱與來源進行驗證。 |
| 詳細資訊 | 指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。 |

> [!Note]
> 請務必新增來源的密碼，在相同的使用者內容下，當 nuget.exe 稍後用來存取封裝來源。 密碼將會儲存在組態檔中加密，且僅能解密在相同的使用者內容中因為它已加密。 例如當您使用組建伺服器還原具有相同的組建伺服器 」 工作來執行的 Windows 使用者的密碼必須加密的 NuGet 封裝。

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
