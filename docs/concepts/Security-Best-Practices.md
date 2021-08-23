---
title: 安全軟體供應鏈的最佳作法
description: 使用 NuGet & GitHub 保護軟體供應鏈安全的最佳做法。
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726973"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>安全軟體供應鏈的最佳作法

開放原始碼隨處都有。 它是在許多專屬的程式碼基底和社區專案中。 對於組織和個人來說，今天的問題不是您是或不是使用開放原始碼，而是您使用的開放原始碼程式碼，還有多少。

如果您不知道軟體供應鏈的內容，其中一個相依性的上游弱點可能是嚴重問題，讓您和您的客戶遭受潛在的危害。 在本檔中，我們將深入探討「軟體供應鏈」的意義、其重要性，以及如何使用最佳做法來協助保護您的專案供應鏈。

![Octoverse 2020-開放原始碼的狀態](media/opensource-percent.png)

## <a name="dependencies"></a>相依性 

「軟體供應鏈」一詞是用來參考您的軟體及其來源的所有專案。 它是您的軟體供應鏈相依的相依性和屬性。 相依性是您的軟體需要執行的相依性。 它可以是程式碼、二進位檔或其他元件，以及它們的來源，例如存放庫或封裝管理員。

它包括撰寫程式碼的人員、發表者、如何檢查安全性問題、已知弱點、支援的版本、授權資訊，以及任何在程式的任何時間點的內容。

您的供應鏈也會將堆疊的其他部分包含在單一應用程式之外，例如您的組建和封裝腳本，或執行應用程式所依賴之基礎結構的軟體。

## <a name="vulnerabilities"></a>弱點

現今的軟體相依性很普遍。 針對您不需要自行撰寫的功能，您的專案使用數百個開放原始碼相依性，是很常見的情況。 這可能表示您大部分的應用程式都是由您未撰寫的程式碼所組成。 

![Octoverse 2020-相依性的狀態](media/dependencies.png)

協力廠商或開放原始碼相依性中可能的弱點，是您無法控制與您撰寫的程式碼緊密相關的相依性，這可能會在您的供應鏈中產生潛在的安全性風險。

如果其中一個相依性有弱點，您也可能會遇到弱點。 這可能會令人驚訝，因為您的其中一個相依性可能會變更，而您甚至不知道。 即使存在於目前的相依性中，但不是可利用的弱點，也可以在未來進行攻擊。 

能夠利用數千個開放原始碼開發人員和程式庫作者的工作，表示數以千計的陌生人可有效地參與您的生產程式碼。 您的產品（透過軟體供應鏈）受未修補的弱點、無害錯誤或甚至惡意的惡意攻擊所影響。

## <a name="supply-chain-compromises"></a>供應鏈的危害

供應鏈的傳統定義來自製造;這是建立和提供事物所需的程式鏈。 它包括規劃、材質供應、製造和零售。 除了資料以外，軟體供應鏈也是很類似的程式碼。 它不是製造，而是開發。 程式碼是來自供應商、商業或開放原始碼，而不是從基礎深入探討，而一般而言，開放原始碼程式碼是來自存放庫。 從存放庫新增程式碼表示您的產品會依賴該程式碼。

在特意將惡意程式碼新增至相依性時，會使用該相依性的供應鏈將程式碼散發至其受害者，以提供軟體供應鏈攻擊的其中一個範例。 供應鏈攻擊是真實的。 有許多方法可以攻擊供應鏈，包括直接插入惡意程式碼作為新的參與者、接管參與者的帳戶，而不會有其他人注意，或甚至是危及簽署金鑰來散發未正式參與的軟體。

軟體供應鏈攻擊本身並不是最終的目標，而是讓攻擊者插入惡意程式碼或提供後門以供日後存取的機會。

![Octoverse 2020-弱點生命週期的狀態](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>未修補的軟體

現今使用開放原始碼是很重要的，預計很快就會變慢。 假設我們不打算停止使用開放原始碼軟體，提供連鎖安全性的威脅就是未修補的軟體。 知道，您要如何解決專案相依性有弱點的風險？

- **瞭解您環境中的內容。** 這需要探索您的相依性和任何可轉移的相依性，以瞭解這些相依性的風險，例如弱點或授許可權制。
- **管理您的相依性。** 探索到新的安全性弱點時，您必須判斷是否受到影響，如果是，則更新為可用的最新版本和安全性修補程式。 這對於審核導入新相依性或定期審核較舊相依性的變更特別重要。
- **監視您的供應鏈。** 這是透過審核您已備妥的控制項來管理您的相依性。 這可協助您針對相依性強制符合更嚴格的條件。

![Octoverse 2020-諮詢的狀態](media/advisories.png)

我們將涵蓋 NuGet 和 GitHub 所提供的各種工具和技術，您可以立即使用這些工具和技術來解決專案內的潛在風險。 

## <a name="knowing-what-is-in-your-environment"></a>瞭解您環境中的內容

### <a name="nuget-dependency-graph"></a>NuGet 相依性圖形

**📦 套件取用者**

您可以直接查看個別的專案檔，以在專案中查看您的 NuGet 相依性。

這通常會在下列兩個位置中找到：

-   [`packages.config`](../reference/packages-config.md) –位於專案根目錄中。
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) –位於專案檔中。 

根據您用來管理 NuGet 相依性的方法，您也可以使用 Visual Studio，直接在[方案總管](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer)或[NuGet 封裝管理員](../consume-packages/install-use-packages-visual-studio.md)中查看相依性。

在 CLI 環境中，您可以使用 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 命令來列出專案或解決方案的相依性。 

如需管理 NuGet 相依性的詳細資訊，[請參閱下列檔](../consume-packages/overview-and-workflow.md)。

### <a name="github-dependency-graph"></a>GitHub 相依性關係圖 

**📦 套件取用者 | 📦🖊 封裝作者**

您可以使用 GitHub 的相依性圖形來查看您的專案相依的套件，以及相依于該套件的存放庫。 這可協助您查看其相依性中偵測到的任何弱點。

如需 GitHub 存放庫相依性的詳細資訊，[請參閱下列檔](https://github.co/dependency-graph)。

### <a name="dependency-versions"></a>相依性版本

**📦 套件取用者 | 📦🖊 封裝作者**

為了確保安全的供應鏈相依性，您會想要確保所有相依性 & 工具都會定期更新為最新的穩定版本，因為它們通常會包含已知弱點的最新功能和安全性修補程式。 您的相依性可以包含您依存的程式碼、您使用的二進位檔、使用的工具和其他元件。 這可能包括：

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK & 執行時間](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet 套件](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>管理您的相依性

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet 已淘汰和易受攻擊的相依性

**📦 套件取用者 | 📦🖊 封裝作者**

您可以使用 [DOTNET CLI](/dotnet/core/tools/dotnet-list-package) 來列出您的專案或解決方案中可能存在的任何已知已淘汰或易受攻擊的相依性。 您可以使用命令 `dotnet list package --deprecated` 或 `dotnet list package --vulnerable` 提供任何已知棄用功能或弱點的清單。

### <a name="github-vulnerable-dependencies"></a>GitHub 易受攻擊的相依性

**📦 套件取用者 | 📦🖊 封裝作者**

如果您的專案是裝載在 GitHub 上，您可以利用[GitHub 安全性](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors)找出專案中的安全性弱點和錯誤，Dependabot 會藉由開啟程式碼基底的提取要求來修正這些問題。 

在導入之前攔截易受攻擊的相依性，是「 [下移](https://en.wikipedia.org/wiki/Shift-left_testing) 」移動的一專案標。 可以取得相依性的相關資訊，例如其授權、可轉移的相依性，以及相依性的存留期，以協助您完成這項作業。

如需有關 Dependabot 警示 & 安全性更新的詳細資訊， [請參閱下列檔](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)。

### <a name="nuget-feeds"></a>NuGet 摘要

**📦 套件取用者**

使用多個公用 & 私用 NuGet 原始檔摘要時，可以從任何饋送下載套件。 為了確保您的組建是可預測的，且不受已知的攻擊（例如相依性 [混淆](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)）的保護，請瞭解您的套件所) 的特定摘要 (是最佳作法。 您可以使用單一摘要或具有 upstreaming 功能的私人摘要來保護。

如需保護套件摘要的詳細資訊，請參閱 [使用私用套件摘要時降低風險的三種方式](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)。

### <a name="client-trust-policies"></a>用戶端信任原則

**📦 套件取用者**

有一些您可以加入宣告的原則，您需要使用這些原則簽署封裝。 這可讓您信任套件作者，只要它是作者簽署的，或是信任套件（如果是由 NuGet org 簽署的儲存機制的特定使用者或帳戶所擁有）。

若要設定用戶端信任原則， [請參閱下列檔](../consume-packages/installing-signed-packages.md)。

### <a name="lock-files"></a>鎖定檔案

**📦 套件取用者**

鎖定檔案會儲存套件內容的雜湊。 如果您要安裝的套件內容雜湊符合鎖定檔案，則會確保封裝重複性。

若要啟用鎖定檔案， [請參閱下列檔](../consume-packages/package-references-in-project-files.md#locking-dependencies)。

## <a name="monitor-your-supply-chain"></a>監視您的供應鏈

### <a name="github-secret-scanning"></a>GitHub 祕密掃描 (英文)

**📦🖊 封裝作者**

GitHub 會掃描 NuGet API 金鑰的存放庫，以防止詐騙使用意外認可的秘密。 

若要深入瞭解秘密掃描，請參閱 [關於秘密掃描](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)。

### <a name="author-package-signing"></a>作者套件簽署

**📦🖊 封裝作者**

[作者簽署](../reference/signed-packages-reference.md) 可讓套件作者在套件上標記其身分識別，並讓取用者確認其來自您的身分。 這可保護您不受內容篡改的攻擊，並可作為套件來源和套件真實性的單一真實來源。 結合用戶端信任原則時，您可以確認套件來自特定的作者。

若要撰寫簽署套件，請參閱 [簽署封裝](../create-packages/sign-a-package.md)。

### <a name="two-factor-authentication-2fa"></a>Two-Factor Authentication (2FA) 

**📦🖊 封裝作者**

啟用雙因素驗證 (2FA) 可以在[登入您的 GitHub 帳戶](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)或[NuGet. 組織公用套件存放庫](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)時，增加額外的安全性層級。 建議您啟用雙重要素驗證來保護您的帳戶。

### <a name="package-id-prefix-reservation"></a>套件識別碼首碼保留項目 

**📦🖊 封裝作者**

若要保護套件的身分識別，您可以保留套件識別碼前置詞與個別的命名空間，以便在您的套件識別碼前置詞正確地落在 [指定的準則](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)時，讓相符的擁有者產生關聯。 

若要瞭解如何保留識別碼首碼，請參閱 [套件識別碼前置詞保留](../nuget-org/id-prefix-reservation.md)。

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>淘汰和取消列出易受攻擊的套件

**📦🖊 封裝作者**

若要在您注意到您所撰寫的封裝中有弱點時保護 .NET 封裝生態系統，最好取代並取消列出套件，讓使用者無法搜尋套件。 如果您使用已被取代且未列出的封裝，您應該避免使用封裝。

若要瞭解如何取代和取消列出套件，請參閱下列有關 [淘汰](../nuget-org/deprecate-packages.md) 和 [取消列出套件](../nuget-org/policies/deleting-packages.md#unlisting-a-package)的檔。

## <a name="summary"></a>摘要

您的軟體供應鏈是任何進入或影響程式碼的程式碼。 雖然供應鏈的危害是真實且越來越普及，但它們仍然很罕見;因此，您可以做的最重要的事，就是藉由 **瞭解您的相依性、管理您的** 相依性，以及 **監視您的供應鏈**，來保護您的供應鏈。

您已瞭解 NuGet 和[GitHub](/learn/modules/maintain-secure-repository-github/)提供的各種方法，現在可讓您更有效地查看、管理及監視您的供應鏈。

如需保護世界軟體的相關資訊，請參閱 [Octoverse 2020 安全性報告的狀態](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)。
