---
title: "建立原生 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "建立包含 C++ 程式碼而非受控程式碼的原生 NuGet 套件，供 C++ 專案使用的詳細資料。"
keywords: "NuGet 原生套件, NuGet C++ 套件, 原生程式碼套件, 以 C++ 專案為目標"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>建立原生套件

原生套件包含原生 C++ 程式碼而非受控程式碼，所以可以用在 C++ 專案中。 (請參閱＜取用＞一節的[原生 C++ 套件](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages)。)

套件必須以 `native` 架構為目標，才能在 C++ 專案中取用。 目前沒有任何版本號碼與此架構建立關聯，因為 NuGet 對所有 C++ 專案一視同仁。

> [!Note]
> `.nuspec` 的 `<tags>` 區段務必包含 *native*，以協助其他開發人員搜尋該標記以找到您的套件。

原生 NuGet 套件先以 `native` 為目標，再提供 `\build`、`\content` 和 `\tools` 資料夾中的檔案。這種情況不使用 `\lib` (NuGet 無法直接將參考新增至 C++ 專案)。 套件也可以在 `\build` 中包含目標與 props 檔案，NuGet 會自動將它匯入取用該套件的專案。 這些檔案必須與 `.targets` 及/或 `.props` 副檔名的套件識別碼同名。 例如，[cpprestsdk](https://nuget.org/packages/cpprestsdk/) 套件在其 `\build` 資料夾中包含 `cpprestsdk.targets` 檔案。

`\build` 資料夾可用於所有 NuGet 套件，而不只是原生套件。 `\build` 資料夾和 `\content`、`\lib` 和 `\tools` 資料夾一樣採用目標架構。 這表示您可以建立 `\build\net40` 資料夾和 `\build\net45` 資料夾，然後 NuGet 會將適當的 props 和目標檔案匯入專案。 (不需要使用 PowerShell 指令碼匯入 MSBuild 目標。)
