# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>基本原理

引進[授權運算式](nuspec.md#license)需求出現有的可靠服務，會提供個別的授權識別碼、 例外狀況識別項或授權運算式的參考文字。
這項服務的額外需求是具有穩定的 URL 結構描述，也是不容易連結腐壞，以便我們可以提供較舊的用戶端的回溯相容性，安全地使用它。

Licenses.nuget.org 可滿足該角色。 Nuget.org 會使用它來提供授權文字參考的封裝，指定使用授權的運算式其授權。 `nuget pack` 或與其他封裝[用戶端工具](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)設定[ `licenseUrl` ](nuspec.md#licenseurl)項目指向提供回溯相容性不支援的舊版用戶端 licenses.nuget.org `license`項目。

## <a name="protocol"></a>通訊協定

Licenses.nuget.org 要檢視其瀏覽器中的人員，提供電腦可讀取的回應。
必須使用 HTTPS 通訊協定，而要求應要以特定方式建構。 它只支援`GET`要求。
它接受授權運算式或授權的例外狀況識別碼做為輸入下面指定的方式。 請注意，，授權運算式的所有項目會區分大小寫，因此所有輸入 licenses.nuget.org 都是區分大小寫以及。

### <a name="license-expressions"></a>授權運算式

#### <a name="request"></a>要求

（當運算式組成的單一授權，包括簡單的情況下） 的授權運算式一定要[URL 編碼](https://tools.ietf.org/html/rfc3986#section-2.1)，當成 licenses.nuget.org 的要求中的路徑。

| 授權運算式 | 若要使用的 URL |
|:---|:---|
MIT                                                | https://licenses.nuget.org/MIT
(MIT)                                              | https://licenses.nuget.org/(MIT)
(LGPL 2.0-僅限使用 FLTK 例外狀況或 Apache-2.0+) | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

服務僅支援授權識別碼和接受的 nuget.org 的授權例外狀況識別項。授權的所有運算式包含不支援的授權識別碼或授權的例外狀況識別碼或，不符合授權運算式語法都視為無效。

#### <a name="response"></a>回應

Licenses.nuget.org 回應包含 HTTP 200 狀態碼和網頁上包含描述的授權運算式的有效授權運算式的要求：
* 如果提供授權運算式，包含 web 網頁會傳回包含該授權參考文字的單一授權識別碼
* 如果提供授權運算式是複合授權運算式，網頁會傳回包含授權運算式與個別的授權或授權的例外狀況參考的連結。

包含無效的授權運算式的任何要求會導致 HTTP 404 回應。

### <a name="license-exceptions"></a>授權例外狀況

#### <a name="request"></a>要求

授權例外狀況識別項必須是 URL 編碼，並當做 licenses.nuget.org 的要求中的路徑。只是單一授權的例外狀況識別項可以在單一要求中提供。 沒有額外的字元，除了授權例外狀況識別項可能存在於 URL 的路徑部分。

| 授權例外狀況識別項 | 若要使用的 URL |
|:---|:---|
FLTK-exception            | https://licenses.nuget.org/FLTK-exception
openvpn-openssl-exception | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a>回應

Licenses.nuget.org 會回應 HTTP 200 回應，包含指定的授權例外狀況的參考文字的網頁與已知的授權例外狀況識別項的要求。

任何包含不支援的授權例外狀況識別項的要求會導致 HTTP 404 回應。