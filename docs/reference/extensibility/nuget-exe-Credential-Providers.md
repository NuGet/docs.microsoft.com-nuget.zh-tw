---
title: nuget.exe 認證提供者
description: nuget.exe 認證提供者會使用摘要進行驗證，並實作為遵循特定慣例的命令列可執行檔。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230781"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>使用 nuget.exe 認證提供者驗證摘要

已針對 `nuget.exe` 特定的認證提供者加入版本 `3.3` 支援。 之後，在版本中 `4.8` 支援在所有命令列案例（`nuget.exe`、`dotnet.exe`、`msbuild.exe`）上工作的[認證提供者](NuGet-Cross-Platform-Authentication-Plugin.md)。

如需有關 `nuget.exe` 的所有驗證方法的詳細資訊，請參閱[使用來自已驗證](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)摘要的套件

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe 認證提供者探索

nuget.exe 認證提供者可透過三種方式來使用：

- **全域**：若要讓 `nuget.exe` 的所有實例都能使用認證提供者，請在目前使用者的設定檔下，將其新增至 `%LocalAppData%\NuGet\CredentialProviders`。 您可能需要建立 `CredentialProviders` 資料夾。 認證提供者可以安裝在 `CredentialProviders` 資料夾的根目錄或子資料夾內。 如果認證提供者有多個檔案/元件，您可以使用子資料夾來保留提供者的組織。

- **從環境變數**：認證提供者可以儲存在任何位置，並可透過將 `%NUGET_CREDENTIALPROVIDERS_PATH%` 環境變數設定為提供者位置，以供 `nuget.exe` 存取。 如果您有多個位置，此變數可以是以分號分隔的清單（例如，`path1;path2`）。

- 與**Nuget.exe 並存**： nuget.exe 認證提供者可以放在與 `nuget.exe`相同的資料夾中。

載入認證提供者時，`nuget.exe` 會依序在上述位置搜尋任何名為 `credentialprovider*.exe`的檔案，然後依照找到的順序載入這些檔案。 如果同一個資料夾中有多個認證提供者，就會依字母順序載入。

## <a name="creating-a-nugetexe-credential-provider"></a>建立 nuget.exe 認證提供者

認證提供者是一種命令列可執行檔，以 `CredentialProvider*.exe`的形式命名，以收集輸入、取得適當的認證，然後傳回適當的結束狀態碼和標準輸出。

提供者必須執行下列動作：

- 判斷它是否可以在起始認證之前，提供目標 URI 的認證。 如果不是，它應該會傳回狀態碼1，而不會有任何認證。
- 不修改 `Nuget.Config` （例如在該處設定認證）。
- 自行處理 HTTP proxy 設定，因為 NuGet 不會提供 proxy 資訊給外掛程式。
- 使用 UTF-8 編碼將 JSON 回應物件（如下所示）寫入至 stdout，以將認證或錯誤詳細資料傳回 `nuget.exe`。
- 選擇性地對 stderr 發出額外的追蹤記錄。 不應該將任何秘密寫入 stderr，因為在詳細資訊層級「正常」或「詳細」的情況下，NuGet 會將這類追蹤回應到主控台。
- 應該忽略未預期的參數，以提供與未來 NuGet 版本的向前相容性。

### <a name="input-parameters"></a>輸入參數

| 參數/切換 |描述|
|----------------|-----------|
| Uri {value} | 需要認證的套件來源 URI。|
| NonInteractive | 提供者不會發出互動式提示（如果有的話）。 |
| IsRetry | 如果存在，表示此嘗試是先前嘗試失敗的重試。 提供者通常會使用此旗標來確保其略過任何現有的快取，並在可能的情況下提示您輸入新的認證|
| 詳細資訊 {值} | 如果有，則會出現下列其中一個值：「normal」、「quiet」或「詳細」。 如果未提供任何值，則預設為「正常」。 提供者應該使用此來表示要發出至標準錯誤資料流程的選擇性記錄層級。 |

### <a name="exit-codes"></a>結束代碼

| 程式碼 |結果 | 描述 |
|----------------|-----------|-----------|
| 0 | Success | 已成功取得認證，並已將其寫入至 stdout。|
| 1 | ProviderNotApplicable | 目前的提供者未提供指定 URI 的認證。|
| 2 | 失敗 | 提供者是指定 URI 的正確提供者，但無法提供認證。 在此情況下，nuget.exe 將不會重試驗證，而且將會失敗。 一般的範例是當使用者取消互動式登入時。 |

### <a name="standard-output"></a>標準輸出

| 屬性 |注意|
|----------------|-----------|
| 使用者名稱 | 已驗證要求的使用者名稱。|
| 密碼 | 已驗證要求的密碼。|
| 訊息 | 關於回應的選擇性詳細資料，僅用於顯示失敗案例中的其他詳細資料。 |

範例 stdout：

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>針對認證提供者進行疑難排解

目前，NuGet 並不提供對自訂認證提供者的多個直接支援，[問題 4598](https://github.com/NuGet/Home/issues/4598)正在追蹤此工作。

您也可以進行下列動作：

- 使用 `-verbosity` 參數執行 nuget.exe，以檢查詳細輸出。
- 將 [調試訊息] 加入至適當位置中的 `stdout`。
- 請確定您使用的是 nuget.exe 3.3 或更高版本。
- 在啟動時使用此程式碼片段附加偵錯工具：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
