---
title: 3.5 Beta2 版本資訊
description: NuGet 3.5 Beta 2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776390"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 版本資訊

[NuGet 3.5-Beta 版注意事項](../release-notes/nuget-3.5-Beta.md)  | [NuGet 3.5-RC 版本](../release-notes/nuget-3.5-RC.md)資訊

NuGet 3.5 Beta 2 RTM 發行于2016年6月27日，Visual Studio 2013 和 nuget.exe

[完整變更記錄](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[問題清單](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Bug 修正

* 已更新錯誤訊息，以在 .NET Core 中缺少密碼 decrpytion 的支援以進行驗證的摘要- [#2942](https://github.com/NuGet/Home/issues/2942)

* 如果 .NET Core 專案為開啟[#2932](https://github.com/NuGet/Home/issues/2932) ，封裝管理員主控台 Get-Package 會失敗

* 修正 NuGet push 命令[#2910](https://github.com/NuGet/Home/issues/2910)中不正確的403處理

* 修正將 disableSourceControlIntegration 設為 true 時，在系結至 TFS 原始檔控制的解決方案中卸載封裝的問題- [#2739](https://github.com/NuGet/Home/issues/2739)

* 修正套件更新以將非目標套件納入考慮- [#2724](https://github.com/NuGet/Home/issues/2724)

* 使用 MSBuild 詳細資訊層級來設定 Nuget 套件管理員 UI 動作的記錄器層級- [#2705](https://github.com/NuGet/Home/issues/2705)

* 修正 NuGet 設定在網站專案中是不正確錯誤-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* 修正套件中 `.csproj` 包含內容檔案時的問題- [#2658](https://github.com/NuGet/Home/issues/2658)

* `NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 無法運作- [#2653](https://github.com/NuGet/Home/issues/2653)

* 修正在套件建立時，Nuget 3.4.3 版本值不能是 null 的問題- [#2648](https://github.com/NuGet/Home/issues/2648)

* Restore 會使用 VSTS 摘要 Nuget.Config 的預存認證- [#2647](https://github.com/NuGet/Home/issues/2647)

* 效能-修正版本比較程式碼中的過度配置- [#2632](https://github.com/NuGet/Home/issues/2632)

* 修正多個 nuget.exe 實例嘗試以平行方式安裝相同套件時的問題 [#2628](https://github.com/NuGet/Home/issues/2628)

* 效能-快取多專案作業的相依性資訊- [#2619](https://github.com/NuGet/Home/issues/2619)

* 修正來源清單空白時，無法從設定新增套件來源的問題- [#2617](https://github.com/NuGet/Home/issues/2617)

* 修正嘗試安裝相依于設計階段 facade 之套件時的誤導錯誤- [#2594](https://github.com/NuGet/Home/issues/2594)

* 從 >packagemanager 主控台安裝具有「全部」設定的封裝，只會嘗試第一個來源 [#2557](https://github.com/NuGet/Home/issues/2557)

* 修正套件的問題，這些封裝在未來 (Mono) 的檔案有寫入時間 [#2518](https://github.com/NuGet/Home/issues/2518)

* 當在 update 命令中尋找專案失敗時顯示例外狀況- [#2418](https://github.com/NuGet/Home/issues/2418)

* 當套件包含檔案時，從 nuget v1.0 + 摘要安裝套件時，無法正確還原套件內容 `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354) -NoCache

* 修正套件安裝 (所有來源) 當套件從1個來源[#2322](https://github.com/NuGet/Home/issues/2322)遺失時的問題

* 如果單一來源失敗授權，請安裝區塊- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本範圍應覆寫-IncludeReferencedProjects 版本- [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 更新會卸載元件強式名稱和私用屬性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 修正 "DefaultPushSource" 的相對檔案路徑問題- [#1746](https://github.com/NuGet/Home/issues/1746)

* 改善更新解析程式失敗訊息- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>功能與行為變更

* nuget.exe push-timeout 參數無法運作- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restore 不會產生 `.props` 專案的檔案，也不會 `.targets` `.nuproj` (3.4.3.855) 中的回歸 [#2711](https://github.com/NuGet/Home/issues/2711)

* 需要擴充性 API 來比較具有 imports 的架構 [#2633](https://github.com/NuGet/Home/issues/2633)

* 使用 #2486 時隱藏相依性選項 `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* 在詳細的輸出中列印出 nuget.exe 版本標頭- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet 應該新增/runtimes/{rid}/nativeassets/{txm}/的支援- [#2782](https://github.com/NuGet/Home/issues/2782)