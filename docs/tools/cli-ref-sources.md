---
title: NuGet CLI 來源命令
description: Nuget.exe 的參考資料來源的命令
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7c416d92c11328ecb020154981b0ddcc5ba9c5e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818343"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="4a2f8-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4a2f8-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="4a2f8-104">**適用於：** 封裝耗用量、 發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="4a2f8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4a2f8-105">管理使用者範圍的組態檔中指定的組態檔位於來源的清單。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="4a2f8-106">使用者範圍的組態檔是位於`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="4a2f8-107">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="4a2f8-108">使用量</span><span class="sxs-lookup"><span data-stu-id="4a2f8-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="4a2f8-109">其中`<operation>`是其中一個*清單、 加入、 移除、 啟用、 停用，* 或*更新*，`<name>`是來源的名稱和`<source>`是來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="4a2f8-110">選項</span><span class="sxs-lookup"><span data-stu-id="4a2f8-110">Options</span></span>

| <span data-ttu-id="4a2f8-111">選項</span><span class="sxs-lookup"><span data-stu-id="4a2f8-111">Option</span></span> | <span data-ttu-id="4a2f8-112">描述</span><span class="sxs-lookup"><span data-stu-id="4a2f8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a2f8-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4a2f8-113">ConfigFile</span></span> | <span data-ttu-id="4a2f8-114">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4a2f8-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4a2f8-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4a2f8-116">ForceEnglishOutput</span></span> | <span data-ttu-id="4a2f8-117">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4a2f8-118">格式</span><span class="sxs-lookup"><span data-stu-id="4a2f8-118">Format</span></span> | <span data-ttu-id="4a2f8-119">適用於`list`動作，而且可以是`Detailed`（預設值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="4a2f8-120">說明</span><span class="sxs-lookup"><span data-stu-id="4a2f8-120">Help</span></span> | <span data-ttu-id="4a2f8-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="4a2f8-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4a2f8-122">NonInteractive</span></span> | <span data-ttu-id="4a2f8-123">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4a2f8-124">密碼</span><span class="sxs-lookup"><span data-stu-id="4a2f8-124">Password</span></span> | <span data-ttu-id="4a2f8-125">指定與來源進行驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="4a2f8-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="4a2f8-126">StorePasswordInClearText</span></span> | <span data-ttu-id="4a2f8-127">表示將密碼儲存在未加密的文字，而不是將以加密的格式儲存的預設行為。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="4a2f8-128">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="4a2f8-128">UserName</span></span> | <span data-ttu-id="4a2f8-129">指定的使用者名稱與來源進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="4a2f8-130">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4a2f8-130">Verbosity</span></span> | <span data-ttu-id="4a2f8-131">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="4a2f8-132">請務必新增來源的密碼，在相同的使用者內容下，當 nuget.exe 稍後用來存取封裝來源。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="4a2f8-133">密碼將會儲存在組態檔中加密，且僅能解密在相同的使用者內容中因為它已加密。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="4a2f8-134">例如當您使用組建伺服器還原具有相同的組建伺服器 」 工作來執行的 Windows 使用者的密碼必須加密的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="4a2f8-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="4a2f8-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4a2f8-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4a2f8-136">範例</span><span class="sxs-lookup"><span data-stu-id="4a2f8-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
