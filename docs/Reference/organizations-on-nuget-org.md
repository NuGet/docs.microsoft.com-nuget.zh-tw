---
title: 在 nuget.org 的組織
description: 在 nuget.org 的組織可協助您管理封裝發佈到群組或小組，公司環境中。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a>Nuget.org 的組織

組織可讓企業和共同作業上使用單一 nuget.org 識別封裝的開放原始碼專案。 封裝取用者組織帳戶會出現在 nuget.org 上現有的使用者帳戶與相同。

## <a name="user-accounts-vs-organization-accounts"></a>與組織帳戶的使用者帳戶

您的使用者帳戶是您在 nuget.org 的身分識別，而且可以是任意數目的組織成員。 封裝可以屬於像它屬於使用者帳戶的組織帳戶。 封裝取用者沒有看到任何使用者帳戶或組織帳戶之間的差異： 兩者都顯示為封裝`owners`。

組織帳戶會有一或多個使用者帳戶做為其成員。 這些成員可以管理一組封裝，同時維持單一識別身分的擁有權。

## <a name="adding-a-new-organization"></a>加入新的組織

若要加入新的組織，選取您的帳戶上 nuget.org，然後選取 **管理組織...** 功能表命令：

![管理員組織在 nuget.org 的功能表選項](media/org-manage-option.png)

在下一個頁面上，選取**加入新的組織**按鈕：

![若要建立新的組織在 nuget.org 的按鈕](media/org-add-new-option.png)

在下一個頁面上，提供組織名稱和電子郵件地址。 因為組織帳戶會共用相同的命名空間，做為使用者帳戶，則必須從現有的組織或使用者帳戶不同的組織名稱。 跨所有帳戶電子郵件地址必須也是唯一。

![Nuget.org 上加入新的組織頁面](media/org-add-new-page.png)

組織帳戶建立之後，您是系統管理員可以送出組織的封裝和加入組織成員。

### <a name="transform-existing-account-to-an-organization"></a>轉換現有的組織帳戶

> [!Warning]
> 帳戶轉換為無法復原： 您無法轉換回給使用者帳戶的組織。

如果您正在為使用單一使用者帳戶的小組管理封裝，並想要將該帳戶轉換成組織中，使用**轉換您的帳戶是組織**選項**管理組織**頁面：

![轉換現有的帳戶是組織在 nuget.org 選項](media/org-transform-option.png)

在下一個頁面上，指定不同的使用者帳戶指派為系統管理員的組織，然後選取**轉換**。

![輸入轉換是組織的使用者帳戶的資訊](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理組織成員

組織系統管理員，您可以新增成員，藉由提供每個成員 nuget.org*使用者帳戶名稱*; 無法使用電子郵件地址。 然後，您會標示每個成員的共同作業者或具有下列權限的系統管理員：

| 權限 | 共同作業者 | 系統管理員 |
| --- | --- | --- |
| 管理組織的封裝<br/>（提交新的封裝、 更新或 unlist 現有的封裝） | [是] | [是] |
| 變更組織中繼資料<br/>（電子郵件地址，通知設定） | 否 | [是] |
| 管理組織成員 | 否 | [是] |
| 要求或 co-ownership 組織封裝要求處理 | 否 | [是] |

## <a name="managing-packages"></a>管理封裝

您可以檢視所有封裝，在您的帳戶及其中您必須是成員的所有組織[管理封裝](https://www.nuget.org/account/Packages)頁面。 若要檢視您的帳戶或任何特定組織專用的封裝，使用帳戶篩選器右上方的頁面。

![使用帳戶篩選來管理封裝](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>將封裝傳送到組織
如果您想要傳送部分封裝到新建立的組織，您可以透過要求來共同擁有封裝的組織帳戶，然後再移除自行為擁有者。 如果您是組織的系統管理員，沒有任何確認才能接受擁有權。 不過，如果您是共同作業者，以擁有者加入組織需要一個接受擁有權的系統管理員。

## <a name="publishing-packages"></a>發行套件

您將封裝發佈到使用者帳戶一樣，是組織發行封裝： 直接上傳至 nuget.org 的封裝，或發送封裝`nuget push`或`dotnet nuget push`CLI 命令。

### <a name="uploading-packages"></a>上傳封裝

當您直接上傳新的封裝上[nuget.org 上載](https://www.nuget.org/packages/manage/upload) 頁面上，您將封裝擁有者的使用者或組織帳戶：

![上傳封裝的帳戶選項](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 金鑰

推播封裝`nuget push`或`dotnet nuget push`CLI 命令，您必須取得 API 金鑰所需的這些命令。 如需詳細資訊，請參閱[發佈封裝](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package)。

在建立新的 API 金鑰時，選取適當的組織中**封裝擁有者**下拉式清單。 您所建立的任何 API 金鑰是僅適用於所選的組織：

![API 金鑰與帳戶選項](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>移除組織

身為使用者，您可以將自己移除組織選取`X`按鈕顯示您組織的成員資格：

![從組織移除使用者帳戶](media/org-remove-self-option.png)

系統管理員可以從組織，包括其他系統管理員移除任何成員。 如果您的組織唯一的系統管理員，您無法移除自己，除非您以系統管理員身分加入另一個成員。

### <a name="deleting-an-organization-account"></a>刪除組織帳戶

這項功能即將推出。
