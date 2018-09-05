---
title: 3.5 Beta2 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.5 Beta 2 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551987"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 版本資訊

[NuGet 3.5 Beta 版本資訊](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 版本資訊](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM 是 2016 年 6 月 27 日發行 Visual Studio 2013 和 nuget.exe

[完整的變更記錄](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[問題清單](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Bug 修正

* 更新的錯誤訊息給不支援已驗證的摘要-.NET Core 中的密碼 decrpytion [# 2942年](https://github.com/NuGet/Home/issues/2942)

* 如果開啟-.NET Core 專案時，就會失敗套件管理員主控台取得封裝[# 2932年](https://github.com/NuGet/Home/issues/2932)

* 在 NuGet push 命令修正不正確地處理 403 [# 2910年](https://github.com/NuGet/Home/issues/2910)

* 修正問題，在解除安裝方案，je-li nastavena disableSourceControlIntegration，繫結至 TFS 原始檔控制中的套件設為 true- [# 2739年](https://github.com/NuGet/Home/issues/2739)

* 修正套件的更新，納入帳戶非目標套件- [# 2724年](https://github.com/NuGet/Home/issues/2724)

* 使用 MSBuild 的詳細資訊層級設定記錄器的層級的 Nuget 套件管理員 UI 動作- [# 2705年](https://github.com/NuGet/Home/issues/2705)

* 修正 NuGet 組態是無效的錯誤，在網站專案-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)

* 修正組件期刊`.csproj`時的內容檔案會包含- [# 2658年](https://github.com/NuGet/Home/issues/2658)

* 在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 無法運作- [# 2653年](https://github.com/NuGet/Home/issues/2653)

* 在-值不可為 null，在封裝建立-Nuget 3.4.3 版本中修正問題[# 2648年](https://github.com/NuGet/Home/issues/2648)

* 還原會使用預存的認證 Nuget.Config，VSTS 摘要- [# 2647年](https://github.com/NuGet/Home/issues/2647)

* 效能-使用中版本 comparsion 程式碼修正過度配置- [# 2632年](https://github.com/NuGet/Home/issues/2632)

* 修正問題，當多個執行個體的 nuget.exe 嘗試以平行方式安裝相同套件[# 2628年](https://github.com/NuGet/Home/issues/2628)

* 效能-快取的多專案作業的相依性資訊- [# 2619年](https://github.com/NuGet/Home/issues/2619)

* 修正問題，當來源清單是空的-時，將會加入從設定的封裝來源不[# 2617年](https://github.com/NuGet/Home/issues/2617)

* 修正誤導錯誤時嘗試安裝套件，取決於設計階段 facade- [# 2594年](https://github.com/NuGet/Home/issues/2594)

* 安裝套件從 PackageManager 主控台中設定 「 All 」 會嘗試第一個來源- [# 2557年](https://github.com/NuGet/Home/issues/2557)

* 修正的問題與寫入的時間在未來的檔案 (Mono)-封裝[# 2518年](https://github.com/NuGet/Home/issues/2518)

* 顯示例外狀況，失敗時尋找專案中更新命令- [# 2418年](https://github.com/NuGet/Home/issues/2418)

* 從 nuget v3.3 + 安裝的套件摘要與引數時未正確地還原套件內容-NoCache 當套件包含`.nupkg`檔案- [# 2354年](https://github.com/NuGet/Home/issues/2354)

* 修正的問題，與套件安裝 （所有來源），當封裝中遺漏 1 的原始檔- [# 2322年](https://github.com/NuGet/Home/issues/2322)

* 如果單一來源授權-就會失敗，請安裝區塊[# 2034年](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本範圍應該覆寫-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新因 '...額外的條件約束中定義 packages.config 可避免這項作業。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 更新卸除組件的強式名稱和私用的屬性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 修正問題相對檔案路徑與"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)

* 改善更新解析程式失敗的訊息- [# 1373年](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>功能與行為變更

* nuget.exe 推送-逾時參數無法運作- [# 2785年](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restore 不會產生`.props`並`.targets`檔案`.nuproj`專案 （在 v3.4.3.855 迴歸）- [# 2711年](https://github.com/NuGet/Home/issues/2711)

* 需要擴充性 API，以比較架構與匯入- [# 2633年](https://github.com/NuGet/Home/issues/2633)

* 使用時，隱藏相依性的選項`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)

* 印出詳細的輸出層中的 nuget.exe 版本標頭[# 1887年](https://github.com/NuGet/Home/issues/1887)

* NuGet 應該新增支援 /runtimes/ {刪除} /nativeassets/ {txm} /- [# 2782年](https://github.com/NuGet/Home/issues/2782)