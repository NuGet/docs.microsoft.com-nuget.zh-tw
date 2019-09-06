---
title: 在 Visual Studio for Mac 中安裝和使用 NuGet 套件
description: 在 Visual Studio for Mac 專案中安裝和使用 NuGet 套件程式的逐步解說教學課程。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238474"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>快速入門：在 Visual Studio for Mac 中安裝和使用套件

NuGet 套件包含可重複使用的程式碼，由其他開發人員提供您在專案中使用。 請參閱[什麼是 NuGet？](../What-is-NuGet.md)了解背景知識。 封裝會使用 NuGet 套件管理員安裝到 Visual Studio for Mac 專案中。 本文示範如何使用熱門的[Newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/)套件和 .net Core 主控台專案來處理常式。 相同的程式也適用于其他任何 Xamarin 或 .NET Core 專案。

安裝之後，請使用 `using <namespace>` 參考程式碼中的套件，其中 \<namespace\> 為您使用的套件專用。 建立參考之後，您可以透過其 API 呼叫套件。

> [!Tip]
> **從 nuget.org 開始**：.NET 開發人員通常是透過瀏覽 *nuget.org* 來尋找可在自己應用程式中重複使用的元件。 您可以直接搜尋 *nuget.org*，或在 Visual Studio 中尋找並安裝套件，如此文章所示。 如需一般資訊，請參閱[尋找和評估 NuGet 套件](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>必要條件

- 適用于 Mac 的 Visual Studio 2019。

您可以從 [visualstudio.com](https://www.visualstudio.com/) 免費安裝 2019 Community Edition，或使用 Professional Edition 或 Enterprise Edition。

如果您是在 Windows 上使用 Visual Studio，請參閱[在 Visual Studio 中安裝和使用套件（僅限 Windows）](install-and-use-a-package-in-visual-studio.md)。

## <a name="create-a-project"></a>建立專案

假設 NuGet 套件 支援與專案相同的目標架構，則該套件就可安裝到任何的 .NET 專案中。

在此逐步解說中，請使用簡單的 .NET Core 主控台應用程式。 在 Visual Studio for Mac 中使用 [檔案 **> 新方案**] 建立專案，然後選取 [ **.Net Core > 應用程式] > 主控台應用程式**範本。 按一下 [下一步]。 出現提示時，接受**目標 Framework**的預設值。

Visual Studio 隨即建立專案，而專案會在 [方案總管] 中開啟。

## <a name="add-the-newtonsoftjson-nuget-package"></a>新增 Newtonsoft.Json NuGet 套件

若要安裝套件，您可以使用 NuGet 套件管理員。 當您安裝套件時，NuGet 會將相依性記錄在您的專案檔`packages.config`或檔案中（視專案格式而定）。 如需詳細資訊，請參閱[套件使用概觀和工作流程](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 封裝管理員

1. 在方案總管中，以滑鼠右鍵按一下 [相依性]，然後選擇 [**新增套件 ...** **]** 。

    ![專案參考的管理 NuGet 套件命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. 選擇 [nuget.org] 作為對話方塊左上角的 [**套件來源**]，然後搜尋 [ **Newtonsoft**]，在清單中選取該套件，然後選取 [**新增套件 ...** ]：

    ![尋找 Newtonsoft.Json 套件](media/QS_Use_Mac-03-NewtonsoftJson.png)

    如果您需要 NuGet 套件管理員的詳細資訊，請參閱[使用 Visual Studio for Mac 安裝和管理套件](../consume-packages/install-use-packages-visual-studio.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在應用程式中使用 Newtonsoft.Json API

在專案中使用 Newtonsoft.Json 套件，您可以呼叫其 `JsonConvert.SerializeObject` 方法，將物件轉換成人類可閱讀的字串。

1. `Program.cs`開啟檔案（位於 Solution Pad），並將檔案內容取代為下列程式碼：

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

1. 藉由選取 [**執行] > 開始調試**程式來建立並執行應用程式：

1. 應用程式執行後，您會看到序列化的 JSON 輸出出現在主控台中：

  ![主控台應用程式的輸出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>後續步驟
恭喜，您安裝並使用了您的第一個 NuGet 套件！

> [!div class="nextstepaction"]
> [使用 Visual Studio for Mac 安裝和管理套件](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

若要深入探索 NuGet 所提供的功能，請選取下列連結。

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [專案檔中的套件參考](../consume-packages/package-references-in-project-files.md)
