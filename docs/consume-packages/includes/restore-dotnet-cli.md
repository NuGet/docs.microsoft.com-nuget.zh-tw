---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825158"
---
使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../../consume-packages/package-references-in-project-files.md)) 中所列的套件。 使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。 截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。

如同其他 `dotnet` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。

使用 `dotnet restore` 還原套件：

```dotnetcli
dotnet restore 
```