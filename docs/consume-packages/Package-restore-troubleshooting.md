---
title: 針對 Visual Studio 中的 NuGet 套件還原進行疑難排解
description: Visual Studio 中常見的 NuGet 還原錯誤描述，以及如何針對這些錯誤進行疑難排解。
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 9f680a714717d1bde0472f2e1266cacfd8bd4d5f
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699722"
---
# <a name="troubleshooting-package-restore-errors"></a>對套件還原錯誤進行疑難排解

本文著重於還原套件時常見的錯誤及其解決步驟。 

套件還原會嘗試將所有套件相依性安裝到符合專案檔 (*.csproj*) 或您的 *packages.config* 檔案中套件參考的正確狀態。  (在 Visual Studio 中，參考會出現在 [相依性 **\ NuGet]** 或 [ **參考** ] 節點底下的方案總管中。 ) 若要遵循還原封裝的必要步驟，請參閱 [還原套件](../consume-packages/package-restore.md#restore-packages)。 如果專案檔 (*.csproj*) 或您的 *packages.config* 檔案中的套件參考不正確 (不符合您在套件還原之後所需的狀態)，則您需要安裝套件或更新套件，而不是使用套件還原。

如果此處的指示不適用於您的情況，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，讓我們能更仔細審視您的案例。 請勿使用可能出現在本頁面的「本頁對您有幫助嗎？」 控制項，因為這無法讓我們與您連絡以取得詳細資訊。

## <a name="quick-solution-for-visual-studio-users"></a>適用於 Visual Studio 使用者的快速解決方案

如果您使用 Visual Studio，請先以下列方式啟用套件還原。 否則，請繼續瀏覽後續各節。

1. 選取 [工具] > [NuGet 套件管理員] > [套件管理員設定] 功能表命令。
1. 設定 [套件還原] 下的兩個選項。
1. 選取 [確定]。
1. 再次建置您的專案。

![在 [工具/選項] 中啟用 NuGet 套件還原](../consume-packages/media/restore-01-autorestoreoptions.png)

這些設定也可以在您的 `NuGet.config` 檔案中變更；請參閱[同意](#consent)一節。 如果您的專案是使用整合 MSBuild 套件還原的舊版專案，您可能需要[遷移](package-restore.md#migrate-to-automatic-package-restore-visual-studio)至自動套件還原。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>此專案參考的 NuGet 套件不在這部電腦上

完整的錯誤訊息：

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

當您嘗試建置包含一或多個 NuGet 套件參考的專案，但這些套件目前並未安裝在電腦上或位於專案中時，就會發生這項錯誤。

- 使用 [PackageReference](package-references-in-project-files.md) 管理格式時，此錯誤可能是來自 packages.config 到 PackageReference 遷移的剩餘問題，需要從專案檔中 [手動移除](../resources/NuGet-FAQ.md#working-with-packages) 。
- 當使用 [packages.config](../reference/packages-config.md) 時，此錯誤表示套件並未安裝在解決方案根目錄的 `packages` 資料夾中。

當您從原始檔控制或另一個下載處取得專案的原始程式碼時，通常就會發生這種情況。 套件通常會從原始檔控制或下載中省略，因為可以從類似 nuget.org 的套件摘要中還原 (請參閱[套件和原始檔控制](Packages-and-Source-Control.md))。 包含套件反而會使存放庫膨脹，或建立不必要的大型 .zip 檔案。

如果您的專案檔包含套件位置的絕對路徑，而您又移動了專案，也會發生錯誤。

請使用下列其中一種方法來還原套件：

- 如果您移動了專案檔，請直接編輯檔案以更新套件參考。
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([自動還原](package-restore.md#restore-packages-automatically-using-visual-studio)或[手動還原](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

成功還原之後，套件應該存在於 *global-packages* 資料夾中。 對於使用 PackageReference 的專案，還原應重新建立 `obj/project.assets.json` 檔案；針對使用 `packages.config` 的專案，套件應該會出現在專案的 `packages` 資料夾中。 專案現在應可順利建置。 如果沒有，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們與您連絡。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>找不到資產檔案 project.assets.json

完整的錯誤訊息：

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

當使用 PackageReference 管理格式時，`project.assets.json` 檔案會維護專案的相依性關係圖，此圖是用來確認電腦上已安裝所有必要套件的。 因為此檔案是透過套件還原動態產生的，因此通常不會新增到原始檔控制。 因此當使用不會自動還原套件的 `msbuild` 之類的工具建立專案時，會發生此錯誤。

在此情況下，請在執行 `msbuild -t:restore` 後接著執行 `msbuild`，或使用 `dotnet build` (會自動還原套件)。 您也可以使用[上一節](#missing)中的任何一個套件還原方法。

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

> [!Important]
> 如果您直接在 `nuget.config` 中編輯 `packageRestore` 設定，請重新啟動 Visual Studio，讓選項對話方塊顯示目前的值。

## <a name="other-potential-conditions"></a>其他可能的情況

- 您可能會因為遺失檔案而遇到建置錯誤，會有訊息指出應使用 NuGet 還原加以下載。 不過，執行還原時有可能會顯示「所有套件均已安裝，沒有可還原的項目」。 在此情況下，請刪除 `packages` 資料夾 (使用 `packages.config` 時) 或 `obj/project.assets.json` 檔案 (使用 PackageReference 時)，並再次執行還原。 如果錯誤持續發生，請從命令列使用 `nuget locals all -clear` 或 `dotnet nuget locals all --clear` 以清除 *global-packages* 和快取資料夾，如 [管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述。

- 從原始檔控制取得專案時，您的專案資料夾可能會設定成唯讀。 請變更資料夾的權限，然後再次嘗試還原套件。

- 您使用的可能是舊版 NuGet。 請查看 [nuget.org/downloads](https://www.nuget.org/downloads) 以取得最新的建議版本。 若是 Visual Studio 2015，建議使用 3.6.0。

如果您遇到其他問題，[請在 GitHub 上提出發生的問題](https://github.com/NuGet/docs.microsoft.com-nuget/issues)以便我們向您取得更多詳細資料。
