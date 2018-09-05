---
title: nuget.exe 認證提供者
description: nuget.exe 認證提供者驗證摘要，並會實作為命令列可執行檔，請遵循特定的慣例。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550185"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 認證提供者使用的驗證摘要

*NuGet 3.3 +*

當`nuget.exe`需要認證以驗證摘要，它們看起來如下：

1. 中的認證會先尋找 NuGet`Nuget.Config`檔案。
1. NuGet 接著會使用外掛程式認證提供者，受限於下面所列的順序。 (範例中，而且[Visual Studio Team Services 認證提供者](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)
1. NuGet 接著會提示使用者輸入認證，在命令列上。

請注意，此處所述的認證提供者只能在運作`nuget.exe`而不是在 'dotnet restore' 或 Visual Studio。 對於使用 Visual Studio 的認證提供者，請參閱[nuget.exe 認證提供者，適用於 Visual Studio](nuget-credential-providers-for-visual-studio.md)

nuget.exe 認證提供者可以用於 3 種方式：

- **全域**： 將認證提供者提供的所有執行個體`nuget.exe`目前的使用者設定檔之下執行，請將它新增至`%LocalAppData%\NuGet\CredentialProviders`。 您可能需要建立`CredentialProviders`資料夾。 認證提供者可以安裝根目錄的`CredentialProviders`資料夾或子資料夾內。 如果認證提供者有多個檔案/組件，您可以使用子資料夾，將組織的提供者。

- **從環境變數**： 認證提供者可以儲存在任何地方，並供`nuget.exe`藉由設定`%NUGET_CREDENTIALPROVIDERS_PATH%`環境變數，以提供者位置。 這個變數可以是以分號分隔的清單 (例如`path1;path2`) 如果您有多個位置。

- **與 nuget.exe**: nuget.exe 認證提供者可以放在相同的資料夾`nuget.exe`。

正在載入認證提供者，當`nuget.exe`搜尋上述的位置，讓任何名為檔案`credentialprovider*.exe`，然後將這些檔案在發現的順序。 如果多個認證提供者存在於相同的資料夾，它們是依字母順序排列的順序載入。

## <a name="creating-a-nugetexe-credential-provider"></a>建立 nuget.exe 認證提供者

認證提供者是命令列可執行檔，在表單名為`CredentialProvider*.exe`，會收集輸入、 取得視需要的認證，則會傳回適當的結束狀態碼和標準輸出。

提供者必須執行下列作業：

- 判斷是否它可以提供認證的目標 URI 初始化認證擷取之前。 如果沒有，它應該會傳回狀態碼為 1 以不含認證。
- 不會修改`Nuget.Config`（如那里設定認證）。
- 在它自己，做為 NuGet 上的控制代碼 HTTP proxy 設定不提供外掛程式的 proxy 資訊。
- 傳回認證或錯誤詳細資料，以`nuget.exe`藉由將寫入 stdout，使用 utf-8 編碼的 JSON 回應物件 （如下所示）。
- 選擇性地發出額外的追蹤記錄至 stderr。 沒有祕密應寫入到 stderr，因為 「 標準 」 或 「 詳細 」 的詳細資訊層級這類追蹤由 NuGet 回應到主控台。
- 未預期的參數應該予以忽略，提供往後相容性與未來版本的 NuGet。

### <a name="input-parameters"></a>輸入的參數

| 參數/切換 |描述|
|----------------|-----------|
| Uri {value} | 封裝來源 URI 需要認證。|
| NonInteractive | 如果有的話，提供者不會發出互動式提示。 |
| IsRetry | 如果存在，表示這項嘗試是重試先前失敗的嘗試。 提供者通常會使用這個旗標，確保他們略過任何現有的快取，並提示您輸入新認證的話。|
| {Value} 的詳細資訊 | 如果有的話，下列值之一: 「 標準 」、 「 靜音 」 或 「 詳細 」。 如果未提供值，則會預設為 「 正常 」。 提供者應該以此做為選擇性的記錄層級表示會發送至標準錯誤資料流。 |

### <a name="exit-codes"></a>結束代碼

| 程式碼 |結果 | 描述 |
|----------------|-----------|-----------|
| 0 | 成功 | 已成功取得認證，而且已寫入至 stdout。|
| 1 | ProviderNotApplicable | 目前的提供者不提供指定之 URI 的認證。|
| 2 | 失敗 | 提供者是正確的提供者指定的 uri，但無法提供認證。 在此情況下，nuget.exe 會將不會重試驗證，而且會失敗。 當使用者取消互動式登入，就會是一個典型的例子。 |

### <a name="standard-output"></a>標準輸出

| 屬性 |注意|
|----------------|-----------|
| 使用者名稱 | 已驗證要求的使用者名稱。|
| 密碼 | 已驗證要求的密碼。|
| 訊息 | 選用的回應，只能用來在失敗情況下顯示其他詳細資料的詳細資料。 |

範例 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>疑難排解認證提供者

目前，NuGet 不進行偵錯自訂認證提供者，提供更直接的支援[發出 4598](https://github.com/NuGet/Home/issues/4598)正在追蹤這項工作。

您也可以進行下列動作：

- 執行使用 nuget.exe`-verbosity`切換參數來檢查詳細的輸出。
- 新增偵錯訊息`stdout`適當位置。
- 請確定您使用 nuget.exe 3.3 或更新版本。
- 附加偵錯工具在啟動時，此程式碼片段：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

進一步的說明，請[提交支援要求 nuget.org](https://www.nuget.org/policies/Contact)。
