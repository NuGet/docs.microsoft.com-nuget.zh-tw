---
title: NuGet CLI 長期路徑支援
description: nuget.exe 長路徑支援的參考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238188"
---
# <a name="long-path-support-nuget-cli"></a> (NuGet CLI 的完整路徑支援) 

**適用于：** 所有 &bullet; **支援的版本：** 4.8 +

針對套件、還原、安裝和大部分其他需要檔案路徑的案例，NuGet.exe 4.8 和更新版本支援檔案和目錄的完整路徑。

## <a name="required-operating-system"></a>需要的作業系統

-   Windows 10 (1607 版或更新版本) 
-   如果您將 .NET Framework 升級至4.6.2 版或更新版本，Windows 10 (2015 年7月發行版本或) 1511 版。
-   Windows Server 2016 (所有版本) 

## <a name="enable-win32-long-paths-group-policy"></a>啟用 [Win32 長路徑] 群組原則

您必須藉由設定群組原則，在這些系統上啟用長路徑支援。

步驟：
1. 啟動 **群組原則編輯器** -在開始搜尋列中輸入「編輯群組原則」，或從 Windows-R) 的 run 命令 (執行 "gpedit.msc"。
2. 在 **本機群組原則編輯器** 中，啟用 [本機電腦原則/電腦設定/系統管理範本/所有設定/啟用 Win32 長路徑]。

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> 啟用其他 NuGet 工具以支援長路徑
>
> -   無論作業系統或版本為何，Dotnet CLI 都支援長路徑。
> -   Visual Studio 或 `msbuild -t:restore` 還不支援長路徑。
> -   使用 NuGet 程式庫執行還原和其他命令的軟體，會在 NuGet.exe 運作的相同系統上支援長路徑（如果它們也是 `longPathAware` 在其 windows 資訊清單中設定，並透過 `UseLegacyPathHandling` App.Config 設定為， `false` [請參閱詳細資訊](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)）。