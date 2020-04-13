---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427113"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>基本原理

引進[授權運算式](../reference/nuspec.md#license)後，出現要有可靠服務的需求，該服務得提供個別授權識別碼的參考文字、例外狀況識別碼或授權運算式。
這項服務的另一項需求是要有穩定的 URL 結構描述，也就是連結不容易腐壞，以便我們可以安全地用它為較舊的用戶端提供回溯相容性。

Licenses.nuget.org 可滿足該角色。 Nuget.org 使用它來為使用授權運算式指定授權的套件提供授權文字參考。 `nuget pack` 或使用其他[用戶端工具](../install-nuget-client-tools.md)來封裝會設定 [`licenseUrl`](../reference/nuspec.md#licenseurl) 元素以指向 licenses.nuget.org，為不支援 `license` 元素的舊版用戶端提供回溯相容性。

## <a name="protocol"></a>通訊協定

Licenses.nuget.org 是為了讓人們在瀏覽器中檢視並不會提供任何電腦可讀取的回應。
必須使用 HTTPS 通訊協定，而要求應該要以特定方式建構。 它只支援 `GET` 要求。
它接受授權運算式或授權例外狀況識別碼，作為以下方式指定的輸入。 請注意，授權運算式的所有元素都會區分大小寫，因此對 licenses.nuget.org 的所有輸入也都會區分大小寫。

### <a name="license-expressions"></a>授權運算式

#### <a name="request"></a>要求

授權運算式 (包括運算式由單一授權組成的簡單情況) 必須要 [URL 編碼](https://tools.ietf.org/html/rfc3986#section-2.1)，且用作 licenses.nuget.org 要求中的路徑。

| 授權運算式 | 要使用的 URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (僅限 LGPL 2.0，FLTK 或 Apache-2.0+ 例外) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

該服務僅支援nuget.org接受的許可證標識符和許可證例外標識符。包含不支援的許可證識別碼或許可證異常識別碼或不符合許可證表達式語法的所有許可證表達式都被視爲無效。

#### <a name="response"></a>回應

Licenses.nuget.org 會回應包含有效授權運算式且具有 HTTP 200 狀態碼的要求，以及包含授權運算式描述的網頁：

* 如果提供的授權運算式包含單一授權識別碼，則會傳回包含該授權參考文字的網頁；
* 如果提供的授權運算式是複合授權運算式，則會傳回包含授權運算式以及個別授權或授權例外狀況參考連結的網頁。

包含無效授權運算式的任何要求會導致 HTTP 404 回應。

### <a name="license-exceptions"></a>授權例外狀況

#### <a name="request"></a>要求

許可證異常識別碼必須對網址進行編碼,並用作請求licenses.nuget.org中的路徑。在單個請求中只能提供單個許可證異常標識符。 除了授權例外狀況識別碼以外沒有額外字元可以存在於 URL 的路徑部分中。

| 授權例外狀況識別碼 | 要使用的 URL |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>回應

Licenses.nuget.org 會回應具有已知授權例外狀況識別碼和 HTTP 200 回應的要求，以及指定授權例外狀況參考文字的網頁。

任何包含不支援授權例外狀況識別碼的要求會導致 HTTP 404 回應。