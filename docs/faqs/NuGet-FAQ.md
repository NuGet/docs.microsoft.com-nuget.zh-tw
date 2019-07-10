---
title: NuGet 常見問題集
description: 在命令列上和 Visual Studio 中使用 NuGet 的常見問題和解答
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8bc6af90638408847af6e97cebcbf428f1d5d886
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467755"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 常見問題集

**執行 NuGet 所需的作業為何？**

[安裝指南](../install-nuget-client-tools.md)包含 UI 和命令列工具的所有資訊。

**NuGet 支援 Mono 嗎？**

命令列工具 `nuget.exe` 會在 Mono 3.2+ 下建置並執行，而且可以在 Mono 中建立套件。

雖然 `nuget.exe` 完整運作於 Windows 上，但是 Linux 和 OS X 上已有已知問題。請參閱 GitHub 上的 [Mono 問題](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。

[圖形化用戶端](https://github.com/mrward/monodevelop-nuget-addin)可作為 MonoDevelop 的增益集。

**如何判斷套件所包含的內容，以及它對我的應用程式而言是否穩定而且有用？**

了解套件的主要來源是其在 nuget.org 上的清單頁面 (或另一個私人摘要)。 nuget.org 上的每個套件頁面都會包含套件的描述、其版本歷程記錄和使用量統計資料。 套件頁面上的 [資訊]  區段也會包含專案網站的連結，而在專案網站中，您一般可以找到許多範例和其他文件協助您了解如何使用套件。

如需詳細資訊，請參閱[尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)。

## <a name="nuget-in-visual-studio"></a>Visual Studio 中的 NuGet

**在不同的 Visual Studio 產品中，如何支援 NuGet？**

- Windows 上的 Visual Studio 支援[套件管理員 UI](../tools/package-manager-ui.md) 和[套件管理員主控台](../tools/package-manager-console.md)。
- Visual Studio for Mac 具有內建 NuGet 功能，如[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)中所述。
- Visual Studio Code (所有平台) 沒有任何直接 NuGet 整合。 請使用 [NuGet CLI](../tools/nuget-exe-cli-reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。
- Azure DevOps 提供[還原 NuGet 套件的建置步驟](/vsts/build-release/tasks/package/nuget)。 您也可以[在 Azure DevOps 上裝載私人 NuGet 套件摘要](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)。

**如何檢查已安裝 NuGet 工具的確切版本？**

在 Visual Studio 中，使用 [說明] > [關於 Microsoft Visual Studio]  命令，並查看 [NuGet 套件管理員]  旁邊所顯示的版本。

或者，啟動 [套件管理員主控台] ([工具] > [NuGet 套件管理員] > [套件管理員主控台]  )，並輸入 `$host` 以查看 NuGet 的相關資訊 (包含版本)。

**NuGet 支援哪些程式設計語言？**

NuGet 一般適用於 .NET 語言，並且設計目的是將 .NET 程式庫帶入專案中。 在某些專案類型中，它也支援 MSBuild 和 Visual Studio 自動化，因此在各種程度上也支援其他專案和語言。

最新版的 NuGet 支援 C#、Visual Basic、F#、WiX 和 C++。

**NuGet 支援哪些專案範本？**

NuGet 完整支援各種專案範本，例如 Windows、Web、Cloud、SharePoint、Wix 等等。

**如何更新屬於 Visual Studio 範本的套件？**

移至套件管理員 UI 中的 [更新]  索引標籤，然後選取 [全部更新]  ，或使用套件管理員主控台中的 [`Update-Package` 命令](../tools/ps-ref-update-package.md)。

若要更新範本本身，您需要手動更新範本存放庫。 請參閱有關本主題的 [Xavier Decoster 部落格](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。 請注意，您必須自負這項作業的風險；因為，如果所有相依性的最新版本彼此不相容，則手動更新可能會損毀範本。

**可以在 Visual Studio 外部使用 NuGet 嗎？**

是，NuGet 只能直接從命令列運作。 請參閱[安裝指南](../install-nuget-client-tools.md)和 [CLI 參考](../tools/nuget-exe-cli-reference.md)。

## <a name="nuget-command-line"></a>NuGet 命令列

**如何取得最新版的 NuGet 命令列工具？**

請參閱[安裝指南](../install-nuget-client-tools.md)。

**nuget.exe 的授權為何？**

您可以根據 MIT 授權的規定來轉散發 nuget.exe。 您負責更新和維護您選擇要轉散發的任何 nuget.exe 複本。

**可以擴充 NuGet 命令列工具嗎？**

是，可以將自訂命令新增至 `nuget.exe`，如 [Rob Reynold 文章](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet 套件管理員主控台 (Windows 上的 Visual Studio)

**如何在套件管理員主控台中存取 DTE 物件？**

Visual Studio 自動化物件模型中的最上層物件稱為 DTE (開發工具環境) 物件。 此主控台透過名為 `$DTE` 的變數提供這個項目。 如需詳細資訊，請參閱＜Visual Studio 擴充性＞文件中的 [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) (自動化模型概觀)。

**我嘗試將 $DTE 變數轉換為類型 DTE2，但得到錯誤：Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". (無法將類型 "EnvDTE.DTEClass" 的 "EnvDTE.DTEClass" 值轉換為類型 "EnvDTE80.DTE2"。)有什麼問題？**

這是 PowerShell 如何與 COM 物件互動的已知問題。 請嘗試下列動作：

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` 是 NuGet PowerShell 主機所新增的 Helper 函式。

## <a name="creating-and-publishing-packages"></a>建立並發行套件

**如何在摘要中列出我的套件？**

請參閱[建立並發行套件](../quickstart/create-and-publish-a-package.md)。

**我的程式庫有多個版本將目標設為不同的 .NET Framework 版本。如何建置支援此項目的單一套件？**

請參閱[支援多個 .NET Framework 版本和設定檔](../create-packages/supporting-multiple-target-frameworks.md)。

**如何設定我自己的存放庫或摘要？**

請參閱[裝載套件概觀](../hosting-packages/overview.md)。

**如何將套件大量上傳至 NuGet 摘要？**

請參閱[大量發行 NuGet 套件](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com)。

## <a name="working-with-packages"></a>使用套件

**專案層級套件與方案層級套件之間的差異為何？**

只要在方案中安裝方案層級套件 (NuGet 3.x+) 一次，就可以用於方案中的所有專案。 專案層級套件會安裝在使用它的每個專案中。 方案層級套件也可能會安裝可從套件管理員主控台內呼叫的新命令。

**可以在沒有網際網路連線的情況下安裝 NuGet 套件嗎？**

是，請參閱 Scott Hanselman 的部落格文章 [How to access NuGet when nuget.org is down (or you're on a plane](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (如何在 nuget.org 關閉 (或您在飛機上) 時存取 NuGet) (hanselman.com)。

**如何將套件從預設套件資料夾安裝至不同位置？**

請使用 `nuget config -set repositoryPath=<path>` 在 `Nuget.Config` 中設定 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 設定。

**如何避免將 NuGet 套件資料夾新增至原始檔控制嗎？**

將 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) 設定為 `true`。 此索引鍵作用於方案層級，因此需要新增至 `$(Solutiondir)\.nuget\Nuget.Config` 檔案。 從 Visual Studio 啟用套件還原時會自動建立這個檔案。

**如何關閉套件還原？**

請參閱[啟用和停用套件還原](../consume-packages/package-restore.md#enable-and-disable-package-restore)。

**安裝含遠端相依性的本機套件時，為什麼收到「無法解決相依性錯誤」？**

將本機套件安裝至專案時，您需要選取**所有**來源。 這會彙總所有摘要，而不是只使用一個。 出現此錯誤的原因是本機存放庫使用者經常會因公司原則而想要避免不小心安裝遠端套件。

**我在同一個資料夾中有多個專案，我該如何為每個專案使用不同的 packages.config 檔案？**

在不同專案位於不同資料夾的大部分專案中，這在 NuGet 識別每個專案中的 `packages.config` 檔案時不是問題。 相同的資料夾中有 NuGet 3.3+ 和多個專案時，您可以將專案名稱插入至使用模式 `packages.{project-name}.config` 的 `packages.config` 檔案名稱，而且 NuGet 會使用該檔案。

因為每個專案檔都包含它自己的相依性清單，所以使用 PackageReference 時，這不是問題。

**我在存放庫清單中看不到 nuget.org，要如何取得它？**

- 將 `https://api.nuget.org/v3/index.json` 新增至來源清單，或者
- 刪除 `%appdata%\.nuget\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)，讓 NuGet 重新加以建立。
