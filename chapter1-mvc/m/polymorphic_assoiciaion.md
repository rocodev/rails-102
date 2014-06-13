# Polymorphic Assoiciaion

Polymorphic Associations是 Rails 內可以讓兩個不同的 Model 同時 has_many 一個 model的做法，最常見的情況就是要做留言系統的時候。

假設我們希望使用者可以針對文章留言，也可以針對看版留言，但是這些留言所需要的欄位都一樣，我們沒有必要新增像`TopicComment`和`BoardComment`這樣的model
只需要新增一個`Comment` model 再用 Polymorphic Associations 關聯就可以了。

## 範例

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



而 Comment裡面 必須包含兩個欄位分別是`commentable_id`和`commentable_type`

`commentable_type`記錄 model 名稱

`commentable_id`記錄該 model 下的資料id

Rails3之後的 migration 可以單獨寫`t.references :imageable, polymorphic: true`就會自動生成這兩個欄位。

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

### 作用示意圖

![](http://guides.rubyonrails.org/images/polymorphic.png)

## 參考資料

* http://guides.rubyonrails.org/association_basics.html#polymorphic-associations
* http://railscasts.com/episodes/154-polymorphic-association
