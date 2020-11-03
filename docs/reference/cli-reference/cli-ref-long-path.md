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
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="e1394-103"> (NuGet CLI 的完整路徑支援) </span><span class="sxs-lookup"><span data-stu-id="e1394-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="e1394-104">**適用于：** 所有 &bullet; **支援的版本：** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="e1394-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="e1394-105">針對套件、還原、安裝和大部分其他需要檔案路徑的案例，NuGet.exe 4.8 和更新版本支援檔案和目錄的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="e1394-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="e1394-106">需要的作業系統</span><span class="sxs-lookup"><span data-stu-id="e1394-106">Required Operating System</span></span>

-   <span data-ttu-id="e1394-107">Windows 10 (1607 版或更新版本) </span><span class="sxs-lookup"><span data-stu-id="e1394-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="e1394-108">如果您將 .NET Framework 升級至4.6.2 版或更新版本，Windows 10 (2015 年7月發行版本或) 1511 版。</span><span class="sxs-lookup"><span data-stu-id="e1394-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="e1394-109">Windows Server 2016 (所有版本) </span><span class="sxs-lookup"><span data-stu-id="e1394-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="e1394-110">啟用 [Win32 長路徑] 群組原則</span><span class="sxs-lookup"><span data-stu-id="e1394-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="e1394-111">您必須藉由設定群組原則，在這些系統上啟用長路徑支援。</span><span class="sxs-lookup"><span data-stu-id="e1394-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="e1394-112">步驟：</span><span class="sxs-lookup"><span data-stu-id="e1394-112">Steps:</span></span>
1. <span data-ttu-id="e1394-113">啟動 **群組原則編輯器** -在開始搜尋列中輸入「編輯群組原則」，或從 Windows-R) 的 run 命令 (執行 "gpedit.msc"。</span><span class="sxs-lookup"><span data-stu-id="e1394-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="e1394-114">在 **本機群組原則編輯器** 中，啟用 [本機電腦原則/電腦設定/系統管理範本/所有設定/啟用 Win32 長路徑]。</span><span class="sxs-lookup"><span data-stu-id="e1394-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![長路徑原則](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="e1394-116">啟用其他 NuGet 工具以支援長路徑</span><span class="sxs-lookup"><span data-stu-id="e1394-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="e1394-117">無論作業系統或版本為何，Dotnet CLI 都支援長路徑。</span><span class="sxs-lookup"><span data-stu-id="e1394-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="e1394-118">Visual Studio 或 `msbuild -t:restore` 還不支援長路徑。</span><span class="sxs-lookup"><span data-stu-id="e1394-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="e1394-119">使用 NuGet 程式庫執行還原和其他命令的軟體，會在 NuGet.exe 運作的相同系統上支援長路徑（如果它們也是 `longPathAware` 在其 windows 資訊清單中設定，並透過 `UseLegacyPathHandling` App.Config 設定為， `false` [請參閱詳細資訊](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)）。</span><span class="sxs-lookup"><span data-stu-id="e1394-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>