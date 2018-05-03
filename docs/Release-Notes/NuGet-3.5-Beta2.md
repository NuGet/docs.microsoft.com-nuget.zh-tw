---
title: 3.5 Beta2 前版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 Beta 2 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 前版本資訊

[NuGet 3.5 Beta 版本資訊](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 版本資訊](../release-notes/nuget-3.5-RC.md)

Visual Studio 2013 和 nuget.exe NuGet 3.5 Beta 2 RTM 2016 年 6 月 27 日發行

[完整的變更記錄](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[問題清單](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Bug 修正

* 更新的錯誤訊息至不支援在.NET Core 的已驗證的摘要-的密碼 decrpytion [# 2942年](https://github.com/NuGet/Home/issues/2942)

* 封裝管理員主控台取得封裝失敗，則.NET Core 專案開啟- [# 2932年](https://github.com/NuGet/Home/issues/2932)

* NuGet 推入命令中修正不正確地處理 403 [# 2910年](https://github.com/NuGet/Home/issues/2910)

* 請修正問題，在解除安裝 disableSourceControlIntegration 設定時，繫結至 TFS 原始檔控制的方案中的套件設為 true- [# 2739年](https://github.com/NuGet/Home/issues/2739)

* 修正納入帳戶非目標的封裝-封裝更新[# 2724年](https://github.com/NuGet/Home/issues/2724)

* 使用 MSBuild 的詳細資訊層級設定記錄器等級 Nuget 套件管理員的 UI 動作- [# 2705年](https://github.com/NuGet/Home/issues/2705)

* 修正 NuGet 組態是無效的錯誤，在網站專案-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)

* 修正從組件問題`.csproj`時所包含的內容檔案[# 2658年](https://github.com/NuGet/Home/issues/2658)

* 在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 無法運作- [# 2653年](https://github.com/NuGet/Home/issues/2653)

* 值不可為 null，在封裝建立-Nuget 3.4.3 版本中修正問題[# 2648年](https://github.com/NuGet/Home/issues/2648)

* 還原會使用預存的認證 Nuget.Config，VSTS 摘要- [# 2647年](https://github.com/NuGet/Home/issues/2647)

* 效能-使用版本 comparsion 程式碼中修正過度配置- [# 2632年](https://github.com/NuGet/Home/issues/2632)

* 修正問題，當 nuget.exe 的多個執行個體嘗試安裝相同的封裝，以平行方式- [# 2628年](https://github.com/NuGet/Home/issues/2628)

* 效能-快取相依性資訊的多個專案作業- [# 2619年](https://github.com/NuGet/Home/issues/2619)

* 修正問題的來源清單是空的時，將會加入從設定的封裝來源無法[# 2617年](https://github.com/NuGet/Home/issues/2617)

* 修正 Misleading 錯誤時嘗試安裝封裝相依於設計階段外貌- [# 2594年](https://github.com/NuGet/Home/issues/2594)

* 設定"All"PackageManager 主控台從安裝封裝會嘗試第一個來源- [# 2557年](https://github.com/NuGet/Home/issues/2557)

* 修正問題的封裝，寫入時間在未來使用的檔案 （單聲道）- [# 2518年](https://github.com/NuGet/Home/issues/2518)

* 顯示例外狀況時失敗正在尋找專案中沒有更新命令- [# 2418年](https://github.com/NuGet/Home/issues/2418)

* 從 nuget v3.3 + 安裝的套件摘要與引數時未正確地還原套件內容-NoCache 當封裝包含`.nupkg`檔案- [# 2354年](https://github.com/NuGet/Home/issues/2354)

* 修正問題封裝 （所有來源） 時都安裝封裝遺漏來源 1- [# 2322年](https://github.com/NuGet/Home/issues/2322)

* 如果單一來源授權-就會失敗，請安裝區塊[# 2034年](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本範圍應該覆寫-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 此組件強式名稱和私用屬性，會卸除 nuget.exe 更新。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 相對檔案路徑與修正問題，如"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)

* 改善更新解析程式失敗的訊息- [# 1373年](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>功能與行為變更

* nuget.exe 推送的逾時參數無法運作- [# 2785年](https://github.com/NuGet/Home/issues/2785)

* 不會產生 nuget.exe 還原`.props`和`.targets`檔案`.nuproj`專案 （在 v3.4.3.855 迴歸）- [# 2711年](https://github.com/NuGet/Home/issues/2711)

* 需要擴充性 API 來比較架構來使用匯入- [# 2633年](https://github.com/NuGet/Home/issues/2633)

* 隱藏相依性的選項，當使用`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)

* 列印出 nuget.exe 版本標頭中詳細的輸出- [# 1887年](https://github.com/NuGet/Home/issues/1887)

* NuGet 應該加入支援 /runtimes/ {刪除} /nativeassets/ {txm} /- [# 2782年](https://github.com/NuGet/Home/issues/2782)