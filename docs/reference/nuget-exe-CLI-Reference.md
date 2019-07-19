---
title: NuGet 命令列介面 (CLI) 參考
description: Nuget.exe CLI 的命令列參考索引
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327465"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 參考

Nuget 命令列介面 (CLI) `nuget.exe`提供 nuget 功能的完整範圍, 可安裝、建立、發行和管理套件, 而不需要對專案檔進行任何變更。

若要使用任何命令, 請開啟命令視窗或 bash shell, 然後`nuget`依序執行命令和適當的選項, `nuget help pack`例如 (以在 pack 命令上查看說明)。

本檔反映最新版本的 NuGet CLI。 如需您所使用之任何指定版本的確切詳細資料`nuget help` , 請針對所要的命令執行。

若要了解如何使用 `nuget.exe` CLI 的基本命令，請參閱[使用 nuget.exe CLI 安裝和使用套件](../consume-packages/install-use-packages-nuget-cli.md)。

## <a name="installing-nugetexe"></a>安裝 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要在 Visual Studio 的 [套件管理員主控台] 中提供 NuGet CLI, 請參閱[在主控台中使用 NUGET.EXE cli](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

如需確切詳細資料, 請參閱[功能可用性](../install-nuget-client-tools.md#feature-availability)。

- Windows 上的所有命令都可供使用。
- 所有命令會使用在 Mono 上執行的 nuget.exe, 但指定給`pack`、 `restore`和`update`的除外。
- `locals` `restore` `delete`您也可以透過 dotnet CLI `push` , 在 Mac 和 Linux 上取得、、、和命令。 `pack`

## <a name="commands-and-applicability"></a>命令和適用性

可用的命令和適用于封裝建立、套件耗用量, 以及/或將封裝發佈至主機的適用性:

| 一般命令 | 適用的角色 | NuGet 版本 | 說明 |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | 建立 | 2.7+ | 從`.nuspec`或專案檔建立 NuGet 套件。 在 Mono 上執行時, 不支援從專案檔建立封裝。 |
| [push](cli-reference/cli-ref-push.md) | 發佈 | All | 將封裝發佈至封裝來源。 |
| [config](cli-reference/cli-ref-config.md) | All | All | 取得或設定 NuGet 設定值。 |
| [help or ?](cli-reference/cli-ref-help.md) | All | All | 顯示命令的說明資訊或協助。 |
| [locals](cli-reference/cli-ref-locals.md) | 使用 | 3.3+ | 列出*全域封裝*、 *HTTP*快取和*暫存*資料夾的位置, 並清除這些資料夾的內容。 |
| [restore](cli-reference/cli-ref-restore.md) | 使用 | 2.7+ | 還原使用中的套件管理格式所參考的所有套件。 在 Mono 上執行時, 不支援使用 PackageReference 格式來還原封裝。 |
| [setapikey](cli-reference/cli-ref-setapikey.md) | 發行, 耗用量 | All | 當套件來源需要存取金鑰時, 為指定的套件來源儲存 API 金鑰。 |
| [spec](cli-reference/cli-ref-spec.md) | 建立 | All | `.nuspec`產生檔案, 並在從 Visual Studio 專案產生檔案時使用權杖。 |

| 次要命令 | 適用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | 發佈 | 3.3+ | 使用階層式配置將封裝新增至非 HTTP 封裝來源。 針對 HTTP 來源, 請使用*push*。 |
| [delete](cli-reference/cli-ref-delete.md) | 發佈 | All | 從封裝來源移除或取消列出封裝。 |
| [init](cli-reference/cli-ref-init.md) | 建立 | 3.3+ | 使用階層式配置, 將封裝從資料夾新增至套件來源。 |
| [install](cli-reference/cli-ref-install.md) | 使用 | All | 將封裝安裝到目前的專案中, 但不會修改專案或參考檔案。 |
| [list](cli-reference/cli-ref-list.md) | 耗用量, 也許發佈 | All | 顯示來自指定來源的封裝。 |
| [mirror](cli-reference/cli-ref-mirror.md) | 發佈 | 3\.2 + 中已淘汰 | 將封裝及其相依性從來源鏡像到目標存放庫。 |
| [sources](cli-reference/cli-ref-sources.md) | 耗用量, 發佈 | All | 管理設定檔案中的封裝來源。 |
| [update](cli-reference/cli-ref-update.md) | 使用 | All | 將專案的套件更新為最新的可用版本。 在 Mono 上執行時不支援。 |

不同的命令會利用各種[環境變數](cli-reference/cli-ref-environment-variables.md)。

依適用角色的 NuGet CLI 命令:

| 角色 | 命令 |
| --- | --- |
| 使用 | +`config`、`help`、`install`、`list`、`locals`、`restore`、`setapikey`、`sources`、`update` |
| 建立 | `config`, `help`, `init`, `pack`, `spec` |
| 發佈 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

例如, 只關心使用套件的開發人員, 只需要瞭解 NuGet 命令的子集。

> [!Note]
> 命令選項名稱不區分大小寫。 已被取代的選項不會包含在此參考中, `NoPrompt`例如 ( `NonInteractive`已取代) `Verbose`和 (由`Verbosity`取代)。
