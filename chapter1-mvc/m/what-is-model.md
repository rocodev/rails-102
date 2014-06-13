#Model

## Model是什麼？

Model是 繼承於 ActiveRecord 的 Class，所以每個 Model 都可以取用 ActiveRecord 裡面的 Method，例如我們有一個 Model叫做 Post，這個Model會長這樣：

```ruby
class Post < ActiveRecord::Base
end

```
而這個 Model 將會負責操作`Posts`的資料庫，由於Post Model繼承ActiveRecord，所以我們可以用ActiveRecord的method，例如：

```ruby
# first就是ActiveRecord的Method
Post.first
# => 回傳第一個Post
```

## 什麼東西應該放在Model

只要是跟操作資料庫有關的行為基本上都應該儘量放在Model裡面實作，大部份情況是要操作已經叫出來的實例變數。（若對 Ruby 的變數不太了解請先參考[Ruby系列教學](../chapter3-ruby/README.md)）


