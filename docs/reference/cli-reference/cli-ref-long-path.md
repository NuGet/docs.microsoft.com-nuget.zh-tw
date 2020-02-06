---
title: NuGet CLI 長路徑支援
description: Nuget .exe 長路徑支援的參考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036951"
---
# <a name="long-path-support-nuget-cli"></a>長路徑支援（NuGet CLI）

**適用于：** 所有 &bullet;**支援的版本：** 4.8 +

Nuget.exe 4.8 和更新版本支援檔案和目錄的長路徑，適用于套件、還原、安裝和大多數其他需要檔案路徑的案例。

## <a name="required-operating-system"></a>需要的作業系統

-   Windows 10 （版本1607或更新版本）
-   Windows 10 （2015年7月版本或1511版）如果您將 .NET Framework 升級為4.6.2 或更新版本。
-   Windows Server 2016 （所有版本）

## <a name="enable-win32-long-paths-group-policy"></a>啟用「Win32 長路徑」群組原則

其中一項需要藉由設定群組原則，在這些系統上啟用長路徑支援。

步驟：
1. 啟動**群組原則編輯器**-在 [開始搜尋] 列中輸入 "編輯群組原則"，或從 [執行] 命令執行 "gpedit.msc" （Windows-R）。
2. 在 **本機群組原則編輯器**中，啟用 本機電腦原則/電腦設定/系統管理範本/所有設定/啟用 Win32 長路徑。

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> 啟用其他 NuGet 工具以支援長路徑
>
> -   Dotnet CLI 支援長路徑，而不論作業系統或版本為何。
> -   Visual Studio 或 `msbuild -t:restore` 尚不支援長路徑。
> -   使用 NuGet 程式庫執行還原和其他命令的軟體，將會在 Nuget.exe 運作所在的相同系統上支援長路徑，如果它們也在其 windows 資訊清單中設定 `longPathAware`，並透過 App.config 設定 `UseLegacyPathHandling` `false`，[請參閱詳細資訊](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

