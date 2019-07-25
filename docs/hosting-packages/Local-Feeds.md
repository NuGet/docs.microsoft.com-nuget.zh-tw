---
title: 設定本機 NuGet 摘要
description: 如何使用區域網路上的資料夾建立 NuGet 套件的本機摘要
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317597"
---
# <a name="local-feeds"></a>本機摘要

本機的 NuGet 套件摘要只是您區域網路 (或只是您自己的電腦) 上放置套件的階層式資料夾結構。 然後，這些摘要會和所有其他使用 CLI、套件管理員 UI 和套件管理員主控台的 NuGet 作業一起，作為套件來源。

若要啟用來源，請使用[套件管理員 UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) 或 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) 命令，將其路徑名稱 (例如 `\\myserver\packages`) 新增至來源清單。

> [!Note]
> NuGet 3.3+ 支援階層式資料夾結構。 舊版的 NuGet 只使用包含套件的單一資料夾，此類資料夾的效能遠低於階層式結構。

## <a name="initializing-and-maintaining-hierarchical-folders"></a>初始化和維護階層式資料夾

階層式版本的資料夾樹狀目錄有下列的一般結構：

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

當您使用 [`nuget add`](../reference/cli-reference/cli-ref-add.md) 命令將套件複製到摘要時，NuGet 會自動建立此結構：

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` 命令一次使用一個套件，這在設定有多個套件的摘要時會很不方便。

在這種情況下，使用 [`nuget init`](../reference/cli-reference/cli-ref-init.md) 命令將資料夾中所有套件複製到摘要，如同分別對每個套件執行 `nuget add`。 例如，下列命令會將所有的套件從 `c:\packages` 複製到 `\\myserver\packages` 的階層式樹狀結構：

```cli
nuget init c:\packages \\myserver\packages
```

與 `add` 命令一樣，`init` 會為每個套件識別碼建立一個資料夾，各自包含一個版本號碼資料夾，裡面是合適的套件。
