---
title: "針對 Visual Studio 中的 NuGet 套件還原進行疑難排解 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio 中常見的 NuGet 還原錯誤描述，以及如何針對這些錯誤進行疑難排解。"
keywords: "NuGet 套件還原, 還原套件, 進行疑難排解, 疑難排解"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>對套件還原錯誤進行疑難排解

本文著重於還原套件時常見的錯誤及其解決步驟。 如需還原套件的完整詳細資料，請參閱[套件還原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。

如果此處的指示不適用於您的情況，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，讓我們能更仔細審視您的案例。 請勿使用可能出現在本頁面的「本頁對您有幫助嗎？」 控制項，因為這無法讓我們與您連絡以取得詳細資訊。

## <a name="quick-solution-for-visual-studio-users"></a>適用於 Visual Studio 使用者的快速解決方案

如果您使用 Visual Studio，請先以下列方式啟用套件還原。 否則，請繼續瀏覽後續各節。

1. 選取 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令。
1. 設定 [套件還原] 下的兩個選項。
1. 選取 [確定]。
1. 再次建置您的專案。

![在 [工具/選項] 中啟用 NuGet 套件還原](../consume-packages/media/restore-01-autorestoreoptions.png)

這些設定也可以在您的 `NuGet.config` 檔案中變更；請參閱[同意](#consent)一節。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>此專案參考的 NuGet 套件不在這部電腦上

完整的錯誤訊息：

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

當您嘗試建置包含一或多個 NuGet 套件參考的專案，但這些套件目前並未在專案中快取時，就會發生這項錯誤。 (如該專案使用 `packages.config`，套件會在位於解決方案根目錄的 `packages` 資料夾中快取；或者，如果該專案使用 PackageReference 格式，則會在 `obj/project.assets.json` 檔案之中。)

當您從原始檔控制或另一個下載處取得專案的原始程式碼時，通常就會發生這種情況。 套件通常會從原始檔控制或下載中省略，因為可以從類似 nuget.org 的套件摘要中還原 (請參閱[套件和原始檔控制](Packages-and-Source-Control.md))。 包含套件反而會使存放庫膨脹，或建立不必要的大型 .zip 檔案。

請使用下列其中一種方法來還原套件：

- 在 Visual Studio 中，選取 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令，設定 [套件還原] 下的兩個選項，然後選取 [確定]，以啟用套件還原。 然後再次建置解決方案。
- 若是 .NET Core 專案，請執行 `dotnet restore` 或 `dotnet build` (會自動執行還原)。
- 在命令列上執行 `nuget restore` (除了以 `dotnet` 建立的專案在此情況下會使用 `dotnet restore`)。
- 對於使用 PackageReference 格式的專案，在命令列上執行 `msbuild /t:restore`。

成功還原之後，您應該會看到 `packages` 資料夾 (使用 `packages.config` 時) 或 `obj/project.assets.json` 檔案 (使用 PackageReference 時)。 專案現在應可順利建置。 如果沒有，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們與您連絡。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>找不到資產檔案 project.assets.json

完整的錯誤訊息：

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

這項錯誤的發生原因與[上一節](#missing)說明的相同，補救方法也一樣。 例如，在已經從原始檔控制取得的 .NET Core 專案上執行 `msbuild`，不會自動還原套件。 在此情況下，請在執行 `msbuild /t:restore` 後接著執行 `msbuild`，或使用 `dotnet build` (會自動還原套件)。

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>有一或多個 NuGet 套件必須還原，但因為未獲得同意而無法還原

完整的錯誤訊息：

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

此錯誤指出您的 NuGet 組態已停用套件還原。

您可以在 Visual Studio 中變更適用的設定，如先前在[適用於 Visual Studio 使用者的快速解決方案](#quick-solution-for-visual-studio-users)所述。

您也可以直接在適用的 `nuget.config` 檔案上編輯這些設定 (在 Windows 上通常為 `%AppData%\NuGet\NuGet.Config`，在 Mac/Linux 上則為 `~/.nuget/NuGet/NuGet.Config`)。 請確認 `packageRestore` 底下的 `enabled` 和 `automatic` 金鑰設定為 True：

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

請注意，如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。

## <a name="other-potential-conditions"></a>其他可能的情況

- 您可能會因為遺失檔案而遇到建置錯誤，會有訊息指出應使用 NuGet 還原加以下載。 不過，執行還原時有可能會顯示「所有套件均已安裝，沒有可還原的項目」。 在此情況下，請刪除 `packages` 資料夾 (使用 `packages.config` 時) 或 `obj/project.assets.json` 檔案 (使用 PackageReference 時)，並再次執行還原。

- 從原始檔控制取得專案時，您的專案資料夾可能會設定成唯讀。 請變更資料夾的權限，然後再次嘗試還原套件。

- 您使用的可能是舊版 NuGet。 請查看 [nuget.org/downloads](https://www.nuget.org/downloads) 以取得最新的建議版本。 若是 Visual Studio 2015，建議使用 3.6.0。

如果您遇到其他問題，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們向您取得更多詳細資料。