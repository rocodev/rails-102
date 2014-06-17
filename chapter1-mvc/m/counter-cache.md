# counter_cache

`counter_cache` 是在做關聯性資料庫時計算資料量的一個方法。


照樣舉「Board」has_many「Topics」的例子來看
正常我們會寫類似下方的程式碼來算出這個 Board 內有多少個 Topics：

```ruby
@board.topics.size
```

這代表每次我們要算數量的時候都得下一個sql指令去算有多少topics，一樣是會造成效能問題。

所以 Rails 內建了 `counter_cache` 的方法，我們只要在 Topic model 內加上`counter_cache: true`

```ruby
class Topic < ActiveRecord::Base
	belongs_to :board, counter_cache: true
end
```

然後在 Board 的資料庫內新增一個叫做`topics_count`的欄位

這樣以後當這個 Board內的 topics 有增減的時候，Rails就會幫我們增減`topics_count`的欄位，如此一來下次再下`@board.topics.size`的指令時 Rails就會預設去找`topics_count`的欄位，不用重新下 SQL指令計算。

### 自定 Counter Cache 欄位：

我們也可以覆蓋 Rails的預設規定，自己定義要增減的欄位名稱，例如把`topics_count`改成`count_of_topics`：
```ruby
class Topic < ActiveRecord::Base
	belongs_to :board, counter_cache: :count_of_topics
end
```

