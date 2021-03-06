前後端分離，你應該知道的八件事
===

> 前後端不分離，是怎樣的？大概也只有我們這些『老古董』們，才對此有更多感受。不對，那些寫 React 的人，可能會對此也有一些體會。

今天，如果有一個前端工程師說，不知道前後端分離是什麼。那麼，要麼是剛畢業不久的，要麼是從老版的公司裡出來的員工，要麼是剛從時光機裡出來的。

前後端分離
---

我剛開始接觸前後端分離的時候，正值它開始慢慢擴散的時候，也還沒有意識到它帶來的好處。覺得它甚是麻煩，當我改一個介面的時候，我需要同時修改兩部分的程式碼，以及對應的測試。反而，還不如直接修改原有的模板來得簡單。

可是當我去使用這個，由前後端分離做成的單頁面應用時，我開始覺得這些是值得。當頁面載入完後，每開啟一個新的連結時，不再需要等網路返回給我結果；我也能快速的回到上一個頁面，像一個 APP 一樣的體現這樣的應用。整個過程裡，我們只是不斷地從後臺去獲取資料，不需要重複地請求頁面——因為這些頁面的模板已經存在本地了，我們所缺少的只是實時的資料。

後來，當我從架構去考慮這件事時，我才發現這種花費是值得的。

### 什麼是前後端分離？

前後端分離和微服務一樣，漸漸地影響了新的大型系統的架構。微服務和前後端分離要解決是類似的問題，**解耦**——可以解耦複雜的業務邏輯，解耦架構。可要是說相像吧，訊息隊伍和前後端便相似一些，通過傳遞資料的形式來解耦元件。

前後端分離意味著，**前後端之間使用 JSON 來交流，兩個開發團隊之間使用 API 作為契約進行互動**。從此，後臺選用的技術棧不影響前臺。當後臺開發人員選擇 Java 的時候，我可以不用 JSP 來編寫前端頁面，繼續使用我的 React 又或者 Angular。而我使用 React 時，也不影響後臺使用某一個框架。

概念我們已經清楚了，但是還有一個問題：我們真的需要前後端分離嗎？

### 真的需要前後端分離嗎？

過去，聽說 TDD (Test-driven development，測試驅動開發) 可以改善程式碼的質量，我們便實施了 TDD；接著，聽說 BDD (Behavior-driven development，行為驅動開發)  可以交付符合業務需求的軟體，我們便實施了 BDD；後來，聽說 DDD (Domain-driven design，領域驅動設計) 可以分離業務程式碼與基礎程式碼，我們便實施了 DDD。今天，聽說了前後端分離很流行，於是我們就實施了前後端分離——這就是傳說中的 HDD（Hype-driven Development，熱鬧驅動開發）。

前後端分離在過去的兩三年裡，確實特別的熱鬧。但是我們怎麼才能知道，是不是需要這樣的架構呢？

- **頁面互動是否複雜 ？** 是簡單的提供頁面給使用者瀏覽？或者想要支援複雜的使用者操作？
- **是否需要搜尋引擎優化？**如果需要的話，那麼從一開始我們就需要考慮後端渲染。
- **能提升開發效率嗎？**如果不能有效的提升開發效率，為什麼要作死呢？
- **是否會提供 API 給 APP？**如果我們已經有一個 API 提供給 APP，那麼要做這件事就很容易了。如果未來會有的話，那麼我們更應該嘗試去分離。
- **前端的修改是不是非常頻繁？**如果不需要經常修改的話，那麼這種優化便沒有優勢。

當然了，如果老闆說，我們需要前後端分離，那就做唄！很多時候，一些技術決策都會由於戰略原因，而發生一些有意思的變化。

### 前後端分離將遇到的那些挑戰

而，當我們決定需要前後端分離時，我們仍然還需要面對一系列的問題：

- **是否足夠的安全？**如果我們設計出來的架構不夠安全，那麼這一系列的操作都是白搭。我們怎麼去儲存使用者資料，使用 LocalStorage 的話，還要考慮加密。採用哪種認證方式來讓使用者登入，並儲存相應的狀態？
- **是否有足夠的技術來支撐前後端分離？**有沒有能力建立出符合 RESTful 風格的 API？
- **是否有能力維護 API 介面？**當前端或者後臺需要修改介面時，是否能輕鬆地修改。
- **前後端協作的成本高不高？**前端和後臺兩個團隊是不是很容易合作？是不是可以輕鬆地進行聯調？
- **前後端職責是否能明確？**即：**後臺提供資料，前端負責顯示**。
- **是否建立了前端的錯誤追蹤機制？**能否幫助我們快速地定位出問題。

當我們在不同的項目組上嘗試時，就會發現主要的挑戰是溝通上的挑戰，而非技術上的侷限。

前後端分離的核心：後臺提供資料，前端負責顯示
---

我曾經有過使用 PHP 和 Java 開發後臺程式碼的經歷，仍然也主要是集中在前端領域。在這樣的傳統架構裡，編寫前端頁面可不是一件容易的事。後臺只會傳給前端一個 ModelAndView，然後前端就要撲哧撲哧地去豐富業務邏輯。

傳統的 MVC 架構裡，因為某些原因有相當多的業務邏輯，會被放置到 View 層，也就是模板層裡。換句話來說，就是這些邏輯都會被放到前端。我們看到的可能就不是各種``if``、``else``還有簡單的``equal``判斷，還會包含一些複雜的業務邏輯，比如說對某些產品進行特殊的處理。

如果這個時候，我們還需要做各種頁面互動，如填寫表單、Popup、動態資料等等，就不再是簡單的和模板引擎打交道了。我們需要編寫大量的 JavaScript 程式碼，因為業務的不斷增加，僅使用 jQuery 無法管理如此複雜的程式碼。

### 輸出邏輯：資料顯示

而僅僅只是因為邏輯複雜的前端程式碼，無法影響大部分團隊進行前後端分離——因為它沒有業務價值。實際上是先有了單頁面應用，才會出現前後端分離。單頁面應用可以讓使用者不需要下載 APP，就可以擁有相似的體現。並且與早期的移動網頁相比，擁有更好的體驗。

為了達到這樣的目的，後臺似乎返回對應的 Model 即可，稍微修改一下 Controller 的邏輯，然後返回這些資料。

```javascript
[{
    "content": "",
    "date": "2017-03-04",
    "description": "前後端分離，你應該知道的八件事\r\n\r\n前後端不分離，是怎樣的？大概也只有我們這些『老古董』們，才對此有更多感受。不對，那些寫 React 的人，可能會對此也有一些體會。",
    "id": 1,
    "slug": "iamafe-frontend-backend",
    "title": "我的職業是前端工程師:  前後端分離，你應該知道的八件事",
    "user": ""
}]
```

前端在一個 API 請求之後，可以直接渲染這些資料成 HTML。在這個時候，我們仍然可以看到，上面資料中的 date 欄位值 2017-03-04 的格式，和我們日常用的 2017 年 3 月 4 號的不一樣。所以，我們需要在前端引入 ``moment`` 這樣的庫，然後解析這個值。如果僅僅是這樣的處理，那麼應該由後臺幫我們轉換這個值。

與此同時，後臺應該按時間來對部落格進行排序。前端只需要遍歷這個陣列，隨後取出相應的值顯示即可，不需要做任何的邏輯處理。

遺憾的是，在真正的項目中開發的時候，並不能達到這麼完美的狀態。特別是，為了提高使用者體驗時，我們可能就會將資料儲存在本地，隨後直接操作這些資料，對其進行排序，篩選等等的操作。除此，還有諸如表格、圖表等等的高階樣式，也需要處理這些資料。

而當使用者需要提交資料的時候，這些邏輯就會落到前端上。

### 不可避免的前端邏輯：表單

如果一個前端應用只顯示資料的話，那麼這個應用就沒有充足的理由，做成一個單頁面應用——單頁面應用是為了更好的互動而存在的。當我們註冊、登入、購買東西時，就需要開始與表單進行處理。

合理的表單驗證模式應該是：**雙向驗證**。

前端在使用者輸入的過程中就需要實時地檢查，是否帶有特殊符號、值是否是在允許的範圍內、是不是符合相應的規範等等。而不是等使用者填寫完內容並提交後，再由服務端來告訴使用者說，“你的使用者名稱不符合規範”。

服務在收到前端收到的資料後，不管前端有沒有進行驗證，都應該按後臺的邏輯進行驗證。

於是乎在這個時候，這些邏輯就被無可避免地放到前臺裡了。
