---
title: " (CLI) 參考的 NuGet 命令列介面"
description: nuget.exe CLI 的命令列參考索引
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: e9343f1fdddcf839322849925372587e685aef4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623145"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 參考

 (CLI) 的 NuGet 命令列介面 `nuget.exe` 可提供 nuget 功能的完整範圍，以安裝、建立、發行和管理套件，而不需要對專案檔進行任何變更。

若要使用任何命令，請開啟命令視窗或 bash shell，然後執行 `nuget` 命令和適當的選項，例如 `nuget help pack` (來查看 pack 命令) 的說明。

本檔反映最新版本的 NuGet CLI。 如需您所使用之任何指定版本的確切詳細資料，請執行所 `nuget help` 需的命令。

若要了解如何使用 `nuget.exe` CLI 的基本命令，請參閱[使用 nuget.exe CLI 安裝和使用套件](../consume-packages/install-use-packages-nuget-cli.md)。

## <a name="installing-nugetexe"></a>安裝 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要在 Visual Studio 的封裝管理員主控台內提供 NuGet CLI，請參閱在 [主控台中使用 nuget.exe CLI](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

如需確切詳細資料，請參閱 [功能可用性](../install-nuget-client-tools.md#feature-availability) 。

- 所有命令都可在 Windows 上使用。
- 所有命令都適用于 Mono 上執行的 nuget.exe，除了針對、和所指定的位置 `pack` `restore` `update` 。
- 您 `pack` `restore` `delete` `locals` `push` 也可以透過 dotnet CLI，在 Mac 和 Linux 上使用、、、和命令。

## <a name="commands-and-applicability"></a>命令和適用性

可用的命令和適用于封裝建立、套件耗用量，以及/或將套件發行至主機的適用性：

| 常見命令 | 適用角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | 建立 | 2.7+ | 從或專案檔建立 NuGet 套件 `.nuspec` 。 在 Mono 上執行時，不支援從專案檔建立套件。 |
| [push](cli-reference/cli-ref-push.md) | 發佈 | 全部 | 將封裝發佈至套件來源。 |
| [config](cli-reference/cli-ref-config.md) | 全部 | 全部 | 取得或設定 NuGet 設定值。 |
| [help or ?](cli-reference/cli-ref-help.md) | 全部 | 全部 | 顯示命令的說明資訊或說明。 |
| [locals](cli-reference/cli-ref-locals.md) | 耗用量 | 3.3 + | 列出 *全域套件*、 *HTTP*快取和 *暫存* 資料夾的位置，並清除這些資料夾的內容。 |
| [restore](cli-reference/cli-ref-restore.md) | 耗用量 | 2.7+ | 還原使用中封裝管理格式所參考的所有套件。 在 Mono 上執行時，不支援使用 PackageReference 格式來還原封裝。 |
| [setapikey](cli-reference/cli-ref-setapikey.md) | 發佈、耗用量 | 全部 | 當套件來源需要存取金鑰時，為指定的套件來源儲存 API 金鑰。 |
| [spec](cli-reference/cli-ref-spec.md) | 建立 | 全部 | `.nuspec`如果從 Visual Studio 專案產生檔案，則會使用標記產生檔案。 |

| 次要命令 | 適用角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | 發佈 | 3.3 + | 使用階層式配置將封裝新增至非 HTTP 套件來源。 若為 HTTP 來源，請使用 *push*。 |
| [delete](cli-reference/cli-ref-delete.md) | 發佈 | 全部 | 從套件來源移除或取消列出封裝。 |
| [init](cli-reference/cli-ref-init.md) | 建立 | 3.3 + | 使用階層式配置將封裝從資料夾新增至套件來源。 |
| [install](cli-reference/cli-ref-install.md) | 耗用量 | 全部 | 將封裝安裝至目前的專案，但不會修改專案或參考檔案。 |
| list | 耗用量，或許是發佈 | 全部 | 顯示指定來源的封裝。 |
| [mirror](cli-reference/cli-ref-mirror.md) | 發佈 | 3.2 + 中已淘汰 | 將封裝及其相依性從來源鏡像至目標存放庫。 |
| [search](cli-reference/cli-ref-search.md) | 耗用量 | 5.8 + | 使用提供的查詢字串來搜尋指定的來源。 |
| [sources](cli-reference/cli-ref-sources.md) | 耗用量、發佈 | 全部 | 管理設定檔中的套件來源。 |
| [update](cli-reference/cli-ref-update.md) | 耗用量 | 全部 | 將專案的封裝更新為最新的可用版本。 在 Mono 上執行時不支援。 |

不同的命令會利用不同的 [環境變數](cli-reference/cli-ref-environment-variables.md)。

適用角色的 NuGet CLI 命令：

| 角色 | 命令 |
| --- | --- |
| 耗用量 | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| 建立 | `config`, `help`, `init`, `pack`, `spec` |
| 發佈 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

例如，只在意取用套件的開發人員只需要瞭解 NuGet 命令的子集。

> [!Note]
> 命令選項名稱不區分大小寫。 已淘汰的選項不會包含在此參考中，例如 `NoPrompt` (由) 取代， `NonInteractive` 而且 `Verbose` (由 `Verbosity`) 取代。
