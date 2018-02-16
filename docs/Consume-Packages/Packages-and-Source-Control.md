---
title: "NuGet 套件和原始檔控制 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "如何在版本設定和原始檔控制系統內處理 NuGet 套件的考量，以及如何以 git 和 TFVC 省略套件。"
keywords: "NuGet 原始檔控制, NuGet 版本設定, NuGet 和 git, NuGet 和 TFS, NuGet 和 TFVC, 省略套件, 原始檔控制存放庫, 版本設定存放庫"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6261625d5d7eaa748f9ad15510b7b2af3c814e44
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>在原始檔控制系統中省略 NuGet 套件

開發人員通常會省略其原始檔控制存放庫的 NuGet 套件，改為依賴[套件還原](../consume-packages/package-restore.md)先重新安裝專案的相依性再建置。

依賴套件還原的原因包括：

1. 分散式版本設定系統，例如 Git，包含存放庫內每個檔案每個版本的完整複本。 經常更新的二進位檔案會導致明顯膨脹，並會增加複製存放庫所花費的時間。
1. 當套件包含在存放庫中時，開發人員傾向直接參考磁碟上的套件內容，而不是透過 NuGet 參考套件，這會導致專案中的硬式編碼路徑名稱。
1. 清除任何未使用過的套件資料夾的解決方案會變得愈來愈困難，因為需要確保不刪除仍在使用的任何套件。
1. 透過略過套件的方式，維護程式碼和來自其他相依人員的套件之間的清楚擁有權界限。 許多 NuGet 套件已在自己的原始檔控制存放庫中進行維護。

雖然套件還原是 NuGet 的預設行為，但仍需某些手動工作從原始檔控制省略套件，&mdash;也就是專案中的 `packages` 資料夾&mdash;，如下列各節中所述。

## <a name="omitting-packages-with-git"></a>使用 Git 省略套件

使用 [.gitignore 檔案](https://git-scm.com/docs/gitignore)以免在原始檔控制中包含 `packages` 資料夾。 如需參考，請參閱 [Visual Studio 專案的範例 `.gitignore`](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)。

`.gitignore` 檔案的重要部分為：

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>使用 Team Foundation 版本設定略過套件

> [!Note]
> 如果可能，請先遵循下列指示再將專案新增至原始檔控制。 否則，請手動刪除存放庫的 `packages` 資料夾，並先簽入該變更再繼續。

停用原始檔控制與所選檔案的 TFVC 整合：

1. 在解決方案資料夾 (`.sln` 檔案所在的資料夾) 中建立名為 `.nuget` 的資料夾。
    - 提示：在 Windows 中，在 Windows 檔案總管中建立這個資料夾，要使用名稱 `.nuget.`「加」結尾後置點。

1. 在該資料夾中，建立名為 `NuGet.Config` 的檔案，再開啟進行編輯。

1. 新增下列文字作為最小值，其中 [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) 設定會指示 Visual Studio 略過 `packages` 資料夾中的所有內容：

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. 如果您使用的是 TFS 2010 或更舊的版本，請隱匿工作區對應中的 `packages` 資料夾。

1. 在 TFS 2012 或更新版本，或使用 Visual Studio Team Services 的版本上，依[新增檔案到伺服器](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore)所述建立 `.tfignore` 檔案。 在該檔案中納入以下內容，明確忽略在存放庫層級和其他幾個中繼檔案中對 `\packages` 資料夾的修改。 (您可以在 Windows 檔案總管中，使用 `.tfignore.` 加結尾後置點的名稱來建立檔案，但可能需要先停用 [Hide known file extensions] \(隱藏已知副檔名) 選項。)：

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. 將 `NuGet.Config` 和 `.tfignore` 新增至原始檔控制，並簽入變更。
