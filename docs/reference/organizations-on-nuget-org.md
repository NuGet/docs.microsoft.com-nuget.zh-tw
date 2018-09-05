---
title: 在 nuget.org 上的組織
description: 在 nuget.org 上的組織，可協助您管理封裝發佈到群組或小組，公司環境中。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551224"
---
# <a name="organization-on-nugetorg"></a>在 nuget.org 上的組織

組織可讓企業和共同作業使用單一的 nuget.org 的身分識別的封裝上的開放原始碼專案。 套件取用者的組織帳戶會出現在 nuget.org 上的現有使用者帳戶相同。

## <a name="user-accounts-vs-organization-accounts"></a>與組織帳戶的使用者帳戶

您的使用者帳戶是您在 nuget.org 上的身分識別，並可以是任意數目的組織成員。 封裝可以隸屬於組織帳戶，例如它可以屬於的使用者帳戶。 套件取用者看不到任何使用者帳戶或組織帳戶之間的差異： 套件的形式同時出現`owners`。

組織帳戶會有一或多個使用者帳戶做為其成員。 這些成員可以管理一組套件，同時維持單一身分識別的擁有權。

## <a name="adding-a-new-organization"></a>加入新的組織

若要加入新的組織，選取您的帳戶在 nuget.org 上，然後選取 **管理組織...** 功能表命令：

![在 nuget.org 上的管理員組織的功能表選項](media/org-manage-option.png)

在下一步 頁面上，選取**新增新的組織**按鈕：

![若要建立新的組織在 nuget.org 上的按鈕](media/org-add-new-option.png)

在下一步 頁面上，提供組織名稱和電子郵件地址。 因為組織帳戶會共用相同的命名空間，做為使用者帳戶，則必須不同於其他現有的組織或使用者帳戶的組織名稱。 電子郵件地址也必須是唯一的所有帳戶。

![在 nuget.org 上新增新的組織頁面](media/org-add-new-page.png)

組織帳戶建立之後，您是系統管理員和可以送出組織的套件並新增組織的成員。

### <a name="transform-existing-account-to-an-organization"></a>轉換至組織的現有帳戶

> [!Warning]
> 帳戶轉換是無法復原： 您無法轉換回給使用者帳戶的組織。

如果您使用單一使用者帳戶小組的形式管理套件，並想要將該帳戶轉換成組織中，使用**轉換您的組織帳戶**選項**管理組織**頁面上：

![在 nuget.org 上的選項來轉換到組織現有的帳戶](media/org-transform-option.png)

在下一步 頁面上，指定不同的使用者帳戶，若要指派的組織系統管理員身分，然後選取**轉換**。

![輸入轉換為組織的使用者帳戶的資訊](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理組織的成員

組織系統管理員，您可以藉由提供每個成員的 nuget.org 新增成員*使用者帳戶名稱*; 無法使用電子郵件地址。 然後，您會標示為共同作業者或具有下列權限的系統管理員的每個成員：

| 權限 | 共同作業者 | 系統管理員 |
| --- | --- | --- |
| 管理組織的套件<br/>（提交新的套件、 更新或取消列出現有的封裝） | 是 | 是 |
| 變更組織中繼資料<br/>（電子郵件地址，通知設定） | 否 | 是 |
| 管理組織的成員 | 否 | 是 |
| 要求或 co-ownership 組織封裝要求處理 | 否 | 是 |

## <a name="managing-packages"></a>管理套件

您可以檢視所有封裝，在您的帳戶和其中您必須是成員的所有組織[管理套件](https://www.nuget.org/account/Packages)頁面。 若要檢視您的帳戶或任何特定的組織特定的封裝，使用的帳戶篩選器右上方的頁面。

![帳戶篩選器使用管理套件](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>將封裝傳送到組織
如果您想要將有些套件傳輸至新建立的組織，則可以要求共同擁有封裝的組織帳戶，然後再為擁有者移除自己。 如果您是組織的系統管理員，則需要接受擁有權不確認。 不過，如果您是共同作業者，新增為擁有者的組織需要其中一個接受擁有權的系統管理員。

## <a name="publishing-packages"></a>發行套件

您將套件發佈到組織像您將套件發佈到使用者帳戶： 直接上傳至 nuget.org 的封裝，或將封裝推送`nuget push`或`dotnet nuget push`CLI 命令。

### <a name="uploading-packages"></a>將套件上傳

當您直接上傳新的封裝上[nuget.org 上傳](https://www.nuget.org/packages/manage/upload) 頁面上，您將套件擁有者的使用者或組織帳戶：

![上傳封裝的帳戶 選項](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 金鑰

若要將封裝推送`nuget push`或`dotnet nuget push`CLI 命令，您必須取得 API 金鑰所需的這些命令。 如需詳細資訊，請參閱 <<c0> [ 發行套件](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。

當建立新的 API 金鑰，請選取適當的組織中**套件擁有者**下拉式清單。 任何您所建立的 API 金鑰是僅適用於所選的組織：

![API 金鑰與帳戶選項](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>移除組織

身為使用者，您可以自行從組織移除選取`X`按鈕顯示您的組織成員資格：

![從組織移除使用者帳戶](media/org-remove-self-option.png)

系統管理員可以移除任何成員，從組織，包括其他系統管理員。 如果您是組織的唯一系統管理員，您無法移除自己，除非您以系統管理員身分新增另一個成員。

### <a name="deleting-an-organization-account"></a>刪除組織帳戶

這項功能即將登場。
