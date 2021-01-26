---
title: nuget.exe 認證提供者
description: nuget.exe 認證提供者會使用摘要進行驗證，而且會實作為遵循特定慣例的命令列可執行檔。
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777770"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>使用 nuget.exe 認證提供者驗證摘要

`3.3`已針對 `nuget.exe` 特定的認證提供者新增版本支援。 從那時起，在 `4.8` 支援所有命令列案例 (的 [認證提供者](NuGet-Cross-Platform-Authentication-Plugin.md) 版本中 `nuget.exe` ， `dotnet.exe` `msbuild.exe` 已加入) 。

如需所有驗證方法的詳細資訊，請參閱 [使用已驗證](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) 摘要的套件 `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe 認證提供者探索

您可以使用下列三種方式來使用 nuget.exe 認證提供者：

- **全域**：若要讓認證提供者可以 `nuget.exe` 在目前使用者的設定檔下執行的所有實例，請將它新增至 `%LocalAppData%\NuGet\CredentialProviders` 。 您可能需要建立 `CredentialProviders` 資料夾。 認證提供者可以安裝在資料夾的根目錄 `CredentialProviders`  或子資料夾內。 如果認證提供者有多個檔案/元件，您可以使用子資料夾來將提供者組織。

- **從環境變數**：認證提供者可以在任何地方儲存，並藉 `nuget.exe` 由將 `%NUGET_CREDENTIALPROVIDERS_PATH%` 環境變數設為提供者位置來存取。 此變數可以是以分號分隔的清單 (例如， `path1;path2` 如果您有多個位置，則) 。

- 此外 **nuget.exe**： nuget.exe 認證提供者可放置在與相同的資料夾中 `nuget.exe` 。

載入認證提供者時， `nuget.exe` 會依序在上述位置搜尋任何名為的檔案 `credentialprovider*.exe` ，然後依找到這些檔案的順序載入這些檔案。 如果同一個資料夾中有多個認證提供者，就會依字母順序載入。

## <a name="creating-a-nugetexe-credential-provider"></a>建立 nuget.exe 的認證提供者

認證提供者是以表單命名的命令列可執行檔，可 `CredentialProvider*.exe` 收集輸入、適當地取得認證，然後傳回適當的結束狀態碼和標準輸出。

提供者必須執行下列動作：

- 判斷是否可以在起始認證取得之前，提供目標 URI 的認證。 如果沒有，則應該傳回狀態碼1，且不含任何認證。
- 請勿修改 `Nuget.Config` (，例如) 設定認證。
- 本身會處理 HTTP proxy 設定，因為 NuGet 不會提供 proxy 資訊給外掛程式。
- 使用 UTF-8 編碼方式，藉由撰寫 JSON 回應物件以將認證或錯誤詳細資料傳回給 `nuget.exe` (，請參閱下面) 至 stdout。
- （選擇性）將額外的追蹤記錄發出到 stderr。 不應該將秘密寫入至 stderr，因為在詳細資訊層級「正常」或「詳細」的情況下，這類追蹤會由 NuGet 回應到主控台。
- 應忽略非預期的參數，以提供與未來 NuGet 版本的向前相容性。

### <a name="input-parameters"></a>輸入參數

| 參數/切換 |描述|
|----------------|-----------|
| Uri {value} | 需要認證的套件來源 URI。|
| NonInteractive | 如果有的話，提供者不會發出互動式提示。 |
| IsRetry | 如果有的話，表示此嘗試嘗試重試先前失敗的嘗試。 提供者通常會使用此旗標來確保它們略過任何現有的快取，並在可能的情況下提示輸入新的認證。|
| 詳細資訊 {value} | 如果有的話，會有下列其中一個值：「標準」、「安靜」或「詳細」。 如果未提供任何值，則預設為「正常」。 提供者應該使用這個來指出要發出至標準錯誤資料流程的選擇性記錄層級。 |

### <a name="exit-codes"></a>結束代碼

| 程式碼 |結果 | 描述 |
|----------------|-----------|-----------|
| 0 | 成功 | 已成功取得認證，並已將其寫入至 stdout。|
| 1 | ProviderNotApplicable | 目前的提供者不會提供指定 URI 的認證。|
| 2 | 失敗 | 提供者是指定 URI 的正確提供者，但無法提供認證。 在此情況下，nuget.exe 將不會重試驗證，而且將會失敗。 典型的範例是當使用者取消互動式登入時。 |

### <a name="standard-output"></a>標準輸出

| 屬性 |備註|
|----------------|-----------|
| 使用者名稱 | 已驗證要求的使用者名稱。|
| 密碼 | 已驗證要求的密碼。|
| 訊息 | 關於回應的選擇性詳細資料，只用于顯示失敗案例中的其他詳細資料。 |

範例 stdout：

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>認證提供者的疑難排解

目前，NuGet 不提供對自訂認證提供者的多個直接支援： [問題 4598](https://github.com/NuGet/Home/issues/4598) 正在追蹤這項工作。

您也可以進行下列動作：

- 使用參數執行 nuget.exe， `-verbosity` 以檢查詳細的輸出。
- 將 debug 訊息新增至 `stdout` 適當的位置。
- 請確定您使用的是 nuget.exe 3.3 或更高版本。
- 使用下列程式碼片段在啟動時附加偵錯工具：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
