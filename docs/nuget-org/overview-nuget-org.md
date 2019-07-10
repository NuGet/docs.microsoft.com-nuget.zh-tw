---
title: NuGet.org 概觀
description: NuGet.org 概觀
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427013"
---
# <a name="overview-of-nugetorg"></a>NuGet.org 概觀

NuGet.org 是 NuGet 套件的公用主機，每天都有數百萬的 .NET 和 .NET Core 開發人員採用 NuGet 套件。

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet.org 在 NuGet 生態系統中的角色

在公用主機的角色中，NuGet.org 本身會在 [nuget.org](https://www.nuget.org) 維護具有超過 100,000 個獨特套件的中央存放庫。NuGet.org 不是套件的唯一可能主機。 NuGet 技術也讓您能夠在雲端 (例如在 Azure DevOps 上)、私人網路或甚至只是在本機檔案系統中，私下裝載套件。 如果您對於不同的主機或裝載選項有興趣，請參閱[裝載您自己的 NuGet 摘要](../hosting-packages/overview.md)。

NuGet.org 如同 NuGet 套件的任何主機，都是作為套件「建立者」  與套件「取用者」  之間的聯繫點。 建立者會建置有用的 NuGet 套件，並加以發佈。 取用者接著會搜尋可存取主機上的實用和相容套件，並下載這些套件且將其包含在專案中。 一旦安裝於專案，套件的 API 就可供專案程式碼的其餘部分使用。

![套件建立者、套件主機與套件取用者之間的關聯性](media/nuget-roles.png)

## <a name="accounts"></a>帳戶

若要在 NuGet.org 上發佈套件，請先建立[個人 (使用者) 帳戶](individual-accounts.md)。 這會成為您在 NuGet.org 上的身分識別。

NuGet.org 也可讓您建立[組織帳戶](organizations-on-nuget-org.md)。 組織帳戶有一或多個作為其成員的個人帳戶。 成員可以管理一組套件，同時維持擁有權的單一身分識別。 透過您的個人帳戶，您可以是任意數目組織的成員。

套件可以屬於組織帳戶，就像可以屬於個人帳戶一樣。 套件取用者看不到個人帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。

## <a name="api-keys"></a>API 金鑰

一旦擁有要發佈的 NuGet 套件 ( *.nupkg*) 時，您會使用 nuget.exe CLI 或 donet.exe CLI 以及從 NuGet.org 取得的 [API 金鑰](scoped-api-keys.md)，將它發佈到 NuGet.org。

當您[發佈套件](../create-packages/creating-a-package.md)時，請在 CLI 命令中包含 API 金鑰值。

## <a name="id-prefixes"></a>識別碼首碼

當您發佈套件時，可以[保留識別碼首碼](id-prefix-reservation.md) 以保留並保護您的身分識別。 套件取用者安裝套件時會提供其額外的資訊，指出他們取用的套件在其識別屬性中沒有欺騙成分。

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org 的 API 端點

若要以 NuGet 用戶端來將 NuGet.org 作為套件存放庫使用，您應使用下列 V3 API 端點： 

`https://api.nuget.org/v3/index.json`

舊版用戶端仍可以使用 V2 通訊協定來連線到 NuGet.org。但請注意，使用 V2 通訊協定會造成 NuGet 用戶端 3.0 或更新版本的服務變得緩慢且較不穩定：

`https://www.nuget.org/api/v2` (**V2 通訊協定已淘汰！** )
