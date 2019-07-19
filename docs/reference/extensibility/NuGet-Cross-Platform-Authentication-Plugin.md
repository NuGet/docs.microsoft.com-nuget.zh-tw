---
title: NuGet 跨平台驗證外掛程式
description: 適用于 Nuget.exe、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平臺驗證外掛程式
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317284"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 跨平台驗證外掛程式

在 4.8 + 版本中, 所有 NuGet 用戶端 (Nuget.exe、Visual Studio、dotnet 和 Msbuild.exe) 都可以使用建置於[NuGet 跨平臺外掛程式](NuGet-Cross-Platform-Plugins.md)模型之上的驗證外掛程式。

## <a name="authentication-in-dotnetexe"></a>Dotnet 中的驗證

Visual Studio 和 Nuget.exe 預設是互動式的。 Nuget.exe 包含將它設為[非互動](../nuget-exe-CLI-Reference.md)的交換器。
此外, Nuget.exe 和 Visual Studio 外掛程式會提示使用者輸入。
在 dotnet 中, 不會出現提示, 而且預設值為非互動式。

Dotnet 中的驗證機制是裝置流程。 以互動方式執行「還原」或「新增封裝」作業時, 會在命令列上提供作業封鎖, 以及使用者如何完成驗證的指示。
當使用者完成驗證時, 作業將會繼續。

若要讓作業成為互動式作業, 應該`--interactive`傳遞一個。
目前只有明確`dotnet restore`和`dotnet add package`命令支援互動式交換器。
`dotnet build` 和`dotnet publish`上沒有互動開關。

## <a name="authentication-in-msbuild"></a>MSBuild 中的驗證

如同 dotnet, Msbuild.exe 預設為非互動式, 而 Msbuild.exe 驗證機制是裝置流程。
若要讓還原暫停並等候驗證, 請使用`msbuild -t:restore -p:NuGetInteractive="true"`呼叫 restore。

## <a name="creating-a-cross-platform-authentication-plugin"></a>建立跨平臺驗證外掛程式

您可以在[Microsoft 認證提供者外掛程式](https://github.com/Microsoft/artifacts-credprovider)中找到範例執行。

外掛程式必須符合 NuGet 用戶端工具所設定的安全性需求, 這點非常重要。
外掛程式的最低必要版本為「驗證外掛程式」 ( *2.0.0*)。
NuGet 將會執行與外掛程式的交握, 並查詢支援的作業宣告。
如需特定訊息的詳細資訊, 請參閱 NuGet 跨平臺外掛程式[通訊協定訊息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)。

NuGet 會設定記錄層級, 並將 proxy 資訊提供給外掛程式 (如果適用的話)。
只有在 NuGet 已將記錄層級設定為外掛程式之後, 才可接受記錄至 NuGet 主控台。

- .NET Framework 外掛程式驗證行為

在 .NET Framework 中, 允許外掛程式以對話方塊的形式提示使用者輸入。

- .NET Core 外掛程式驗證行為

在 .NET Core 中, 無法顯示對話方塊。 外掛程式應該使用裝置流程來進行驗證。
外掛程式可以透過指示將記錄訊息傳送至 NuGet, 並提供使用者的指示。
請注意, 在記錄層級設定為外掛程式之後, 才可以使用記錄。
NuGet 不會從命令列進行任何互動式輸入。

當用戶端呼叫具有取得驗證認證的外掛程式時, 外掛程式必須符合互動性交換器, 並遵循對話參數。 

下表摘要說明外掛程式在所有組合中的行為方式。

| IsNonInteractive | CanShowDialog | 外掛程式行為 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 參數的優先順序高於對話方塊參數。 不允許外掛程式彈出對話方塊。 此組合僅適用于 .NET Framework 外掛程式 |
| true | False | IsNonInteractive 參數的優先順序高於對話方塊參數。 不允許封鎖此外掛程式。 此組合僅適用于 .NET Core 外掛程式 |
| False | true | 外掛程式應該會顯示對話方塊。 此組合僅適用于 .NET Framework 外掛程式 |
| False | False | 外掛程式應該/無法顯示對話方塊。 外掛程式應該使用裝置流程, 透過記錄器記錄指示訊息來進行驗證。 此組合僅適用于 .NET Core 外掛程式 |

撰寫外掛程式之前, 請參閱下列規格。

- [NuGet 套件下載外掛程式](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet 跨平臺驗證外掛程式](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
