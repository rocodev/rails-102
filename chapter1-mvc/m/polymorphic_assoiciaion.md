# Polymorphic Assoiciaion

Polymorphic Associations是rails內可以讓兩個不同的Model同時has_many一個model的做法，最常見的情況就是要做留言系統的時候。

假設我們希望使用者可以針對文章留言，也可以針對看版留言，但是這些留言所需要的欄位都一樣，我們沒有必要新增像`TopicComment`和`BoardComment`這樣的model
只需要新增一個`Comment`model再用Polymorphic Associations關聯就可以了。

Model的設定如下：
```ruby
class Comment < ActiveRecord::Base
  belongs_to :commentable, :polymorphic => true
end

class Board < ActiveRecord::Base
  has_many :comments, :as => :commentable
end

class Topic < ActiveRecord::Base
  has_many :comments, :as => :commentable
end
```



而Comment裡面必須包含兩個欄位分別是`commentable_id`和`commentable_type`

`commentable_type`記錄你的model名稱

`commentable_id`記錄該model下的資料id

rails3之後的migration可以單獨寫`t.references :imageable, polymorphic: true`就會自動生成這兩個欄位

```ruby
class CreatePictures < ActiveRecord::Migration
  def change
    create_table :pictures do |t|
      t.string :name
      t.references :imageable, polymorphic: true
      t.timestamps
    end
  end
end
```

作用示意圖：

![](http://guides.rubyonrails.org/images/polymorphic.png)

參考資料：
* http://guides.rubyonrails.org/association_basics.html#polymorphic-associations
