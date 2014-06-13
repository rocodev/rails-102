# render :text

render純文字，沒有用過這個功能，但猜想若是要把複雜的code包在js裡面的時候，可能會出現單雙引號打架之類的問題，所以用render的方式吐出string也許是一種方法。

```ruby
render "嗨，自己的文字自己render"
```
