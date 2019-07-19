---
title: NuGet CLI 長路徑支援
description: Nuget .exe 長路徑支援的參考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327675"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="944e3-103">長路徑支援 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="944e3-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="944e3-104">**適用于:** 所有&bullet; **支援的版本:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="944e3-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="944e3-105">Nuget.exe 4.8 和更新版本支援檔案和目錄的長路徑, 適用于套件、還原、安裝和大多數其他需要檔案路徑的案例。</span><span class="sxs-lookup"><span data-stu-id="944e3-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="944e3-106">需要的作業系統</span><span class="sxs-lookup"><span data-stu-id="944e3-106">Required Operating System</span></span>

-   <span data-ttu-id="944e3-107">Windows 10 (版本1607或更新版本)</span><span class="sxs-lookup"><span data-stu-id="944e3-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="944e3-108">Windows 10 (2015 年7月版本或1511版) 如果您將 .NET Framework 升級為4.6.2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="944e3-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="944e3-109">Windows Server 2016 (所有版本)</span><span class="sxs-lookup"><span data-stu-id="944e3-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="944e3-110">啟用「Win32 長路徑」群組原則</span><span class="sxs-lookup"><span data-stu-id="944e3-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="944e3-111">其中一項需要藉由設定群組原則, 在這些系統上啟用長路徑支援。</span><span class="sxs-lookup"><span data-stu-id="944e3-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="944e3-112">步驟</span><span class="sxs-lookup"><span data-stu-id="944e3-112">Steps:</span></span>
1. <span data-ttu-id="944e3-113">啟動**群組原則編輯器**-在 [開始搜尋] 列中輸入 "編輯群組原則", 或從 [執行] 命令執行 "gpedit.msc" (Windows-R)。</span><span class="sxs-lookup"><span data-stu-id="944e3-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="944e3-114">在 **本機群組原則編輯器**中, 啟用 本機電腦原則/電腦設定/系統管理範本/所有設定/啟用 Win32 長路徑。</span><span class="sxs-lookup"><span data-stu-id="944e3-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="944e3-116">啟用其他 NuGet 工具以支援長路徑</span><span class="sxs-lookup"><span data-stu-id="944e3-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="944e3-117">Dotnet CLI 支援長路徑, 而不論作業系統或版本為何。</span><span class="sxs-lookup"><span data-stu-id="944e3-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="944e3-118">Visual Studio 或 msbuild t:restore 尚未支援長路徑。</span><span class="sxs-lookup"><span data-stu-id="944e3-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="944e3-119">使用 NuGet 程式庫執行還原和其他命令的軟體, 將會在 Nuget.exe 運作所在的相同系統上支援長路徑, 如果它們也在其 windows 資訊清單中設定 longPathAware, 並透過 App.config[將 UseLegacyPathHandling 設為 false查看詳細資訊](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="944e3-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

