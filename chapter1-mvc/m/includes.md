# includes

當我們操作關聯性資料時，可以使用includes將關聯資料先抓出來，這樣每次要調用資料時就不是去資料庫搜尋，而是從已經調閱出來的資料搜尋，可以提高效能。舉例說明：

假設「Board」has_many「Topics」，原本我們會這樣寫：

```ruby
class Board < ActiveRecord::Base
  def
    @boards = Board.all
  end
end
```

這種情況下若我們在view裡面寫`@board.topics`，假設我們共有10個board，系統會這樣幫我們找資料：

1.到資料庫裡找board_id = 1 的topic

2.到資料庫裡找board_id = 2 的topic

.....

10.到資料庫裡找board_id = 10 的topic


這樣的做法有個很弔詭的地方在於我們重複搜尋了資料庫10次，造成效能問題。

若加上 `includes`後會是這樣：

```ruby
class Board < ActiveRecord::Base
  def
    @boards = Board.includes(:topics).all
  end
end
```

這種時候我們若在view裡面寫`@board.topics`，假設我們共有10個board，系統會這樣幫我們找資料：

1.到資料庫裡把topic全部抓出來

2.從抓出來的 topic中找到 board_id 相對應的topic。

這樣做我們就只需要搜尋一次，直接減少了資料庫的負擔。


