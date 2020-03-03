---
ms.openlocfilehash: fadb6091f9f1e4f380c3896f790fd61ce80e9683
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230568"
---
<span data-ttu-id="3dbfc-101">套件的選擇性描述（顯示在封裝的 [NuGet.org] 頁面上）會從 `.csproj` 檔案中使用的 `<description></description` 提取，或透過[nuspec](../../reference/nuspec.md)檔案中的 `$description` 提取。</span><span class="sxs-lookup"><span data-stu-id="3dbfc-101">The package's optional description, displayed on the package's NuGet.org page, is either pulled in from the `<description></description` used in the `.csproj` file or pulled in via the `$description` in the [.nuspec file](../../reference/nuspec.md).</span></span>

<span data-ttu-id="3dbfc-102">[_描述_] 欄位的範例會顯示在 .net 封裝之 `.csproj` 檔案的下列 XML 文字中：</span><span class="sxs-lookup"><span data-stu-id="3dbfc-102">An example of a _description_ field is shown in the following XML text of the `.csproj` file for a .NET package:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
