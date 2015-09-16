##第二章：Analytics.js 基礎 (二)

###第一節 自訂維度 ( Dimensions ) 和指標 ( Matrics )
這一節說明如何透過 Google Analytics 為自己網站定義與收集特殊的資料。要使用自定義的維度或指標，必須先在 Google Analytics 網站設定維度或指標定義，然後在自己的網站加上 Analytics.js 的設定。 
  
###一、Google Analytics 網站的設定
1. 登入 [Google Analytics](https://www.google.com/analytics/) 網站。
2. 點選頁籤 `管理(Admin)` ，在 `資源(Property)` 區塊點選 `自訂定義(Custom Definitions)`，顯示下拉選單的兩個項目：`自訂維度(Custom Dimensions)` 和 `自訂指標(Custom Matrics)`。
3. 點選 `自訂維度` 進入頁面，點選按紐 `新增自訂維度` ，自己定義這個維度的名稱和適用範圍。定義完成後，GA 自動產生 JavaScript 程式碼，例如：  

		var dimensionValue = 'SOME_DIMENSION_VALUE';
		ga('set', 'dimension1', dimensionValue);  
`dimension1` 是 GA 自動為這個客製維度定義的變數名稱，數字 `1` 是 GA 自動添加的索引(index)。
4. 點選 `自訂指標` 進入頁面，點選按紐 `新增自訂指標` ，自己定義這個指標的名稱、適用範圍、格式、大小值。定義完成後，GA 自動產生 JavaScript 程式碼，例如：  
  
		var metricValue = '123';
		ga('set', 'metric1', metricValue);  
`metric1` 是 GA 自動為這個客製指標定義的變數名稱，數字 `1` 是 GA 自動添加的索引(index)。  

###二、從網站送資料給 GA
知道如何在 Google Analytics 網站設定維度或指標定義之後，我們假設一個情境：你的 PHP 網站有許多作者文章，你想記錄每一個作者的瀏覽次數。  

假設你已經在 Google Analytics 網站定義一個名為 `Author` 的維度，接下來你只要在網站的 template 加上以下程式碼，當有人瀏覽某作者文章，便可以利用 Analytics.js 傳送作者姓名給 GA。  

		ga('send', 'pageview', {
 		   'dimension5': '<?=$author?>'
		});

  

###第二節 自訂事件追蹤 ( Event Tracking )
如果你想紀錄某個按鈕事件有多少不同人點擊，Analytics.js 提供很簡便的做法。  

一、事件追蹤的語法：  

		ga('send', 'event', 'button', 'click', 'nav buttons', 6);  
參數類型：  

1. `button` 表示 category
2.  `click` 表示 action
3. `nav buttons` 表示 label
4. `6` 表示 value  

二、情境範例： 

你想紀錄某個按鈕事件有多少不同人點擊。  
  
HTML  

		 < button id="button" > Download click < /button >  
JavaScript   
 
		$('#button').on('click', function() {
		    ga('send', 'event', 'button', 'click', 'download-buttons');
		});  
Google Analytics 網站  

1. 登入 [Google Analytics](https://www.google.com/analytics/) 網站。  
2. 點選頁籤 `報表(Reporting)`  
3. 選擇左側欄位的 `即時(Real-time)` > `事件(Events)` ，在`事件`頁面可以見到結果。  
4. 選擇左側欄位的 `行為()` > `事件(Events)` ，在`事件`頁面可以見到結果。