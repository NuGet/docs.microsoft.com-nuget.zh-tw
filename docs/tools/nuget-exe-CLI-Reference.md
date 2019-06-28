---
title: NuGet 命令列介面 (CLI) 參考
description: Nuget.exe CLI 命令列參考索引
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426015"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 參考

NuGet 命令列介面 (CLI)、 `nuget.exe`，提供 NuGet 功能，以安裝、 建立、 發行和管理套件不會對專案檔進行任何變更的完整範圍。

若要使用的任何命令，開啟 命令 視窗或 bash 殼層，然後執行`nuget`後面的命令和適當的選項，例如`nuget help pack`（若要檢視 pack 命令上的 說明）。

這份文件會反映最新版的 NuGet CLI。 如您使用任何特定版本的確切詳細資料，執行`nuget help`所需的命令。

若要了解如何使用基本命令搭配`nuget.exe`CLI，請參閱 <<c2> [ 安裝及使用套件使用 nuget.exe CLI](../consume-packages/install-use-packages-nuget-cli.md)。

## <a name="installing-nugetexe"></a>安裝的 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要在 Visual Studio 套件管理員主控台內取得 NuGet CLI，請參閱[使用 nuget.exe CLI，在主控台中](package-manager-console.md#using-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

請參閱[功能可用性](../install-nuget-client-tools.md#feature-availability)的確切詳細資料。

- 在 Windows 上，所有命令都都可用。
- 所有命令都使用 nuget.exe 在 Mono 上執行以外，指出`pack`， `restore`，和`update`。
- `pack`， `restore`， `delete`， `locals`，和`push`也會提供在 Mac 和 Linux 上透過 dotnet CLI 命令。

## <a name="commands-and-applicability"></a>命令和適用性

可用的命令和建立套件、 套件耗用量，及/或發佈套件到主機的適用性：

| 常用命令 | 適用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 建立 | 2.7+ | 建立 NuGet 套件從`.nuspec`或專案檔。 Mono 上執行時，不支援從專案檔中建立封裝。 |
| [push](cli-ref-push.md) | 發佈 | All | 將封裝發佈到套件來源。 |
| [config](cli-ref-config.md) | All | All | 取得或設定 NuGet 組態值。 |
| [help or ?](cli-ref-help.md) | All | All | 顯示說明資訊或命令的說明。 |
| [locals](cli-ref-locals.md) | 使用 | 3.3+ | 列出位置*全域套件*， *http 快取*，並*temp*資料夾並清除這些資料夾的內容。 |
| [restore](cli-ref-restore.md) | 使用 | 2.7+ | 還原使用中的套件管理格式所參考的所有套件。 Mono 上執行時，不支援還原使用 PackageReference 格式的封裝。 |
| [setapikey](cli-ref-setapikey.md) | 發行，耗用量 | All | 指定的套件來源的 API 金鑰時儲存該封裝來源的存取需要的索引鍵。 |
| [spec](cli-ref-spec.md) | 建立 | All | 會產生`.nuspec`檔案、 使用權杖，如果從 Visual Studio 專案中產生檔案。 |

| 第二個命令 | 適用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 發佈 | 3.3+ | 將封裝加入至非 HTTP 套件來源使用階層式版面配置。 對於 HTTP 來源，使用*推播*。 |
| [delete](cli-ref-delete.md) | 發佈 | All | 移除或取消列出套件從套件來源。 |
| [init](cli-ref-init.md) | 建立 | 3.3+ | 將套件從資料夾新增至套件來源使用階層式版面配置。 |
| [install](cli-ref-install.md) | 使用 | All | 到目前的封裝的安裝專案，但不修改的專案或參考檔案。 |
| [list](cli-ref-list.md) | 耗用量，或許發行 | All | 顯示從指定來源的封裝。 |
| [mirror](cli-ref-mirror.md) | 發佈 | 中已被取代 3.2 + | 鏡像處理封裝和從來源到目標存放庫及其相依性。 |
| [sources](cli-ref-sources.md) | 耗用量發行 | All | 管理組態檔中的套件來源。 |
| [update](cli-ref-update.md) | 使用 | All | 專案的套件會更新為最新可用版本。 在 Mono 上執行時，不支援。 |

不同的命令讓使用的各種[環境變數](cli-ref-environment-variables.md)。

適用於角色的 NuGet CLI 命令：

| 角色 | 命令 |
| --- | --- |
| 使用 | +`config`、`help`、`install`、`list`、`locals`、`restore`、`setapikey`、`sources`、`update` |
| 建立 | `config`, `help`, `init`, `pack`, `spec` |
| 發佈 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

開發人員只關心使用套件，例如，只需要了解該子集 NuGet 命令。

> [!Note]
> 命令選項名稱不區分大小寫。 已被取代的選項不包含在此參考中，這類`NoPrompt`(取代`NonInteractive`) 和`Verbose`(取代`Verbosity`)。
