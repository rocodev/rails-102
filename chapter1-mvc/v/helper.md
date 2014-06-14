# 什麼是 helper


Helper 是一些使用在 Rails 的 View 當中，用 Ruby 產生/整理 HTML code 的一些小方法。通常被放在 `app/helpers` 下。預設的 Helper 名字是對應 Controller 的，產生一個 Controller 時，通常會產生一個同名的 Helper。如 `PostsController` 與 `PostsHelper`。


使用 Helper 的情境多半是：

* 產生的 HTML code 需要與原始程式碼進行一些邏輯混合，但不希望 View 裡面搞得太髒。
* 需要與預設的 Rails 內建的一些方便 Helper 交叉使用。

使用 Helper 封裝程式碼可以帶給專案以下一些優點：

* Don't repeat yourself（DRY）程式碼不重複
* Good Encapsulation好的封裝性
* 提供 view 模板良好的組織
* 易於修改程式碼

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
