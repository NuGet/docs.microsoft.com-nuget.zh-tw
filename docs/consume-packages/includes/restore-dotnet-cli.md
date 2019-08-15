---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860612"
---
使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令來還原專案檔 (請參閱 [PackageReference](../../consume-packages/package-references-in-project-files.md)) 中所列的套件。 使用 .NET Core 2.0 和更新版本時，會使用 `dotnet build` 和 `dotnet run` 自動完成還原。 截至 NuGet 4.0，這會執行與 `nuget restore` 相同的程式碼。

如同其他 `dotnet` CLI 命令，請先開啟命令列並切換至包含您專案檔的目錄。

使用 `dotnet restore` 還原套件：

```cli
dotnet restore 
```