---
title: NuGet CLI 來源命令
description: Nuget.exe 來源命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327595"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="52a30-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="52a30-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="52a30-104">**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="52a30-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="52a30-105">管理位於使用者範圍設定檔或指定的設定檔中的來源清單。</span><span class="sxs-lookup"><span data-stu-id="52a30-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="52a30-106">使用者範圍設定檔位於`%appdata%\NuGet\NuGet.Config` (Windows) 和`~/.nuget/NuGet/NuGet.Config` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="52a30-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="52a30-107">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="52a30-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="52a30-108">使用量</span><span class="sxs-lookup"><span data-stu-id="52a30-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="52a30-109">其中`<operation>` , 是*清單、新增、移除、啟用、停*用或*更新* `<name>`其中之一, 是來源的名稱, 而`<source>`是來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="52a30-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="52a30-110">您一次只能在一個來源上操作。</span><span class="sxs-lookup"><span data-stu-id="52a30-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="52a30-111">選項</span><span class="sxs-lookup"><span data-stu-id="52a30-111">Options</span></span>

| <span data-ttu-id="52a30-112">選項</span><span class="sxs-lookup"><span data-stu-id="52a30-112">Option</span></span> | <span data-ttu-id="52a30-113">描述</span><span class="sxs-lookup"><span data-stu-id="52a30-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52a30-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="52a30-114">ConfigFile</span></span> | <span data-ttu-id="52a30-115">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="52a30-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="52a30-116">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="52a30-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="52a30-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="52a30-117">ForceEnglishOutput</span></span> | <span data-ttu-id="52a30-118">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="52a30-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="52a30-119">格式</span><span class="sxs-lookup"><span data-stu-id="52a30-119">Format</span></span> | <span data-ttu-id="52a30-120">適用于`Detailed` `Short`動作, 而且可以是 (預設值) 或。 `list`</span><span class="sxs-lookup"><span data-stu-id="52a30-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="52a30-121">Help</span><span class="sxs-lookup"><span data-stu-id="52a30-121">Help</span></span> | <span data-ttu-id="52a30-122">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="52a30-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="52a30-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="52a30-123">NonInteractive</span></span> | <span data-ttu-id="52a30-124">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="52a30-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="52a30-125">密碼</span><span class="sxs-lookup"><span data-stu-id="52a30-125">Password</span></span> | <span data-ttu-id="52a30-126">指定用來驗證來源的密碼。</span><span class="sxs-lookup"><span data-stu-id="52a30-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="52a30-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="52a30-127">StorePasswordInClearText</span></span> | <span data-ttu-id="52a30-128">表示將密碼儲存為未加密的文字, 而不是儲存加密格式的預設行為。</span><span class="sxs-lookup"><span data-stu-id="52a30-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="52a30-129">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="52a30-129">UserName</span></span> | <span data-ttu-id="52a30-130">指定用來驗證來源的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="52a30-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="52a30-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="52a30-131">Verbosity</span></span> | <span data-ttu-id="52a30-132">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="52a30-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="52a30-133">請務必在與 nuget.exe 相同的使用者內容下新增來源的密碼, 以供稍後用來存取封裝來源。</span><span class="sxs-lookup"><span data-stu-id="52a30-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="52a30-134">密碼會以加密方式儲存在設定檔中, 而且只能在加密的相同使用者內容中進行解密。</span><span class="sxs-lookup"><span data-stu-id="52a30-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="52a30-135">例如, 當您使用組建伺服器來還原 NuGet 套件時, 必須使用組建伺服器工作執行所在的相同 Windows 使用者來加密密碼。</span><span class="sxs-lookup"><span data-stu-id="52a30-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="52a30-136">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="52a30-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="52a30-137">範例</span><span class="sxs-lookup"><span data-stu-id="52a30-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
