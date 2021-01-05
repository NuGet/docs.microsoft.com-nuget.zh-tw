---
title: Visual Studio 中的 NuGet API
description: NuGet 透過 Visual Studio 中的 Managed Extensibility Framework 匯出的 API 介面參考
author: nkolev92
ms.author: nikolev
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 3592280d5398e13e71403023fbb361b5e26e7786
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699872"
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="cfdef-103">Visual Studio 中的 NuGet API</span><span class="sxs-lookup"><span data-stu-id="cfdef-103">NuGet API in Visual Studio</span></span>

<span data-ttu-id="cfdef-104">除了 Visual Studio 中的套件管理員 UI 與主控台以外，NuGet 也會透過 [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index) 匯出某些有用的服務。</span><span class="sxs-lookup"><span data-stu-id="cfdef-104">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span></span> <span data-ttu-id="cfdef-105">這個介面允許 Visual Studio 中的其他元件與 NuGet 互動，NuGet 可以用於安裝和解除安裝套件，以及取得已安裝套件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="cfdef-105">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="cfdef-106">多年來，NuGet 已新增許多服務，這些服務全都位於元件的 `NuGet.VisualStudio` 命名空間中 `NuGet.VisualStudio.dll` ：</span><span class="sxs-lookup"><span data-stu-id="cfdef-106">Over the years, NuGet has added many services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

<span data-ttu-id="cfdef-107">從 NuGet 3.3 +，NuGet 會匯出下列</span><span class="sxs-lookup"><span data-stu-id="cfdef-107">As of NuGet 3.3+, NuGet exports the following</span></span>

- <span data-ttu-id="cfdef-108">[`IRegistryKey`](#iregistrykey-interface)：從登錄子機碼取出值的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-108">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span> <span data-ttu-id="cfdef-109"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-109">(3.3+)</span></span>
- <span data-ttu-id="cfdef-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) 包含取得 NuGet 作業認證的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) Contains methods to get credentials for NuGet operations.</span></span> <span data-ttu-id="cfdef-111"> (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-111">(4.0+)</span></span>
- <span data-ttu-id="cfdef-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) 包含的方法可探索架構與架構之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="cfdef-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="cfdef-113"> (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-113">(4.0+)</span></span>
- <span data-ttu-id="cfdef-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) 包含的方法可探索架構與架構之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="cfdef-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="cfdef-115"> (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-115">(4.0+)</span></span>
- <span data-ttu-id="cfdef-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) 包含的方法可探索架構與架構之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="cfdef-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="cfdef-117"> (5.8 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-117">(5.8+)</span></span>
- <span data-ttu-id="cfdef-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) 處理字串與 [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) 之間轉換的介面 (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) An interface for dealing with the conversion between strings and [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) (4.0+)</span></span>
- <span data-ttu-id="cfdef-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) 剖析 .NET Framework 字串的介面。</span><span class="sxs-lookup"><span data-stu-id="cfdef-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) An interface to parse .NET Framework strings.</span></span> <span data-ttu-id="cfdef-120">請參閱 [NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser)。</span><span class="sxs-lookup"><span data-stu-id="cfdef-120">See [NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser).</span></span> <span data-ttu-id="cfdef-121"> (5.8 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-121">(5.8+)</span></span>
- <span data-ttu-id="cfdef-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) 從解決方案 (4.0 +) 的封裝 (s) 執行 powershell 腳本</span><span class="sxs-lookup"><span data-stu-id="cfdef-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) Execute powershell scripts from package(s) in a solution (4.0+)</span></span>
- <span data-ttu-id="cfdef-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) 代表 .NET 目標 Framework 標記之元件的類型。</span><span class="sxs-lookup"><span data-stu-id="cfdef-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) A type that represents the components of a .NET Target Framework Moniker.</span></span> <span data-ttu-id="cfdef-124"> (5.8 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-124">(5.8+)</span></span>
- <span data-ttu-id="cfdef-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface)：將 NuGet 套件安裝至專案的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span> <span data-ttu-id="cfdef-126"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-126">(3.3+)</span></span>
- <span data-ttu-id="cfdef-127">[' IVsPackageInstaller2](#ivspackageinstaller2-interface) 包含在目前方案內的專案中，將最新版本的單一套件安裝至專案的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-127">[\`IVsPackageInstaller2](#ivspackageinstaller2-interface) Contains method to install latest version of a single package into a project within the current solution.</span></span>
- <span data-ttu-id="cfdef-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface)：套件安裝/卸載的事件。</span><span class="sxs-lookup"><span data-stu-id="cfdef-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span> <span data-ttu-id="cfdef-129"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-129">(3.3+)</span></span>
- <span data-ttu-id="cfdef-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface)：套件安裝/卸載的批次事件。</span><span class="sxs-lookup"><span data-stu-id="cfdef-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span> <span data-ttu-id="cfdef-131"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-131">(3.3+)</span></span>
- <span data-ttu-id="cfdef-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface)：用來在目前方案中取出已安裝套件的方法，並檢查是否已在專案中安裝指定的套件。</span><span class="sxs-lookup"><span data-stu-id="cfdef-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span> <span data-ttu-id="cfdef-133"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-133">(3.3+)</span></span>
- <span data-ttu-id="cfdef-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface)：提供 NuGet 套件替代封裝管理員建議的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span> <span data-ttu-id="cfdef-135"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-135">(3.3+)</span></span>
- <span data-ttu-id="cfdef-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface)：用來取得已安裝套件之相關資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface): Methods to retrieve information about an installed package.</span></span> <span data-ttu-id="cfdef-137"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-137">(3.3+)</span></span>
- <span data-ttu-id="cfdef-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface)：用來取得正在執行之 NuGet 動作之專案相關資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): Methods to retrieve information about a project where NuGet actions are being executed.</span></span> <span data-ttu-id="cfdef-139"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-139">(3.3+)</span></span>
- <span data-ttu-id="cfdef-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface)：還原專案中安裝之套件的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span> <span data-ttu-id="cfdef-141"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-141">(3.3+)</span></span>
- <span data-ttu-id="cfdef-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface)：用來取得 NuGet 套件來源清單的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span> <span data-ttu-id="cfdef-143"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-143">(3.3+)</span></span>
- <span data-ttu-id="cfdef-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface)：從專案卸載 NuGet 套件的方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span> <span data-ttu-id="cfdef-145"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-145">(3.3+)</span></span>
- <span data-ttu-id="cfdef-146">[`IVsPathContext`](#ivspathcontext-interface) 目前內容特定的 NuGet 路徑資訊 (例如專案內容) 。</span><span class="sxs-lookup"><span data-stu-id="cfdef-146">[`IVsPathContext`](#ivspathcontext-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="cfdef-147"> (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-147">(4.0+)</span></span>
- <span data-ttu-id="cfdef-148">[`IVsPathContext2`](#ivspathcontext2-interface) 目前內容特定的 NuGet 路徑資訊 (例如專案內容) 。</span><span class="sxs-lookup"><span data-stu-id="cfdef-148">[`IVsPathContext2`](#ivspathcontext2-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="cfdef-149"> (5.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-149">(5.0+)</span></span>
- <span data-ttu-id="cfdef-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) 用來初始化 [IVsPathCoNtext](#ivspathcontext-interface) 實例的 factory。</span><span class="sxs-lookup"><span data-stu-id="cfdef-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) A factory to initialize [IVsPathContext](#ivspathcontext-interface) instances.</span></span> <span data-ttu-id="cfdef-151"> (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-151">(4.0+)</span></span>
- <span data-ttu-id="cfdef-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) 用來初始化 [IVsPathCoNtext2](#ivspathcontext2-interface) 實例的 factory。</span><span class="sxs-lookup"><span data-stu-id="cfdef-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) A factory to initialize [IVsPathContext2](#ivspathcontext2-interface) instances.</span></span> <span data-ttu-id="cfdef-153"> (5.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-153">(5.0+)</span></span>
- <span data-ttu-id="cfdef-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface)  包含專案 (4.3 + 上舊版 project.js的遷移作業結果) </span><span class="sxs-lookup"><span data-stu-id="cfdef-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface)  Contains the result of the migrate operation on a legacy project.json project (4.3+)</span></span>
- <span data-ttu-id="cfdef-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) 包含方法，可將以傳統專案為基礎的 project.js遷移至 PackageReference 型專案。</span><span class="sxs-lookup"><span data-stu-id="cfdef-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) Contains methods to migrate a project.json based legacy project to PackageReference based project.</span></span> <span data-ttu-id="cfdef-156"> (4.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-156">(4.3+)</span></span>
- <span data-ttu-id="cfdef-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) 用來比較兩個不透明版本字串的介面，方法是將它們視為 NuGet 語義 (4.0 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) An interface for comparing two opaque version strings by treating them as NuGet semantic (4.0+)</span></span>
- <span data-ttu-id="cfdef-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface)：專為專案/專案範本所設計，可包含預先安裝的套件;這個介面 *並非* 用來從程式碼叫用，也沒有公用方法。</span><span class="sxs-lookup"><span data-stu-id="cfdef-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span> <span data-ttu-id="cfdef-159"> (3.3 +) </span><span class="sxs-lookup"><span data-stu-id="cfdef-159">(3.3+)</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="cfdef-160">使用 NuGet 服務</span><span class="sxs-lookup"><span data-stu-id="cfdef-160">Using NuGet services</span></span>

1. <span data-ttu-id="cfdef-161">將 [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) 套件安裝至包含元件的專案 `NuGet.VisualStudio.dll` 。</span><span class="sxs-lookup"><span data-stu-id="cfdef-161">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="cfdef-162">安裝之後，套件會自動將組件參考的 **內嵌 Interop 類型** 屬性設為 **True**。</span><span class="sxs-lookup"><span data-stu-id="cfdef-162">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="cfdef-163">這可讓您的程式碼在使用者更新為較新版本的 NuGet 時具有版本變更方面的彈性。</span><span class="sxs-lookup"><span data-stu-id="cfdef-163">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="cfdef-164">除了您的程式碼中的公用介面，請不要使用任何其他類型，而且不要參考任何其他 NuGet 組件，包括 `NuGet.Core.dll`。</span><span class="sxs-lookup"><span data-stu-id="cfdef-164">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="cfdef-165">若要使用服務，請透過 [MEF 匯入屬性](/dotnet/framework/mef/index#imports-and-exports-with-attributes)匯入它，或透過 [IComponentModel 服務](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel)。</span><span class="sxs-lookup"><span data-stu-id="cfdef-165">To use a service, import it through the [MEF Import attribute](/dotnet/framework/mef/index#imports-and-exports-with-attributes), or through the [IComponentModel service](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="cfdef-166">NuGet.VisualStudio 原始程式碼包含在 [NuGet.Clients 儲存機制](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio) 內，供您參考。</span><span class="sxs-lookup"><span data-stu-id="cfdef-166">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="cfdef-167">IRegistryKey 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-167">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivscredentialprovider-interface"></a><span data-ttu-id="cfdef-168">IVsCredentialProvider 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-168">IVsCredentialProvider interface</span></span>

```cs
    /// <summary>
    /// Contains methods to get credentials for NuGet operations.
    /// </summary>
    public interface IVsCredentialProvider
    {
        /// <summary>
        /// Get credentials for the supplied package source Uri.
        /// </summary>
        /// <param name="uri">The NuGet package source Uri for which credentials are being requested. Implementors are
        /// expected to first determine if this is a package source for which they can supply credentials.
        /// If not, then Null should be returned.</param>
        /// <param name="proxy">Web proxy to use when comunicating on the network.  Null if there is no proxy
        /// authentication configured.</param>
        /// <param name="isProxyRequest">True if if this request is to get proxy authentication
        /// credentials. If the implementation is not valid for acquiring proxy credentials, then
        /// null should be returned.</param>
        /// <param name="isRetry">True if credentials were previously acquired for this uri, but
        /// the supplied credentials did not allow authorized access.</param>
        /// <param name="nonInteractive">If true, then interactive prompts must not be allowed.</param>
        /// <param name="cancellationToken">This cancellation token should be checked to determine if the
        /// operation requesting credentials has been cancelled.</param>
        /// <returns>Credentials acquired by this provider for the given package source uri.
        /// If the provider does not handle requests for the input parameter set, then null should be returned.
        /// If the provider does handle the request, but cannot supply credentials, an exception should be thrown.</returns>
        Task<ICredentials> GetCredentialsAsync(Uri uri,
            IWebProxy proxy,
            bool isProxyRequest,
            bool isRetry,
            bool nonInteractive,
            CancellationToken cancellationToken);
    }
```

## <a name="ivsframeworkcompatibility-interface"></a><span data-ttu-id="cfdef-169">IVsFrameworkCompatibility 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-169">IVsFrameworkCompatibility interface</span></span>

```cs
    /// <summary>
    /// Contains methods to discover frameworks and compatibility between frameworks.
    /// </summary>
    public interface IVsFrameworkCompatibility
    {
        /// <summary>
        /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
        /// </summary>
        IEnumerable<FrameworkName> GetNetStandardFrameworks();

        /// <summary>
        /// Gets frameworks that support packages of the provided .NETStandard version.
        /// </summary>
        /// <remarks>
        /// The result list is not exhaustive as it is meant to human-readable. For example,
        /// equivalent frameworks are not returned. Additionally, a framework name with version X
        /// in the result implies that framework names with versions greater than or equal to X
        /// but having the same <see cref="FrameworkName.Identifier"/> are also supported.
        /// </remarks>
        /// <param name="frameworkName">The .NETStandard version to get supporting frameworks for.</param>
        IEnumerable<FrameworkName> GetFrameworksSupportingNetStandard(FrameworkName frameworkName);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(FrameworkName targetFramework, IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility2-interface"></a><span data-ttu-id="cfdef-170">IVsFrameworkCompatibility2 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-170">IVsFrameworkCompatibility2 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility2 : IVsFrameworkCompatibility
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(
            FrameworkName targetFramework,
            IEnumerable<FrameworkName> fallbackTargetFrameworks,
            IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility3-interface"></a><span data-ttu-id="cfdef-171">IVsFrameworkCompatibility3 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-171">IVsFrameworkCompatibility3 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility3
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworks cannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(IVsNuGetFramework targetFramework, IEnumerable<IVsNuGetFramework> frameworks);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworkscannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(
            IVsNuGetFramework targetFramework,
            IEnumerable<IVsNuGetFramework> fallbackTargetFrameworks,
            IEnumerable<IVsNuGetFramework> frameworks);
    }
```

## <a name="ivsframeworkparser-interface"></a><span data-ttu-id="cfdef-172">IVsFrameworkParser 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-172">IVsFrameworkParser interface</span></span>

```cs
    /// <summary>
    /// An interface for dealing with the conversion between strings and <see cref="FrameworkName"/>
    /// instances.
    /// </summary>
    public interface IVsFrameworkParser
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full framework name
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <param name="shortOrFullName">The framework string.</param>
        /// <exception cref="ArgumentNullException">If the provided string is null.</exception>
        /// <exception cref="ArgumentException">If the provided string cannot be parsed.</exception>
        /// <returns>The parsed framework.</returns>
        FrameworkName ParseFrameworkName(string shortOrFullName);

        /// <summary>
        /// Gets the shortened version of the framework name from a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <remarks>
        /// For example, ".NETFramework,Version=v4.5" is converted to "net45". This is the value
        /// used inside of .nupkg folder structures as well as in project.json files.
        /// </remarks>
        /// <param name="frameworkName">The framework name.</param>
        /// <exception cref="ArgumentNullException">If the input is null.</exception>
        /// <exception cref="ArgumentException">
        /// If the provided framework name cannot be converted to a short name.
        /// </exception>
        /// <returns>The short framework name. </returns>
        string GetShortFrameworkName(FrameworkName frameworkName);
    }
```

## <a name="ivsframeworkparser2-interface"></a><span data-ttu-id="cfdef-173">IVsFrameworkParser2 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-173">IVsFrameworkParser2 interface</span></span>

```cs
    /// <summary>An interface to parse .NET Framework strings. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.</summary>
    public interface IVsFrameworkParser2
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full Target Framework Moniker
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="IVsNuGetFramework"/>
        /// instance.
        /// </summary>
        /// <param name="input">The framework string</param>
        /// <param name="nuGetFramework">The resulting <see cref="IVsNuGetFramework"/>. If the method returns false, this return NuGet's "Unsupported" framework details.</param>
        /// <returns>A boolean to specify whether the input could be parsed into a valid <see cref="IVsNuGetFramework"/> object.</returns>
        /// <remarks>This API is not needed to get framework information about loaded projects, and should not be used to parse the project's TargetFramework property. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.<br/>
        /// This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        bool TryParse(string input, out IVsNuGetFramework nuGetFramework);
    }
```

## <a name="ivsglobalpackagesinitscriptexecutor-interface"></a><span data-ttu-id="cfdef-174">IVsGlobalPackagesInitScriptExecutor 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-174">IVsGlobalPackagesInitScriptExecutor interface</span></span>

```cs
    /// <summary>
    /// Execute powershell scripts from package(s) in a solution
    /// </summary>
    /// <remarks>Intended for internal use only.</remarks>
    public interface IVsGlobalPackagesInitScriptExecutor
    {
        /// <summary>
        /// Executes the init script of the given package if available.
        /// 1) If the init.ps1 script has already been executed by the powershell host, it will not be executed again.
        /// True is returned.
        /// 2) If the package is found in the global packages folder it will be used.
        /// If not, it will return false and do nothing.
        /// 3) Also, note if other scripts are executing while this call was made, it will wait for them to complete.
        /// </summary>
        /// <param name="packageId">Id of the package whose init.ps1 will be executed.</param>
        /// <param name="packageVersion">Version of the package whose init.ps1 will be executed.</param>
        /// <returns>Returns true if the script was executed or has been executed already.</returns>
        /// <remarks>This method throws if the init.ps1 being executed throws.</remarks>
        Task<bool> ExecuteInitScriptAsync(string packageId, string packageVersion);
    }
```

## <a name="ivsnugetframework-interface"></a><span data-ttu-id="cfdef-175">IVsNuGetFramework 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-175">IVsNuGetFramework interface</span></span>

```cs
    /// <summary>A type that represents the components of a .NET Target Framework Moniker.</summary>
    /// <remarks><see cref="System.Runtime.Versioning.FrameworkName"/> does not support .NET 5 Target Framework Monikers with a platform, but this type does.</remarks>
    public interface IVsNuGetFramework
    {
        /// <summary>The framework moniker.</summary>
        string TargetFrameworkMoniker { get; }

        /// <summary>The platform moniker.</summary>
        string TargetPlatformMoniker { get; }

        /// <summary>The platform minimum version.</summary>
        /// <remarks>This property is read by <see cref="IVsFrameworkCompatibility3" />, but will always have a null value when returned from <see cref="IVsFrameworkParser2"/>.</remarks>
        string TargetPlatformMinVersion { get; }
    }
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="cfdef-176">IVsPackageInstaller 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-176">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstaller2-interface"></a><span data-ttu-id="cfdef-177">IVsPackageinstaller2 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-177">IVsPackageinstaller2 interface</span></span>

```cs
   [Guid("4F3B122B-A53B-432C-8D85-0FAFB8BE4FF4")]
    public interface IVsPackageInstaller2 : IVsPackageInstaller
    {
        /// <summary>
        /// Installs the latest version of a single package from the specified package source.
        /// </summary>
        /// <param name="source">
        /// The package source to install the package from. This value can be <c>null</c>
        /// to indicate that the user's configured sources should be used. Otherwise,
        /// this should be the source path as a string. If the user has credentials
        /// configured for a source, this value must exactly match the configured source
        /// value.
        /// </param>
        /// <param name="project">The target project for package installation.</param>
        /// <param name="packageId">The package ID of the package to install.</param>
        /// <param name="includePrerelease">
        /// Whether or not to consider prerelease versions when finding the latest version
        /// to install.
        /// </param>
        /// <param name="ignoreDependencies">
        /// A boolean indicating whether or not to ignore the package's dependencies
        /// during installation.
        /// </param>
        /// <exception cref="InvalidOperationException">
        /// Thrown when <see paramref="includePrerelease"/> is <c>false</c> and no stable version
        /// of the package exists.
        /// </exception>
        void InstallLatestPackage(
            string source,
            Project project,
            string packageId,
            bool includePrerelease,
            bool ignoreDependencies);
    }
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="cfdef-178">IVsPackageInstallerEvents 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-178">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="cfdef-179">IVsPackageInstallerProjectEvents 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-179">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="cfdef-180">IVsPackageInstallerServices 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-180">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="cfdef-181">IVsPackageManagerProvider 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-181">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="cfdef-182">IVsPackageMetadata 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-182">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="cfdef-183">IVsPackageProjectMetadata 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-183">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="cfdef-184">IVsPackageRestorer 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-184">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="cfdef-185">IVsPackageSourceProvider 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-185">IVsPackageSourceProvider interface</span></span>

```cs
/// <summary>
/// A public API for retrieving the list of NuGet package sources.
/// </summary>
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <remarks>Does not require the UI thread.</remarks>
    /// <exception cref="ArgumentException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="ArgumentNullException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidOperationException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidDataException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="cfdef-186">IVsPackageUninstaller 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-186">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivspathcontext-interface"></a><span data-ttu-id="cfdef-187">IVsPathCoNtext 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-187">IVsPathContext interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context).
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    [ComImport]
    [Guid("24A1A187-75EE-4296-A8B3-59F0E0707119")]
    public interface IVsPathContext
    {
        /// <summary>
        /// User package folder directory. The path returned is an absolute path.
        /// </summary>
        string UserPackageFolder { get; }

        /// <summary>
        /// Fallback package folder locations. The paths (if any) in the returned list are absolute paths. If no
        /// fallback package folders are configured, an empty list is returned. The item type of this sequence is
        /// <see cref="string"/>.
        /// </summary>
        IEnumerable FallbackPackageFolders { get; }

        /// <summary>
        /// Fetch a package directory containing the provided asset path.
        /// </summary>
        /// <param name="packageAssetPath">Absolute path to package asset file.</param>
        /// <param name="packageDirectoryPath">Full path to a package directory. 
        /// <code>null</code> if returned falue is <code>false</code>.</param>
        /// <returns>
        /// <code>true</code> when a package containing the given file was found, <code>false</code> - otherwise.
        /// </returns>
        /// <example>
        /// Suppose the project is a packages.config project and the following asset paths are provided:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final\lib\net45\NuGet.Versioning.dll
        /// - C:\path\to\non\package\assembly\Newtonsoft.Json.dll
        /// - C:\src\MyOtherProject\packages\NuGet.Core.2.12.0\lib\net40\NuGet.Core.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.Fake.dll
        /// 
        /// The result will be:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final
        /// - null
        /// - null
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// </example>
        bool TryResolvePackageAsset(string packageAssetPath, out string packageDirectoryPath);
    }
```

## <a name="ivspathcontext2-interface"></a><span data-ttu-id="cfdef-188">IVsPathCoNtext2 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-188">IVsPathContext2 interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context) or solution context
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    public interface IVsPathContext2 : IVsPathContext
    {
        /// <summary>
        /// Solution packages folder directory. This will always be set irrespective if folder actually exists or not.
        /// The path returned is an absolute path.
        /// </summary>
        string SolutionPackageFolder { get; }
    }
```

## <a name="ivspathcontextprovider-interface"></a><span data-ttu-id="cfdef-189">IVsPathCoNtextProvider 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-189">IVsPathContextProvider interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext"/> instances.
    /// </summary>
    public interface IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/>.
        /// </summary>
        /// <param name="projectUniqueName">
        /// Unique identificator of the project. Should be a full path to project file.
        /// </param>
        /// <param name="context">The path context associated with given project.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// False, otherwise, e.g. when provided project is not managed by NuGet.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if projectUniqueName is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateContext(string projectUniqueName, out IVsPathContext context);
    }
```

## <a name="ivspathcontextprovider2-interface"></a><span data-ttu-id="cfdef-190">IVsPathCoNtextProvider2 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-190">IVsPathContextProvider2 interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext2"/> instances.
    /// </summary>
    public interface IVsPathContextProvider2 : IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="solutionDirectory">
        /// path to the solution directory. Must be an absolute path.
        /// It will be performant to pass the solution directory if it's available.
        /// </param>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if solutionDirectory is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(string solutionDirectory, out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/> containing only the user wide and machine wide configurations.
        /// If a solution is loaded, note that the values in the path context might not be the actual effective values for the solution.
        /// If a customer has overriden the `globalPackagesFolder` key or cleared the `fallbackPackageFolders`, these values will be incorrect.
        /// It is important to keep this scenario in mind when working with this path. To predict differences you can call this in combination with <see cref="TryCreateSolutionContext(out IVsPathContext2)"/>.
        /// </summary>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <remarks>
        /// This method can be safely invoked from a background thread. Do note that this method might switch to the UI thread internally, so be mindful of blocking the UI thread on this.
        /// </remarks>
        bool TryCreateNoSolutionContext(out IVsPathContext vsPathContext);

```

## <a name="ivsprojectjsontopackagereferencemigrateresult-interface"></a><span data-ttu-id="cfdef-191">IVsProjectJsonToPackageReferenceMigrateResult 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-191">IVsProjectJsonToPackageReferenceMigrateResult interface</span></span>

```cs
    /// <summary>
    /// Contains the result of the migrate operation on a legacy project.json project
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrateResult
    {
        /// <summary>
        /// Returns the success value of the migration operation.
        /// </summary>
        bool IsSuccess { get; }

        /// <summary>
        /// If migrate operation was unsuccessful, stores the error message in the exception.
        /// </summary>
        string ErrorMessage { get; }
    }
```

## <a name="ivsprojectjsontopackagereferencemigrator-interface"></a><span data-ttu-id="cfdef-192">IVsProjectJsonToPackageReferenceMigrator 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-192">IVsProjectJsonToPackageReferenceMigrator interface</span></span>

```cs
    /// <summary>
    /// Contains methods to migrate a project.json based legacy project to PackageReference based project.
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrator
    {
        /// <summary>
        /// Migrates a legacy Project.json based project to Package Reference based project. The result 
        /// should be casted to type <see cref="IVsProjectJsonToPackageReferenceMigrateResult"/>
        /// The backup of the original project file and project.json file is created in the Backup folder
        /// in the root of the project directory.
        /// </summary>
        /// <param name="projectUniqueName">The full path to the project that needs to be migrated</param>
        Task<object> MigrateProjectJsonToPackageReferenceAsync(string projectUniqueName);

    }
```

## <a name="ivssemanticversioncomparer-interface"></a><span data-ttu-id="cfdef-193">IVsSemanticVersionComparer 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-193">IVsSemanticVersionComparer interface</span></span>

```cs
    /// <summary>
    /// An interface for comparing two opaque version strings by treating them as NuGet semantic
    /// versions.
    /// </summary>
    public interface IVsSemanticVersionComparer
    {
        /// <summary>
        /// Compares two version strings as if they were NuGet semantic version
        /// strings. Returns a number less than zero if <paramref name="versionA"/>
        /// is less than <paramref name="versionB"/>. Returns zero if the two versions 
        /// are equivalent. Returns a number greater than zero if <paramref name="versionA"/>
        /// is greater than <paramref name="versionB"/>.
        /// </summary>
        /// <param name="versionA">The first version string.</param>
        /// <param name="versionB">The second version string.</param>
        /// <exception cref="ArgumentNullException">If either version string is null.</exception>
        /// <exception cref="ArgumentException">If either string cannot be parsed.</exception>
        /// <returns>
        /// A standard comparison integer based on the relationship between the
        /// two provided versions.
        /// </returns>
        int Compare(string versionA, string versionB);
    }
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="cfdef-194">IVsTemplateWizard 介面</span><span class="sxs-lookup"><span data-stu-id="cfdef-194">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
