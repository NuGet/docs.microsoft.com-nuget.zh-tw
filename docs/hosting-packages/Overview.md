---
title: 裝載您自己的 NuGet 摘要概觀
description: 在本機或遠端開啟裝載您自己的 NuGet 套件摘要或資源庫的概觀。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 45d8a6557ee02998f3d12b128ee2dc4fd6ae48bb
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145588"
---
# <a name="hosting-your-own-nuget-feeds"></a>裝載您自己的 NuGet 摘要

而不是向公眾開放套件，您可能只想向有限的對象發行套件，例如您的組織或工作群組。 此外，有些公司可能想要限制其開發人員可以使用的協力廠商程式庫，因此引導這些開發人員離開有限的套件來源，而不是離開 nuget.org。

針對所有這類用途，NuGet 以下列方式支援設定私用的套件來源：

- 本機摘要：套件只位於適當的網路檔案共用，且最好使用 `nuget init` 和 `nuget add` 建立階層式資料夾結構 (NuGet 3.3+)。 如需詳細資料，請參閱[本機摘要](../hosting-packages/local-feeds.md)。
- NuGet.Server：套件可以透過本機 HTTP 伺服器提供。 如需詳細資料，請參閱 [NuGet.Server](../hosting-packages/nuget-server.md)。
- NuGet 資源庫：套件會裝載在使用 [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (NuGet 資源庫專案) 的網際網路伺服器上 (github.com)。 NuGet 資源庫讓使用者能夠管理及使用功能，例如大量 web UI，在瀏覽器中搜尋和瀏覽套件，類似 nuget.org。

另外還有數個 NuGet 裝載產品支援遠端私用摘要，包括：

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)，也適用於 Team Foundation Server 2017 及更新版本。
- [MyGet](http://myget.org)
- Inedo 的 [ProGet](http://inedo.com/proget)
- [NuGet 伺服器](http://nugetserver.net/)，Inedo 社群專案
- [NuGet 伺服器 (開放原始碼)](http://nuget-server.net)，類似於 Inedo NuGet 伺服器的開放原始碼實作
- [LiGet](https://github.com/ai-traders/liget)，這是一個在 docker 中的 kestrel 上執行的 NuGet V2 伺服器開放原始碼實作
- [BaGet](https://github.com/loic-sharma/BaGet)，這是建置於 ASP.NET Core 之上的 NuGet V3 伺服器開放原始碼實作
- [Sleet](https://github.com/emgarten/sleet)，這是開放原始碼 NuGet V3 靜態摘要產生器
- JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。
- Sonatype 的 [Nexus](http://www.sonatype.org/nexus/)。
- JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。

不論套件的裝載方式為何，您都要將它們新增至 `NuGet.Config` 的可用來源清單中，才能存取它們。 如[套件來源](../tools/package-manager-ui.md#package-sources)中所述在 Visual Studio 中完成，或從命令列使用 [`nuget sources`](../tools/cli-ref-sources.md) 完成。 來源的路徑可以是本機資料夾的路徑名稱、網路名稱或 URL。
