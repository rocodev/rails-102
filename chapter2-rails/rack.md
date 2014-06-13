# Rack

> Rack provides a minimal interface between webservers supporting Ruby and Ruby frameworks.

簡單來講 Rack 就是讓 Ruby 以及 Ruby Web 框架跟 Web Server互動的橋樑，所有與 Server 的互動都會經過 Rack。

所以確切的說，我們幾乎在 Rails controller / route 內寫的大部分 code 都是在跟 Rack 互動，Rack會負責再幫我們跟 Server互動，扮演秘書的角色。


對 Webserver 的開發者來說，世界上有千百種 Framework，每新增一個 Framework 就樣讓 Server 支援它會是一件很恐怖的工作，所以就需要一個共同的規範`rack SPEC`，只要 Framework 都遵守著rack spec，server就只需要處理 Rack送來的訊號就可以了。

而這個SPEC其實就是一個帶 environment 參數的call method，由 Rack跟 server 拿這個enviroment應該要回傳的資料，並回串一個由三個主要區塊「HTTP狀態」、「HTTP Headers」、「HTTP內容」組成的字串。


而所謂的 Rack middleware就是指在 Rack 和 Application 中間的 application，我們的每個request其實都是經過很多層的middleware才傳到Rails App中，所以有些不需要給 Rails處理的工作就可以在middleware中做，對效能有幫助。

TODO: Learn what is `rails Metal`


## 參考資料：

* http://webcache.googleusercontent.com/search?q=cache:eBrDs9kEBksJ:wp.xdite.net/%3Fp%3D1557+&cd=1&hl=zh-TW&ct=clnk&gl=tw
* http://www.whatcodecraves.com/articles/2012/07/23/ruby-on-rack
* http://rack.github.io/
* http://guides.rubyonrails.org/rails_on_rack.html#resources
* middleware應用：http://railscasts.com/episodes/151-rack-middleware
