##第二天：Analytics.js 基礎


Universal Analytics Web Tracking (analytics.js)採用非同步的方式採集使用者操弄網頁的行為。  
------
	< script >  
	    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
	      (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
	      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
	    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

	    ga('create', 'UA-XXXX-Y', 'auto');
	    ga('send', 'pageview');  
	< /script >

要使用 analytics.js 函式庫來測量使用者和你的網頁之間的互動，請在你的網頁</head>之前貼上面的程式碼。  

__這一段程式碼做甚麼事？__當用戶開啟你的網頁，這段程式碼會非同步下載 analytics.js，創建一個名為 ga 的全域方法，利用 ga() 創建一個追蹤物件(以下稱 tracker )，tracker 的作用是採集、儲存用戶的使用行為在 tracker 物件。目前，這段程式碼只會送出 pageview 給 Google Analytics 。

慢慢解釋程式碼的意思。首先你可以看到`function(i,s,o,g,r,a,m)`有參數代碼`i,s,o,g,r,a,m`。Google文件已經清楚解釋意思，如下所示：  

	@param {Window}      i The global context object.  
	@param {Document}    s The DOM document object.  
	@param {string}      o Must be 'script'.  
	@param {string}      g URL of the analytics.js script. Inherits protocol from page.  
	@param {string}      r Global name of analytics object.  Defaults to 'ga'.  
	@param {DOMElement?} a Async script tag.  
	@param {DOMElement?} m First script tag in document.  
  

 `i['GoogleAnalyticsObject'] = r;` 這段碼使我們可以變更analytics物件的名稱。  

`i[r] = i[r] || function() {(i[r].q = i[r].q || []).push(arguments)},` 創建ga()方法。  

` i[r].l = 1 * new Date();` 設定時間  

`ga('create', 'UA-XXXX-Y', 'auto');` 創建一個 tracker 物件。  
 
`ga('send', 'pageview');` 發送 pageview hit  

###ga()的作用  


`ga( )`是 analytics.js 提供的單一存取介面，讓我們只能透過 ga() 來操弄 analytics.js。這樣的程式架構很像設計模式中的「命令模式」，你只要輸入參數(命令)，不需知道 analytics.js 如何執行。" ga "這個名稱是可以自訂的，你可以改為其他你想要的名稱，例如 myTracker。在以下這段程式碼修改：  

`(window,document,'script','//www.google-analytics.com/analytics.js','myTracker');`
###create
ga('`create`', 'UA-XXXX-Y', 'auto'); 是呼叫 create 方法，替'UA-XXXX-Y'創建一個 tracker 物件，用戶的使用行為都紀錄在這個 tracker 物件。參數 auto 告訴 analytics.js 自動依照 domain 紀錄 cookie。  
###send
ga('`send`', 'pageview'); 是呼叫 send 方法，向 Google Analytics 遞交儲存在 tracker 物件的用戶使用行為。這裡是告訴 Google Analytics ，有一個人瀏覽了這一個網頁。 
你可以為 pageview 添加一個 callback 方法，以下是名稱為 hitCallback 的 callback 方法：

	ga('send', 'pageview', {
 	  'page': '/my-new-page',
  	  'hitCallback': function() {
   	     alert('analytics.js done sending data');
 	   }
	});
  

你也可以針對某個頁面，發送一些特定的事件。例如替頁面 Products 發送幾個事件：1.頁面點擊、2.圖片A點擊事件、3.圖片B點擊事件。可以這樣寫：
  
	ga('set', 'page', '/Products');
	ga('send', 'pageview');                    //頁面點擊
	ga('send', 'event', 'imageA', 'clicked');  //圖片A點擊事件
	ga('send', 'event', 'imageB', 'clicked');  //圖片B點擊事件
###push function
有時候你想在analytics.js下載完成後做一些事情，你可以把方法當參數傳給ga()，像是 C# 的委派 (delegate)。以下程式碼會在analytics.js下載完成後，跳出視窗。  

	ga(function() {
 	   alert('library done loading');
	});
###強制使用 SSL (HTTPS)
如果有安全性的考量，你想強迫 Google Analytics 總是以 SSL 協定來傳送資料，可以這樣寫： 
 
	ga('create', 'UA-XXXX-Y', 'auto');
	ga('set', 'forceSSL', true); ** 強迫 Google Analytics 總是以 SSL 協定來傳送資料 **
	ga('send', 'pageview');tracker

###創建多個 Tracker
你可能需要在一個頁面放置許多 tracker 物件，這也沒問題：  

	ga('create', 'UA-XXXX-Y', 'auto'); ** 第一個tracker物件。預設的 tracker 。**

	ga('create', 'UA-12345-6', 'auto', {'name': 'newTracker'}); ** 第二個名為「newTracker」的tracker物件 **

發送資訊給「newTracker」物件：  

	ga('newTracker.send','pageview');
使用`getByName()`取得「newTracker」物件： 
 
  
	ga(function() {
  	    var newTracker = ga.getByName('newTracker');
	});
使用`getAll()`取得所有 tracker 物件，回傳一個陣列：  

	ga(function() {
 	   var allTrackers = ga.getAll();
	});
###隱藏IP
如果你不想將IP傳給 Google Analytics ，可以透過設定來隱藏：  

	ga('set', 'anonymizeIp', true); ** 用戶觸發任何事件，隱藏IP不回傳給 Google Analytics **
###暫時停用 Goole Analytics
有時在一些情況，你不想移除程式碼，僅是暫時停用 Google Analytics。你可以這樣做，在 Google Analytics 程式碼__之前__加上：  

	window['ga-disable-UA-XXXX-Y'] = true;

或者你可以寫個小功能，讓用戶自己選擇是否停用 Google Analytics。以下是簡單範例：  

	<a href="javascript:gaOptout()">Click here to opt-out of Google Analytics</a>  

	< script >
	    // Set to the same value as the web property used on the site
	    var gaProperty = 'UA-XXXX-Y';

	    // Disable tracking if the opt-out cookie exists.
	    var disableStr = 'ga-disable-' + gaProperty;
	    if (document.cookie.indexOf(disableStr + '=true') > -1) {
 	        window[disableStr] = true;
	    }

	    // Opt-out function
	    function gaOptout() {
 	        document.cookie = disableStr + '=true; expires=Thu, 31 Dec 2099 23:59:59 UTC; path=/';
 	        window[disableStr] = true;
	    }
	< /script >
今日小結
-------

`ga( )`是analytics.js提供的單一存取介面，讓我們透過ga()來操弄 analytics.js 


參考連結
-------
與我聯絡
---
> * 部落格：[我，傑夫。開發人](https://jeffprogrammer.wordpress.com/)  
> * Email ：[jeff.juan@chihche.com](mailto:jeff.juan@chihche.com)