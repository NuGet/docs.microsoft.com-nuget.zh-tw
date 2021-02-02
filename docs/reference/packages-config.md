---
title: NuGet packages.config 檔案參考
description: 在某些專案類型中，packages.config 會維護專案中所使用的 NuGet 套件清單。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: da682197d4a156f9dff8ce169aab449a5392ef41
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2021
ms.locfileid: "99260299"
---
# <a name="packagesconfig-reference"></a>packages.config 參考

`packages.config` 檔案用於某些專案類型，以維護專案所參考的套件清單。 這可讓 NuGet 在專案要傳輸到不同的電腦（例如組建伺服器）時，輕鬆地還原專案的相依性，而不需要所有套件。

如果使用的話， `packages.config` 通常位於專案根目錄中。 當第一個 NuGet 作業執行時，它會自動建立，但也可以在執行任何命令（例如）之前手動建立 `nuget restore` 。

使用 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 的專案不會使用 `packages.config` 。

## <a name="schema"></a>結構描述

結構描述十分簡單：標準 XML 標頭後面是包含一或多個 `<package>` 項目的單一 `<packages>` 節點，而每個參考都會有一個。 每個 `<package>` 項目都可以有下列屬性：

| 屬性 | 必要 | 描述 |
| --- | --- | --- |
| id | 是 | 套件的識別碼，例如 Newtonsoft.json 或 Microsoft.AspNet.Mvc。 | 
| version | 是 | 要安裝之套件的確切版本，例如 3.1.1 或 4.2.5.11-beta。 版本字串必須包含至少三個數字；第四個數字是選擇性的，即發行前版本尾碼。 不允許使用範圍。 | 
| targetFramework | 否 | 要在安裝套件時套用的[目標架構 Moniker (TFM)](target-frameworks.md)。 安裝套件時，這一開始設定為專案的目標。 因此，不同 `<package>` 項目可以有不同 TFM。 例如，如果您所建立專案的目標設為 .NET 4.5.2，則當時所安裝的套件將會使用 net452 的 TFM。 如果您稍後將專案的目標重設為 .NET 4.6，並新增更多套件，則它們會使用 net46 的 TFM。 專案目標與 `targetFramework` 屬性之間的不相容將會產生警告，在此情況下，您可以重新安裝受影響的套件。 | 
| allowedVersions | 否 | 此套件在套件更新期間套用的允許版本範圍 (請參閱[限制升級版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 它「不」會影響在安裝或還原作業期間所安裝的套件。 如需語法，請參閱[套件版本控制](../concepts/package-versioning.md#version-ranges)。 PackageManager UI 也會停用允許範圍之外的所有版本。 | 
| developmentDependency | 否 | 如果取用專案本身會建立 NuGet 套件，則將相依性的這個項目設定為 `true` 可在建立取用套件時防止包含該套件。 預設為 `false`。 | 

## <a name="examples"></a>範例

下列 `packages.config` 參照兩個相依性：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

下列 `packages.config` 參照九個套件，但因 `developmentDependency` 屬性而建置取用套件時不會包含 `Microsoft.Net.Compilers`。 Newtonsoft.Json 的參考也只會限制 8.x 和 9.x 版的更新。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
