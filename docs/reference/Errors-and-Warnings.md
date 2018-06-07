---
title: NuGet 錯誤和警告參考
description: 警告和錯誤各種 NuGet 作業期間發出 NuGet 從的完整參考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 368a9554c5caf92b709f9b29e16b8a7cdb264eec
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818512"
---
# <a name="errors-and-warnings"></a>錯誤和警告

在 NuGet 4.3.0+ 錯誤和警告本主題中所述的編號，並提供可協助您解決相關的問題的詳細的資訊。

錯誤和警告此處所列都僅能使用[PackageReference 基礎](../consume-packages/package-references-in-project-files.md)專案和 NuGet 4.3.0+。 NuGet 會隱藏警告或提高這些錯誤的 MSBuild 屬性也為準。 如需詳細資訊，請參閱[如何： 隱藏編譯器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文件中。

**錯誤**

| 群組 | 錯誤號碼 |
| --- | --- |
| [無效的輸入的錯誤](#invalid-input-errors) | [NU1001](#nu1001)， [NU1002](#nu1002)， [NU1003](#nu1003) |
| [遺失封裝和專案的錯誤](#missing-package-and-project-errors) | [NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (先前 NU1607) [NU1108](#nu1108) (先前 NU1606) |
| [相容性錯誤](#compatibility-errors) | [NU1201](#nu1201)， [NU1202](#nu1202)， [NU1203](#nu1203)， [NU1401](#nu1401) |

**警告**

| 群組 | 警告編號 |
| --- | --- |
| [無效的輸入的警告](#invalid-input-warnings) | [NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503) |
| [未預期的封裝版本警告](#unexpected-package-version-warnings) | [NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605) |
| [解決衝突的警告](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [封裝後援警告](#package-fallback-warnings) | [NU1701](#nu1701) |
| [摘要的警告](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet 的內部錯誤和警告](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000)， [NU1500](#nu1500) |
| [簽署的封裝 （建立及驗證）](#signed-packages-creation-and-verification)| [NU3000](#nu3000)， [NU3001](#nu3001)， [NU3002](#nu3002)， [NU3004](#nu3004)， [NU3008](#nu3008)， [NU3018](#nu3018)， [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>無效的輸入的錯誤

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **問題** | 專案未包含一或多個架構。 |
| **範例訊息** | *專案找到了 c:\tmp\projA.csproj 中未指定任何目標架構* |
| **方案** | 新增`TargetFramework`或`TargetFrameworks`屬性，以指定的專案檔。 |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **問題** | 輸入與清除關鍵字的組合無效。 |
| **範例訊息** | *搭配其他的值不能使用 'CLEAR'* |
| **方案** | 清除單獨使用，並省略其他所有的輸入。 |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **問題** | `PackageTargetFallback` 和`AssetTargetFallback`選取資產時，提供不同的行為，而且無法一起使用。 |
| **範例訊息** | *PackageTargetFallback 和 AssetTargetFallback 無法一起使用。從專案環境移除 PackageTargetFallback(deprecated) 參考。* |
| **方案** | 移除已被取代`PackageTargetFallback`從專案的項目。 |

## <a name="missing-package-and-project-errors"></a>遺失封裝和專案的錯誤

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **問題** | 相依性群組無法解析。 這是泛型類型不是封裝或專案的問題。 |
| **範例訊息** | *無法解析 net45 System.Missing* |
| **方案** | 開啟專案檔，並檢查其相依性的清單。 請檢查每個相依性存在套件來源使用，以及封裝支援此專案的目標架構。 |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **問題** | 任何來源上找不到封裝。 |
| **範例訊息** | *找不到封裝 System.Missing。無封裝存在具有此 id 來源中： dotnet 核心、 dotnet roslyn、 nuget.org* |
| **方案** | 檢查以確定您使用正確的封裝識別碼和版本號碼的 Visual Studio 中的專案的相依性。 也請檢查[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)識別封裝來源您預期會使用。 如果您使用具有封裝[語意版本設定 2.0.0](../reference/package-versioning.md#semantic-versioning-200)，請確定您使用換行字元、 V3 `https://api.nuget.org/v3/index.json`，請在[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)。 |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **問題** | 找到的封裝識別碼，但任何來源上找不到指定的相依性範圍內的版本。 封裝並不是使用者，可能指定的範圍。 |
| **範例訊息** | *找不到版本套件 NuGet.Versioning (> = 9.0.1)<br/> -找到 30 位在 nuget.org 的版本 [最近的版本： 4.0.0]<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -找到 9版本 NuGetVolatile 中的 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn* |
| **方案** | 編輯專案檔以便可以正確封裝版本。 也請檢查[NuGet 組態](../consume-packages/Configuring-NuGet-Behavior.md)識別封裝來源您預期會使用。 您可能需要變更 requeted 版本，如果此封裝直接專案參考。 |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **問題** | 指定的專案相依性範圍的穩定版本，但該範圍中找不到任何穩定版本。 找不到發行前版本，但不是允許。 |
| **範例訊息** | *找不到版本為穩定套件 NuGet.Versioning (> = 3.0.0)<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn* |
| **方案** |  編輯專案檔，以包含發行前版本中的版本範圍。 請參閱[封裝版本控制](../reference/Package-Versioning.md)。 |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **問題** | ProjectReference 指向不存在的檔案。 |
| **範例訊息** | *專案參考不存在 'c:\a.csproj'。請檢查該專案的參考有效，且專案檔已存在。* |
| **方案** | 編輯專案檔，請更正路徑參考的專案，或移除的參考完全不再需要。 |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **問題** | 專案檔存在，但沒有還原資訊並未提供它。 |
| **範例訊息** | *無法讀取 'c:\a.csproj' 的專案資訊。專案檔可能無效或遺漏目標所需的還原。* |
| **方案** | 在 Visual Studio 中，錯誤可能表示專案已卸載，在這種情況下重新載入專案。 從命令列，這可能表示檔案已損毀或不包含自訂 「 呼叫後匯入 「 還原若要讀取專案所需的目標。 專案檔無效，而且包含 「 呼叫後匯入 」 目標核取。 |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **問題** | 無法解析相依性條件約束。 |
| **範例訊息** | *無法滿足 {id} 的衝突要求: {衝突 path} Framework: {目標圖表}* |
| **方案** | 編輯專案檔來指定相依性，而不是正確的版本更開放式的範圍。 |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (先前 NU1607)

| | |
| --- | --- |
| **問題** | 無法解析封裝之間的相依性條件約束。 |
| **範例訊息** | *偵測到 NuGet.Versioning 版本衝突。參照套件，直接從專案以解決此問題。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning （= 3.5.0）]-> [<br/> NuGet.Configuration 4.0.0]-> [的 NuGet.Versioning （等於 4.0.0）* |
| **方案** | 封裝名稱中有相依性條件約束，確切的版本上不允許其他封裝，以提高版本，如有需要。 加入所需的正確版本的套件直接 （在專案檔） 的參考。 |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (先前 NU1606)

| | |
| --- | --- |
| **問題** | 偵測到循環相依性。 |
| **範例訊息** | *偵測到循環： a-> B-A >* |
| **方案** | 封裝被撰寫不正確;請連絡封裝擁有者，以修正 bug。 |

## <a name="compatibility-errors"></a>相容性錯誤

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **問題** | 相依性專案未包含與目前的專案相容的架構。 一般而言，此專案的目標架構是版本高於使用的專案。 |
| **範例訊息** | *專案 ServerWeb 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。專案 ServerWeb 支援：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)* |
| **方案** | 將專案的目標 framework 變更為相同或較低的版本比使用的專案。 |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **問題** | 相依性封裝未包含任何與專案相容的資產。 |
| **範例訊息** | *封裝 System.ComponentModel.EventBasedAsync 4.0.11 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。封裝 System.ComponentModel.EventBasedAsync 4.0.11 支援：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = 4.5 版)<br/> -netcore50 (。NETCore，Version = v5.0)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可攜式 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，設定檔 = Profile259)<br/> -win8 (Windows，Version = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **方案** | 將專案的目標 framework 變更為套件支援。 |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **問題** | 封裝不支援專案的`RuntimeIdentifier`。 |
| **範例訊息** | *System.Example 1.0.0 提供 net461，a.dll 的編譯階段的參考組件，但沒有相容的執行階段組件。* |
| **方案** | 變更`RuntimeIdentifier`視專案中使用的值。 |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **問題** | 此封裝需要的功能或安裝的 NuGet 版本目前不支援的架構。 |
| **範例訊息** | *'NuGet.Versioning' 封裝需要 NuGet 用戶端版本 '5.0.0' 或以上版本，但是目前 NuGet 版本是 '4.3.0'。* |
| **方案** | 安裝 NuGet 較新的版本。 請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md)。 |

## <a name="invalid-input-warnings"></a>無效的輸入的警告

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **問題** | 專案還原操作嘗試在找不到。 |
| **範例訊息** | *資料夾 'c:\projects\a' 沒有可還原的專案。* |
| **方案** | 包含專案的資料夾中執行 nuget 還原。 |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **問題** | `RuntimeSupports` 包含無效的設定檔。 一般而言，支援的設定檔中未找到`runtime.json`從目前的相依性套件的檔案。|
| **範例訊息** | *未知的相容性設定檔： aaa* |
| **方案** | 請檢查`RuntimeSupports`專案中的值。 |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **問題** | 相依性專案不會匯入 NuGet 的還原目標。 這類似於 NU1105 但此處已略過專案，而不會引發還原失敗的所有忽略。 在複雜的解決方案通常會其他類型可能不支援還原的專案。 |
| **範例訊息** | *正在略過專案 'c:\a.csproj' 的還原。專案檔可能無效或遺漏目標所需的還原。* |
| **方案** | 這種情形，不會匯入一般 props/目標自動匯入還原的專案。 如果專案不需要還原可以忽略此參數。 否則，請編輯受影響的專案，以便將還原的目標。 |

## <a name="unexpected-package-version-warnings"></a>未預期的封裝版本警告

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **問題** | 直接專案相依性是只有當更新的版本比指定的專案。 |
| **範例訊息** | *指定的相依性為 NuGet.Versioning (> = 3.5.0) 但 NuGet.Versioning 4.0.0 結果。* |
| **方案** | 適當版本來更新專案中的相依性。 |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **問題** | 封裝的相依性遺漏下限。 這不允許還原，若要尋找*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **範例訊息** | *NuGet.Packaging 4.0.0 不提供相依性 NuGet.Versioning (> 3.5.0) 下限 （內含）。3.6.0 的近似最符合項目已解決。* |
| **方案** | 這通常是撰寫錯誤的封裝。 請連絡封裝作者以解決此問題。 |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **問題** | 封裝的相依性指定找不到的版本。 通常，封裝來源不包含預期的下限版本。 較高的版本來取代，這不同於封裝所撰寫針對。<br/><br/>這表示找不到該還原*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **範例訊息** | NuGet.Packaging 4.0.0 取決於 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。 5.0.0 的近似最符合項目已解決。 |
| **方案** | 如果封裝應該沒有釋出，這可能是封裝撰寫錯誤。 請連絡封裝作者以解決此問題。 如果已發行的封裝，然後檢查它是否可用上您所使用的封裝來源。 如果使用的私用的來源，您可能需要更新該摘要上的封裝。 |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **問題** | 專案相依性不會定義繫結至較低。<br/><br/>這表示找不到該還原*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **範例訊息** | *專案相依性 NuGet.Versioning (< = 9.0.0) doe 包含下限 （內含）。相依性版本，以確保結果一致還原包含下限。* |
| **方案** | 更新專案的`PackageReference``Version`包含繫結至較低的屬性。 |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **問題** | 相依性套件指定版本上的條件約束的封裝版本高於還原最後都會解析。 也就是 「 最接近獲勝 」 規則解析封裝時，因為圖形中的最接近的封裝可能已覆寫遠方的封裝。 |
| **範例訊息** | *偵測到套件降級： 3.5.0 來從 4.0.0 NuGet.Versioning。直接從要選取不同版本的專案參考封裝。<br/>NuGet.Packaging 3.5.0]-> [NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0]-> [NuGet.Configuration 4.0.0]-> [NuGet.Versioning 4.0.0* |
| **方案** | 直接將參考加入至您想要使用的封裝更高版本的專案。 |

## <a name="resolver-conflict-warnings"></a>解決衝突的警告

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **問題** | 解析的封裝高於允許的相依性條件約束。 這表示，直接在專案所參考的封裝會覆寫從其他套件相依性條件約束。|
| **範例訊息** | *外部相依性條件約束的偵測到的套件版本： x 1.0.0 需要的 y （= 1.0.0），但 y 2.0.0 的版本是已解決。* |
| **方案** | 在某些情況下，這是有意如此，可以隱藏的警告。 否則，變更以擴大其版本條件約束的封裝專案的參考。 |

## <a name="package-fallback-warnings"></a>封裝後援警告

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **問題** | `PackageTargetFallback` / `AssetTargetFallback` 用來從封裝中選取的資產。 警告會讓使用者知道資產可能不相容的 100%。 |
| **範例訊息** | *已還原封裝 'NuGet.Versioning'，'可攜式 net45 + win8' 改為使用專案目標 framework 'netstandard1.5'。此封裝可能無法完全相容，您的專案。* |
| **方案** | 將專案的目標 framework 變更為套件支援。 |

## <a name="feed-warnings"></a>摘要的警告

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **問題** | 讀取摘要時，發生錯誤時`IgnoreFailedSources`設為 true，將它轉換成非嚴重警告。 這可能會包含任何訊息，而且是泛型。 |
| **範例訊息** | N/A |
| **方案** | 編輯您的設定以指定有效的來源。 |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet 的內部錯誤和警告

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **問題** | 從 NuGet 非特定的內部錯誤。 |
| **方案** | 檢查記錄檔，如需詳細資訊 |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **問題** | 從 NuGet 非特定內部警告。 |
| **方案** | 檢查記錄檔，如需詳細資訊 |

## <a name="signed-packages-creation-and-verification"></a>簽署的封裝 （建立及驗證）

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **問題** | 簽署封裝驗證和非特定錯誤相關封裝簽章。 |
| **方案** | 請檢查記錄以取得詳細資訊。 |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **問題** | 無效的引數設為 [簽署命令](../tools/cli-ref-sign.md)或[確認命令](../tools/cli-ref-verify.md)。 |
| **方案** | 檢查並更正提供的引數。 |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **問題** | `-Timestamper`未指定選項與[nuget 登命令](../tools/cli-ref-sign.md)。 |
| **範例訊息** | *'-Timestamper' 無法提供選項。已簽署的套件不會加。* |
| **方案** | 指定`-Timestamper`選項與`nuget sign`。 |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **問題** | 不帶正負號的封裝提供給[nuget 確認命令](../tools/cli-ref-verify.md)。 |
| **方案** | 執行`nuget verify`與已簽署封裝。 請參閱[簽署封裝](../create-packages/Sign-a-Package.md)。 |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **問題** | 套件完整性檢查失敗，這表示已簽署的封裝要簽署後已遭竄改。 |
| **方案** | 掃描您的防毒軟體的電腦。 然後從電腦移除封裝、 重新安裝它，然後再次嘗試操作。 如果此問題持續發生，請連絡封裝來源的擁有者及封裝擁有者。 |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **問題** | 主要簽章的憑證鏈結建立失敗。 主要簽署憑證不受信任，撤銷，或憑證的撤銷資訊無法使用。 |
| **範例訊息** | *警告： NU3018： 撤銷功能無法檢查撤銷憑證。* |
| **方案** | 使用受信任且有效的憑證。 請檢查網際網路連線。 |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **問題** | 時間戳記簽章的憑證鏈結建立失敗。 時間戳記簽章憑證不受信任，撤銷，或憑證的撤銷資訊無法使用。 |
| **範例訊息** | *警告： NU3028： 撤銷功能無法檢查撤銷憑證。* |
| **方案** | 使用受信任且有效的憑證。 請檢查網際網路連線。 |
