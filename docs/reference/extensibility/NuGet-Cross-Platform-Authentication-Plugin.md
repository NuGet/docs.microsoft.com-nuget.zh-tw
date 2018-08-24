---
title: NuGet 跨平台驗證外掛程式
description: NuGet NuGet.exe、 dotnet.exe，msbuild.exe 和 Visual Studio 跨平台驗證外掛程式
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 02db20e72f67463fffc45f3cba891ae670d67067
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794164"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 跨平台驗證外掛程式

在版本 4.8 + 中，所有的 NuGet 用戶端 (NuGet.exe，Visual Studio、 dotnet.exe 和 MSBuild.exe) 可以使用頂端的內建的驗證外掛程式[跨平台外掛程式的 NuGet](NuGet-Cross-Platform-Plugins.md)模型。

## <a name="authentication-in-dotnetexe"></a>Dotnet.exe 中的驗證

Visual Studio 和 NuGet.exe 所互動的預設值。 NuGet.exe 會包含的交換器容易[非互動式](../../tools/nuget-exe-CLI-Reference.md)。
此外 NuGet.exe 和 Visual Studio 外掛程式會提示使用者輸入。
Dotnet.exe 中沒有任何提示，而且預設值為非互動式。

Dotnet.exe 中的驗證機制是裝置流程。 當還原或新增作業封鎖與使用者完成驗證將會提供如何在命令列的指示，以互動方式執行封裝作業。
當使用者完成驗證作業會繼續。

若要讓作業更具互動性，其中應傳入`--interactive`。
目前只有明確`dotnet restore`和`dotnet add package`命令支援互動式切換。
在沒有沒有互動式的交換器`dotnet build`和`dotnet publish`。

## <a name="authentication-in-msbuild"></a>在 MSBuild 中的驗證

類似於 dotnet.exe，MSBuild.exe 預設為非互動式 MSBuild.exe 驗證機制是裝置流程。
若要允許暫停並等候驗證還原，呼叫還原與`msbuild /t:restore /p:NuGetInteractive="true"`。

## <a name="creating-a-cross-platform-authentication-plugin"></a>建立跨平台驗證外掛程式

範例實作可在[MSCredProvider 外掛程式](https://github.com/Microsoft/mscredprovider)。

它是非常重要的外掛程式符合規定的 NuGet 用戶端工具的安全性需求。
要驗證外掛程式的外掛程式版本所需的最小*2.0.0*。
NuGet 會執行的外掛程式和查詢的交握，支援此作業的宣告。
跨平台外掛程式 NuGet，請參閱[通訊協定訊息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)如需詳細資訊的特定訊息。

NuGet 會將記錄層級設定，並提供 proxy 資訊，以適時的外掛程式。
NuGet 登入主控台才可接受 NuGet 已設定為外掛程式的記錄層級之後。

- .NET framework 增益集的驗證行為

在.NET Framework，外掛程式可以提示使用者輸入，在對話方塊的表單中。

- .NET core 外掛程式驗證行為

在.NET Core，不會顯示一個對話方塊。 外掛程式應該使用裝置流程驗證。
此外掛程式可以傳送給 NuGet 記錄訊息，指示給使用者。
請注意，記錄至外掛程式設定的記錄層級之後。
NuGet 不會從命令列的任何互動輸入。

當用戶端呼叫以取得的驗證認證的外掛程式時，外掛程式必須符合使用者互動性參數，並採用對話方塊交換器。 

下表摘要說明此外掛程式的所有組合的行為方式。

| IsNonInteractive | CanShowDialog | 外掛程式行為 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 參數的優先順序高於對話方塊交換器。 此外掛程式不是允許快顯對話方塊。 這種組合是唯一有效的.NET Framework 外掛程式 |
| true | False | IsNonInteractive 參數的優先順序高於對話方塊交換器。 封鎖不允許此外掛程式。 這種組合是唯一有效的.NET Core 外掛程式 |
| False | true | 此外掛程式應該會顯示一個對話方塊。 這種組合是唯一有效的.NET Framework 外掛程式 |
| False | False | 此外掛程式可以應該不會顯示對話方塊。 此外掛程式應該使用裝置流程來驗證記錄透過記錄器指示訊息。 這種組合是唯一有效的.NET Core 外掛程式 |

請參閱下列規格之前撰寫的外掛程式。

- [NuGet 封裝下載外掛程式](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [跨平台驗證外掛程式的 NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
