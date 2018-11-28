---
title: NuGet CLI 長路徑支援
description: Nuget.exe 長路徑支援的參考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453490"
---
# <a name="long-path-support-nuget-cli"></a>長路徑支援 (NuGet CLI)

**適用於：** 所有&bullet;**支援的版本：** 4.8 +

NuGet.exe 4.8 及更新版本支援長路徑的檔案和目錄的案例，例如組件、 還原、 安裝和大部分需要的檔案路徑的其他案例。

## <a name="required-operating-system"></a>所需的作業系統

-   Windows 10 （版本 1607 或更新版本）
-   Windows 10 （2015 年 7 月版本或版本 1511年） 如果您升級.NET Framework 版本 4.6.2 或更新版本。
-   Windows Server 2016 （所有版本）

## <a name="enable-win32-long-paths-group-policy"></a>啟用 「 Win32 長路徑 」 群組原則

您需要藉由設定群組原則啟用長路徑支援，這些系統上。

步驟：
1. 啟動**群組原則編輯器**-輸入 [開始搜尋] 列中的 [編輯群組原則]，或從 [執行] 命令 (Windows-R) 執行 「 gpedit.msc"。
2. 在**本機群組原則編輯器**，啟用 「 本機電腦原則/電腦設定/系統管理範本/所有的設定/啟用 Win32 長的路徑 」。

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> 啟用其他的 NuGet 工具，以支援長路徑
>
> -   Dotnet CLI 支援不論作業系統或版本的完整路徑。
> -   Visual Studio 或 msbuild-t： 還原尚不支援長路徑。
> -   軟體使用 NuGet 程式庫來執行還原，以及其他命令，將支援長路徑的相同系統上，NuGet.exe 適用於，如果同時設定在其 windows longPathAware 並且設定 UseLegacyPathHandling 設為 false，透過 App.Config [請參閱詳細的資訊](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

