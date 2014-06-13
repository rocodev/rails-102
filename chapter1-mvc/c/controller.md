# Controller


## 什麼是Controller

Controller主要是扮演橋樑的角色，負責跟Model要資料並把資料傳給View。另外一方面也會接收View傳來的各種http request傳給Model。

## 什麼東西應該放在Controller


基本上屬於「過程中應該被處理」的動作都應該放在controller，比方說有一個view需要前20筆的Products資料，我們不可能把所有的Products都丟給view然後再在View裡面判斷前20筆，這樣會很悲劇。所以在這種情況下，這個View對應的Controller就要負責「跟Model拿資料」以及「只拿20筆資料」的動作。

這個感覺有點像是球團、球員和經紀人三者的關係：

球團扮演的角色是Model，負責出錢、辦比賽。

球員扮演的角色是View，負責拿錢、比賽。

而經紀人就是Controller，負責幫球員跟各個球團議價，讓球團跟球員能夠專注於自己的事情。

所以只要抱著Model處理資料庫，View處理前端呈現這樣的原則，就知道什麼東西應該放在controller了。

