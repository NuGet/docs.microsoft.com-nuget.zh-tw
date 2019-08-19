---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860564"
---
使用 [restore](../../reference/cli-reference/cli-ref-restore.md) 命令，它會下載並安裝 *packages* 資料夾遺漏的任何套件。

針對移轉至 PackageReference 的專案，請改為使用 [msbuild -t:restore](../package-restore.md#restore-using-msbuild) 來還原套件。

`restore` 只會將套件新增至磁碟，但不會變更專案的相依性。 若要還原專案相依性，請修改 `packages.config`，然後使用 `restore` 命令。

如同其他 `nuget.exe` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。

使用 `restore` 還原套件：

```cli
nuget restore MySolution.sln
```