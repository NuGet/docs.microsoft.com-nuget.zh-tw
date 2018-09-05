---
title: NuGet CLI 來源命令
description: Nuget.exe 的參考來源的命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548104"
---
# <a name="sources-command-nuget-cli"></a>sources 命令 (NuGet CLI)

**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有

管理在使用者範圍的組態檔，或是指定的組態檔中的來源清單。 使用者範圍的組態檔是位於`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。

請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>使用量

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>`是其中一個*清單中，新增、 移除、 啟用、 停用，* 或*更新*，`<name>`是原始碼的名稱和`<source>`是來源的 URL。

## <a name="options"></a>選項

| 選項 | 描述 |
| --- | --- |
| ConfigFile | 若要套用 NuGet 組態檔。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。 |
| 格式 | 適用於`list`動作，而且不可`Detailed`（預設值） 或`Short`。 |
| 說明 | 顯示說明命令的資訊。 |
| NonInteractive | 隱藏提示使用者輸入或確認。 |
| 密碼 | 指定與來源進行驗證的密碼。 |
| StorePasswordInClearText | 表示將密碼儲存在未加密的文字，而不是儲存以加密的格式的預設行為。 |
| 使用者名稱 | 指定與來源進行驗證的使用者名稱。 |
| 詳細資訊 | 指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。 |

> [!Note]
> 請務必新增來源的密碼，在相同的使用者內容下，nuget.exe 稍後會用來存取封裝來源。 密碼將會儲存在組態檔中加密，且僅能解密在相同的使用者內容中，已經過加密。 例如當您使用組建伺服器具有相同的 Windows 使用者在其下執行組建伺服器工作會還原 NuGet 套件必須加密的密碼。

另請參閱[環境變數](cli-ref-environment-variables.md)

## <a name="examples"></a>範例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
