---
title: NuGet 錯誤和警告參考
description: 在各種 NuGet 作業期間，從 NuGet 發出的警告和錯誤的完整參考。
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 196b0650866902d753b261dc1bd196ea6601b9df
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775417"
---
# <a name="errors-and-warnings"></a>錯誤和警告

在 NuGet 4.3.0 + 中，錯誤和警告會依照本主題中所述的編號，並提供詳細資訊以協助您解決相關問題。

此處所列的錯誤和警告僅適用于以 [PackageReference 為基礎](../consume-packages/package-references-in-project-files.md) 的專案和 NuGet 4.3.0 +。 NuGet 也會接受 MSBuild 屬性來抑制警告，或將其提升為錯誤。 如需詳細資訊，請參閱 Visual Studio 檔中的 [如何：隱藏編譯器警告](/visualstudio/ide/how-to-suppress-compiler-warnings) 。

## <a name="errors"></a>Errors

| Group | 錯誤號碼 |
| --- | --- |
| 不正確輸入錯誤 | [NU1001](./errors-and-warnings/NU1001.md)、 [NU1002](./errors-and-warnings/NU1002.md)、 [NU1003](./errors-and-warnings/NU1003.md) |
| 遺失套件和專案錯誤 | [NU1100](./errors-and-warnings/NU1100.md)、 [NU1101](./errors-and-warnings/NU1101.md)、 [NU1102](./errors-and-warnings/NU1102.md)、 [NU1103](./errors-and-warnings/NU1103.md)、 [NU1104](./errors-and-warnings/NU1104.md)、 [NU1105](./errors-and-warnings/NU1105.md)、 [NU1106](./errors-and-warnings/NU1106.md)、 [NU1107](./errors-and-warnings/NU1107.md)、 [NU1108](./errors-and-warnings/NU1108.md) |
| 相容性錯誤 | [NU1201](./errors-and-warnings/NU1201.md)、 [NU1202](./errors-and-warnings/NU1202.md)、 [NU1203](./errors-and-warnings/NU1203.md)、 [NU1401](./errors-and-warnings/NU1401.md) |
| NuGet 內部錯誤 | [NU1000](./errors-and-warnings/NU1000.md) |
| 簽署的套件錯誤 (建立和驗證)  | [NU3001](./errors-and-warnings/NU3001.md)、 [NU3004](./errors-and-warnings/NU3004.md)、 [NU3005](./errors-and-warnings/NU3005.md)、 [>nu3008](./errors-and-warnings/NU3008.md)、 [NU3034](./errors-and-warnings/NU3034.md)|
| 套件錯誤 | [NU5000](./errors-and-warnings/NU5000.md)、 [NU5001](./errors-and-warnings/NU5001.md)、 [NU5002](./errors-and-warnings/NU5002.md)、 [NU5003](./errors-and-warnings/NU5003.md)、 [NU5004](./errors-and-warnings/NU5004.md)、 [NU5005](./errors-and-warnings/NU5005.md)、 [NU5007](./errors-and-warnings/NU5007.md)、 [NU5008](./errors-and-warnings/NU5008.md)、 [NU5009](./errors-and-warnings/NU5009.md)、 [NU5010](./errors-and-warnings/NU5010.md)、 [NU5011](./errors-and-warnings/NU5011.md)、NU5012、 [NU5013](./errors-and-warnings/NU5013.md)、 [NU5014、NU5015](./errors-and-warnings/NU5014.md) [、](./errors-and-warnings/NU5015.md) [NU5016、NU5017](./errors-and-warnings/NU5012.md) [、NU5018](./errors-and-warnings/NU5017.md) [、](./errors-and-warnings/NU5018.md) [NU5019、NU5020](./errors-and-warnings/NU5016.md) [、NU5021](./errors-and-warnings/NU5020.md) [、NU5022](./errors-and-warnings/NU5021.md) [、](./errors-and-warnings/NU5022.md) [NU5023、NU5024](./errors-and-warnings/NU5019.md) [、NU5025](./errors-and-warnings/NU5024.md) [、NU5026](./errors-and-warnings/NU5025.md) [、](./errors-and-warnings/NU5026.md) [NU5027、NU5028](./errors-and-warnings/NU5023.md) [、NU5029](./errors-and-warnings/NU5028.md) [、NU5036](./errors-and-warnings/NU5029.md) [、、](./errors-and-warnings/NU5027.md)、、、、、 [、](./errors-and-warnings/NU5036.md)
| 授權特定套件錯誤 | [NU5030](./errors-and-warnings/NU5030.md)、 [NU5031](./errors-and-warnings/NU5031.md)、 [NU5032](./errors-and-warnings/NU5032.md)、 [NU5033](./errors-and-warnings/NU5033.md)、 [NU5034](./errors-and-warnings/NU5034.md)、 [NU5035](./errors-and-warnings/NU5035.md)

## <a name="warnings"></a>警告

| Group | 警告編號 |
| --- | --- |
| 不正確輸入警告 | [NU1501](./errors-and-warnings/NU1501.md)、 [NU1502](./errors-and-warnings/NU1502.md)、 [NU1503](./errors-and-warnings/NU1503.md) |
| 未預期的套件版本警告 | [NU1601](./errors-and-warnings/NU1601.md)、 [NU1602](./errors-and-warnings/NU1602.md)、 [NU1603](./errors-and-warnings/NU1603.md)、 [NU1604](./errors-and-warnings/NU1604.md)、 [NU1605](./errors-and-warnings/NU1605.md)、 [NU1606](./errors-and-warnings/NU1108.md)、 [NU1607](./errors-and-warnings/NU1107.md) |
| 解析程式衝突警告 | [NU1608](./errors-and-warnings/NU1608.md) |
| 封裝回復警告 | [NU1701](./errors-and-warnings/NU1701.md) |
| 摘要警告 | [NU1801](./errors-and-warnings/NU1801.md) |
| NuGet 內部警告 | [NU1500](./errors-and-warnings/NU1500.md) |
| 簽署的封裝警告 (建立和驗證)  | [NU3000](./errors-and-warnings/NU3000.md)、 [NU3002](./errors-and-warnings/NU3002.md)、 [NU3003](./errors-and-warnings/NU3003.md)、 [NU3006](./errors-and-warnings/NU3006.md)、 [NU3007](./errors-and-warnings/NU3007.md)、 [NU3009](./errors-and-warnings/NU3009.md)、 [NU3010](./errors-and-warnings/NU3010.md)、 [NU3011](./errors-and-warnings/NU3011.md)、 [NU3012](./errors-and-warnings/NU3012.md)、 [NU3013](./errors-and-warnings/NU3013.md)、 [NU3014](./errors-and-warnings/NU3014.md)、 [NU3015、NU3016](./errors-and-warnings/NU3015.md)、NU3017 [、NU3018](./errors-and-warnings/NU3017.md) [、NU3019](./errors-and-warnings/NU3018.md) [、](./errors-and-warnings/NU3019.md) [NU3020、NU3021](./errors-and-warnings/NU3016.md) [、NU3022](./errors-and-warnings/NU3021.md) [、NU3023](./errors-and-warnings/NU3022.md) [、](./errors-and-warnings/NU3023.md) [NU3024、NU3025](./errors-and-warnings/NU3020.md) [、NU3026](./errors-and-warnings/NU3025.md) [、NU3027](./errors-and-warnings/NU3026.md) [、](./errors-and-warnings/NU3027.md) [NU3028、NU3029](./errors-and-warnings/NU3024.md) [、NU3030](./errors-and-warnings/NU3029.md) [、NU3031](./errors-and-warnings/NU3030.md) [、](./errors-and-warnings/NU3031.md) [NU3032、NU3033](./errors-and-warnings/NU3028.md) [、NU3035](./errors-and-warnings/NU3033.md) [、NU3036](./errors-and-warnings/NU3035.md)、 [NU3037](./errors-and-warnings/NU3037.md)、 [NU3038、](./errors-and-warnings/NU3038.md) [NU3040、](./errors-and-warnings/NU3036.md) [、、](./errors-and-warnings/NU3032.md) [、](./errors-and-warnings/NU3040.md) |
| 套件警告 | [NU5100](./errors-and-warnings/NU5100.md)、 [NU5101](./errors-and-warnings/NU5101.md)、 [NU5102](./errors-and-warnings/NU5102.md)、 [NU5103](./errors-and-warnings/NU5103.md)、 [NU5104](./errors-and-warnings/NU5104.md)、 [NU5105](./errors-and-warnings/NU5105.md)、 [NU5106](./errors-and-warnings/NU5106.md)、 [NU5107](./errors-and-warnings/NU5107.md)、 [NU5108](./errors-and-warnings/NU5108.md)、 [NU5109](./errors-and-warnings/NU5109.md)、 [NU5110](./errors-and-warnings/NU5110.md)、NU5111、 [NU5112](./errors-and-warnings/NU5112.md)、 [NU5114](./errors-and-warnings/NU5114.md)、 [NU5115、](./errors-and-warnings/NU5115.md) [NU5116、NU5117](./errors-and-warnings/NU5111.md) [、NU5118](./errors-and-warnings/NU5117.md) [、](./errors-and-warnings/NU5118.md) [NU5119、NU5120](./errors-and-warnings/NU5116.md) [、NU5121](./errors-and-warnings/NU5120.md) [、NU5122](./errors-and-warnings/NU5121.md) [、](./errors-and-warnings/NU5122.md) [NU5123、NU5127](./errors-and-warnings/NU5119.md) [、NU5128](./errors-and-warnings/NU5127.md) [、](./errors-and-warnings/NU5128.md) [NU5129、NU5130](./errors-and-warnings/NU5123.md)、 [NU5131、NU5500](./errors-and-warnings/NU5500.md) 、、 [、](./errors-and-warnings/NU5130.md)、 [、](./errors-and-warnings/NU5129.md)、、 [、](./errors-and-warnings/NU5131.md)
| 授權特定套件警告 | [NU5124](./errors-and-warnings/NU5124.md)、 [NU5125](./errors-and-warnings/NU5125.md)
| 圖示特定套件警告 | [NU5046](./errors-and-warnings/NU5046.md)、 [NU5047](./errors-and-warnings/NU5047.md)、 [NU5048](./errors-and-warnings/NU5048.md)
