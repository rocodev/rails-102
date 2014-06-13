# render :template

render 的中文意思是「渲染」，所以 render template就是「渲染」指定的模板，render的特性是不跑 controller action，直接將該 action下 預設的模板傳出來，我們也可以自己指定要哪個特定的模板。

舉例說明：

render 特定的模板

render views/foo/bar.html.erb

```ruby
render "foo/bar"
```
render 同一個 controller 下的 action 的 view，用 symbol和string都是一樣的：

```ruby
render :foobar
render "foobar"
```

