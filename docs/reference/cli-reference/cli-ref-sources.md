---
title: NuGet CLI 來源命令
description: nuget.exe 來源命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622586"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="75359-103">NuGet CLI (的來源命令) </span><span class="sxs-lookup"><span data-stu-id="75359-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="75359-104">**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="75359-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="75359-105">管理位於使用者範圍設定檔或指定設定檔中的來源清單。</span><span class="sxs-lookup"><span data-stu-id="75359-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="75359-106">使用者範圍設定檔位於 `%appdata%\NuGet\NuGet.Config` (Windows) 和 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="75359-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="75359-107">請注意，nuget.org 的來源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="75359-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="75359-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="75359-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="75359-109">其中 `<operation>` 一個 *清單、新增、移除、啟用、停* 用或 *更新* `<name>` 是來源的名稱，而 `<source>` 是來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="75359-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="75359-110">您一次只能在一個來源上操作。</span><span class="sxs-lookup"><span data-stu-id="75359-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="75359-111">選項。</span><span class="sxs-lookup"><span data-stu-id="75359-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="75359-112">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="75359-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="75359-113">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="75359-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="75359-114">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="75359-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="75359-115">適用于 `list` 動作，而且可以 `Detailed` (預設) 或 `Short` 。</span><span class="sxs-lookup"><span data-stu-id="75359-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="75359-116">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="75359-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="75359-117">來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="75359-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="75359-118">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="75359-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="75359-119">指定用來驗證來源的密碼。</span><span class="sxs-lookup"><span data-stu-id="75359-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="75359-120">封裝 (s) 來源的路徑。</span><span class="sxs-lookup"><span data-stu-id="75359-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="75359-121">表示以未加密的文字儲存密碼，而不是儲存加密表單的預設行為。</span><span class="sxs-lookup"><span data-stu-id="75359-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="75359-122">指定要向來源進行驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="75359-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="75359-123">此來源的有效驗證類型清單（以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="75359-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="75359-124">依預設，所有驗證類型都有效。</span><span class="sxs-lookup"><span data-stu-id="75359-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="75359-125">範例： `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="75359-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="75359-126">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="75359-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="75359-127">請務必在與稍後用來存取套件來源的 nuget.exe 相同的使用者內容下新增來源的密碼。</span><span class="sxs-lookup"><span data-stu-id="75359-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="75359-128">密碼會以加密方式儲存在設定檔中，而且只能在其加密時于相同的使用者內容中進行解密。</span><span class="sxs-lookup"><span data-stu-id="75359-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="75359-129">因此，例如，當您使用組建伺服器還原 NuGet 套件時，必須使用組建伺服器工作將執行所在的相同 Windows 使用者來加密密碼。</span><span class="sxs-lookup"><span data-stu-id="75359-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="75359-130">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75359-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75359-131">範例</span><span class="sxs-lookup"><span data-stu-id="75359-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
