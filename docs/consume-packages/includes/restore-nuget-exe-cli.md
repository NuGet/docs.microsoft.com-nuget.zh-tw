---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860564"
---
<span data-ttu-id="7e980-101">使用 [restore](../../reference/cli-reference/cli-ref-restore.md) 命令，它會下載並安裝 *packages* 資料夾遺漏的任何套件。</span><span class="sxs-lookup"><span data-stu-id="7e980-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="7e980-102">針對移轉至 PackageReference 的專案，請改為使用 [msbuild -t:restore](../package-restore.md#restore-using-msbuild) 來還原套件。</span><span class="sxs-lookup"><span data-stu-id="7e980-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="7e980-103">`restore` 只會將套件新增至磁碟，但不會變更專案的相依性。</span><span class="sxs-lookup"><span data-stu-id="7e980-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="7e980-104">若要還原專案相依性，請修改 `packages.config`，然後使用 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="7e980-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="7e980-105">如同其他 `nuget.exe` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="7e980-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="7e980-106">使用 `restore` 還原套件：</span><span class="sxs-lookup"><span data-stu-id="7e980-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```