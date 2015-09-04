##Chapter 1 初探 Google Analytics


Google Analytics 是一個由Google所提供的網站流量統計服務。舊版本: Classic Analytics Web Tracking (ga.js)新版本: (通用分析)Universal Analytics Web Tracking (analytics.js)  

*  舊版更新至新版的方法：https://developers.google.com/analytics/devguides/collection/upgrade/
  
  
新舊版的差異
---
* __使用 User ID 連結多個裝置、工作階段及參與度資料__  
  User ID 是通用 Analytics (分析) 的一項功能，可供您將專屬編號與多個工作階段 (以及這些工作階段中的任何活動) 相連結。將專屬編號和任何相關參與度資料傳送至 Google Analytics (分析) 時，所有活動都會歸為報表中的某位使用者所有。透過 User ID，您可以獲得更準確的使用者人數、分析已登入使用者的體驗，並存取新的「跨裝置」報表。

  如果要執行 User ID，您必須能夠產生自己的專屬編號，以一致的方式將編號指定給使用者，並在每次傳送資料至 Google Analytics (分析) 時加入這些編號。
舉例來說，您可以將自家認證系統產生的專屬編號傳送至 Google Analytics (分析) 做為 User ID 的值。系統會將指定專屬編號時發生的任何互動 (例如連結點擊以及網頁或畫面瀏覽) 透過 User ID 傳送並連結到 Google Analytics (分析)。

  使用 User ID 與未使用 User ID 時的資料比較
在未使用 User ID 功能執行 Google Analytics (分析) 的情況下，每次有人從其他裝置存取您的內容並開啟了新的工作階段時，就會採計為一個不重複使用者。舉例來說，如果使用者於某一天在手機上進行搜尋、三天後在筆電上購買、一個月後又在平板電腦上要求客戶服務，雖然這些動作都使用同一個登入帳戶，但在標準的 Google Analytics (分析) 執行方式中仍會採計為三個不重複使用者。這種方式雖然可以讓您收集關於每次互動和每種裝置的資料，但無法判斷任何形式的關係是否存在，只能看到各自獨立的資料點。

  必讀
https://support.google.com/analytics/answer/3123662?vid=0-635765822098027433-1198057273


* __新式追蹤程式碼，從任何數位裝置收集資料__  
  通用 Analytics (分析) 帶來了三種新版追蹤程式碼，您可以視自己的技術需求加以安裝；analytics.js JavaScript 程式庫適用於網站，Google Analytics SDK (v2 或更新版本) 專用來追蹤行動應用程式，Measurement Protocol 則可以用來追蹤其他數位裝置 (例如遊戲主機和資訊查詢機)。

  這些全新的資料收集方式考量到開發人員的需求，追蹤程式碼建立和自訂起來更輕鬆；特別值得一提的是對網站進行跨網域追蹤也更簡易，而且數據更加精確。

* __提供更多設定選項，您可以到帳戶管理員網頁加以設定__  
通用 Analytics (分析) 提供更多設定選項，您可以到帳戶管理員網頁加以設定：
隨機搜尋來源
工作階段和廣告活動逾時的處理方式
排除推薦連結
排除搜尋字詞

* __建立自訂維度和指標來收集您業務特有的資料__  
您自行建立的自訂維度和指標作用跟預設維度和指標相同，唯一的差別在於自訂維度和指標用來收集 Google Analytics (分析) 無法自動追蹤的資料。

* __執行加強型電子商務__  
部署通用 Analytics (分析) 之後，您可以使用 ec.js 外掛程式標記您的網站，然後使用加強型電子商務報表分析您的使用者購物和購買行為、內部和外部行銷策略的成功要素、以及產品的經濟成效。


  
###與我聯絡
***
> * 部落格：fsdsdfsd  
> * Faacebook: fsdfsdfsdfsd