---
title: NuGet CLI 來源命令
description: Nuget.exe 的參考來源的命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610630"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b310c-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b310c-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b310c-104">**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="b310c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b310c-105">管理在使用者範圍的組態檔，或是指定的組態檔中的來源清單。</span><span class="sxs-lookup"><span data-stu-id="b310c-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="b310c-106">使用者範圍的組態檔是位於`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="b310c-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="b310c-107">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="b310c-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b310c-108">使用量</span><span class="sxs-lookup"><span data-stu-id="b310c-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b310c-109">其中`<operation>`是其中一個*清單中，新增、 移除、 啟用、 停用，* 或*更新*，`<name>`是原始碼的名稱和`<source>`是來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="b310c-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="b310c-110">您可以操作一次只能有一個來源。</span><span class="sxs-lookup"><span data-stu-id="b310c-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="b310c-111">選項</span><span class="sxs-lookup"><span data-stu-id="b310c-111">Options</span></span>

| <span data-ttu-id="b310c-112">選項</span><span class="sxs-lookup"><span data-stu-id="b310c-112">Option</span></span> | <span data-ttu-id="b310c-113">描述</span><span class="sxs-lookup"><span data-stu-id="b310c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b310c-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b310c-114">ConfigFile</span></span> | <span data-ttu-id="b310c-115">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="b310c-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b310c-116">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="b310c-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b310c-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b310c-117">ForceEnglishOutput</span></span> | <span data-ttu-id="b310c-118">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="b310c-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b310c-119">格式</span><span class="sxs-lookup"><span data-stu-id="b310c-119">Format</span></span> | <span data-ttu-id="b310c-120">適用於`list`動作，而且不可`Detailed`（預設值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="b310c-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b310c-121">Help</span><span class="sxs-lookup"><span data-stu-id="b310c-121">Help</span></span> | <span data-ttu-id="b310c-122">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="b310c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="b310c-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b310c-123">NonInteractive</span></span> | <span data-ttu-id="b310c-124">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="b310c-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b310c-125">密碼</span><span class="sxs-lookup"><span data-stu-id="b310c-125">Password</span></span> | <span data-ttu-id="b310c-126">指定與來源進行驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="b310c-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b310c-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b310c-127">StorePasswordInClearText</span></span> | <span data-ttu-id="b310c-128">表示將密碼儲存在未加密的文字，而不是儲存以加密的格式的預設行為。</span><span class="sxs-lookup"><span data-stu-id="b310c-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b310c-129">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b310c-129">UserName</span></span> | <span data-ttu-id="b310c-130">指定與來源進行驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b310c-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b310c-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b310c-131">Verbosity</span></span> | <span data-ttu-id="b310c-132">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="b310c-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="b310c-133">請務必新增來源的密碼，在相同的使用者內容下，nuget.exe 稍後會用來存取封裝來源。</span><span class="sxs-lookup"><span data-stu-id="b310c-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b310c-134">密碼將會儲存在組態檔中加密，且僅能解密在相同的使用者內容中，已經過加密。</span><span class="sxs-lookup"><span data-stu-id="b310c-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b310c-135">例如當您使用組建伺服器具有相同的 Windows 使用者在其下執行組建伺服器工作會還原 NuGet 套件必須加密的密碼。</span><span class="sxs-lookup"><span data-stu-id="b310c-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b310c-136">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b310c-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b310c-137">範例</span><span class="sxs-lookup"><span data-stu-id="b310c-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
