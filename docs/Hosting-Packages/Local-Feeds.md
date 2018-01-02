---
title: "設定本機 NuGet 摘要 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "如何使用區域網路上的資料夾建立 NuGet 套件的本機摘要"
keywords: "NuGet 摘要, NuGet 資源庫, 本機套件摘要"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a>本機摘要

本機的 NuGet 套件摘要只是您區域網路 (或只是您自己的電腦) 上放置套件的階層式資料夾結構。 然後，這些摘要會和所有其他使用 CLI、套件管理員 UI 和套件管理員主控台的 NuGet 作業一起，作為套件來源。

若要啟用來源，請使用[套件管理員 UI](../tools/package-manager-ui.md#package-sources) 或 [`nuget sources`](../tools/cli-ref-sources.md) 命令，將其路徑名稱 (例如 `\\myserver\packages`) 新增至來源清單。

> [!Note]
> NuGet 3.3+ 支援階層式資料夾結構。 舊版的 NuGet 只使用包含套件的單一資料夾，此類資料夾的效能遠低於階層式結構。

## <a name="initializing-and-maintaining-hierarchical-folders"></a>初始化和維護階層式資料夾

階層式版本的資料夾樹狀目錄有下列的一般結構：

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

當您使用 [`nuget add`](../tools/cli-ref-add.md) 命令將套件複製到摘要時，NuGet 會自動建立此結構：

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` 命令一次使用一個套件，這在設定有多個套件的摘要時會很不方便。

在這種情況下，使用 [`nuget init`](../tools/cli-ref-init.md) 命令將資料夾中所有套件複製到摘要，如同分別對每個套件執行 `nuget add`。 例如，下列命令會將所有的套件從 `c:\packages` 複製到 `\\myserver\packages` 的階層式樹狀結構：

```
nuget init c:\packages \\myserver\packages
```

與 `add` 命令一樣，`init` 會為每個套件識別碼建立一個資料夾，各自包含一個版本號碼資料夾，裡面是合適的套件。
