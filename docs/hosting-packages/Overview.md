---
title: 裝載您自己的 NuGet 摘要概觀
description: 在本機或遠端開啟裝載您自己的 NuGet 套件摘要或資源庫的概觀。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3ca023c8d39b9b36388f5f517b50ca5cd2347cc0
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610448"
---
# <a name="hosting-your-own-nuget-feeds"></a>裝載您自己的 NuGet 摘要

而不是向公眾開放套件，您可能只想向有限的對象發行套件，例如您的組織或工作群組。 此外，有些公司可能想要限制其開發人員可以使用的協力廠商程式庫，因此引導這些開發人員離開有限的套件來源，而不是離開 nuget.org。

針對所有這類用途，NuGet 以下列方式支援設定私用的套件來源：

- 本機摘要：套件只位於適當的網路檔案共用，最好使用 `nuget init` 和 `nuget add`，以建立階層式資料夾結構 (NuGet 3.3+)。 如需詳細資料，請參閱[本機摘要](../hosting-packages/local-feeds.md)。
- NuGet.Server：套件可以透過本機 HTTP 伺服器提供。 如需詳細資料，請參閱 [NuGet.Server](../hosting-packages/nuget-server.md)。
- NuGet 資源庫：套件裝載在使用 [NuGet 資源庫專案](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps)的網際網路伺服器上 (github.com)。 NuGet 資源庫讓使用者能夠管理及使用功能，例如大量 web UI，在瀏覽器中搜尋和瀏覽套件，類似 nuget.org。

另外還有數個其他的 NuGet 裝載產品，例如[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) ，以及支援遠端私人摘要的[GitHub package registry](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) 。 以下是這類產品的清單：

- JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)，也適用於 Team Foundation Server 2017 及更新版本。
- [BaGet](https://github.com/loic-sharma/BaGet)，這是建置於 ASP.NET Core 之上的 NuGet V3 伺服器開放原始碼實作
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/)是完全受控的套件管理 SaaS
- [GitHub 套件登錄](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget)，這是一個在 docker 中的 kestrel 上執行的 NuGet V2 伺服器開放原始碼實作
- [MyGet](https://myget.org)
- Sonatype 的 [Nexus](https://www.sonatype.org/nexus/)。
- [NuGet 伺服器 (開放原始碼)](https://github.com/svenkle/nuget-server)，類似於 Inedo NuGet 伺服器的開放原始碼實作
- [NuGet 伺服器](http://nugetserver.net/)，Inedo 社群專案
- Inedo 的 [ProGet](https://inedo.com/proget)
- [Sleet](https://github.com/emgarten/sleet)，這是開放原始碼 NuGet V3 靜態摘要產生器
- JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。

不論套件的裝載方式為何，您都要將它們新增至 `NuGet.Config` 的可用來源清單中，才能存取它們。 如[套件來源](../consume-packages/install-use-packages-visual-studio.md#package-sources)中所述在 Visual Studio 中完成，或從命令列使用 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) 完成。 來源的路徑可以是本機資料夾的路徑名稱、網路名稱或 URL。
