# yield in view


yield 就是會被替換成樣板的地方，基本上所有的 `html.erb` 檔案最後就是顯示在`<%= yield %>`的地方，這樣做的好處是可以將網站的版型固定，只在需要出現內容的地方用 yield 引進來就可以了。

通常 Rails專案中都會有一個`application.html.erb`的檔案，我們的`html.erb`檔就是被引入這裡

`application.html.erb`

```erb
<!DOCTYPE html>
<html>
<head>
  ...
</head>
<body>
  <div class="container">
    # erb檔案就是被引入這裡
    <%= yield %>
  </div>
  #可以指定要yield哪個區塊
  <%= yield(:javascripts) %>
</body>
</html>
```

### 稍微進階一點的做法：

另外我們也可以指定要yield哪個區塊，我們可以用`content_for`的方式讓content替換掉`<%= yield(:javascripts) %>`：

```erb
<%= content_for :javascripts do %>
	#content here
<% end %>
```
