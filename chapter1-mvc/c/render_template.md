# render :template

render的中文意思是給予，所以render template就是給予指定的模板，render的特性是不跑controller action，直接將該action下預設的模板傳出來，我們也可以自己指定要哪個特定的模板。

舉例說明：

render特定的模板

render views/foo/bar.html.erb
```ruby
render "foo/bar"
```
render同一個controller下的action的view，用symbol和string都是一樣的：
```ruby
render :foobar
render "foobar"
```

