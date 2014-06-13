# Controller


## 什麼是 Controller

Controller 主要是扮演橋樑的角色，負責跟 Model 要資料並把資料傳給 View。另外一方面也會接收 View 傳來的各種 HTTP request傳給 Model。

## 什麼東西應該放在Controller

基本上屬於「過程中應該被處理」的動作都應該放在 Controller，比方說有一個 View 需要前20筆的 products資料，我們不可能把所有的 products 都丟給 View ，然後再在 View 裡面判斷前20筆，這樣會很悲劇。所以在這種情況下，這個 View 對應的 Controller 就要負責「跟Model拿資料」以及「只拿20筆資料」的動作。

這個感覺有點像是球團、球員和經紀人三者的關係：

* 球團扮演的角色是 Model，負責出錢、辦比賽。
* 球員扮演的角色是 View，負責拿錢、比賽。
* 而經紀人就是 Controller，負責幫球員跟各個球團議價，讓球團跟球員能夠專注於自己的事情。

所以只要抱著「Model 處理資料庫，View處理前端呈現」這樣的原則，就知道什麼東西應該放在controller了。

