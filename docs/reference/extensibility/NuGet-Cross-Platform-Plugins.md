---
title: 跨平台外掛程式的 NuGet
description: NuGet NuGet.exe、 dotnet.exe，msbuild.exe 和 Visual Studio 跨平台的外掛程式
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794182"
---
# <a name="nuget-cross-platform-plugins"></a>跨平台外掛程式的 NuGet

已新增 nuget 4.8 + 跨平台的外掛程式支援。
這是藉由建置新的外掛程式擴充性模型，必須符合一組嚴格的作業的規則，來達成與。
外掛程式是獨立的可執行檔 (在.NET Core 世界 runnables)，NuGet 用戶端啟動個別的處理序。
這是 true 寫入一次，隨處執行外掛程式。 它會使用所有的 NuGet 用戶端工具。
增益集可以是 （NuGet.exe，MSBuild.exe 和 Visual Studio） 的.NET Framework 或.NET Core (dotnet.exe)。
定義建立版本的通訊協定之間 NuGet 用戶端和外掛程式。 啟動交握期間的 2 個處理程序會交涉的通訊協定版本。

若要涵蓋所有的 NuGet 用戶端工具案例，則需要.NET Framework 和.NET 核心外掛程式。
以下描述的用戶端/架構組合的外掛程式。

| 用戶端工具  | 架構 |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| 在 Mono 上的 NuGet.exe | .NET Framework |

## <a name="how-does-it-work"></a>如何運作

高層級的工作流程可以如下所述：

1. NuGet 會探索可用的外掛程式。
1. 適用時，NuGet 會逐一依優先順序並開始逐一進行中的外掛程式。
1. NuGet 會使用可以服務此要求的第一個外掛程式。
1. 當您不再需要時，將會關閉增益集。

## <a name="general-plugin-requirements"></a>一般外掛程式需求

在目前的通訊協定版本*2.0.0*。
在此版本中，需求如下：

- 有有效且信任 Authenticode 簽章的組件會在 Windows 和 Mono 執行。 沒有任何特殊的信任需求尚未執行 Linux 和 Mac 上的組件。 [相關的問題](https://github.com/NuGet/Home/issues/6702)
- 支援無狀態的 NuGet 用戶端工具的目前安全性內容下啟動。 比方說，NuGet 用戶端工具不會執行提高權限或稍後所述的外掛程式通訊協定以外的其他初始化。
- 除非另有明確指定，則為非互動式的。
- 遵守交涉的外掛程式通訊協定版本。
- 在合理時間內回應所有的要求。
- 接受任何進行中作業的取消要求。

技術規格所述的下列規格中的更多詳細資料：

- [NuGet 封裝下載外掛程式](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [跨平台驗證外掛程式的 NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>用戶端-外掛程式互動

NuGet 用戶端工具和外掛程式與 JSON 通訊標準資料流 （stdin、 stdout、 stderr） 中。 所有的資料必須是 utf-8 編碼。
外掛程式會啟動與引數"-外掛程式 」。 如果使用者直接啟動可執行檔，而不需要這個引數的外掛程式，外掛程式可以提供資訊而非通訊協定交握正在等候訊息。
通訊協定交握逾時是 5 秒。 此外掛程式應該先完成中的設定為除了盡量。
NuGet 用戶端工具會藉由 NuGet 來源的服務索引的傳入查詢的外掛程式支援的作業。 外掛程式可用來檢查有支援的服務類型的服務索引。

NuGet 用戶端工具和外掛程式之間的通訊是雙向。 每個要求會有 5 秒的逾時。 如果作業花費的時間應該在個別的程序應該傳送進度訊息，以防止要求逾時。在 1 分鐘的閒置時間後外掛程式會被視為閒置，並已關閉。

## <a name="plugin-installation-and-discovery"></a>安裝外掛程式和探索

透過慣例為基礎的目錄結構，並發現外掛程式。
CI/CD 案例和進階使用者可以使用環境變數覆寫行為。

- `NUGET_PLUGIN_PATHS` -定義將用於 NuGet 程序中，保留的優先順序的外掛程式。 如果設定這個環境變數，它會覆寫慣例為基礎的探索。
-  使用者位置]、 [中的 NuGet 首頁位置`%UserProfile%/.nuget/plugins`。 此位置無法被覆寫。 不同的根目錄會用於.NET Core 和.NET Framework 的外掛程式。

| 架構 | 根探索位置  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

每個外掛程式應該安裝在它自己的資料夾中。
外掛程式的進入點會與.dll 擴充功能適用於.NET Core 和.NET Framework 的.exe 副檔名之安裝資料夾的名稱。

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
> 目前沒有任何使用者劇本，外掛程式的安裝。 很簡單，只要將所需的檔案移至預先決定的位置。

## <a name="supported-operations"></a>支援的作業

以新的 「 外掛程式 」 通訊協定支援兩個作業。

| 作業名稱 | 最小通訊協定版本 | 最低 NuGet 用戶端版本 |
| -------------- | ----------------------- | --------------------- |
| 下載套件 | 1.0.0 | 4.3.0 |
| [驗證](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>執行正確的執行階段下的外掛程式

Dotnet.exe 案例中的 NuGet，外掛程式需要能夠在該特定的執行階段的 dotnet.exe 下執行。
它是外掛程式提供者和取用者，以確定會使用相容的 dotnet.exe/plugin 組合上。
可能的問題可能發生的使用者位置有更多的外掛程式時，例如，2.0 執行階段下的 dotnet.exe 便會嘗試使用 2.1 執行階段撰寫的外掛程式。

## <a name="capabilities-caching"></a>快取的功能

安全性驗證和具現化的外掛程式是成本高昂。 不過平均 NuGet 使用者才可能會有的驗證外掛程式，會比驗證作業，方法會更頻繁地發生下載作業。
若要改善體驗，NuGet 會快取指定之要求的作業宣告。 此快取每個外掛程式與外掛程式索引鍵所外掛程式的路徑，而且此功能快取的到期日為 30 天。 

快取位於`%LocalAppData%/NuGet/plugins-cache`並將它覆寫環境變數`NUGET_PLUGINS_CACHE_PATH`。 若要清除這[快取](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，可以執行 [區域變數] 命令搭配`plugins-cache`選項。
`all` [區域變數] 選項也會立即刪除外掛程式快取。 

## <a name="protocol-messages-index"></a>通訊協定訊息的索引

通訊協定版本*1.0.0*訊息：

1.  關閉
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含任何承載
    * 不需要回應。  適當的回應是外掛程式處理序立即結束。

2.  將檔案複製在封裝中
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 套件識別碼和版本
        * 套件來源存放庫位置
        * 目的地目錄路徑
        * 可列舉的封裝複製到目的地目錄路徑中的檔案
    * 回應會包含：
        * 回應碼，表示作業結果
        * 可列舉的完整路徑複製之檔案中的目的地目錄，如果作業成功

3.  複製封裝檔案 (.nupkg)
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 套件識別碼和版本
        * 套件來源存放庫位置
        * 目的地檔案路徑
    * 回應會包含：
        * 回應碼，表示作業結果

4.  取得認證
    * 要求方向： 外掛程式]-> [NuGet
    * 要求將會包含：
        * 套件來源存放庫位置
        * 從使用目前的認證套件來源存放庫取得 HTTP 狀態碼
    * 回應會包含：
        * 回應碼，表示作業結果
        * 使用者名稱，如果有的話
        * 密碼，如果有的話

5.  取得封裝中的檔案
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 套件識別碼和版本
        * 套件來源存放庫位置
    * 回應會包含：
        * 回應碼，表示作業結果
        * 可列舉的檔案路徑中的封裝，如果作業成功

6.  取得作業的宣告 
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 服務 index.json，套件來源
        * 套件來源存放庫位置
    * 回應會包含：
        * 回應碼，表示作業結果
        * 可列舉的支援的作業 (例如： 套件下載) 如果作業成功。  如果外掛程式不支援的套件來源，此外掛程式必須傳回空集合的支援的作業。

> [!Note]
> 此訊息已更新版本中*2.0.0*。 它是在用戶端，以保留回溯相容性。

7.  取得封裝雜湊
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 套件識別碼和版本
        * 套件來源存放庫位置
        * 雜湊演算法
    * 回應會包含：
        * 回應碼，表示作業結果
        * 封裝檔案的雜湊，使用要求的雜湊演算法，如果作業成功

8.  取得封裝版本
    * 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 套件識別碼
        * 套件來源存放庫位置
    * 回應會包含：
        * 回應碼，表示作業結果
        * 可列舉的套件版本，如果作業成功

9.  取得服務索引
    * 要求方向： 外掛程式]-> [NuGet
    * 要求將會包含：
        * 套件來源存放庫位置
    * 回應會包含：
        * 回應碼，表示作業結果
        * 服務索引，如果作業成功

10.  交握
     * 要求方向： NuGet <>-外掛程式
     * 要求將會包含：
         * 目前的外掛程式通訊協定版本
         * 支援的最低外掛程式通訊協定版本
     * 回應會包含：
         * 回應碼，表示作業結果
         * 如果作業成功交涉通訊協定版本。  失敗會導致終止的外掛程式。

11.  初始化
     * 要求方向： NuGet]-> [外掛程式
     * 要求將會包含：
         * NuGet 用戶端工具的版本
         * NuGet 用戶端工具有效語言。  這會將考量 ForceEnglishOutput 設定中，如果使用。
         * 預設要求逾時，會取代預設的通訊協定。
     * 回應會包含：
         * 回應碼，用來表示作業的結果。  失敗會導致終止的外掛程式。

12.  記錄檔
     * 要求方向： 外掛程式]-> [NuGet
     * 要求將會包含：
         * 要求記錄層級
         * 要記錄的訊息
     * 回應會包含：
         * 回應碼，用來表示作業的結果。

13.  監視 NuGet 處理序結束
     * 要求方向： NuGet]-> [外掛程式
     * 要求將會包含：
         * NuGet 處理序識別碼
     * 回應會包含：
         * 回應碼，用來表示作業的結果。

14.  預先擷取的封裝
     * 要求方向： NuGet]-> [外掛程式
     * 要求將會包含：
         * 套件識別碼和版本
         * 套件來源存放庫位置
     * 回應會包含：
         * 回應碼，表示作業結果

15.  設定認證
     * 要求方向： NuGet]-> [外掛程式
     * 要求將會包含：
         * 套件來源存放庫位置
         * 最後一個已知的套件來源使用者名稱，如果有的話
         * 最後一個已知的封裝來源密碼，如果有的話
         * 最後一個已知的 proxy 使用者名稱，如果有的話
         * 最後一個已知的 proxy 密碼，如果有的話
     * 回應會包含：
         * 回應碼，表示作業結果

16.  設定記錄層級
     * 要求方向： NuGet]-> [外掛程式
     * 要求將會包含：
         * 預設記錄層級
     * 回應會包含：
         * 回應碼，表示作業結果

通訊協定版本*2.0.0*訊息

17. 取得作業的宣告

* 要求方向： NuGet]-> [外掛程式
    * 要求將會包含：
        * 服務 index.json，套件來源
        * 套件來源存放庫位置
    * 回應會包含：
        * 回應碼，表示作業結果
        * 可列舉的支援的作業，如果作業成功。  如果外掛程式不支援的套件來源，此外掛程式必須傳回空集合的支援的作業。

    如果服務索引和套件來源為 null 時，外掛程式可以回答與驗證。

18. 取得驗證認證

* 要求方向： NuGet]-> [外掛程式
* 要求將會包含：
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* 回應會包含
    * 使用者名稱
    * 密碼
    * 訊息
    * 驗證類型清單
    * MessageResponseCode