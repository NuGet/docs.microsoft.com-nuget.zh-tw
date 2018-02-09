---
title: "如何管理 NuGet 中的套件快取 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "如何管理存在電腦上的不同 NuGet 套件快取，安裝或還原套件時會使用這些快取。"
keywords: "NuGet 套件快取, 套件快取, NuGet 快取, 管理快取, 本機 NuGet 快取, 全域 NuGet 快取, NuGet locals 命令, 清除快取"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84bc34e02572a912fb86ce1a5cf54d8ff212ac6e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="managing-the-nuget-cache"></a>管理 NuGet 快取

NuGet 會管理數個本機快取，以免下載電腦上已有的套件，並提供離線支援。 NuGet 會在安裝或重新安裝套件時自動切換回快取，而不需網路連線。

使用 [locals 命令](../tools/cli-ref-locals.md) 取得快取位置：

```cli
nuget locals all -list
```

一般輸出如下：

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

如果遇到套件安裝問題，或想要確保安裝的是遠端資源庫的套件，請使用 `locals -clear` 選項：

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

請注意，目前僅支援從 NuGet 命令列管理快取，不支援在 Visual Studio 中或透過套件管理員主控台。 此外，NuGet 3.6 和更新版本不支援管理 2.x 快取。

使用 `nuget locals` 時會發生下列錯誤：

- **本機資源清除失敗：無法刪除一或多個檔案**
- **目錄不是空的**

這些都表示您沒有刪除快取中檔案的權限，或另一個處理序正在使用快取中的一或多個檔案，檔案必須先關閉才能移除。
