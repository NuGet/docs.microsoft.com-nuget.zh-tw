---
title: "nuget.exe 認證提供者 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 認證提供者使用摘要驗證，而且會實作為命令列可執行檔，請遵循特定的慣例。"
keywords: "nuget.exe 認證提供者認證提供者 API，驗證使用的摘要，驗證組件庫"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>搭配 nuget.exe 認證提供者使用的驗證摘要

*NuGet 3.3 +*

當`nuget.exe`需要使用摘要驗證的認證會以下列方式尋找它們：

1. 中的認證會先尋找 NuGet`Nuget.Config`檔案。
1. NuGet 接著會使用外掛程式的認證提供者，受限於如下所示的順序。 (範例中，且[Visual Studio Team Services 認證提供者](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)
1. NuGet 接著會提示使用者提供認證，在命令列上。

請注意，此處所述的認證提供者只在工作`nuget.exe`而不是在 'dotnet restore' 或 Visual Studio。 Visual Studio 中的認證提供者，請參閱[nuget.exe for Visual Studio 的認證提供者](nuget-credential-providers-for-visual-studio.md)

nuget.exe 認證提供者可用以 3 種方式：

- **全域**： 若要使用的所有執行個體的認證提供者`nuget.exe`執行目前的使用者設定檔 下，將它加入至`%LocalAppData%\NuGet\CredentialProviders`。 您可能需要建立`CredentialProviders`資料夾。 認證提供者可以安裝根目錄的`CredentialProviders`資料夾或子資料夾內。 如果認證提供者有多個檔案/組件，您可以使用子資料夾，將組織的提供者。

- **環境變數從**： 認證提供者可以儲存在任何地方，並存取`nuget.exe`藉由設定`%NUGET_CREDENTIALPROVIDERS_PATH%`環境變數，以提供者位置。 這個變數可以是以分號分隔的清單 (例如， `path1;path2`) 如果您有多個位置。

- **連同 nuget.exe**: nuget.exe 認證提供者可以放在相同的資料夾`nuget.exe`。

認證提供者，在載入時`nuget.exe`搜尋上述的位置，讓任何名為檔案`credentialprovider*.exe`，接著會載入這些檔案在發現的順序。 如果多個認證提供者存在相同資料夾中，變更就會依字母順序排列的順序載入。

## <a name="creating-a-nugetexe-credential-provider"></a>建立 nuget.exe 認證提供者

認證提供者是命令列可執行檔中以`CredentialProvider*.exe`，，會收集輸入取得適當的認證，然後傳回適當的結束狀態碼和標準輸出。

提供者必須執行下列作業：

- 判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。 如果沒有，則應該傳回狀態碼不含認證的 1。
- 不會修改`Nuget.Config`（如那里設定認證）。
- 控制代碼 HTTP proxy 設定，在其專屬且為 NuGet 不提供外掛程式的 proxy 資訊。
- 傳回認證或錯誤詳細資料給`nuget.exe`寫入 stdout、 使用 utf-8 編碼的 JSON 回應物件 （如下所示）。
- 選擇性地發出其他的追蹤記錄至 stderr。 密碼應該寫入至 stderr，因為在 「 標準 」 或 「 詳細 」 的詳細資訊層級這類追蹤所 nuget 傳到主控台。
- 應忽略非預期的參數，提供往後相容性，在未來版本的 NuGet。

### <a name="input-parameters"></a>輸入的參數

| 參數/切換 |描述|
|----------------|-----------|
| Uri 的 {value} | 封裝來源 URI 需要認證。|
| NonInteractive | 如果有的話，提供者不會發出互動式提示。 |
| IsRetry | 如果有的話，表示這項嘗試是先前的失敗嘗試的重試。 提供者通常使用這個旗標，以確保它們略過任何現有的快取，並盡可能提示您輸入新的認證。|
| 詳細等級 {value} | 如果有的話，下列值之一: 「 標準 」、 「 無訊息 」 或 「 詳細 」。 如果未提供值，預設為"normal"。 提供者應該使用這個選擇性記錄的層級的指示來發出至標準錯誤資料流。 |

### <a name="exit-codes"></a>結束代碼

| 程式碼 |結果 | 描述 |
|----------------|-----------|-----------|
| 0 | 成功 | 已成功取得認證，並已寫入至 stdout。|
| 1 | ProviderNotApplicable | 目前的提供者不提供認證指定的 uri。|
| 2 | 失敗 | 提供者是正確的提供者指定的 uri，但無法提供認證。 在此情況下，nuget.exe 將不會重試驗證，而且會失敗。 典型的範例是當使用者取消互動式登入。 |

### <a name="standard-output"></a>標準輸出

| 屬性 |注意|
|----------------|-----------|
| 使用者名稱 | 已驗證要求的使用者名稱。|
| 密碼 | 已驗證要求的密碼。|
| 訊息 | 選擇性回應，只能用來顯示其他詳細資料中的失敗情況相關的詳細資料。 |

範例 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>疑難排解認證提供者

目前，NuGet 不直接支援的偵錯提供自訂認證提供者;[發出 4598](https://github.com/NuGet/Home/issues/4598)是否會追蹤這項工作。

您也可以進行下列動作：

- 執行與 nuget.exe`-verbosity`檢查詳細的輸出參數。
- 加入至偵錯訊息`stdout`適當位置。
- 請確定您使用 nuget.exe 3.3 或更高版本。
- 附加偵錯工具在啟動時，此程式碼片段：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

取得進一步的協助，[提交支援要求 nuget.org](https://www.nuget.org/policies/Contact)。
