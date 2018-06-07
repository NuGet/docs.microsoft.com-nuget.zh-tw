---
title: NuGet 命令列介面 (CLI) 參考
description: Nuget.exe CLI 的命令列參考索引
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 477883ce1579ba3e4b586dff2cf01e31e7afdb3f
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817872"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 參考

NuGet 命令列介面 (CLI) ( `nuget.exe`，提供 NuGet 功能來安裝、 建立、 發行和管理封裝，而不需要進行任何變更的專案檔案的完整範圍。

若要使用的任何命令，開啟命令視窗或撞殼層，然後執行`nuget`後面的命令和適當的選項，例如`nuget help pack`（若要檢視組件命令上的 [說明]）。

這份文件會反映最新版本的 NuGet CLI。 對於任何指定的版本，您所使用的確切詳細資料，執行`nuget help`所需的命令。

## <a name="installing-nugetexe"></a>安裝 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要使用 NuGet CLI 封裝管理員主控台內，在 Visual Studio 中，請參閱[使用主控台中的 nuget.exe CLI](package-manager-console.md#using-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

請參閱[功能可用性](../install-nuget-client-tools.md#feature-availability)的確切詳細資料。

- 在 Windows 上的所有命令都都可用。
- 所有命令都使用 nuget.exe 除了所指定的執行上 Mono `pack`， `restore`，和`update`。
- `pack`， `restore`， `delete`， `locals`，和`push`也會提供在 Mac 和 Linux 上透過 dotnet CLI 命令。

## <a name="commands-and-applicability"></a>命令和適用性

可用的命令，來建立封裝、 封裝耗用量，及/或發行套件至主機的適用性：

| 常見命令 | 適用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 建立 | 2.7+ | 建立來源的 NuGet 封裝`.nuspec`或專案檔。 單聲道上執行時，不支援從專案檔中建立封裝。 |
| [push](cli-ref-push.md) | 發佈 | 全部 | 將封裝發佈到套件來源。 |
| [config](cli-ref-config.md) | 全部 | 全部 | 取得或設定 NuGet 組態值。 |
| [help or ?](cli-ref-help.md) | 全部 | 全部 | 顯示說明資訊或命令的說明。 |
| [locals](cli-ref-locals.md) | 使用 | 3.3+ | 列出位置*全域封裝*， *http 快取*，和*temp*資料夾並清除這些資料夾的內容。 |
| [restore](cli-ref-restore.md) | 使用 | 2.7+ | 還原使用中的封裝管理格式所參考的所有封裝。 單聲道上執行時，不支援還原使用 PackageReference 格式的封裝。 |
| [setapikey](cli-ref-setapikey.md) | 發佈、 耗用量 | 全部 | 儲存該封裝來源需要索引鍵存取的 API 金鑰指定的套件來源。 |
| [spec](cli-ref-spec.md) | 建立 | 全部 | 會產生`.nuspec`檔案，如果從 Visual Studio 專案中產生檔案，請使用語彙基元。 |

| 第二個命令 | 適用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 發佈 | 3.3+ | 將封裝加入至使用階層式配置的非 HTTP 封裝來源。 HTTP 的來源，請使用*發送*。 |
| [delete](cli-ref-delete.md) | 發佈 | 全部 | 移除或 unlists 從套件來源的封裝。 |
| [init](cli-ref-init.md) | 建立 | 3.3+ | 從資料夾將使用階層式配置的封裝來源封裝。 |
| [install](cli-ref-install.md) | 使用 | 全部 | 到目前的封裝會安裝專案，但不修改的專案或參考檔案。 |
| [list](cli-ref-list.md) | 耗用量，可能發佈 | 全部 | 顯示從指定的來源封裝。 |
| [mirror](cli-ref-mirror.md) | 發佈 | 3.2 + 中已被取代 | 反映封裝及其相依性從來源到目標儲存機制。 |
| [sources](cli-ref-sources.md) | 耗用量發行 | 全部 | 管理組態檔中的封裝來源。 |
| [update](cli-ref-update.md) | 使用 | 全部 | 更新專案的封裝，以最新可用版本。 單聲道上執行時，不支援。 |

不同的命令，請使用各種[環境變數](cli-ref-environment-variables.md)。

NuGet CLI 命令所適用的角色：

| 角色 | 命令 |
| --- | --- |
| 使用 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 建立 | `config`, `help`, `init`, `pack`, `spec` |
| 發佈 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

開發人員只與使用封裝，例如，只需要了解該子集的 NuGet 命令。

> [!Note]
> 命令選項名稱不區分大小寫。 已被取代的選項中不包含此參考，例如`NoPrompt`(取代`NonInteractive`) 和`Verbose`(取代`Verbosity`)。
