# Google 地圖清單匯出書籤

把 Google 地圖的「已儲存清單」匯出成 **CSV、KML、GeoJSON、GPX、JSON** 的書籤小工具（bookmarklet）。

不用安裝擴充功能，也不用 API 金鑰。在 Google 地圖打開清單，點一下書籤，勾好格式就能下載含地址和經緯度的檔案。

👉 **安裝頁面：<https://pinxian53.github.io/gmaps-list-export/>**

## 安裝

1. 打開上面的安裝頁面（或直接在瀏覽器開啟本專案的 `index.html`）。
2. 把「匯出地圖清單」按鈕拖到書籤列。
   - 看不到書籤列：按 `Ctrl+Shift+B`（Mac 是 `⌘+Shift+B`）。
   - 拖不動：按「複製程式碼」，在書籤列按右鍵 →「新增網頁」，把程式碼貼到「網址」欄。

支援桌機版 Chrome、Edge、Firefox。

## 使用

1. 在電腦瀏覽器打開清單的分享連結，或從 Google 地圖左側「已儲存」點進某個清單。
2. 確認網址是清單頁面（含 `/placelists/list/` 或 `!2s`）。
3. 點書籤列上的「匯出地圖清單」，頁面會跳出匯出視窗，顯示清單名稱和地點數。
4. 勾選格式後按「下載」。工具會記住你上次勾選的格式。

> 一次勾多種格式時，Chrome 第一次可能會詢問是否允許下載多個檔案，按允許即可。

## 匯出格式

| 格式 | 適用 |
| --- | --- |
| CSV | Excel、Google 試算表（含 BOM，中文不會亂碼） |
| KML | Google My Maps、Google Earth |
| GeoJSON | QGIS、Leaflet、Mapbox |
| GPX | GPS 裝置、OsmAnd、Organic Maps |
| JSON | 完整原始資料，寫程式用 |

沒有座標的地點只會出現在 CSV 和 JSON。

### CSV 欄位

| 欄位 | 內容 |
| --- | --- |
| `name` | 地點名稱 |
| `address` | 地址 |
| `lat` / `lng` | 緯度、經度 |
| `maps_url` | 用名稱加地址搜尋該地點的 Google 地圖連結 |
| `cid` | Google 內部的地點編號 |
| `place_id` | 短格式地點 ID（`/g/…`） |

## 運作方式

書籤在 Google 地圖頁面中執行，用你目前的登入狀態呼叫 Google 地圖網頁自己使用的清單 API（`/maps/preview/entitylist/getlist`），解析回傳的地點資料後，在瀏覽器本機產生檔案下載。

- 資料只在你的瀏覽器裡處理，不會傳到任何第三方伺服器。
- 勾選的格式存在 Google 地圖網域的 `localStorage`（`__gmle_formats`）。

## 限制

- 使用的是**未公開 API**，Google 改版後可能失效。
- 一次最多抓 **500** 個地點，超過時匯出視窗會提醒。
- 只能匯出你有檢視權限的清單。
- 手機瀏覽器的書籤通常無法執行這類程式，請在電腦上使用。

## 專案結構

```
index.html   # 安裝頁面，書籤程式碼內嵌在「匯出地圖清單」按鈕的 href
README.md
```

## 免責聲明

本專案為非官方工具，與 Google 無關。請遵守 Google 地圖服務條款，僅匯出你有權使用的資料。
