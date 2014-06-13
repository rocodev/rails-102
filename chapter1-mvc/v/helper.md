# 什麼是 helper


Helper是rails簡化View的方法之一，rails有內建的一系列helper可以用，常見的有link_to、form_for、content_tag等等。

此外我們也可以自己建立Helper，將View中需要邏輯判斷或是不斷重複的code寫進helper內，例如：

```ruby
module BoardsHelper
#回傳board的name，避免在view中做太多判斷
  def render_board_name(board)
  	if board.present?
    	board.name
    else
    	"unknown"
    end
  end
#常常重複的區段也可以寫進helper，統一管理
  def render_board_name_path(board)
    link_to(board.name, board_path(board))
  end
end
```
在view中可以直接取用如下
```erb
<%= render_board_name_path(@board) %>
```
