---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, Page Rule

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# 使用頁面規則
{:#use-page-rules}

「頁面規則」指定一些設定及值，以套用至參照網域的特定 URL 型樣。「頁面規則」可協助您根據網站中的每一個個別 URL 來管理安全、效能及可靠性。下表說明可供所有客戶使用的「頁面規則」、它們產生的行為，以及您在使用它們之前應記住的任何特殊考量。

## 安全
{:#page-rules-security}

|**設定** |**行為** |**考量** |
|-----------|----------|----------------|
|**瀏覽器完整性檢查**|尋找濫發垃圾郵件者所濫用的一般 HTTP 標頭，並拒絕對頁面的存取。它也會封鎖沒有使用者代理程式或新增非標準使用者代理程式的訪客（濫用機器人、搜索器或 API 也常使用）。| |
|**停用安全**|停用下列特性：<ul><li>電子郵件模糊化</li> <li>伺服器端排除</li> <li>WAF</li></ul>|如果規則設為停用安全，而且另一個規則設為啟用 WAF，則會優先使用 WAF 規則，而不論其出現順序為何。|
|**電子郵件模糊化**|開啟或關閉「電子郵件模糊化」。| |
|**IP 地理定位標頭**|包括訪客位置的區碼/國碼與對網站的所有要求。在 `CF-IPCountry` HTTP 標頭中可以找到這項資訊。| |  
|**安全層次**|控制用戶端威脅評分必須有多高，用戶端才會遇到盤查頁面。您可以使用此設定，讓網站在訪客造訪您的網站時，一律向訪客呈現**防禦模式**盤查。| |
|**伺服器端排除**|開啟或關閉「伺服器端排除」。| |
|**TLS**|控制所使用的 TLS 模式。| |
|**WAF**|開啟或關閉 WAF。| |  
|**自動 HTTPS 重寫**|開啟或關閉「自動 HTTPS 重寫」。| |
|**機會性加密**|開啟或關閉「機會性加密」。| |
|**快取欺詐保護**|開啟或關閉「快取欺詐保護」。| |
|**一律使用 HTTPS**|建立 `301` 重新導向，將任何 `http://` URL 轉換為 `https://` URL。|使用此設定會停用配置規則的所有其他設定，因為 IBM CIS 會針對要求強制重新導向至 `HTTPS`，而此要求會變成接著針對「頁面規則」評估的新要求。|
|**真正用戶端 IP 標頭**|CIS 會以 `True-Client-IP` 標頭傳送一般使用者的 IP 位址。|僅限企業|

## 效能
{:#page-rules-performance}

|**設定** |**行為** |**考量** |
|-----------|----------|----------------|
|**瀏覽器快取 TTL**|控制用戶端瀏覽器所快取的資源保持有效多久的時間。| |
|**略過 Cookie 上的快取**|除非我們看到特定名稱的 Cookie，否則會提供快取的物件，例如，除非我們看到指出客戶已登入的 `SessionID` Cookie，否則會提供首頁的快取版本，因此應該呈現個人化內容。| |
|**快取層次**|**略過** - 不快取符合該「頁面規則」的資源。<br>**無查詢字串** - 沒有查詢字串時，只會從快取中遞送資源。<br>**忽略查詢字串** - 將相同的資源遞送給與查詢字串無關的每一個人。<br>**標準** - 每次查詢字串變更時，都會遞送不同的資源。<br> **快取所有項目** - 快取符合「頁面規則」的資源。|依預設，不會快取 HTML 內容。必須寫入快取靜態 HTML 內容的「頁面規則」。|
|**邊緣快取 TTL**|控制 IBM CIS 將在快取中保留檔案多久的時間。|指定快取層次時，這是選用設定。|
|**解析置換**|變更符合頁面規則的要求會解析成的 URL 或 IP。||
|**Cookie 上的快取**|根據正規表示式與 Cookie 名稱的比對來套用`快取所有項目`選項（`快取層次`設定）。如果您同時將這項設定以及`略過 Cookie 上的快取`新增至相同的頁面規則，則 `Cookie 上的快取`優先於`略過 Cookie 上的快取`。|僅限企業|
|**停用效能**|關閉：<ul><li>`縮製 Web 內容`</li><li>`影像載入最佳化`</li><li>`影像大小最佳化`</li><li>`Script 載入最佳化`</li></ul> |僅限企業|
|**縮製 Web 內容**|從這些檔案中移除所有不必要的字元，來縮製 HTML、CSS 及/或 JavaScript 檔案。|僅限企業|
|**影像載入最佳化**|透過下列項目，根據網路連線及裝置類型來改善包含影像之頁面的載入時間：<ul><li>**影像虛擬化** - 將影像取代為低解析度位置保留元影像，其與原始影像具有相同維度（包括第三方影像）。當頁面完全呈現後，完整解析影像就會延遲載入（在瀏覽器視圖埠中設定影像的優先順序）。此處理程序可讓頁面快速呈現，並使瀏覽器重排減至最少。</li><li>**要求串流化** - 將影像的多個個別網路要求結合成單一要求。</li></ul> |僅限企業|
|**影像大小最佳化**|透過移除 meta 資料（日期和時間、相機製造商及機型等等）以及儘可能壓縮影像來減少影像檔案大小。檔案大小越小表示影像及網頁的載入時間越快。|僅限企業|
|**排序查詢字串**|不論查詢字串的順序為何，將具有相同查詢字串的檔案都視為快取中的同一個檔案。|僅限企業|
|**回應緩衝**|啟用或停用原點伺服器的回應緩衝。依預設，CIS 會在我們收到封包時將封包傳送給用戶端。啟用「回應緩衝」表示 CIS 會等到擁有整個檔案之後才會轉遞給一般使用者。|僅限企業|
|**Script 載入最佳化**|透過非同步載入 JavaScript（包括協力廠商 Script）來改善繪製時間，使它們不會封鎖頁面內容的呈現。|僅限企業|

## 可靠性
{:#page-rules-reliability}

|**設定** |**行為** |**考量** |
|-----------|----------|----------------|
|**提供過時內容**|如果伺服器關閉，則保持網站的有限版本上線。|如需相關資訊，請檢視[管理 CIS 部署以取得最佳可靠性](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)|
|**原點快取控制**|判定從原點快取的內容及內容更新頻率。|如需相關資訊，請檢視[管理 CIS 部署以取得最佳可靠性](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)|
|**轉遞 URL** |要在網站無法使用時使用的 URL。|使用此項目會停用配置所有其他設定，因為您要將要求轉遞至其他地方。如需相關資訊，請檢視[管理 CIS 部署以取得最佳可靠性](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)|
|**主機標頭置換**|將符合頁面規則之 URI 的主機標頭取代為指定的值。這通常用於 S3 儲存區中管理的內容。|
|**停用應用程式**|關閉所有 CIS 應用程式。|僅限企業|
|**原點錯誤頁面透通**|停用針對從原點伺服器所傳送問題而觸發的 CIS 錯誤頁面，並改為顯示在原點設定的錯誤頁面。|僅限企業||

## 頁面規則 URL 型樣
{:#page-rule-url-patterns}

「頁面規則」將對給定的 URL 型樣生效，並符合下列格式：

`<scheme>://<hostname><:port>/<path>`

使用每一個元件的範例如下：

`https://www.example.com:80/image.png`

*scheme* 及 *port* 是選用元件。如果省略 scheme，則會涵蓋 `http://` 及 `https://` 通訊協定。如果未指定 port，則規則將符合所有埠。您可以在規則型樣中使用 '*' 符號，以執行基本萬用字元相符，讓它符合一連串的類似型樣，而不只是一個型樣。

以下是要記住的三個「頁面規則」重要事項：

 * 只有一個「頁面規則」將對任何給定的要求生效。
 * 「頁面規則」的給定優先順序是從上到下的順序。
 * URL 符合規則之後，只會套用該規則；亦即，如果已對要求觸發「頁面規則」，則任何也符合 URL 型樣的後續規則都不會生效。一般而言，建議您將規則從_最具體_ 到_最不具體_ 進行排序。

「頁面規則」可以予以停用，在這種情況下，這些規則將不會採取任何動作。它們仍然會顯示在清單中，而且可以進行編輯。將**已啟用**切換參數設為**關閉**會建立一開始予以停用的「頁面規則」。

如需相關資訊，請參閱[快取及頁面規則作法文件](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching)。