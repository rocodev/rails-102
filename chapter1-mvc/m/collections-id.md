# collect(&:id)


基本上跟[map](../chapter3-ruby/map.md)是一樣的東西，collect做的事情就是將array內的資料一一拿出來處理，處理完後再傳回array
所以`topics.collect(&:id)`就是把topics內所有的id都拿出來存成另一個array

ex:
```ruby
topics = [{id:1, title:"topic1"}, {id:2, title:"topic2"}]
topics.collect(&:id)
# => [1,2]
```

###稍微進階一點的做法：
假設我們要讓id都變成浮點數(雖然我想不到理由為什麼要變成浮點數，XDrz)

我們可以這樣下指令：

```ruby
t.collect{|t| t.id.to_f }
# 或是更簡單一點：
t.collect(&:id).collect(&:to_f)
# 回傳都會是一樣的
# => [1.0,2.0]
```

## 參考資料

* http://stackoverflow.com/questions/5254732/difference-between-map-and-collect-in-ruby
* http://rubyinrails.com/2014/01/ruby-difference-between-collect-and-map/
