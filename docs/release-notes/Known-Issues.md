---
title: 已知問題
description: NuGet 已知問題，包括驗證、套件安裝和工具。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383654"
---
# <a name="known-issues-with-nuget"></a>NuGet 已知問題

這些是一再回報的最常見 NuGet 已知問題。 如有安裝 NuGet 或管理套件的問題，請查看這些已知問題及其解決方式。

> [!Note]
> 從 NuGet 4.0 開始，已知問題成為各版本資訊的一部分。

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>使用 nuget.exe v3.4.3 之 VSTS 中的 NuGet 摘要驗證問題

**問題：**

當我們使用下列命令儲存認證時，最後會兩次加密個人存取權杖。

$PAT = "您的個人存取權杖" $Feed = "您的 URL" .\nuget.exe 來源新增 -Name Test -Source $Feed -UserName $UserName -Password $PAT

**因應措施：**

使用 [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) 選項以純文字儲存密碼。

## <a name="error-installing-packages-with-nuget-34-341"></a>使用 NuGet 3.4、3.4.1 安裝套件時發生錯誤

**問題：**

在 NuGet 3.4 和 3.4.1 中，使用 NuGet 增益集時不會回報任何可用來源，而且無法在 [組態] 視窗中新增新的來源。 結果類似於下面的映像：

![無任何來源的 NuGet 設定](./media/knownIssue-34-NoSources.PNG)

意外清空 `%AppData%\NuGet\` (Windows) 或 `~/.nuget/` (Mac/Linux) 資料夾中的 `NuGet.Config` 檔案。 若要修正此問題：請關閉 Visual Studio (在 Windows 中，如果適用)，刪除 `NuGet.Config` 檔案，然後再次嘗試操作。 NuGet 產生了新的 `NuGet.Config`，而您應該能夠繼續進行。

## <a name="error-installing-packages-with-nuget-27"></a>使用 NuGet 2.7 安裝套件時發生錯誤

**問題：**

在 NuGet 2.7 或更新版本中，當您嘗試安裝任何包含組件參考的套件時，可能會收到錯誤訊息 **「輸入字串格式不正確。」** ，如下：

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

這是因為您的系統上正在取消註冊 `VSLangProj.dll` COM 元件的型別程式庫。 例如，當您並行安裝了兩個版本的 Visual Studio，然後又解除安裝較舊的版本，就會發生此種情況。 這樣做，可能會不小心取消註冊上述的 COM 程式庫。

**解決方案**：

從**提升權限的提示字元**執行此命令，以重新註冊 `VSLangProj.dll` 的型別程式庫

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

如果命令失敗，請檢查檔案是否位在該位置。

如需有關此錯誤的詳細資訊，請參閱此[工作專案](https://nuget.codeplex.com/workitem/3609 "工作專案3609")。

## <a name="build-failure-after-package-update-in-vs-2012"></a>在 VS 2012 中更新套件後組建失敗

問題：您使用的是 VS 2012 RTM。 更新 NuGet 套件時，您會收到這個訊息：「解除安裝一或多個套件無法完成。」 而且系統會提示重新啟動 Visual Studio。 VS 重新啟動之後，您會收到奇怪的組建錯誤。

原因是背景 MSBuild 處理序鎖定了舊套件中的某些檔案。 即使重新啟動 VS 之後，背景 MSBuild 處理序仍在使用舊套件中的檔案，導致組建失敗。

修正方法是安裝 VS 2012 更新，例如 VS 2012 Update 2。

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>從舊版升級至最新的 NuGet 會造成簽章驗證錯誤

如果您執行的是 VS 2010 SP1，嘗試升級 NuGet 時，如果安裝較舊的版本，可能會遇到下列錯誤訊息。

![Visual Studio 延伸模組安裝程式](./media/Visual-Studio-Extension-Installer.png)

檢視記錄檔時，您可能會看到有關 `SignatureMismatchException` 的記錄。

為避免發生這種情形，您可以安裝 [Visual Studio 2010 SP1 Hotfix](http://bit.ly/vsixcertfix)。
也可以選擇因應措施，只解除安裝 NuGet (以系統管理員身分執行 Visual Studio)，再從 VS 延伸模組庫安裝它。 如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>。

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>如果也安裝了反射程式 Visual Studio 增益集，套件管理員主控台會擲回例外狀況。

執行套件管理員主控台時，如已安裝反射程式 VS 增益集，可能會遇到下列例外狀況訊息。

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

或

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

我們已連絡增益集的作者，希望能找到解決之道。

<p class="info">更新：我們已確認最新版的反射程式 6.5 不會讓主控台再出現這個例外狀況。</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>開啟套件管理員主控台因 ObjectSecurity 例外狀況而失敗

嘗試開啟套件管理員主控台時，可能會看到這些錯誤：

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

如果發生此種情況，請遵循 [StackOverflow 上討論](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm)的解決方案來修正它們。

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>如果解決方案包含 InstallShield 限量版專案，[Add Package Library Reference] \(新增套件程式庫參考) 對話方塊就會擲回例外狀況

我們已發現，如果解決方案包含一或多個 InstallShield 限量版專案，開啟 [Add Package Library Reference] \(新增套件程式庫參考) 對話方塊就會擲回例外狀況。 目前除了移除或卸載 InstallShield 專案之外，沒有任何因應措施。

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>[解除安裝] 按鈕呈現灰色？ 需要有系統管理員權限才能安裝/解除安裝 NuGet

如果您嘗試透過 Visual Studio 延伸模組管理員解除安裝 NuGet，您可能注意到 [解除安裝] 按鈕停用。 需要有系統管理員存取權限才能安裝及解除安裝 NuGet。 以系統管理員身分重新啟動 Visual Studio 解除安裝延伸模組。 使用 NuGet 不需要有管理員存取權限。

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>在 Windows XP 開啟套件管理員主控台時，後者會損毀。 出了什麼問題？

NuGet 需要 Powershell 2.0 執行階段。 Windows XP 預設沒有 Powershell 2.0。 您可以從 <https://support.microsoft.com/kb/968929>下載 Powershell 2.0 執行時間。 安裝後，重新啟動 Visual Studio，應該就能夠開啟套件管理員主控台。

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>如果在套件管理員主控台開啟時結束 Visual Studio 2010 SP1 搶鮮版 (Beta)，後者會損毀。

如已安裝 Visual Studio 2010 SP1 搶鮮版 (Beta)，您可能會發現，如果在套件管理員主控台開啟的情況下關閉 Visual Studio，它會損毀。 這是 Visual studio 的已知問題，會在 SP1 RTM 版本中修正。 目前只要忽略損毀或解除安裝 SP1 搶鮮版 (Beta) (如果可以)。

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>項目 'Metadata' 發生無效的子項目例外狀況

如果使用 NuGet 發行前版本安裝了套件組建，以該專案執行 NuGet 的 RTM 版本時，您可能會遇到錯誤訊息，表示「'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' 命名空間的項目 'metadata' 有無效的子項目」。 您需要使用 NuGet 的 RTM 版本來解除安裝並重新安裝每個套件。

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>嘗試安裝或解除安裝會造成錯誤「無法建立已存在的檔案。」

因為某些原因，Visual Studio 會進入很奇怪的狀態，明明已經解除安裝 VSIX 延伸模組，卻會留下某些檔案。 若要解決這個問題：

1. 結束 Visual Studio
1. 開啟下列資料夾 (它可能會在電腦的其他磁碟機上)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<版本>\

1. 刪除所有副檔名為 *.deleteme* 的檔案。
1. 重新開啟 Visual Studio

執行這些步驟之後，應該能夠繼續作業。

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>只有在極少數的情況下，在程式碼分析開啟時進行編譯，會導致錯誤。

如果使用套件管理員主控台安裝 FluentNHibernate，然後在 [程式碼分析] 開啟的情況下編譯專案，您可能會收到下列錯誤。

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

FluentNHibernate 預設需要 NHibernate 3.0.0.2001。 但依照設計，NuGet 會在專案中安裝 NHibernate 3.0.0.4000，並新增合適的繫結重新導向，它才會運作。 如未開啟程式碼分析，您的專案會正常編譯。 相較於編譯器，程式碼分析工具不會正確遵循繫結重新導向使用 3.0.0.4000，而是使用 3.0.0.2001。 執行下列作業，安裝 NHibernate 3.0.0.2001 或通知程式碼分析工具要和編譯器有相同的行為，可以暫時解決此問題：

1. 請移至 *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. 開啟 FxCopCmd.exe.config 並將 `AssemblyReferenceResolveMode` 從 `StrongName` 變更成 `StrongNameIgnoringVersion`。
1. 儲存變更並重建專案。

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Write-Error 命令在 install.ps1/uninstall.ps1/init.ps1 內不起作用

這是已知的問題。 不是呼叫 Write-Error，請嘗試呼叫 throw。

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>在 Windows 2003 上以有限的存取安裝 NuGet，會損毀 Visual Studio

嘗試不以系統管理員身分執行，使用 Visual Studio 延伸模組管理員安裝 NuGet 時，顯示的 [執行身分] 對話方塊預設會勾選 [Run this program with restricted access] \(以限制存取權限執行此程式) 核取方塊。

![[Run As Restricted] (以限制身分執行) 對話方塊](./media/RunAsRestricted.png)

勾選該選項時按一下 [確定] 會損毀 Visual Studio。 請務必先取消核取該選項，再安裝 NuGet。

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>無法解除安裝 NuGet for Windows Phone 工具

Windows Phone 工具不支援 Visual Studio 延伸模組管理員。 為解除安裝 NuGet，請執行下列命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>變更 NuGet 套件識別碼的大小寫會中斷套件還原

根據在[此 GitHub 問題](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932) \(英文\) 上長時間的討論，NuGet 支援可變更 NuGet 套件的大小寫，但對於在 *global-packages* 資料夾中現有大小寫不同套件的使用者，會在還原套件期間造成很複雜的情況。 建議您，只有在能與套件現有的使用者，溝通其建置時間套件還原可能發生中斷時，才要求變更大小寫。

## <a name="reporting-issues"></a>回報問題

若要回報 NuGet 問題，請瀏覽 [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)。
