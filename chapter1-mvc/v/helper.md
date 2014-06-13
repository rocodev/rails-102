# 什麼是 helper


Helper是 Rails 簡化View的方法之一，Rails 有內建的一系列 helper 可以用，常見的有 `link_to`、`form_for`、`content_tag` 等等。

此外我們也可以自己建立 Helper，將View中需要邏輯判斷或是不斷重複的 code 寫進 helper內，例如：

```ruby
module BoardsHelper

 # 回傳board的name，避免在view中做太多判斷
  def render_board_name(board)
  	if board.present?
    	board.name
    else
    	"unknown"
    end
  end

# 常常重複的區段也可以寫進 helper，統一管理
  def render_board_name_path(board)
    link_to(board.name, board_path(board))
  end
end

```

在view中可以直接取用如下

```erb
<%= render_board_name_path(@board) %>
```
