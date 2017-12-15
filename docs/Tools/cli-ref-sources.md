---
title: "NuGet CLI 來源命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Nuget.exe 的參考資料來源的命令"
keywords: "nuget 的來源參考、 來源命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="0d941-104">來源命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0d941-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="0d941-105">**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="0d941-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0d941-106">管理清單的來源位於`%AppData%\NuGet\NuGet.Config`或指定的組態檔。</span><span class="sxs-lookup"><span data-stu-id="0d941-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="0d941-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="0d941-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="0d941-108">其中`<operation>`是其中一個*清單、 加入、 移除、 啟用、 停用，*或*更新*，`<name>`是來源的名稱和`<source>`是來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="0d941-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="0d941-109">選項</span><span class="sxs-lookup"><span data-stu-id="0d941-109">Options</span></span>

| <span data-ttu-id="0d941-110">選項</span><span class="sxs-lookup"><span data-stu-id="0d941-110">Option</span></span> | <span data-ttu-id="0d941-111">說明</span><span class="sxs-lookup"><span data-stu-id="0d941-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d941-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0d941-112">ConfigFile</span></span> | <span data-ttu-id="0d941-113">*（2.5 +)* NuGet 組態檔來套用。</span><span class="sxs-lookup"><span data-stu-id="0d941-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="0d941-114">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="0d941-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="0d941-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0d941-115">ForceEnglishOutput</span></span> | <span data-ttu-id="0d941-116">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="0d941-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0d941-117">格式</span><span class="sxs-lookup"><span data-stu-id="0d941-117">Format</span></span> | <span data-ttu-id="0d941-118">適用於`list`動作，而且可以是`Detailed`（預設值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="0d941-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="0d941-119">說明</span><span class="sxs-lookup"><span data-stu-id="0d941-119">Help</span></span> | <span data-ttu-id="0d941-120">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="0d941-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="0d941-121">非互動式</span><span class="sxs-lookup"><span data-stu-id="0d941-121">NonInteractive</span></span> | <span data-ttu-id="0d941-122">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="0d941-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0d941-123">密碼</span><span class="sxs-lookup"><span data-stu-id="0d941-123">Password</span></span> | <span data-ttu-id="0d941-124">指定與來源進行驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="0d941-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="0d941-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="0d941-125">StorePasswordInClearText</span></span> | <span data-ttu-id="0d941-126">表示將密碼儲存在未加密的文字，而不是將以加密的格式儲存的預設行為。</span><span class="sxs-lookup"><span data-stu-id="0d941-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="0d941-127">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0d941-127">UserName</span></span> | <span data-ttu-id="0d941-128">指定的使用者名稱與來源進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0d941-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="0d941-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="0d941-129">Verbosity</span></span> | <span data-ttu-id="0d941-130">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="0d941-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="0d941-131">請務必新增來源的密碼，在相同的使用者內容下，當 nuget.exe 稍後用來存取封裝來源。</span><span class="sxs-lookup"><span data-stu-id="0d941-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="0d941-132">密碼將會儲存在組態檔中加密，且僅能解密在相同的使用者內容中因為它已加密。</span><span class="sxs-lookup"><span data-stu-id="0d941-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="0d941-133">例如當您使用組建伺服器還原具有相同的組建伺服器 」 工作來執行的 Windows 使用者的密碼必須加密的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="0d941-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="0d941-134">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0d941-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0d941-135">範例</span><span class="sxs-lookup"><span data-stu-id="0d941-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
