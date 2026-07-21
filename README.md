# 北北桃捷運互動票價・路線・時間

> 目前對應版本：`v2026.07.20.24`  
> 主程式：`metro.html`

這是一個可直接在瀏覽器開啟的單一 HTML 互動旅程規劃工具，整合台北捷運、新北捷運、桃園機場捷運與輕軌系統。使用者可在路網圖上點選起點與終點，或透過下拉選單設定車站，查看建議路線、轉乘、成人單程票價、估算搭乘時間，以及步行是否可能更快。

本專案不需要安裝套件、啟動伺服器或連接資料庫；HTML、CSS、JavaScript、路線資料與多語文字均包含在同一個檔案內。

## 主要功能

- 單畫面互動路網，預設以 `R10／BL12 台北車站` 為中心。
- 上方為北、右方為東的地理相對配置；為提高可讀性，不依實際比例尺繪製。
- 第一次點擊車站設為起點，第二次點擊設為終點並自動規劃。
- 起訖站下拉選單依「路線 → 英數站碼」自然排序。
- 自動顯示建議路線、轉乘步驟、票價明細、車上時間、候車與轉乘估算。
- 完成第二個車站選擇並成功計算後，自動展開計算結果。
- 計算結果可展開或收合；收合只隱藏票價、時間與路線步驟，起訖選單仍保留。
- 若估算步行時間短於大眾運輸總時間，額外顯示步行建議、估計距離與時間。
- 支援繁體中文、英文、日文與韓文。
- 語言預設依瀏覽器系統語言決定，並以 Cookie 保存最後一次選擇一年。
- 使用 `file://` 直接開啟且 Cookie 不可用時，以 `localStorage` 作為語言偏好備援。
- 支援系統淺色／深色主題；「更多資訊」視窗會沿用原頁面主題。
- 左下角「捷運路線說明」與右下角「相對方位・非比例尺」說明皆可點擊展開或收合。
- 「更多資訊」視窗包含票價說明、資料來源、估算方法與使用限制。

## 支援路線

目前內建 15 個路線圖層：

### 台北捷運

- BR 文湖線
- R 淡水信義線
- R 新北投支線
- G 松山新店線
- G 小碧潭支線
- O 中和新蘆線・新莊支線
- O 中和新蘆線・蘆洲支線
- BL 板南線
- Y 環狀線

### 桃園捷運

- A 機場捷運普通車
- AX 機場捷運直達車

機場捷運直達車沿普通車相同路徑呈現，並以直達車停靠站與線型區分。

### 新北捷運與輕軌

- V 淡海輕軌・綠山線
- V 淡海輕軌・藍海線一期
- K 安坑輕軌
- LB 三鶯線

## 快速開始

1. 下載或複製主 HTML 檔案。
2. 以 Chrome、Edge、Safari 或 Firefox 開啟。
3. 不需執行安裝指令，也不需本機伺服器。

```text
metro.html
```

也可以將檔案放到任意靜態網站空間，例如 GitHub Pages、Cloudflare Pages、Netlify 或一般 Web Server。

## 操作方式

### 規劃旅程

1. 在地圖上點選第一個車站作為起點。
2. 點選第二個車站作為終點。
3. 系統立即計算並展開結果。
4. 再次點選車站可重新設定起點與終點。

也可以直接使用左上角的出發站與抵達站下拉選單，或使用內建快速路線。

### 搜尋與篩選

- 電腦版可輸入站名或站碼搜尋，例如 `台北車站`、`A12`、`V26`。
- 可依營運系統或路線篩選顯示內容。
- 手機版為減少浮動介面遮擋，不顯示站名搜尋輸入框，仍可透過地圖、下拉選單與快速路線操作。

### 地圖操作

#### 電腦版

- 滑鼠拖曳：移動路網。
- `＋／－`：放大或縮小。
- 「更多地圖選項」：顯示全圖或恢復預設視角。
- 預設及恢復視角以台北車站為中心。

#### 手機版

- 僅支援直立顯示；橫向時會提示轉回直立模式。
- 單指點擊：選擇車站。
- 單指上下滑動：操作頁面或浮動結果區。
- 雙指拖曳：移動路網。
- 雙指捏合：放大或縮小路網。
- 手勢只作用於路網區域，不會縮放整個網頁。
- 初始與最小縮放視角會避開浮動規劃面板、控制圖示與說明區。

## 多語言

介面支援：

- 繁體中文
- English
- 日本語
- 한국어

北捷與桃園捷運站名優先採用營運單位官方多語版本。新北捷運目前以官方中英文名稱為主，日文與韓文名稱依官方中文站名音譯，並在「更多資訊」中標示來源層級。

語言載入順序：

1. `northernMetroLang` Cookie
2. `file://` 模式下的 `localStorage` 備援值
3. 瀏覽器系統語言
4. 無法判斷時預設英文

## 路線與時間計算

路線選擇會綜合：

- 車上行駛時間
- 平均候車時間
- 轉乘步行時間
- 跨系統轉乘

顯示時間為一般營運狀態下的估算，不是即時列車預報，也不會讀取即時誤點、臨時停駛、班距變更或人潮資料。

## 步行時間比較

系統會以起訖站的地理座標估算步行時間。只有當步行估算短於大眾運輸總時間時，才顯示「步行可能更快」。

目前估算參數：

- 以車站座標計算直線距離。
- 道路繞行係數：`1.4`。
- 一般步行速度：`75 公尺／分鐘`。
- 進出站與定位緩衝：`3 分鐘`。

此結果不是實際步行導航，不包含道路封閉、河川、鐵路、高架道路、坡度、號誌、無障礙動線、施工或私人土地等因素。實際步行請搭配地圖導航服務確認。

## 票價說明

- 以一般成人單程票為主要基準。
- 跨營運系統行程原則上採分段計價並顯示票價明細。
- 不包含常客回饋、電子票證折扣、敬老／愛心優惠、定期票或其他活動優惠。
- 特殊試營運或限時票價規則會依目前 HTML 版本內建資料顯示。
- 票價與營運規則可能更新，實際金額仍以各營運單位當日公告為準。

## 地圖配置原則

路網使用地理相對配置，而不是傳統完全幾何化的捷運圖，也不是精確地圖：

- 上方為北。
- 右方為東。
- 鄰近且可步行轉乘的車站群會盡量維持正確相對位置。
- 全路網使用一致的地理變形，避免各路線獨立壓縮後產生錯位。
- 中央密集區會適度展開，以提高車站點選與文字辨識能力。
- 地圖不代表真實距離、行駛曲線或工程線形。

## 資料來源

HTML 內的「更多資訊」提供官方來源連結，主要包含：

- 台北捷運官方路網圖、車站資訊、票價與乘車時間。
- 台北捷運官方票價表。
- 桃園捷運票價、時刻表與官方票價表。
- 新北捷運淡海輕軌、安坑輕軌及三鶯線的車站與票價資訊。
- 台北捷運車站出入口座標開放資料。
- 交通部鐵道局機場捷運車站位置座標。

目前主檔內建的官方來源：

- [台北捷運｜官方路網圖與各站資訊](https://www.metro.taipei/cp.aspx?n=73B51F32ED23C5E1)
- [台北捷運｜票價及乘車時間](https://www.metro.taipei/cp.aspx?n=ECEADC266D7120A7)
- [台北捷運｜官方票價表 PDF](https://www-ws.gov.taipei/Download.ashx?icon=..pdf&n=56Wo5YO56KGoKHBkZuaqlCkucGRm&u=LzAwMS9VcGxvYWQvNDA1L3JlbGZpbGUvMTgyODgvNzYxOC8xMWEzNWM2Mi1jZmQ2LTQzYjctOGVmMi1mMjFjOTE2MjU4OGMucGRm)
- [桃園捷運｜票價與時刻表查詢](https://www.tymetro.com.tw/tymetro-new/tw/_pages/travel-guide/timetable-search.php)
- [桃園捷運｜官方票價表 PDF](https://www.tymetro.com.tw/tymetro-new/tw/_images/document/travel-guide/price.pdf)
- [新北捷運｜淡海輕軌票價](https://www.ntmetro.com.tw/basic/?node=10105)
- [新北捷運｜安坑輕軌票價](https://www.ntmetro.com.tw/basic/?node=10106)
- [新北捷運｜淡海輕軌車站](https://www.ntmetro.com.tw/basic/?node=10136)
- [新北捷運｜安坑輕軌車站](https://www.ntmetro.com.tw/basic/?node=10137)
- [新北捷運｜三鶯線票價與試營運](https://www.ntmetro.com.tw/basic/?node=10166)
- [台北捷運｜車站出入口座標開放資料](https://data.gov.tw/dataset/128428)
- [交通部鐵道局｜機場捷運車站位置座標](https://data.gov.tw/dataset/96942)

## 技術特性

- 單一靜態 HTML 檔案。
- 原生 HTML、CSS、SVG 與 JavaScript。
- 不使用外部 JavaScript 套件。
- 不載入外部字型、圖片或樣式表。
- 可離線使用主要規劃功能。
- 官方資料連結只有在使用者點擊時才需要網路。
- 路網、車站、文字、票價與時間資料均嵌入主檔。

## 專案檔案

```text
README.md
metro.html
```

## 修改與維護建議

若要更新此專案，建議依下列順序處理：

1. 更新車站、路線與轉乘資料。
2. 更新官方票價矩陣或票價規則。
3. 更新行駛時間、候車與轉乘估算。
4. 更新繁中、英文、日文與韓文名稱。
5. 重新校正地理相對座標與鄰近站群。
6. 測試桌面拖曳、手機雙指操作與直立模式。
7. 測試起訖站選擇、快速路線、收合／展開、步行建議與資訊視窗。
8. 更新 HTML 標題、Build 註解、版本標記與本 README。

## 已知限制

- 不是官方網站或官方 App。
- 不提供即時到站、列車位置、故障、施工或營運異常資訊。
- 不保證所有跨系統站外步行路徑皆可通行。
- 不提供精確步行導航。
- 非比例尺路網不能用來直接判斷實際距離。
- 行程排序偏重一般時間估算，不代表所有旅客的最佳方案。
- 票價、試營運規則與路線狀態可能隨時間變更。

## 授權

目前專案未附加正式開源授權。若要公開散布、再製或納入其他產品，請先補充適合的授權條款，並遵守各營運單位資料、名稱、標誌與路線圖的使用規範。

---

# Northern Taiwan Metro Interactive Fare, Route and Travel-Time Planner

> Current matching build: `v2026.07.20.24`  
> Main application: `metro.html`

This project is a self-contained, browser-based journey planner for metro and light-rail services in Taipei, New Taipei and Taoyuan. Users can select an origin and destination directly on the interactive network map or through station selectors, then view a suggested route, transfers, adult single-journey fare, estimated travel time and, when appropriate, a faster walking alternative.

No package installation, web server or database is required. The HTML, CSS, JavaScript, route data and multilingual content are all embedded in one file.

## Key Features

- Single-screen interactive network map centered by default on `R10 / BL12 Taipei Main Station`.
- Geography-aware layout with north at the top and east on the right; the drawing is intentionally not to scale.
- The first station click sets the origin; the second sets the destination and runs the planner automatically.
- Origin and destination selectors use natural ordering by route and alphanumeric station code.
- Displays the suggested route, transfer steps, fare details, in-vehicle time, waiting time and transfer estimates.
- Automatically expands the calculation results after a valid second station is selected.
- Results can be expanded or collapsed; collapsing hides only fare, time and route details while keeping the station controls visible.
- Shows a walking suggestion only when the estimated walk is faster than the public-transport journey.
- Supports Traditional Chinese, English, Japanese and Korean.
- Uses the browser language by default and stores the most recently selected language in a one-year cookie.
- Uses `localStorage` as a fallback for language preference when opened through `file://` and cookies are unavailable.
- Supports the operating system's light and dark appearance; the More Information dialog inherits the same theme.
- The lower-left Route Guide and lower-right Relative Position / Not-to-Scale note can be expanded and collapsed.
- The More Information dialog contains fare notes, data sources, estimation methods and limitations.

## Supported Lines

The current build contains 15 route layers.

### Taipei Metro

- BR Wenhu Line
- R Tamsui–Xinyi Line
- R Xinbeitou Branch Line
- G Songshan–Xindian Line
- G Xiaobitan Branch Line
- O Zhonghe–Xinlu Line, Xinzhuang Branch
- O Zhonghe–Xinlu Line, Luzhou Branch
- BL Bannan Line
- Y Circular Line

### Taoyuan Metro

- A Airport MRT Commuter service
- AX Airport MRT Express service

The express service follows the same visual path as the commuter service and is distinguished by its stopping pattern and line style.

### New Taipei Metro and Light Rail

- V Danhai LRT Green Mountain Line
- V Danhai LRT Blue Coast Line Phase 1
- K Ankeng LRT
- LB Sanying Line

## Quick Start

1. Download or copy the main HTML file.
2. Open it with Chrome, Edge, Safari or Firefox.
3. No installation command or local server is required.

```text
metro.html
```

The file can also be hosted on any static web service, including GitHub Pages, Cloudflare Pages, Netlify or a conventional web server.

## How to Use

### Plan a Journey

1. Click the first station on the map to set the origin.
2. Click the second station to set the destination.
3. The planner calculates and expands the result immediately.
4. Click another station to start a new origin/destination selection.

You can also use the origin and destination selectors in the upper-left panel or choose one of the built-in quick routes.

### Search and Filter

- On desktop, search by station name or code, such as `Taipei Main Station`, `A12` or `V26`.
- Filter the visible map by operator or route group.
- To reduce obstruction from floating controls, the station search input is hidden on mobile. The map, station selectors and quick routes remain available.

### Map Controls

#### Desktop

- Mouse drag: pan the network map.
- `+ / −`: zoom in or out.
- More Map Options: fit the full map or restore the default view.
- The default and restored view are centered on Taipei Main Station.

#### Mobile

- Portrait orientation only; landscape mode displays a prompt to rotate the device.
- Single tap: select a station.
- Single-finger vertical movement: interact with the page or scrollable result panel.
- Two-finger drag: pan the network map.
- Pinch gesture: zoom the network map.
- Gestures are confined to the map and do not zoom the entire webpage.
- The initial and minimum-zoom views account for the floating planner, controls and guide panels so the complete network remains visible.

## Languages

The interface supports:

- Traditional Chinese
- English
- Japanese
- Korean

Taipei Metro and Taoyuan Metro station names use official multilingual names where available. New Taipei Metro primarily publishes official Chinese and English names; Japanese and Korean names are transliterated from the official Chinese names, and this distinction is disclosed in the More Information dialog.

Language preference priority:

1. `northernMetroLang` cookie
2. `localStorage` fallback in `file://` mode
3. Browser system language
4. English when no supported language can be detected

## Route and Travel-Time Calculation

Route selection considers:

- In-vehicle travel time
- Average waiting time
- Transfer walking time
- Transfers between operating systems

All times are general operating estimates. The application does not retrieve real-time arrivals, delays, temporary suspensions, headway changes or crowding information.

## Walking-Time Comparison

The planner estimates walking time from the geographic coordinates of the origin and destination stations. A “Walking may be faster” card is shown only when the estimated walk is shorter than the calculated public-transport journey.

Current parameters:

- Straight-line distance derived from station coordinates
- Road-route factor: `1.4`
- Walking speed: `75 metres per minute`
- Access and orientation allowance: `3 minutes`

This is not turn-by-turn walking navigation. It does not model inaccessible roads, rivers, railway barriers, elevated roads, slopes, signals, construction, private land or accessible-path requirements. Confirm the actual walking route with a mapping service.

## Fare Notes

- Fares primarily use the standard adult single-journey basis.
- Cross-operator journeys are generally calculated in separate fare segments and shown as an itemised total.
- Frequent-rider rewards, stored-value-card discounts, senior or accessibility concessions, passes and promotional discounts are not included.
- Temporary trial-operation or time-limited fare rules are embedded according to the current HTML build.
- Fares and operating rules may change; the operator's current announcement is authoritative.

## Map Layout Principles

The network is a geography-aware diagram rather than a fully geometric metro map or a precise geographic map.

- North is up.
- East is right.
- Nearby stations and walkable interchange groups are kept in the correct relative positions where practical.
- A shared geographic transformation is applied across the complete network to avoid misalignment caused by independently compressing individual lines.
- Dense central areas are expanded for label readability and station selection.
- The map does not represent true distance, track curvature or engineering alignment.

## Data Sources

The application's More Information dialog includes links to official sources, primarily covering:

- Taipei Metro network maps, station information, fares and travel times
- Taipei Metro official fare tables
- Taoyuan Metro fares, timetables and official fare tables
- Danhai LRT, Ankeng LRT and Sanying Line station and fare information
- Taipei Metro station entrance coordinate open data
- Railway Bureau Airport MRT station coordinate data

Official sources embedded in the current build:

- [Taipei Metro — Official network map and station information](https://www.metro.taipei/cp.aspx?n=73B51F32ED23C5E1)
- [Taipei Metro — Fares and travel times](https://www.metro.taipei/cp.aspx?n=ECEADC266D7120A7)
- [Taipei Metro — Official fare-table PDF](https://www-ws.gov.taipei/Download.ashx?icon=..pdf&n=56Wo5YO56KGoKHBkZuaqlCkucGRm&u=LzAwMS9VcGxvYWQvNDA1L3JlbGZpbGUvMTgyODgvNzYxOC8xMWEzNWM2Mi1jZmQ2LTQzYjctOGVmMi1mMjFjOTE2MjU4OGMucGRm)
- [Taoyuan Metro — Fare and timetable search](https://www.tymetro.com.tw/tymetro-new/tw/_pages/travel-guide/timetable-search.php)
- [Taoyuan Metro — Official fare-table PDF](https://www.tymetro.com.tw/tymetro-new/tw/_images/document/travel-guide/price.pdf)
- [New Taipei Metro — Danhai LRT fares](https://www.ntmetro.com.tw/basic/?node=10105)
- [New Taipei Metro — Ankeng LRT fares](https://www.ntmetro.com.tw/basic/?node=10106)
- [New Taipei Metro — Danhai LRT stations](https://www.ntmetro.com.tw/basic/?node=10136)
- [New Taipei Metro — Ankeng LRT stations](https://www.ntmetro.com.tw/basic/?node=10137)
- [New Taipei Metro — Sanying Line fares and trial operation](https://www.ntmetro.com.tw/basic/?node=10166)
- [Taipei Metro — Station entrance coordinate open data](https://data.gov.tw/dataset/128428)
- [Railway Bureau — Airport MRT station coordinates](https://data.gov.tw/dataset/96942)

## Technical Characteristics

- One static HTML file
- Native HTML, CSS, SVG and JavaScript
- No external JavaScript libraries
- No external fonts, images or stylesheets
- Core planning features work offline
- Official-source links require a network connection only when opened
- Network, station, text, fare and time data are embedded in the application file

## Project Files

```text
README.md
metro.html
```

## Suggested Maintenance Workflow

When updating the project:

1. Update station, line and interchange data.
2. Update official fare matrices or fare rules.
3. Update running-time, waiting-time and transfer estimates.
4. Update Traditional Chinese, English, Japanese and Korean names.
5. Recalibrate geographic-relative coordinates and nearby-station groups.
6. Test desktop dragging, mobile two-finger gestures and portrait-only behaviour.
7. Test station selection, quick routes, result expand/collapse, walking suggestions and the information dialog.
8. Update the HTML title, build comment, version stamp and this README.

## Known Limitations

- This is not an official website or official application.
- It does not provide real-time arrivals, train positions, faults, construction or service-disruption information.
- It cannot guarantee that every external walking transfer is physically accessible.
- It is not a precise walking-navigation system.
- The not-to-scale map cannot be used to measure actual distance.
- Journey ranking is based on general estimates and may not be optimal for every passenger.
- Fares, trial-operation rules and route status may change over time.

## Licence

No formal open-source licence is currently included. Before public redistribution, modification or integration into another product, add an appropriate licence and comply with each operator's requirements for data, names, logos and network-map usage.
