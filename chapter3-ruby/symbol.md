# Symbol

要了解 Ruby 中的 Symbol 就必須了解物件的觀念，此篇會有簡單說明，若需要了解更詳細，坊間有許多物件導向的教學書籍可以請讀者多多參考。

##何謂物件？
我們可以想像電腦擁有許多記憶體位置，就像是圖書館擁有許多書櫃，每個記憶體位置假設都可以放一個物件，就如同書櫃上的每個位置都可以放一本書。
每個物件會有特定的 id ，就如同每本書都會有一個索引。

##Ruby與物件
在 Ruby 中，所有東西都是物件，所以當我們要產生新字串的時候，其實我們就是產生了新的物件放在記憶體中，讓我們在 `irb` 中測試看看：
```irb
2.0.0-p481 :001 > "rails102".object_id
# => 2173297300
2.0.0-p481 :002 > "rails102".object_id
# => 2173288960
2.0.0-p481 :003 > "rails102".object_id == "rails102".object_id
# => false
```
由上方的測試中可以發現，每當我們呼叫`"rails102"`的字串，其實都是新增一個物件，各自擁有不同的 id ，就像是兩本同樣名字的書，你可以說他們是同樣內容的書，但並不是「同一本」書。

##Ruby Symbol 的特性

而我們再來看看 Symbol ：
```irb
2.0.0-p481 :001 > :rails102.object_id
# => 538408
2.0.0-p481 :002 > :rails102.object_id
# => 538408
2.0.0-p481 :003 > :rails102.object_id == :rails102.object_id
# => true
```
藉由上方的 Symbol 測試可以發現，我們每次呼叫`:rails102` 時其實都是在叫同一個物件，所以都會有相同的 id （相對於上方字串的測試則是每次呼叫都新增一個物件）。

由於 Symbol 總是呼叫同一個物件的特性，所以很適合當作 Hash 的 key ，也擁有較好的執行效率。

參考資料
* http://ihower.tw/rails3/ruby.html
* https://www.ruby-lang.org/zh_tw/documentation/ruby-from-other-languages/