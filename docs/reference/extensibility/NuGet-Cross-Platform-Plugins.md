---
title: NuGet 跨平臺外掛程式
description: 適用于 Nuget.exe、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平臺外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380505"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet 跨平臺外掛程式

在 NuGet 4.8 + 中，已新增跨平臺外掛程式的支援。
這是透過建立新的外掛程式擴充性模型來達成，必須符合一組嚴格的運算規則。
外掛程式是獨立的可執行檔（在 .NET Core 世界中為 runnables），NuGet 用戶端會在個別的進程中啟動。
這是真正的寫入一次，可在任何地方執行外掛程式。 它會與所有 NuGet 用戶端工具搭配使用。
外掛程式可以是 .NET Framework （Nuget.exe、Msbuild.exe 和 Visual Studio）或 .NET Core （dotnet .exe）。
NuGet 用戶端和外掛程式之間已建立版本的通訊協定。 在啟動信號交換期間，2個進程會協調通訊協定版本。

為了涵蓋所有 NuGet 用戶端工具案例，其中一項需要 .NET Framework 和 .NET Core 外掛程式。
以下說明外掛程式的用戶端/架構組合。

| 用戶端工具  | 架構 |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet .exe | .NET Core |
| Nuget.exe | .NET Framework |
| Msbuild.exe | .NET Framework |
| Mono 上的 Nuget.exe | .NET Framework |

## <a name="how-does-it-work"></a>運作方式

高階工作流程可以描述如下：

1. NuGet 會探索可用的外掛程式。
1. 當適用時，NuGet 會依優先順序逐一查看外掛程式，然後逐一啟動。
1. NuGet 會使用可服務要求的第一個外掛程式。
1. 外掛程式將會在不再需要時關閉。

## <a name="general-plugin-requirements"></a>一般外掛程式需求

目前的通訊協定版本是*2.0.0*。
在此版本底下，需求如下：

- 擁有將在 Windows 和 Mono 上執行的有效、受信任的 Authenticode 簽章元件。 尚未在 Linux 和 Mac 上執行元件的特殊信任需求。 [相關問題](https://github.com/NuGet/Home/issues/6702)
- 支援 NuGet 用戶端工具的目前安全性內容下的無狀態啟動。 例如，NuGet 用戶端工具不會在稍後所述的外掛程式通訊協定以外執行提高許可權或額外的初始化。
- 除非明確指定，否則不是互動式的。
- 遵循已協商的外掛程式通訊協定版本。
- 在合理的時間週期內回應所有要求。
- 接受任何進行中作業的取消要求。

下列規格將更詳細地說明技術規格：

- [NuGet 套件下載外掛程式](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet 跨平臺驗證外掛程式](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>用戶端-外掛程式的互動

NuGet 用戶端工具和外掛程式會透過標準資料流程（stdin、stdout、stderr）與 JSON 進行通訊。 所有資料都必須以 UTF-8 編碼。
外掛程式會以引數 "-外掛程式" 啟動。 如果使用者直接啟動沒有此引數的外掛程式可執行檔，則外掛程式會提供資訊性訊息，而不是等候通訊協定交握。
通訊協定交握時間為5秒。 外掛程式應該盡可能以最少的數量完成中的設定。
NuGet 用戶端工具會藉由傳遞 NuGet 來源的服務索引來查詢外掛程式支援的作業。 外掛程式可以使用服務索引來檢查支援的服務類型是否存在。

NuGet 用戶端工具和外掛程式之間的通訊是雙向的。 每個要求的超時時間為5秒。 如果作業應花費較長的時間，則個別的進程應傳送進度訊息，以防止要求超時。在閒置1分鐘後，外掛程式會被視為閒置並關閉。

## <a name="plugin-installation-and-discovery"></a>外掛程式安裝與探索

這些外掛程式會透過以慣例為基礎的目錄結構來探索。
CI/CD 案例和 power 使用者可以使用環境變數來覆寫行為。 使用環境變數時，只允許絕對路徑。 請注意，`NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 僅適用于 5.3 + 版的 NuGet 工具和更新版本。

- `NUGET_NETFX_PLUGIN_PATHS`-定義 .NET Framework 為基礎的工具（Nuget.exe/Msbuild.exe/Visual Studio）將使用的外掛程式。 優先于 `NUGET_PLUGIN_PATHS`。 （僅限 NuGet 5.3 版 +）
- `NUGET_NETCORE_PLUGIN_PATHS`-定義將由 .NET Core 工具（dotnet）使用的外掛程式。 優先于 `NUGET_PLUGIN_PATHS`。 （僅限 NuGet 5.3 版 +）
- `NUGET_PLUGIN_PATHS`-定義將用於該 NuGet 進程的外掛程式，並保留優先順序。 如果設定此環境變數，則會覆寫以慣例為基礎的探索。 如果指定了其中一個架構特定的變數，則會忽略。
-  使用者位置，`%UserProfile%/.nuget/plugins` 中的 NuGet 首頁位置。 無法覆寫此位置。 .NET Core 和 .NET Framework 外掛程式將會使用不同的根目錄。

| 架構 | 根探索位置  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

每個外掛程式都應該安裝在自己的資料夾中。
外掛程式進入點會是已安裝之資料夾的名稱，以及適用于 .NET Core 的 .dll 副檔名，而 .NET Framework 的 .exe 延伸模組。

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> 目前沒有安裝外掛程式的使用者案例。 就像是將所需的檔案移到預先決定的位置一樣簡單。

## <a name="supported-operations"></a>支援的作業

新的外掛程式通訊協定支援兩個作業。

| 作業名稱 | 最低通訊協定版本 | 最低 NuGet 用戶端版本 |
| -------------- | ----------------------- | --------------------- |
| 下載套件 | 1.0.0 | 4.3.0 |
| [驗證](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>在正確的執行時間下執行外掛程式

在 dotnet 的 NuGet 案例中，外掛程式必須能夠在 dotnet 的特定執行時間下執行。
它位於外掛程式提供者和取用者上，以確保使用相容的 dotnet .exe/外掛程式組合。
使用者位置外掛程式可能會發生問題，例如，2.0 執行時間下的 dotnet 嘗試使用針對2.1 執行時間所撰寫的外掛程式。

## <a name="capabilities-caching"></a>功能快取

外掛程式的安全性驗證和具現化成本很高。 下載作業的執行頻率比驗證作業更頻繁，但平均 NuGet 使用者只可能有驗證外掛程式。
為了改善此體驗，NuGet 會快取指定要求的作業宣告。 此快取是每個外掛程式，其中外掛程式的索引鍵為外掛程式路徑，而此功能快取的到期時間為30天。 

快取位於 `%LocalAppData%/NuGet/plugins-cache` 中，並以環境變數 `NUGET_PLUGINS_CACHE_PATH` 覆寫。 若要清除[此快](../../consume-packages/managing-the-global-packages-and-cache-folders.md)取，可以使用 `plugins-cache` 選項來執行 [區域變數] 命令。
[@No__t_0 區域變數] 選項現在也會刪除外掛程式快取。 

## <a name="protocol-messages-index"></a>通訊協定訊息索引

通訊協定*1.0.0*版訊息：

1.  關閉
    * 要求方向： NuGet-> 外掛程式
    * 要求不會包含任何承載
    * 不需要回應。  適當的回應是讓外掛程式進程立即結束。

2.  複製封裝中的檔案
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 套件識別碼和版本
        * 封裝來源存放庫位置
        * 目的地目錄路徑
        * 封裝中要複製到目的地目錄路徑之檔案的可列舉
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則為目的地目錄中複製之檔案的完整路徑列舉

3.  複製套件檔案（. nupkg）
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 套件識別碼和版本
        * 封裝來源存放庫位置
        * 目的檔案路徑
    * 回應會包含：
        * 指出作業結果的回應碼

4.  取得認證
    * 要求方向：外掛程式-> NuGet
    * 要求將包含：
        * 封裝來源存放庫位置
        * 使用目前認證從封裝來源存放庫取得的 HTTP 狀態碼
    * 回應會包含：
        * 指出作業結果的回應碼
        * 使用者名稱（如果有的話）
        * 密碼（如果有的話）

5.  取得封裝中的檔案
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 套件識別碼和版本
        * 封裝來源存放庫位置
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則為封裝中檔案路徑的可列舉

6.  取得作業宣告 
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 封裝來源的服務索引. json
        * 封裝來源存放庫位置
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則為支援的作業（例如：套件下載）的可列舉。  如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。

> [!Note]
> 此訊息已在版本*2.0.0*中更新。 它是在用戶端上，以保留回溯相容性。

7.  取得封裝雜湊
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 套件識別碼和版本
        * 封裝來源存放庫位置
        * 雜湊演算法
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則使用要求的雜湊演算法來封裝檔案雜湊

8.  取得套件版本
    * 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 套件識別碼
        * 封裝來源存放庫位置
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則為封裝版本的可列舉

9.  取得服務索引
    * 要求方向：外掛程式-> NuGet
    * 要求將包含：
        * 封裝來源存放庫位置
    * 回應會包含：
        * 指出作業結果的回應碼
        * 作業成功時的服務索引

10.  交握
     * 要求方向： NuGet <-> 外掛程式
     * 要求將包含：
         * 目前的外掛程式通訊協定版本
         * 支援的最小外掛程式通訊協定版本
     * 回應會包含：
         * 指出作業結果的回應碼
         * 如果作業成功，則為已協商的通訊協定版本。  失敗會導致外掛程式終止。

11.  Initialize
     * 要求方向： NuGet-> 外掛程式
     * 要求將包含：
         * NuGet 用戶端工具版本
         * NuGet 用戶端工具有效語言。  這會將 ForceEnglishOutput 設定納入考慮（如果使用的話）。
         * 預設的要求超時，會取代通訊協定的預設值。
     * 回應會包含：
         * 表示作業結果的回應碼。  失敗會導致外掛程式終止。

12.  記錄檔
     * 要求方向：外掛程式-> NuGet
     * 要求將包含：
         * 要求的記錄層級
         * 要記錄的訊息
     * 回應會包含：
         * 表示作業結果的回應碼。

13.  監視 NuGet 進程結束
     * 要求方向： NuGet-> 外掛程式
     * 要求將包含：
         * NuGet 處理序識別碼
     * 回應會包含：
         * 表示作業結果的回應碼。

14.  預先提取套件
     * 要求方向： NuGet-> 外掛程式
     * 要求將包含：
         * 套件識別碼和版本
         * 封裝來源存放庫位置
     * 回應會包含：
         * 指出作業結果的回應碼

15.  設定認證
     * 要求方向： NuGet-> 外掛程式
     * 要求將包含：
         * 封裝來源存放庫位置
         * 最後已知的套件來源使用者名稱（如果有的話）
         * 最後已知的套件來源密碼（如果有的話）
         * 最後一個已知的 proxy 使用者名稱（如果有的話）
         * 最後一個已知的 proxy 密碼（如果有的話）
     * 回應會包含：
         * 指出作業結果的回應碼

16.  設定記錄層級
     * 要求方向： NuGet-> 外掛程式
     * 要求將包含：
         * 預設記錄層級
     * 回應會包含：
         * 指出作業結果的回應碼

通訊協定版本*2.0.0*訊息

17. 取得作業宣告

* 要求方向： NuGet-> 外掛程式
    * 要求將包含：
        * 封裝來源的服務索引. json
        * 封裝來源存放庫位置
    * 回應會包含：
        * 指出作業結果的回應碼
        * 如果作業成功，則為支援的作業的可列舉。  如果外掛程式不支援封裝來源，則外掛程式必須傳回一組空的支援作業。

    如果服務索引和封裝來源為 null，則外掛程式可以使用驗證來回答。

18. 取得驗證認證

* 要求方向： NuGet-> 外掛程式
* 要求將包含：
    * URI
    * isRetry
    * 非
    * CanShowDialog
* 回應會包含
    * 使用者名稱
    * 密碼
    * 訊息
    * 驗證類型的清單
    * MessageResponseCode
