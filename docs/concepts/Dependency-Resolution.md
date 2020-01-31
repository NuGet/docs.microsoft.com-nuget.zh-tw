---
title: NuGet 套件相依性解析
description: 在 NuGet 2.x 和 NuGet 3.x+ 中解析和安裝 NuGet 套件相依性之程序的詳細資料。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: c6f50e6eb21826afebcdcd4045c7ab8b6e6489e3
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813321"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet 如何解析套件相依性

只要安裝或重新安裝套件 (包含安裝為[還原](../consume-packages/package-restore.md)程序一部分的套件)，NuGet 也會安裝與這個第一個套件相依的任何其他套件。

這些立即相依性接著會有其自己的相依性，而這會繼續到任意深度。 這會產生所謂的「相依性圖形」，以描述所有層級上套件之間的關聯性。

多個套件具有相同的相依性時，同一個套件識別碼可能會多次出現在圖形中，但可能具有不同版本的條件約束。 不過，專案中只能使用一個指定套件的版本，因此 NuGet 必須選擇要使用的版本。 確切的處理序取決於所使用的套件管理格式。

## <a name="dependency-resolution-with-packagereference"></a>使用 PackageReference 的相依性解析

使用 PackageReference 格式來將套件安裝至專案時，NuGet 會新增適當檔案中一般套件圖形的參考，並事先解決衝突。 此程序稱為「可轉移還原」。 重新安裝或還原套件則是下載圖形中所列套件的程序，導致更快速且更容易預測的組建。 您也可以利用萬用字元 (浮動) 版本 (例如 2.8.\*)，避免用戶端電腦和組建伺服器上對 `nuget update` 的昂貴且容易出錯的呼叫。

若 NuGet 還原程序在建置之前執行，就會先解析記憶體中的相依性，然後將產生的圖形寫入稱為 `project.assets.json` 的檔案。 如果[已啟用鎖定檔案功能](../consume-packages/package-references-in-project-files.md#locking-dependencies)，它也會將已解析的相依性寫入名為 `packages.lock.json` 的鎖定檔案。
資產檔案位於 `MSBuildProjectExtensionsPath`，其預設為專案的 'obj' 資料夾。 MSBuild 接著會讀取這個檔案，並將它轉譯成一組可找到可能參考的資料夾，然後將它們新增至記憶體中的專案樹狀結構。

`project.assets.json` 檔案是暫時的，不應該新增至原始程式碼控制。 它預設會列在 `.gitignore` 和 `.tfignore` 中。 請參閱[套件和原始檔控制](../consume-packages/packages-and-source-control.md)。

### <a name="dependency-resolution-rules"></a>相依性解析規則

可轉移還原會套用四個主要規則以解析相依性：最低適用版本、浮動版本、最近獲取和鄰近相依性。

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>最低適用版本

最低適用版本規則可還原依其相依性所定義之最低可能版本的套件。 除非宣告為[浮動](#floating-versions)，否則它也適用於與應用程式或類別庫的相依性。

例如，在下圖中，將 1.0-beta 視為低於 1.0，因此 NuGet 會選擇 1.0 版：

![選擇最低適用版本](media/projectJson-dependency-1.png)

在下圖中，摘要上未提供 2.1 版，但因為版本條件約束 >= 2.1，所以 NuGet 會挑選它可找到的下一個最低版本，在此情況下為 2.2：

![選擇摘要上下一個可用的最低版本](media/projectJson-dependency-2.png)

如果應用程式指定不適用於摘要的確切版本號碼 (例如 1.2)，則嘗試安裝或還原套件時，NuGet 會失敗並發生錯誤：

![NuGet 會在確切套件版本無法使用時產生錯誤](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>浮動 (萬用字元) 版本

浮動或萬用字元相依性版本是使用 \* 萬用字元所指定，與 6.0.\* 相同。 此版本規格指出「使用最新的 6.0.x 版」；4.\* 表示「使用最新的 4.x 版」。 使用萬用字元，可讓相依性套件繼續發展，而不需要變更取用中應用程式 (或套件)。

使用萬用字元時，NuGet 會解析符合版本模式的套件最高版本，例如，6.0.\* 所取得之套件最高版本的開頭為 6.0：

![在要求浮動版本 6.0.* 時選擇 6.0.1 版](media/projectJson-dependency-4.png)

> [!Note]
> 如需萬用字元和發行前版本之行為的資訊，請參閱[套件版本控制](package-versioning.md#version-ranges-and-wildcards)。


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>最近獲取

應用程式的套件圖形包含相同套件的不同版本時，NuGet 會選擇最接近圖形中應用程式的套件，並忽略所有其他套件。 此行為允許應用程式覆寫相依性圖形中的任何特定套件版本。

在下列範例中，應用程式直接與版本條件約束 >=2.0 的套件 B 相依。 應用程式也與套件 A 相依，而套件 A 接著也與套件 B 相依，但具有 >=1.0 條件約束。 因為與套件 B 2.0 的相依性較接近圖形中的應用程式，所以會使用該版本：

![使用最近獲取規則的應用程式](media/projectJson-dependency-5.png)

>[!Warning]
> 最近獲取規則可能會導致套件版本降級，因此可能中斷圖形中的其他相依性。 因此，會套用此規則，並發出警告來提醒使用者。

此規則也會讓大型相依性圖形具有更高的效率 (例如具有 BCL 套件的圖形)，因為忽略指定的相依性之後，NuGet 也會忽略與圖形該分支的所有剩餘相依性。 例如，在下圖中，因為使用套件 C 2.0，所以 NuGet 會忽略圖形中任何參照舊版套件 C 的分支：

![NuGet 忽略圖形中的套件時，會忽略整個分支](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>鄰近相依性

從應用程式中於圖形的相同距離參照不同的套件版本時，NuGet 會使用符合所有版本需求的最低版本 (如同使用就像[最低適用版本](#lowest-applicable-version)和[浮動版本](#floating-versions)規則一樣)。 例如，在下圖中，2.0 版的套件 B 符合另一個 >=1.0 條件約束，因此予以使用：

![使用符合所有條件約束的較低版本來解析鄰近相依性](media/projectJson-dependency-7.png)

在某些情況下，無法符合所有版本需求。 如下所示，如果套件 A 只需要套件 B 1.0，而套件 C 需要套件 B >=2.0，則 NuGet 無法解析相依性，而且會產生錯誤。

![因確切版本需求而有無法解析的相依性](media/projectJson-dependency-8.png)

在這些情況下，最上層取用者 (應用程式或套件) 應該新增其與套件 B 的專屬直接相依性，因此套用[最近者獲取](#nearest-wins)規則。

## <a name="dependency-resolution-with-packagesconfig"></a>使用 packages.config 的相依性解析

使用 `packages.config`，專案的相依性會寫入至 `packages.config` 作為一般清單。 這些套件的任何相依性也會寫入相同的清單中。 安裝套件之後，NuGet 也可能會修改 `.csproj` 檔案、`app.config`、`web.config` 和其他個別檔案。

使用 `packages.config`，NuGet 會嘗試在每個個別套件安裝期間解決相依性衝突。 也就是說，如果套件 A 已安裝並與套件 B 相依，而且套件 B 已列在 `packages.config` 中作為其他項目的相依性，則 NuGet 會比較所要求的套件 B 版本，並嘗試找到符合所有版本條件約束的版本。 具體來說，NuGet 會選取符合相依性的較低 *major.minor* 版本。

根據預設，NuGet 2.8 會尋找最低的修補程式版本 (請參閱 [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies))。 您可以透過 `Nuget.Config` 中的 `DependencyVersion` 屬性和命令列上的 `-DependencyVersion` 參數，來控制此設定。  

針對較大的相依性圖形，解析相依性的 `packages.config` 程序會更為複雜。 每個新套件安裝都需要周遊整個圖形，而且會引發版本衝突機會。 發生衝突時，會停止安裝，並讓專案處於不定狀態，特別是對專案檔本身進行可能的修改。 使用其他套件管理格式時，這不是問題。

## <a name="managing-dependency-assets"></a>管理相依性資產

使用 PackageReference 格式時，您可以控制從相依性流入最上層專案的資產。 如需詳細資訊，請參閱 [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

最上層專案本身是套件時，也可以搭配使用 `include` 和 `exclude` 屬性與 `.nuspec` 檔案中所列相依性來控制此流量。 請參閱 [.nu-/spec 參考 - 相依性](../reference/nuspec.md#dependencies)。

## <a name="excluding-references"></a>排除參考

在某些情況下，可能會在專案中多次參考同名的組件，並產生設計階段和建置時間錯誤。 請考慮包含 `C.dll` 之自訂版本的專案，並參考也包含 `C.dll` 的套件 C。 同時，專案也與套件 B 相依，而套件 B 也與套件 C 和 `C.dll` 相依。 因此，NuGet 無法決定要使用的 `C.dll`，但您不能只移除專案與套件 C 的相依性，因為套件 B 也與其相依。

若要解決此問題，您必須直接參考想要的 `C.dll` (或使用另一個參考正確項目的套件)，然後新增與排除所有資產之套件 C 的相依性。 這是根據使用中的套件管理格式所進行，如下所示：

- [PackageReference](../consume-packages/package-references-in-project-files.md)：在相依性中新增 `ExcludeAssets="All"`：

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`：從 `.csproj` 檔案中移除套件 C 的參考，讓它只參考您想要的 `C.dll` 版本。
    
## <a name="dependency-updates-during-package-install"></a>套件安裝期間的相依性更新 

如果已符合相依性版本，則不會在其他套件安裝期間更新相依性。 例如，請考慮使用與套件 B 相依並指定 1.0 作為版本號碼的套件 A。 來源存放庫包含 1.0、1.1 和 1.2 版的套件 B。如果在已包含 B 1.0 版的專案中安裝 A，則 B 1.0 仍會維持使用中狀態，因為它符合版本限制。 不過，如果套件 A 要求 1.1 版或更高版本的 B，則會安裝 B 1.2。 

## <a name="resolving-incompatible-package-errors"></a>解決不相容的套件錯誤

在套件還原作業期間，您可能會看到「一或多個套件不相容...」錯誤，或套件與專案目標架構「不相容」。

專案中參考的一或多個套件未指出它們支援專案的目標架構時，會發生此錯誤；也就是說，套件在其 `lib` 資料夾中未包含與專案相容之目標架構的適合 DLL (如需清單，請參閱[目標架構](../reference/target-frameworks.md))。 

例如，如果專案的目標設為 `netstandard1.6`，而且您嘗試安裝只包含 `lib\net20` 和 `\lib\net45` 資料夾中 DLL 的套件，則會看到套件和其相依項的下列這類訊息：

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

若要解決不相容，請執行下列其中一項：

- 將專案的目標重新設為您想要使用的套件所支援的架構。
- 請連絡套件作者，並與他們合作以新增所選擇架構的支援。 基於此用途，[nuget.org](https://www.nuget.org/) 上的每個套件列出頁面都具有**連絡人負責人**連結。
