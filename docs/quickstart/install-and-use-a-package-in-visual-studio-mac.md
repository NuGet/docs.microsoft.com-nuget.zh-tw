---
title: 在 Mac 視覺化工作室中安裝與使用 NuGet 套件
description: 有關在 Mac Visual Studio 中安裝和使用 NuGet 包的過程的演練教程。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238474"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>快速入門:在 Mac 可視化工作室中安裝和使用套件

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 使用 NuGet 套件管理員將程式包安裝到 Mac 視覺化工作室專案。 本文演示了使用流行的[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)包和 .NET 核心控制台項目的過程。 相同的流程適用於任何其他 Xamarin 或 .NET Core 專案。

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 建立參考之後，您可以透過其 API 呼叫套件。

> [!Tip]
> **從nuget.org開始**:流覽*nuget.org*是 .NET 開發人員通常如何在他們自己的應用程式中找到他們可以重用的元件。 您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。 如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>Prerequisites

- 視覺工作室 2019 為 Mac.

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。

如果您在 Windows 上使用視覺化工作室,請參閱[在可視化工作室(僅限 Windows)中安裝和使用套件](install-and-use-a-package-in-visual-studio.md)。

## <a name="create-a-project"></a>建立專案

假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。

在本演練中,請使用簡單的 .NET 核心控制台應用。 使用**檔案>新解決方案**在 Visual Studio 中為 Mac 建立專案 **> >...** 按 [下一步]  。 在提示時接受**目標框架**的預設值。

Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

要安裝包,請使用 NuGet 套件管理員。 安裝包時,NuGet 會記錄專案檔`packages.config`或 檔中的依賴項(具體取決於專案格式)。 如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 套件管理員

1. 在解決方案資源管理器中,右鍵單擊**依賴項**並選擇 **"添加包..."**

    ![專案參考的管理 NuGet 套件命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. 選擇對話框左上角的「nuget.org」作為**包源**,然後搜索**Newtonsoft.Json,** 在清單中選擇該包,然後選擇 **「添加包...":**

    ![尋找 Newtonsoft.Json 套件](media/QS_Use_Mac-03-NewtonsoftJson.png)

    如果您想瞭解有關 NuGet 套件管理員的詳細資訊,請參閱使用[Mac 的 Visual Studio 安裝與管理套件](../consume-packages/install-use-packages-visual-studio.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。

1. 開啟`Program.cs`檔案(位於解決方案板中),並將檔案內容取代為以下代碼:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. 以選擇 **「執行>啟動除錯**產生與執行應用:

1. 套用執行後,您將看到序列化的 JSON 輸出顯示在控制台中:

  ![主控台應用輸出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>後續步驟
恭喜，您安裝並使用了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [使用 Mac 的視覺化工作室安裝和管理套件](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)
