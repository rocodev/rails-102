# STI


全名：單一表格繼承 STI(Single-table inheritance)

rails guide說明片段：
>a way to add inheritance to your models

簡單來講就是讓繼承的submodel可以擁有父類別的表格欄位且繼承父類別的方法

在rails慣例中只要加上`type`這個欄位在父類別的資料庫中就可以了

例：User有分Native跟Foreigner
```ruby
class User < ActiveRecord::Base
end
class Native < User
end
class Foreigner < User
end
```

這樣就可以了，可以新增Native User

```
native = Native.create(:name => "foobar")
native.type # => "Native"
```

STI的使用時機是當我們需要一個擁有一樣特性但是不同行為的model時才使用。

參考資料：

* http://thibaultdenizet.com/tutorial/single-table-inheritance-with-rails-4-part-1/
