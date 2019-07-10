---
title: 您在 NuGet.org 上的組織
description: 在 NuGet.org 上的組織可協助您管理群組發佈或在小組、公司環境中所發佈套件。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427073"
---
# <a name="your-organization-on-nugetorg"></a>您在 NuGet.org 上的組織

組織能讓企業和開放原始碼專案在使用單一 NuGet.org 身分識別的套件上共同作業。 針對套件取用者，會出現和 NuGet.org 現有使用者帳戶相同的組織帳戶。

## <a name="organization-accounts-vs-individual-accounts"></a>組織帳戶與個別帳戶

組織帳戶有一或多個作為其成員的個別 (使用者) 帳戶。 這些成員可以管理一組套件，同時維持擁有權的單一身分識別。

個別帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目的組織成員。 套件可以屬於組織帳戶，如同其可屬於個別帳戶。 套件取用者看不到個別帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。

## <a name="adding-a-new-organization"></a>新增組織

若要新增組織，請選取您在 NuGet.org 上的帳戶，然後選取 [管理組織]  功能表命令：

![NuGet.org 上的管理員組織功能表選項](media/org-manage-option.png)

在下一個頁面上，選取 [新增組織]  按鈕：

![在 NuGet.org 上建立新組織的按鈕](media/org-add-new-option.png)

在下一個頁面上，提供組織名稱和電子郵件地址。 因為組織帳戶會共用和使用者帳戶相同的命名空間，所以組織名稱必須不同於任何其他現有的組織或使用者帳戶。 電子郵件地址在所有帳戶中也必須是唯一的。

![在 NuGet.org 上新增組織頁面](media/org-add-new-page.png)

建立組織帳戶之後，您就是管理員，且可以送出組織套件並新增組織成員。

### <a name="transform-existing-account-to-an-organization"></a>將現有帳戶轉換成組織

> [!Warning]
> 帳戶轉換無法復原：您無法將組織轉換回使用者帳戶。

如果您要使用單一使用者帳戶以小組形式管理套件，且想要將該帳戶轉換成組織，請使用 [管理組織]  頁面上的 [Transform your account to an organization] \(將帳戶轉換成組織\)  選項：

![NuGet.org 上將現有帳戶轉換成組織的選項](media/org-transform-option.png)

在下個頁面上，指定將不同的使用者帳戶指派為組織管理員，然後選取 [轉換]  。

![輸入資訊以將使用者帳戶轉換為組織](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理組織成員

身為組織管理員，您可以藉由提供每個成員的 NuGet.org「使用者帳戶名稱」  來新增成員；無法使用電子郵件地址。 然後，將每個成員標示為具有下列權限的共同作業者或管理員：

| 權限 | 共同作業者 | 系統管理員 |
| --- | --- | --- |
| 管理組織的套件<br/>(提交新套件、更新或取消列出現有的套件) | 是 | 是 |
| 變更組織中繼資料<br/>(電子郵件地址、通知設定) | 否 | 是 |
| 管理組織成員 | 否 | 是 |
| 要求或處理組織套件的共用擁有權要求 | 否 | 是 |

## <a name="managing-packages"></a>管理套件

您可以在 [[管理套件]](https://www.nuget.org/account/Packages) 頁面中檢視您所有帳戶和隸屬所有組織中的所有套件。 若要檢視帳戶或任何特定組織的特定套件，請使用頁面右上方的帳戶篩選器。

![使用帳戶篩選器管理套件](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>將套件傳輸到組織
如果您想要將部分套件傳輸至新建立的組織，您可以要求組織帳戶共同擁有該套件，然後以擁有者身分移除自己來完成此操作。 如果您是組織的管理員，則不需要確認即可接受擁有權。 不過，如果您是共同作業者，當以擁有者身分來新增組織時將需要其中一位管理員來接受擁有權。

## <a name="publishing-packages"></a>發行套件

將套件發佈到組織就像將套件發佈到使用者帳戶一樣：直接將套件上傳至 NuGet.org，或透過 `nuget push` 或 `dotnet nuget push` CLI 命令推送套件。

### <a name="uploading-packages"></a>上傳套件

當您在 [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) (NuGet.org 上傳) 頁面直接上傳新套件時，您會將套件擁有者指派給使用者或組織帳戶：

![使用帳戶選項上傳套件](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 金鑰

若要透過 `nuget push` 或 `dotnet nuget push` CLI 命令推送套件，您必須取得這些命令需要的 API 金鑰。 如需詳細資料，請參閱[發佈套件](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。

建立新的 API 金鑰時，請在 [Package Owner] \(套件擁有者\)  下拉式清單中選取適當的組織。 您建立的任何 API 金鑰僅適用於所選組織：

![具有帳戶選項的 API 金鑰](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>移除組織

身為使用者，您可以選取組織成員資格顯示的 **X** 按鈕，將自己從組織中移除：

![從組織中移除使用者帳戶](media/org-remove-self-option.png)

管理員可以從組織中移除任何成員，包括其他管理員。 如果您是組織唯一的管理員，除非您將其他成員新增為管理員，否則無法移除自己。

### <a name="deleting-an-organization-account"></a>刪除組織帳戶

您可以按一下組織頁面顯示的 [刪除]  按鈕，刪除組織帳戶。

![刪除組織](media/org-delete-option.png)

若要刪除組織，您必須按一下 [刪除組織]  確認按鈕確認作業。
