# scope

scope 的作用就是將時常使用或是複雜的ORM語法組合成懶人包，這樣下次要用的時候只要把懶人包拿出來就可以了，舉例說明：

```ruby
class Topic < ActiveRecord::Base
	scope :recent, -> { order("created_at DESC") } 
end
```

上面這段code我們定義了`recent`這個scope，以後我們只要下`recent`這個指令就等於下`order("created_at DESC")`是一樣的。如此一來就可以讓程式碼更為簡潔。

## 使用情境

* 當有過於複雜的資料查詢
* 當有重覆使用的資料查詢


## 使用方式

### 沒帶參數的方式

```ruby
class Post < ActiveRecord::Base
  scope :published, -> { where(published: true) }
end
```          

### 帶有參數的方式

```
class Post < ActiveRecord::Base
  scope :created_before, ->(time) { where("created_at < ?", time) }
end
```

### 可以串接在一起，順序沒有影響

```ruby
class Event < ActiveRecord::Base
  scope :published, -> { where(published: true) }
  scope :created_before, ->(time) { where("created_at < ?", time) }
end
```        

`Event.published.created_before(Time.now)`

## 參考資料

* http://guides.rubyonrails.org/active_record_querying.html
