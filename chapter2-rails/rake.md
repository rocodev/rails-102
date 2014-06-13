# Rake

注意喲，別把 Rake 和 [Rack](rack.md)搞混了。

Rake 可以讓每個script之間可以有清楚的相依性，且能夠只執行程式需要執行的部分，作用大概就跟管家很像，當我們要管家去掃地時，不用告訴管家你要先去拿掃把、然後走去庭院、然後開始掃地，只要單純地說「去掃地」就好了，而在這當中「拿掃把」、「走去庭院」、「開始掃地」都是不同的script，管家（rack）會依序執行它。而且他也會記得他掃過的區域，不會每次掃地都一直重新掃一樣的地方。


例如我們可以寫一個`dev.rake`的檔案，並用`rake dev:build`的方式執行下面這段script中的build task

```ruby
namespace :dev do
	desc "Rebuild system"
	task :build => ["tmp:clear", "log:clear", "db:drop", "db:create", "db:migrate"]
	task :rebuild => [ "dev:build", "db:seed" ]
end
```

rake就會按照順序執行完後面的一系列rake script。

