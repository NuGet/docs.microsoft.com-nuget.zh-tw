---
title: "NuGet 還原錯誤和警告參考 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "警告和錯誤發出從 NuGet 封裝還原期間的完整參考"
keywords: "NuGet 錯誤、 NuGet 警告診斷"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
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
ms.openlocfilehash: c7d77af04744888ce8af92d617a2ffc7daef4eb0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="errors-and-warnings"></a>錯誤和警告

在 NuGet 4.3.0、 錯誤和警告本主題中所述的編號，並提供可協助您解決相關的問題的詳細的資訊。 

錯誤和警告此處所列都僅能使用[PackageReference 基礎](../Consume-Packages/Package-References-in-Project-Files.md)專案和 NuGet 4.3.0。 NuGet 會隱藏警告或提高這些錯誤的 MSBuild 屬性也為準。 如需詳細資訊，請參閱[如何： 隱藏編譯器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文件中。

**錯誤**

| 群組 | 錯誤號碼 |
| --- | --- |
| [無效的輸入的錯誤](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [遺失封裝和專案的錯誤](#missing-package-and-project-errors) | [NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (先前 NU1607) [NU1108](#nu1108) (先前 NU1606) |
| [相容性錯誤](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**警告**

| 群組 | 警告編號 |
| --- | --- |
| [無效的輸入的警告](#invalid-input-warnings) | [NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503) |
| [未預期的封裝版本警告](#unexpected-package-version-warnings) | [NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605) |
| [解決衝突的警告](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [封裝後援警告](#package-fallback-warnings) | [NU1701](#nu1701) |
| [摘要的警告](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet 的內部錯誤和警告](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>無效的輸入的錯誤

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **問題** | 專案未包含一或多個架構。 |
| **常見的原因** | 專案不包含`TargetFramework`或`TargetFrameworks`屬性。 |
| **範例訊息** | *專案找到了 c:\tmp\projA.csproj 中未指定任何目標架構* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **問題** | 輸入與清除關鍵字的組合無效。 |
| **常見的原因** | 清除不結合其他輸入。 |
| **範例訊息** | *搭配其他的值不能使用 'CLEAR'* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **問題** | `PackageTargetFallback`和`AssetTargetFallback`選取資產時，提供不同的行為，而且無法一起使用。 |
| **常見的原因** | 同時`PackageTargetFallback`和`AssetTargetFallback`存在於專案中。 |
| **範例訊息** | *PackageTargetFallback 和 AssetTargetFallback 無法一起使用。從專案環境移除 PackageTargetFallback(deprecated) 參考。* |

## <a name="missing-package-and-project-errors"></a>遺失封裝和專案的錯誤

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **問題** | 相依性群組無法解析。 這是泛型類型不是封裝或專案的問題。 |
| **常見的原因** | 專案包含不存在的項目上的相依性。 |
| **範例訊息** | *無法解析 net45 System.Missing* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **問題** | 任何來源上找不到封裝。 |
| **常見的原因** | 正確的套件來源遺漏或封裝識別碼不正確。 |
| **範例訊息** | *找不到封裝 System.Missing。無封裝存在具有此 id 來源中： dotnet 核心、 dotnet roslyn、 nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **問題** | 找到的封裝識別碼，但任何來源上找不到指定的相依性範圍內的版本。 |
| **常見的原因** | 正確的套件來源遺漏或相依性範圍不正確。 封裝並不是使用者，可能指定的範圍。 使用者可能需要切換至 可用的版本，如果此封裝直接參考由專案。 |
| **範例訊息** | *找不到版本套件 NuGet.Versioning (> = 9.0.1)<br/> -找到 30 位在 nuget.org 的版本 [最近的版本： 4.0.0]<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -找到 9版本 NuGetVolatile 中的 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **問題** | 相依性範圍中找不到任何穩定版本。 找不到發行前版本，但不是允許。 |
| **常見的原因** | 指定相依性範圍的穩定版本的專案。 使用者必須變更要包含發行前版本的版本範圍。 |
| **範例訊息** | *找不到版本為穩定套件 NuGet.Versioning (> = 3.0.0)<br/> -dotnet buildtools 中的找到 10 版本 [最近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最近的版本： 3.0.0-beta-00032]<br/> -0 版本位於 dotnet 核心<br/>-0 版本位於 dotnet roslyn* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **問題** | ProjectReference 指向不存在的檔案。 |
| **常見的原因** | 磁碟中的專案檔遺漏或參考不正確。 |
| **範例訊息** | *專案參考不存在 'c:\a.csproj'。請檢查該專案的參考有效，且專案檔已存在。* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **問題** | 專案檔存在，但沒有還原資訊並未提供它。 |
| **常見的原因** | 在 Visual Studio 中，這可能表示專案已卸載。 從命令列中，這可能表示檔案已損毀或還原若要讀取專案所需的匯入目標之後，它不包含自訂。 |
| **範例訊息** | *無法讀取 'c:\a.csproj' 的專案資訊。專案檔可能無效或遺漏目標所需的還原。* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **問題** | 無法解析相依性條件約束。 |
| **常見的原因** | 封裝包含確切版本，而未限制範圍不是封裝的相依性。 |
| **範例訊息** | *無法滿足 {id} 的衝突要求: {衝突 path} Framework: {目標圖表}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (先前 NU1607)

| | |
| --- | --- |
| **問題** | 無法解析封裝之間的相依性條件約束。 |
| **常見的原因** | 封裝名稱中有相依性條件約束，確切的版本上不允許其他封裝，以提高版本，如有需要。 |
| **範例訊息** | *偵測到 NuGet.Versioning 版本衝突。參照套件，直接從專案以解決此問題。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning （= 3.5.0）]-> [<br/> NuGet.Configuration 4.0.0]-> [的 NuGet.Versioning （等於 4.0.0）* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (先前 NU1606)

| | |
| --- | --- |
| **問題** | 偵測到循環相依性。 |
| **常見的原因** | 封裝被撰寫不正確。 |
| **範例訊息** | *偵測到循環： a-> B-A >* |

## <a name="compatibility-errors"></a>相容性錯誤

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **問題** | 相依性專案未包含與目前的專案相容的架構。 |
| **常見的原因** | 專案的目標 framework 是版本高於使用的專案。 |
| **範例訊息** | *專案 ServerWeb 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。專案 ServerWeb 支援：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **問題** | 相依性封裝未包含任何與專案相容的資產。 |
| **常見的原因** | 封裝不支援此專案的目標架構。 |
| **範例訊息** | *封裝 System.ComponentModel.EventBasedAsync 4.0.11 與不相容 netstandard1.3 (。NETStandard，Version = v1.3)。封裝 System.ComponentModel.EventBasedAsync 4.0.11 支援：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = 4.5 版)<br/> -netcore50 (。NETCore，Version = v5.0)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可攜式 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，設定檔 = Profile259)<br/> -win8 (Windows，Version = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **問題** | 封裝不支援專案的`RuntimeIdentifier`。 |
| **常見的原因** | 封裝不支援目前`RuntimeIdentifier`。 變更`RuntimeIdentifier`如有需要在專案中使用的值。 |
| **範例訊息** | *System.Example 1.0.0 提供 net461，a.dll 的編譯階段的參考組件，但沒有相容的執行階段組件。* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **問題** | 此封裝需要的功能或安裝的 NuGet 版本目前不支援的架構。 |
| **常見的原因** | 升級 NuGet，若要修正此問題。 |
| **範例訊息** | *'NuGet.Versioning' 封裝需要 NuGet 用戶端版本 '5.0.0' 或以上版本，但是目前 NuGet 版本是 '4.3.0'。若要升級 NuGet，請前往 http://docs.nuget.org/consume/installing-nuget。* |

## <a name="invalid-input-warnings"></a>無效的輸入的警告

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **問題** | 專案還原操作嘗試在找不到。 |
| **常見的原因** | 專案遺漏。 |
| **範例訊息** | *資料夾 'c:\projects\a' 沒有可還原的專案。* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **問題** | `RuntimeSupports`包含無效的設定檔。 |
| **常見的原因** | 中找不到支援的設定檔`runtime.json`從目前的相依性套件的檔案。 |
| **範例訊息** | *未知的相容性設定檔： aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **問題** | 相依性專案不會匯入 NuGet 的還原目標。 這類似於 NU1105 但此處已略過專案，而不會引發還原失敗的所有忽略。 在複雜的解決方案通常會其他類型可能不支援還原的專案。 |
| **常見的原因** | 這種情形，不會匯入一般 props/目標自動匯入還原的專案。 如果專案不需要還原可以忽略此參數。 |
| **範例訊息** | *正在略過專案 'c:\a.csproj' 的還原。專案檔可能無效或遺漏目標所需的還原。* |

## <a name="unexpected-package-version-warnings"></a>未預期的封裝版本警告

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **問題** | 直接專案相依性是只有當更新的版本比指定的專案。 |
| **常見的原因** | 另一個相依性套件需要更高的版本，然後兩點封裝。 |
| **範例訊息** | *指定的相依性為 NuGet.Versioning (> = 3.5.0) 但 NuGet.Versioning 4.0.0 結果。* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **問題** | 封裝的相依性遺漏下限。 這不允許還原，若要尋找*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **常見的原因** | 這通常是撰寫錯誤的封裝。 |
| **範例訊息** | *NuGet.Packaging 4.0.0 不提供相依性 NuGet.Versioning (> 3.5.0) 下限 （內含）。3.6.0 的近似最符合項目已解決。* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **問題** | 封裝的相依性指定找不到的版本。 較高的版本來取代，這不同於封裝所撰寫針對。<br/><br/>這表示找不到該還原*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **常見的原因** | 封裝來源不包含預期的下限版本。 如果封裝應該沒有釋出，這可能是封裝撰寫錯誤。 |
| **範例訊息** | NuGet.Packaging 4.0.0 取決於 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。 5.0.0 的近似最符合項目已解決。 |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **問題** | 專案相依性不會定義繫結至較低。<br/><br/>這表示找不到該還原*最符合項目*。 每個還原會浮動由上至下嘗試尋找可以使用較低版本。 這表示該還原會檢查所有來源而不是使用套件已存在於使用者套件資料夾中的每次上線。 |
| **常見的原因** | 專案的*PackageReference* *版本*屬性應該更新為包含下限。 |
| **範例訊息** | *專案相依性 NuGet.Versioning (< = 9.0.0) doe 包含下限 （內含）。相依性版本，以確保結果一致還原包含下限。* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **問題** | 相依性套件指定版本上的條件約束的封裝版本高於還原最後都會解析。 |
| **常見的原因** | 最接近的 wins 解析封裝時。 圖形中的最接近的封裝可能會覆寫遠方的封裝。 |
| **範例訊息** | *偵測到套件降級： 3.5.0 來從 4.0.0 NuGet.Versioning。直接從要選取不同版本的專案參考封裝。<br/>NuGet.Packaging 3.5.0]-> [NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0]-> [NuGet.Configuration 4.0.0]-> [NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>解決衝突的警告

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **問題** | 解析封裝高於允許的相依性條件約束。 在某些情況下，這是有意如此，可以隱藏的警告。 |
| **常見的原因** | 直接在專案所參考的封裝將會覆寫從其他套件相依性條件約束。   |
| **範例訊息** | *外部相依性條件約束的偵測到的套件版本： x 1.0.0 需要的 y （= 1.0.0），但 y 2.0.0 的版本是已解決。* |

## <a name="package-fallback-warnings"></a>封裝後援警告

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **問題** | *PackageTargetFallback/AssetTargetFallback*用來從封裝中選取的資產。 這是要讓使用者知道資產可能不相容的 100%的警告。 |
| **常見的原因** | 封裝不支援專案架構。 |
| **範例訊息** | *已還原封裝 'NuGet.Versioning'，'可攜式 net45 + win8' 改為使用專案目標 framework 'netstandard1.5'。此封裝可能無法完全相容，您的專案。* |

## <a name="feed-warnings"></a>摘要的警告

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **問題** | 讀取摘要時，發生錯誤時`IgnoreFailedSources`設為 true，將它轉換成非嚴重警告。 這可能會包含任何訊息，而且是泛型。 |
| **常見的原因** | 來源無效。 |
| **範例訊息** | N/A |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet 的內部錯誤和警告

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **問題** | 從 NuGet 非特定的內部錯誤。 |
| **常見的原因** | 檢查記錄檔，如需詳細資訊 |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **問題** | 從 NuGet 非特定內部警告。 |
| **常見的原因** | 檢查記錄檔，如需詳細資訊 |
