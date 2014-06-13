# filters : before_filter, after_filter, around_filter
`before_filter`的意思就是要求rails在run controller下的action前要先跑指定的method，相對的`after_filter`就是跑完action後才要跑的method，至於`around_filter`就是之前之後都要跑(嘖嘖，真貪心)。以下為`before_filter`的示範：

```ruby
class TopicsController < ApplicationController
  #rails4之後也可以使用before_action
  before_filter :find_board
  def index
  	@topics = @board.topics
  end

  def find_board
  	@board = Board.find(params[:id])
  end
end
```
我們在TopicsController上方要求它在每次執行action前都要`find_board`，所以就不用在index裡面再定義一次`@board`，如此一來若有很多action就不會有重複的程式碼產生。

此外我們也可以限定filter要作用的action，例如：
```ruby
before_filter :find_board, :only => [:index]
```
這樣controller在執行時就只會針對index這個action執行find_board。
