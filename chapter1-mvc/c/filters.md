# Filters : before_action, after_action, around_action

`before_action`的意思就是要求 Rails在run controller下的 action 前要先跑指定的method。相對的`after_action`就是跑完 action 後才要跑的method，至於`around_action`就是之前之後都要跑(嘖嘖，真貪心)。

以下為`before_filter`的示範：

```ruby
class TopicsController < ApplicationController

  before_action :find_board

  def index
  	@topics = @board.topics
  end

  def find_board
  	@board = Board.find(params[:id])
  end
end
```

我們在 TopicsController 上方要求它在每次執行 action 前都要`find_board`，所以就不用在 index 裡面再定義一次`@board`，如此一來若有很多action就不會有重複的程式碼產生。

此外我們也可以限定filter要作用的action，例如：

```ruby
before_action :find_board, :only => [:index]
```
這樣 Controller在執行時就只會針對 index 這個 action 執行 `find_board`。
