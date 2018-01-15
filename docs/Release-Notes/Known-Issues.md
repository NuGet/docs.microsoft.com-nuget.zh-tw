---
title: "NuGet 的已知問題 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 42e7a619-1c69-454b-8243-16e2f9f950d0
description: "NuGet 已知問題，包括驗證、套件安裝和工具。"
keywords: "NuGet 已知問題, NuGet 問題"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ce145212da3830216e123f39257a6707712f88c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="eace2-104">NuGet 已知問題</span><span class="sxs-lookup"><span data-stu-id="eace2-104">Known Issues with NuGet</span></span>

<span data-ttu-id="eace2-105">這些是一再回報的最常見 NuGet 已知問題。</span><span class="sxs-lookup"><span data-stu-id="eace2-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="eace2-106">如有安裝 NuGet 或管理套件的問題，請查看這些已知問題及其解決方式。</span><span class="sxs-lookup"><span data-stu-id="eace2-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="eace2-107">從 NuGet 4.0 開始，已知問題成為各版本資訊的一部分。</span><span class="sxs-lookup"><span data-stu-id="eace2-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="eace2-108">使用 nuget.exe v3.4.3 之 VSTS 中的 NuGet 摘要驗證問題</span><span class="sxs-lookup"><span data-stu-id="eace2-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="eace2-109">**問題：**</span><span class="sxs-lookup"><span data-stu-id="eace2-109">**Problem:**</span></span>

<span data-ttu-id="eace2-110">當我們使用下列命令儲存認證時，最後會兩次加密個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eace2-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="eace2-111">$PAT = "您的個人存取權杖" $Feed = "您的 URL" .\nuget.exe 來源新增 -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="eace2-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="eace2-112">**因應措施：**</span><span class="sxs-lookup"><span data-stu-id="eace2-112">**Workaround:**</span></span>

<span data-ttu-id="eace2-113">使用 [-StorePasswordInClearText](../tools/cli-ref-sources.md) 選項以純文字儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="eace2-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="eace2-114">使用 NuGet 3.4、3.4.1 安裝套件時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="eace2-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="eace2-115">**問題：**</span><span class="sxs-lookup"><span data-stu-id="eace2-115">**Problem:**</span></span>

<span data-ttu-id="eace2-116">在 NuGet 3.4 和 3.4.1 中，使用 NuGet 增益集時不會回報任何可用來源，而且無法在 [組態] 視窗中新增新的來源。</span><span class="sxs-lookup"><span data-stu-id="eace2-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="eace2-117">結果類似於下面的映像：</span><span class="sxs-lookup"><span data-stu-id="eace2-117">The result is similar to the image below:</span></span>

![無任何來源的 NuGet 設定](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="eace2-119">意外清空 `%AppData%\NuGet\` 資料夾中的 `NuGet.Config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="eace2-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="eace2-120">若要修正此問題：請關閉 Visual Studio 2015，刪除 `%AppData%\NuGet\` 資料夾的 `NuGet.Config` 檔案，然後重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="eace2-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="eace2-121">會產生新的 `NuGet.Config` 檔案，您就可以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="eace2-121">A new `NuGet.Config` file will be generated and you will be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="eace2-122">使用 NuGet 2.7 安裝套件時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="eace2-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="eace2-123">**問題：**</span><span class="sxs-lookup"><span data-stu-id="eace2-123">**Problem:**</span></span>

<span data-ttu-id="eace2-124">在 NuGet 2.7 或更新版本中，當您嘗試安裝任何包含組件參考的套件時，可能會收到錯誤訊息**「輸入字串格式不正確。」**，如下：</span><span class="sxs-lookup"><span data-stu-id="eace2-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```


<span data-ttu-id="eace2-125">這是因為您的系統上正在取消註冊 `VSLangProj.dll` COM 元件的型別程式庫。</span><span class="sxs-lookup"><span data-stu-id="eace2-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="eace2-126">例如，當您並行安裝了兩個版本的 Visual Studio，然後又解除安裝較舊的版本，就會發生此種情況。</span><span class="sxs-lookup"><span data-stu-id="eace2-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="eace2-127">這樣做，可能會不小心取消註冊上述的 COM 程式庫。</span><span class="sxs-lookup"><span data-stu-id="eace2-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="eace2-128">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="eace2-128">**Solution:**:</span></span>

<span data-ttu-id="eace2-129">從**提升權限的提示字元**執行此命令，以重新註冊 `VSLangProj.dll` 的型別程式庫</span><span class="sxs-lookup"><span data-stu-id="eace2-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="eace2-130">如果命令失敗，請檢查檔案是否位在該位置。</span><span class="sxs-lookup"><span data-stu-id="eace2-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="eace2-131">如需此錯誤的詳細資訊，請參閱此[工作項目](https://nuget.codeplex.com/workitem/3609 "工作項目 3609")。</span><span class="sxs-lookup"><span data-stu-id="eace2-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="eace2-132">在 VS 2012 中更新套件後組建失敗</span><span class="sxs-lookup"><span data-stu-id="eace2-132">Build failure after package update in VS 2012</span></span>
<span data-ttu-id="eace2-133">問題：您使用的是 VS 2012 RTM。</span><span class="sxs-lookup"><span data-stu-id="eace2-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="eace2-134">更新 NuGet 套件時，您會收到這個訊息：「解除安裝一或多個套件無法完成。」</span><span class="sxs-lookup"><span data-stu-id="eace2-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="eace2-135">而且系統會提示重新啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="eace2-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="eace2-136">VS 重新啟動之後，您會收到奇怪的組建錯誤。</span><span class="sxs-lookup"><span data-stu-id="eace2-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="eace2-137">原因是背景 MSBuild 處理序鎖定了舊套件中的某些檔案。</span><span class="sxs-lookup"><span data-stu-id="eace2-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span>
<span data-ttu-id="eace2-138">即使重新啟動 VS 之後，背景 MSBuild 處理序仍在使用舊套件中的檔案，導致組建失敗。</span><span class="sxs-lookup"><span data-stu-id="eace2-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="eace2-139">修正方法是安裝 VS 2012 更新，例如 [VS 2012 Update 2](http://www.microsoft.com/download/details.aspx?id=38188)。</span><span class="sxs-lookup"><span data-stu-id="eace2-139">The fix is to install VS 2012 Update, e.g. [VS 2012 Update 2](http://www.microsoft.com/download/details.aspx?id=38188).</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="eace2-140">從舊版升級至最新的 NuGet 會造成簽章驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="eace2-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="eace2-141">如果您執行的是 VS 2010 SP1，嘗試升級 NuGet 時，如果安裝較舊的版本，可能會遇到下列錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="eace2-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio 延伸模組安裝程式](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="eace2-143">檢視記錄檔時，您可能會看到有關 `SignatureMismatchException` 的記錄。</span><span class="sxs-lookup"><span data-stu-id="eace2-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="eace2-144">為避免發生這種情形，您可以安裝 [Visual Studio 2010 SP1 Hotfix](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="eace2-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="eace2-145">也可以選擇因應措施，只解除安裝 NuGet (以系統管理員身分執行 Visual Studio)，再從 VS 延伸模組庫安裝它。</span><span class="sxs-lookup"><span data-stu-id="eace2-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="eace2-146">如需詳細資訊，請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="eace2-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="eace2-147">如果也安裝了反射程式 Visual Studio 增益集，套件管理員主控台會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eace2-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="eace2-148">執行套件管理員主控台時，如已安裝反射程式 VS 增益集，可能會遇到下列例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="eace2-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="eace2-149">或</span><span class="sxs-lookup"><span data-stu-id="eace2-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="eace2-150">我們已連絡增益集的作者，希望能找到解決之道。</span><span class="sxs-lookup"><span data-stu-id="eace2-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="eace2-151">更新：我們已確認最新版的反射程式 6.5 不會讓主控台再出現這個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eace2-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="eace2-152">開啟套件管理員主控台因 ObjectSecurity 例外狀況而失敗</span><span class="sxs-lookup"><span data-stu-id="eace2-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="eace2-153">嘗試開啟套件管理員主控台時，可能會看到這些錯誤：</span><span class="sxs-lookup"><span data-stu-id="eace2-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="eace2-154">如果發生此種情況，請遵循 [StackOverflow 上討論](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)的解決方案來修正它們。</span><span class="sxs-lookup"><span data-stu-id="eace2-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="eace2-155">如果解決方案包含 InstallShield 限量版專案，[Add Package Library Reference]\ (新增套件程式庫參考) 對話方塊就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eace2-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project.</span></span>

<span data-ttu-id="eace2-156">我們已發現，如果解決方案包含一或多個 InstallShield 限量版專案，開啟 [Add Package Library Reference]\ (新增套件程式庫參考) 對話方塊就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eace2-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="eace2-157">目前除了移除或卸載 InstallShield 專案之外，沒有任何因應措施。</span><span class="sxs-lookup"><span data-stu-id="eace2-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="eace2-158">[解除安裝] 按鈕呈現灰色？</span><span class="sxs-lookup"><span data-stu-id="eace2-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="eace2-159">需要有系統管理員權限才能安裝/解除安裝 NuGet</span><span class="sxs-lookup"><span data-stu-id="eace2-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="eace2-160">如果您嘗試透過 Visual Studio 延伸模組管理員解除安裝 NuGet，您可能注意到 [解除安裝] 按鈕停用。</span><span class="sxs-lookup"><span data-stu-id="eace2-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span>
<span data-ttu-id="eace2-161">需要有系統管理員存取權限才能安裝及解除安裝 NuGet。</span><span class="sxs-lookup"><span data-stu-id="eace2-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="eace2-162">以系統管理員身分重新啟動 Visual Studio 解除安裝延伸模組。</span><span class="sxs-lookup"><span data-stu-id="eace2-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span>
<span data-ttu-id="eace2-163">使用 NuGet 不需要有管理員存取權限。</span><span class="sxs-lookup"><span data-stu-id="eace2-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="eace2-164">在 Windows XP 開啟套件管理員主控台時，後者會損毀。</span><span class="sxs-lookup"><span data-stu-id="eace2-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="eace2-165">出了什麼問題？</span><span class="sxs-lookup"><span data-stu-id="eace2-165">What's wrong?</span></span>

<span data-ttu-id="eace2-166">NuGet 需要 Powershell 2.0 執行階段。</span><span class="sxs-lookup"><span data-stu-id="eace2-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="eace2-167">Windows XP 預設沒有 Powershell 2.0。</span><span class="sxs-lookup"><span data-stu-id="eace2-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="eace2-168">您可以從 [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) 下載 Powershell 2.0 執行階段。</span><span class="sxs-lookup"><span data-stu-id="eace2-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="eace2-169">安裝後，重新啟動 Visual Studio，應該就能夠開啟套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="eace2-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="eace2-170">如果在套件管理員主控台開啟時結束 Visual Studio 2010 SP1 搶鮮版 (Beta)，後者會損毀。</span><span class="sxs-lookup"><span data-stu-id="eace2-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="eace2-171">如已安裝 Visual Studio 2010 SP1 搶鮮版 (Beta)，您可能會發現，如果在套件管理員主控台開啟的情況下關閉 Visual Studio，它會損毀。</span><span class="sxs-lookup"><span data-stu-id="eace2-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="eace2-172">這是 Visual studio 的已知問題，會在 SP1 RTM 版本中修正。</span><span class="sxs-lookup"><span data-stu-id="eace2-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span>
<span data-ttu-id="eace2-173">目前只要忽略損毀或解除安裝 SP1 搶鮮版 (Beta) (如果可以)。</span><span class="sxs-lookup"><span data-stu-id="eace2-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="eace2-174">項目 'Metadata' 發生無效的子項目例外狀況</span><span class="sxs-lookup"><span data-stu-id="eace2-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="eace2-175">如果使用 NuGet 發行前版本安裝了套件組建，以該專案執行 NuGet 的 RTM 版本時，您可能會遇到錯誤訊息，表示「'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' 命名空間的項目 'metadata' 有無效的子項目」。</span><span class="sxs-lookup"><span data-stu-id="eace2-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="eace2-176">您需要使用 NuGet 的 RTM 版本解除安裝並重新安裝每個套件。</span><span class="sxs-lookup"><span data-stu-id="eace2-176">You'll need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-existsrdquo"></a><span data-ttu-id="eace2-177">嘗試安裝或解除安裝會造成錯誤「無法建立已存在的檔案。」</span><span class="sxs-lookup"><span data-stu-id="eace2-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists.&rdquo;</span></span>

<span data-ttu-id="eace2-178">因為某些原因，Visual Studio 會進入很奇怪的狀態，明明已經解除安裝 VSIX 延伸模組，卻會留下某些檔案。</span><span class="sxs-lookup"><span data-stu-id="eace2-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="eace2-179">若要解決這個問題：</span><span class="sxs-lookup"><span data-stu-id="eace2-179">To work around this issue:</span></span>

1. <span data-ttu-id="eace2-180">結束 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eace2-180">Exit Visual Studio</span></span>
2. <span data-ttu-id="eace2-181">開啟下列資料夾 (它可能會在電腦的其他磁碟機上)</span><span class="sxs-lookup"><span data-stu-id="eace2-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="eace2-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<版本>\\</span><span class="sxs-lookup"><span data-stu-id="eace2-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

3. <span data-ttu-id="eace2-183">刪除所有副檔名為 *.deleteme* 的檔案。</span><span class="sxs-lookup"><span data-stu-id="eace2-183">Delete all the files with the *.deleteme* extensions.</span></span>
4. <span data-ttu-id="eace2-184">重新開啟 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eace2-184">Re-open Visual Studio</span></span>

<span data-ttu-id="eace2-185">執行這些步驟之後，應該能夠繼續作業。</span><span class="sxs-lookup"><span data-stu-id="eace2-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="eace2-186">只有在極少數的情況下，在程式碼分析開啟時進行編譯，會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="eace2-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="eace2-187">如果使用套件管理員主控台安裝 FluentNHibernate，然後在 [程式碼分析] 開啟的情況下編譯專案，您可能會收到下列錯誤。</span><span class="sxs-lookup"><span data-stu-id="eace2-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="eace2-188">FluentNHibernate 預設需要 NHibernate 3.0.0.2001。</span><span class="sxs-lookup"><span data-stu-id="eace2-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="eace2-189">但依照設計，NuGet 會在專案中安裝 NHibernate 3.0.0.4000，並新增合適的繫結重新導向，它才會運作。</span><span class="sxs-lookup"><span data-stu-id="eace2-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="eace2-190">如未開啟程式碼分析，您的專案會正常編譯。</span><span class="sxs-lookup"><span data-stu-id="eace2-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="eace2-191">相較於編譯器，程式碼分析工具不會正確遵循繫結重新導向使用 3.0.0.4000，而是使用 3.0.0.2001。</span><span class="sxs-lookup"><span data-stu-id="eace2-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="eace2-192">執行下列作業，安裝 NHibernate 3.0.0.2001 或通知程式碼分析工具要和編譯器有相同的行為，可以暫時解決此問題：</span><span class="sxs-lookup"><span data-stu-id="eace2-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="eace2-193">請移至 *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="eace2-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="eace2-194">開啟 FxCopCmd.exe.config 並將 `AssemblyReferenceResolveMode` 從 `StrongName` 變更成 `StrongNameIgnoringVersion`。</span><span class="sxs-lookup"><span data-stu-id="eace2-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="eace2-195">儲存變更並重建專案。</span><span class="sxs-lookup"><span data-stu-id="eace2-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="eace2-196">Write-Error 命令在 install.ps1/uninstall.ps1/init.ps1 內不起作用</span><span class="sxs-lookup"><span data-stu-id="eace2-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="eace2-197">這是已知的問題。</span><span class="sxs-lookup"><span data-stu-id="eace2-197">This is a known issue.</span></span> <span data-ttu-id="eace2-198">不是呼叫 Write-Error，請嘗試呼叫 throw。</span><span class="sxs-lookup"><span data-stu-id="eace2-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="eace2-199">在 Windows 2003 上以有限的存取安裝 NuGet，會損毀 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eace2-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>
<span data-ttu-id="eace2-200">嘗試不以系統管理員身分執行，使用 Visual Studio 延伸模組管理員安裝 NuGet 時，顯示的 [執行身分] 對話方塊預設會勾選 [Run this program with restricted access]\ (以限制存取權限執行此程式) 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="eace2-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![[Run As Restricted] (以限制身分執行) 對話方塊](./media/RunAsRestricted.png)

<span data-ttu-id="eace2-202">勾選該選項時按一下 [確定] 會損毀 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="eace2-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="eace2-203">請務必先取消核取該選項，再安裝 NuGet。</span><span class="sxs-lookup"><span data-stu-id="eace2-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="eace2-204">無法解除安裝 NuGet for Windows Phone 工具</span><span class="sxs-lookup"><span data-stu-id="eace2-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>
<span data-ttu-id="eace2-205">Windows Phone 工具不支援 Visual Studio 延伸模組管理員。</span><span class="sxs-lookup"><span data-stu-id="eace2-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="eace2-206">為解除安裝 NuGet，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="eace2-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="eace2-207">變更 NuGet 套件識別碼的大小寫會中斷套件還原</span><span class="sxs-lookup"><span data-stu-id="eace2-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>
<span data-ttu-id="eace2-208">如[此 GitHub 問題](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)上所討論的長度，NuGet 支援可變更 NuGet 套件的大小寫，但對在本機套件快取中現有大小寫不同套件的使用者，會在還原套件期間造成很複雜的情況。</span><span class="sxs-lookup"><span data-stu-id="eace2-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="eace2-209">建議您，只有在能與套件現有的使用者，溝通其建置時間套件還原可能發生中斷時，才要求變更大小寫。</span><span class="sxs-lookup"><span data-stu-id="eace2-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="eace2-210">回報問題</span><span class="sxs-lookup"><span data-stu-id="eace2-210">Reporting Issues</span></span>
<span data-ttu-id="eace2-211">若要回報 NuGet 用戶端問題，請前往[這裡](https://nuget.codeplex.com/WorkItem/Create)。</span><span class="sxs-lookup"><span data-stu-id="eace2-211">For reporting issues on NuGet Clients, please go [here](https://nuget.codeplex.com/WorkItem/Create).</span></span>
<span data-ttu-id="eace2-212">若要回報 NuGet 資源庫問題，請前往[這裡](https://github.com/nuget/nugetgallery/issues)。</span><span class="sxs-lookup"><span data-stu-id="eace2-212">For reporting issues on NuGet Gallery, please go [here](https://github.com/nuget/nugetgallery/issues).</span></span>
