---
title: "NuGet 常見問題集 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "在命令列上和 Visual Studio 中使用 NuGet 以及使用 NuGet 資源庫的常見問題和解答。"
keywords: "NuGet 問與答, 問題和解答, 常見問題, NuGet 版本, 套件版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d19a24a2d1955e996e18d44fee346865d36493f8
ms.sourcegitcommit: e5b7cf6675be9891341c196afe822cea6f71d60c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="nuget-frequently-asked-questions"></a>NuGet 常見問題集

本主題內容：

- [快速入門](#getting-started)
- [Visual Studio 中的 NuGet](#nuget-in-visual-studio)
- [NuGet 命令列](#nuget-command-line)
- [NuGet 套件管理員主控台](#nuget-package-manager-console)
- [建立並發行套件](#creating-and-publishing-packages)
- [使用套件](#working-with-packages)
- [在 nuget.org 上管理套件](#managing-packages-on-nugetorg)
- [無法存取 nuget.org](#nugetorg-not-accessible)

## <a name="getting-started"></a>使用者入門

**執行 NuGet 所需的作業為何？**

[安裝指南](../guides/install-nuget.md)包含 UI 和命令列工具的所有資訊。

**NuGet 支援 Mono 嗎？**

命令列工具 `nuget.exe` 會在 Mono 3.2+ 下建置並執行，而且可以在 Mono 中建立套件。

雖然 `nuget.exe` 完整運作於 Windows 上，但是 Linux 和 OS X 上已有已知問題。請參閱 GitHub 上的 [Mono 問題](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)。

[圖形化用戶端](https://github.com/mrward/monodevelop-nuget-addin)可作為 MonoDevelop 的增益集。

**如何判斷套件所包含的內容，以及它對我的應用程式而言是否穩定而且有用？**

了解套件的主要來源是其在 nuget.org 上的清單頁面 (或另一個私人摘要)。 nuget.org 上的每個套件頁面都會包含套件的描述、其版本歷程記錄和使用量統計資料。 套件頁面上的 [資訊] 區段也會包含專案網站的連結，而在專案網站中，您一般可以找到許多範例和其他文件協助您了解如何使用套件。

如需詳細資訊，請參閱[尋找及選擇套件](../Consume-Packages/Finding-and-Choosing-Packages.md)。

## <a name="nuget-in-visual-studio"></a>Visual Studio 中的 NuGet

**在不同的 Visual Studio 產品中，如何支援 NuGet？**

- Windows 上的 Visual Studio 支援[套件管理員 UI](../tools/Package-Manager-UI.md) 和[套件管理員主控台](../tools/Package-Manager-Console.md)。
- Visual Studio for Mac 具有內建 NuGet 功能，如[在專案中包含 NuGet 套件](/visualstudio/mac/nuget-walkthrough)中所述。
- Visual Studio Code (所有平台) 沒有任何直接 NuGet 整合。 請使用 [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) 或 [dotnet CLI](../tools/dotnet-commands.md)。
- Visual Studio Team Services 提供[還原 NuGet 套件的建置步驟](/vsts/build-release/tasks/package/nuget)。 您也可以[在 Team Services 上裝載私用 NuGet 套件摘要](https://www.visualstudio.com/docs/package/nuget/publish)。

**如何檢查已安裝 NuGet 工具的確切版本？**

在 Visual Studio 中，使用 [說明] > [關於 Microsoft Visual Studio] 命令，並查看 [NuGet 套件管理員] 旁邊所顯示的版本。

或者，啟動 [套件管理員主控台] ([工具] > [NuGet 套件管理員] > [套件管理員主控台])，並輸入 `$host` 以查看 NuGet 的相關資訊 (包含版本)。

**NuGet 支援哪些程式設計語言？**

NuGet 一般適用於 .NET 語言，並且設計目的是將 .NET 程式庫帶入專案中。 在某些專案類型中，它也支援 MSBuild 和 Visual Studio 自動化，因此在各種程度上也支援其他專案和語言。

最新版的 NuGet 支援 C#、Visual Basic、F#、WiX 和 C++。

**NuGet 支援哪些專案範本？**

NuGet 完整支援各種專案範本，例如 Windows、Web、Cloud、SharePoint、Wix 等等。

**如何更新屬於 Visual Studio 範本的套件？**

移至套件管理員 UI 中的 [更新] 索引標籤，然後選取 [全部更新]，或使用套件管理員主控台中的 [`Update-Package` 命令](../Tools/ps-ref-update-package.md)。

若要更新範本本身，您需要手動更新範本存放庫。 請參閱有關本主題的 [Xavier Decoster 部落格](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)。 請注意，您必須自負這項作業的風險；因為，如果所有相依性的最新版本彼此不相容，則手動更新可能會損毀範本。

**可以在 Visual Studio 外部使用 NuGet 嗎？**

是，NuGet 只能直接從命令列運作。 請參閱[安裝指南](../guides/install-nuget.md)和 [CLI 參考](../tools/nuget-exe-CLI-Reference.md)。

## <a name="nuget-command-line"></a>NuGet 命令列

**如何取得最新版的 NuGet 命令列工具？**

請參閱[安裝指南](../guides/install-nuget.md)。

**可以擴充 NuGet 命令列工具嗎？**

是，可以將自訂命令新增至 `nuget.exe`，如 [Rob Reynold 文章](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)中所述。

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet 套件管理員主控台 (Windows 上的 Visual Studio)

**如何在套件管理員主控台中存取 DTE 物件？**

Visual Studio 自動化物件模型中的最上層物件稱為 DTE (開發工具環境) 物件。 此主控台透過名為 `$DTE` 的變數提供這個項目。 如需詳細資訊，請參閱＜Visual Studio 擴充性＞文件中的 [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) (自動化模型概觀)。

**我嘗試將 $DTE 變數轉換為類型 DTE2，但收到錯誤：無法將 "EnvDTE.DTEClass" 類型的 "EnvDTE.DTEClass" 值轉換為 "EnvDTE80.DTE2" 類型。有什麼問題？**

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

請使用 `nuget config -set repositoryPath=<path>` 在 `Nuget.Config` 中設定 [`repositoryPath`](../Schema/nuget-config-file.md#config-section) 設定。

**如何避免將 NuGet 套件資料夾新增至原始檔控制嗎？**

將 `Nuget.Config` 中的 [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) 設定為 `true`。 此索引鍵作用於方案層級，因此需要新增至 `$(Solutiondir)\.nuget\Nuget.Config` 檔案。 從 Visual Studio 啟用套件還原時會自動建立這個檔案。

**如何關閉套件還原？**

請參閱[啟用和停用套件還原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。

**安裝含遠端相依性的本機套件時，為什麼收到「無法解決相依性錯誤」？**

將本機套件安裝至專案時，您需要選取**所有**來源。 這會彙總所有摘要，而不是只使用一個。 出現此錯誤的原因是本機存放庫使用者經常會因公司原則而想要避免不小心安裝遠端套件。

**我在同一個資料夾中有多個專案，我該如何為每個專案使用不同的 packages.config 檔案？**

在不同專案位於不同資料夾的大部分專案中，這在 NuGet 識別每個專案中的 `packages.config` 檔案時不是問題。 相同的資料夾中有 NuGet 3.3+ 和多個專案時，您可以將專案名稱插入至使用模式 `packages.{project-name}.config` 的 `packages.config` 檔案名稱，而且 NuGet 會使用該檔案。

因為每個專案檔都包含它自己的相依性清單，所以使用 PackageReference 時，這不是問題。

**我在存放庫清單中看不到 nuget.org，要如何取得它？**

- 將 `https://api.nuget.org/v3/index.json` 新增至來源清單，或者
- 刪除 `%appdata%\.nuget\NuGet.Config`，並讓 NuGet 重新予以建立。

**如果套件未提供特定授權資訊，則預設授權條款是什麼？**

每個套件都是受套件隨附的條款所控管。 您應該先檢閱適用的條款，再存取、下載或取得任何套件。 在 nuget.org 上，使用套件頁面上的 [授權資訊] 連結。

如果套件未指定授權條款，請使用 nuget.org 套件頁面上的 [連絡擁有者] 連結直接連絡套件擁有者。 Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。


## <a name="managing-packages-on-nugetorg"></a>在 nuget.org 上管理套件

**我可以在上傳套件之後編輯套件中繼資料嗎？為什麼必須編輯 nuspec 及上傳新的套件才能變更套件中繼資料？**

NuGet 需要所有套件皆已簽署。 套件簽署的設計原則是已簽署的套件內容必須是不可變的，其中包含 nuspec。 編輯套件中繼資料會導致 nuspec 變更，並讓現有簽章失效。 建議修改現有工作流程，使其不需要在建立套件之後編輯套件中繼資料。

請注意，會自動從您套件本身產生針對套件所列出的相依性，而且無法進行編輯。

此外，將套件上傳至 [staging.nuget.org](http://staging.nuget.org) 是測試和驗證套件的不錯方式，而不需要將套件設為可在公用資源庫中使用。

**可以保留將在未來發行之套件的名稱嗎？**

可以。 要求帳戶的套件識別碼前置詞，即可在 [nuget.org](https://www.nuget.org/) 上保留套件的識別碼。 若要要求套件識別碼前置詞，請使用套件擁有者顯示名稱和所要求的套件識別碼前置詞，將郵件傳送至 nuget.org 上的帳戶。  

**如何宣告套件擁有權？**

請參閱[在 nuget.org 上管理套件擁有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。

**如何處理違反我軟體授權的套件擁有者？**

鼓勵 NuGet 社群合作，以解決套件擁有者與其他軟體擁有者之間可能發生的任何爭議。 我們已製作可在要求 nuget.org 管理員仲裁之前遵循的[爭議解決程序](../policies/dispute-resolution.md)。

**建議將測試套件上傳至 nuget.org 嗎？**

基於測試目的，您可以使用 [staging.nuget.org](http://staging.nuget.org) 或替代公用 NuGet 伺服器 (例如 [myget.org](https://myget.org) 或 [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/))。

請注意，可能不會保留上傳至 staging.nuget.org 的套件。 請參閱 [Goodbye 預覽](http://blog.nuget.org/20130419/goodbye-preview.html)。

**我可以上傳至 nuget.org 的套件大小上限為何？**

nuget.org 允許最多 250MB 的套件，但建議盡可能保持 1MB 的套件，並使用相依性將套件連結在一起。 根據經驗法則，套件只包含一個組件來避免發生衝突。

NuGet 使用 HTTP 來下載套件，因此較大的套件與較小的套件相較之下更有可能會讓安裝失敗。

可能會在多個套件之間共用相依性，讓 NuGet 套件取用者的總下載大小變小。

相依性大部分是靜態的，而且永遠不會變更。 使用程式碼修正 Bug 時，可能不需要更新相依性。 如果您組合相依性，則每次最後都會得到較大的套件。 將 NuGet 套件分割為相關相依性，以更精細地調整您套件取用者的升級。

## <a name="nugetorg-not-accessible"></a>無法存取 nuget.org

**為何無法從 nuget.org 下載套件或將套件上傳至其中？**

首先，請確定您使用最新版的 NuGet。 如果該版本持續失敗，請[連絡支援人員](https://www.nuget.org/policies/Contact)，並提供其他連線疑難排解資訊，包含：

- 您所使用的 NuGet 版本
- 您所使用的套件來源
- 含詳細之詳細資訊的還原記錄
- MTR 或 Fiddler 追蹤 (請參閱下面)
- 您的地理區域
- 作業系統版本
- 電腦組態 (CPU、網路、硬碟機)
- 是否為受 Proxy 或防火牆保護的電腦
- 電腦上所安裝的 .NET 版本
- 您所使用的跨平台工具 (例如 .NET CLI 或 DNU) 版本

*擷取 MTR：*

- 從 [http://winmtr.net/download/](http://winmtr.net/) 下載 WinMTR
- 輸入 `api.nuget.org` 作為主機名稱，然後按一下 [啟動]。
- 等到 [已傳送] 資料行 >= 100。

    ![擷取 MTR](media/mtr.png)

- 將文字複製至剪貼簿。

*擷取 Fiddler：*

- 安裝最新版的 [Fiddler](http://www.telerik.com/download/fiddler)。
- 啟動 Fiddler，並使用 [檔案] > [擷取流量] 功能表來停用擷取流量。
- 移除所有工作階段 (選取清單中的所有項目，並按 **Delete** 鍵)。
- 設定 Fiddler 擷取 HTTPS 流量，方法是核取 [工具] > [Fiddler 選項] 功能表的 [HTTPS] 索引標籤中的 [Decrypt HTTPS traffic] (將 HTTPS 流量解密)。
- 關閉 Visual Studio。
- 啟用 [檔案] > [擷取流量] 功能表。
- 啟動 Visual Studio 或 nuget.exe，然後執行無法運作的動作。 這些動作所產生的流量應該會顯示在 Fiddler 中。
- 執行動作之後，請使用 [檔案] > [儲存] > [所有工作階段] 來儲存所擷取的工作階段。

注意：可能必須將 `HTTP_PROXY` 環境變數設定為 `http://127.0.0.1:8888`，以透過 Fiddler 路由傳送 NuGet 流量。

如果該作業失敗，請嘗試[這篇 StackOverflow 文章所提及的祕訣](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。

**nuget.org 的 API 端點為何？**

V3：`https://api.nuget.org/v3/index.json` V2：`https://www.nuget.org/api/v2/` (請注意，V2 API 已被取代，無法與 NuGet 4+ 搭配使用。)
