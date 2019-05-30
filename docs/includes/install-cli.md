---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271505"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 及更新版本需要.NET Framework 4.7.2 或更新版本才能執行。

1. 請瀏覽 [nuget.org/downloads](https://nuget.org/downloads) 並選取 NuGet 3.3 或更高版本 (2.8.6 與 Mono 不相容)。 一律建議使用最新版本，需要 4.1.0 以上版本才能將套件發行至 nuget.org。
1. 每個下載項目直接是 `nuget.exe` 檔案。 指示您的瀏覽器將檔案儲存到您選擇的資料夾。 該檔案*不是*安裝程式；如果直接從瀏覽器執行，您將不會看到任何項目。
1. 將放置 `nuget.exe` 的資料夾新增至您的 PATH 環境變數中，以便從任何地方使用 CLI 工具。

#### <a name="macoslinux"></a>macOS/Linux

行為可能會隨作業系統發佈而稍微不同。

1. 安裝 [Mono 4.4.2 或更新版本](http://www.mono-project.com/docs/getting-started/install/)。

1. 在殼層提示字元中執行下列命令：

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. 將下列指令碼加入到適用於您的作業系統的檔案 (通常為 `~/.bash_aliases` 或 `~/.bash_profile`) 來建立別名：

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. 重新載入殼層。  輸入 `nuget` (不含任何參數) 來測試安裝。 NuGet CLI 說明應該會顯示。
