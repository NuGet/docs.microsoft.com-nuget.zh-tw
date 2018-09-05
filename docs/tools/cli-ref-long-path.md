---
title: NuGet CLI 長路徑支援
description: Nuget.exe 長路徑支援的參考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547822"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="52794-103">長路徑支援 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="52794-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="52794-104">**適用於：** 所有&bullet;**支援的版本：** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="52794-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="52794-105">NuGet.exe 4.8 及更新版本支援長路徑的檔案和目錄的案例，例如組件、 還原、 安裝和大部分需要的檔案路徑的其他案例。</span><span class="sxs-lookup"><span data-stu-id="52794-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="52794-106">所需的作業系統</span><span class="sxs-lookup"><span data-stu-id="52794-106">Required Operating System</span></span>

-   <span data-ttu-id="52794-107">Windows 10 （版本 1607 或更新版本）</span><span class="sxs-lookup"><span data-stu-id="52794-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="52794-108">Windows 10 （2015 年 7 月版本或版本 1511年） 如果您升級.NET Framework 版本 4.6.2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="52794-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="52794-109">Windows Server 2016 （所有版本）</span><span class="sxs-lookup"><span data-stu-id="52794-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="52794-110">啟用 「 Win32 長路徑 」 群組原則</span><span class="sxs-lookup"><span data-stu-id="52794-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="52794-111">您需要藉由設定群組原則啟用長路徑支援，這些系統上。</span><span class="sxs-lookup"><span data-stu-id="52794-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="52794-112">步驟：</span><span class="sxs-lookup"><span data-stu-id="52794-112">Steps:</span></span>
1. <span data-ttu-id="52794-113">啟動**群組原則編輯器**-輸入 [開始搜尋] 列中的 [編輯群組原則]，或從 [執行] 命令 (Windows-R) 執行 「 gpedit.msc"。</span><span class="sxs-lookup"><span data-stu-id="52794-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="52794-114">在**本機群組原則編輯器**，啟用 「 本機電腦原則/電腦設定/系統管理範本/所有的設定/啟用 Win32 長的路徑 」。</span><span class="sxs-lookup"><span data-stu-id="52794-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="52794-116">啟用其他的 NuGet 工具，以支援長路徑</span><span class="sxs-lookup"><span data-stu-id="52794-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="52794-117">Dotnet CLI 支援不論作業系統或版本的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="52794-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="52794-118">Visual Studio 或 msbuild /t: restore 尚不支援長路徑。</span><span class="sxs-lookup"><span data-stu-id="52794-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="52794-119">軟體使用 NuGet 程式庫來執行還原，以及其他命令，將支援長路徑的相同系統上，NuGet.exe 適用於，如果同時設定在其 windows longPathAware 並且設定 UseLegacyPathHandling 設為 false，透過 App.Config [請參閱詳細的資訊](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="52794-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

