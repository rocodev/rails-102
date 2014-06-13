# render :layout

Rails 預設的 layout 是`app/view/layouts/application.html.erb`這個檔案。

但有時候我們會希望預設的版型不一樣，比方說我們的 admin頁面 head 內不希望加上GA和一些有的沒的追蹤script。

這時候我們就可以建立一個新的layout版型`app/view/layouts/admin.html.erb`

只要在controller中指定使用admin layout即可：
```ruby
class AdminsController < ApplicationController
  layout "admin"
end
```

### 稍微進階一點的做法：

我們也可以指定某個 action 要使用admin layout：

```ruby
class AdminsController < ApplicationController
   layout "admin", :only => :new
   # 另外也可以在render的時候就指定要使用哪一個layout
   def show
      render :layout => "admin"
   end

   # 甚至可以指定模板再指定layout
   def index
    render :template => "others/weired_topics", layout: "admin"
  end
end
```


