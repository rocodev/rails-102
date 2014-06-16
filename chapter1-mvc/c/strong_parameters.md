# Strong Parameters

Rails 的 Form 綁 Model 設計非常直觀直覺，表單欄位直接對應到 Model 欄位。但也因此，容易被 Hack 猜中關鍵欄位的慣例，在瀏覽器自造欄位入侵測試，因而產生安全疑慮。

在 Rails 4 時，維護團隊發明一套方法能夠有效地解決這個問題。這套機制就是 Strong Parameters。

Strong Parameters 的想法是若 params 沒有被 permit，就是非法欄位，無法被直接送進 create / update method 更新。

## 使用方法

``` ruby
class PeopleController < ActionController::Base
  def update
    person.update_attributes!(person_params)
    redirect_to :back
  end

  private
    def person_params
      params.require(:person).permit(:name, :age)
    end
end
```

## Nested Attributes with Strong Parameters

在有些情況我們會需要做 Nested Form，這時候就需要將 Nested Form 的 Attributes 也加到 Strong Parameters 內。

假設每一個 Person Model 有都可以有一頂 Hat，在新增 Person 的時候用 Nested Form 同時新增 Hat 的顏色。我們應該這樣做：

###1.在 Person Modle 中宣告我們可以接受 hat 的 attributes：
```ruby
class Person < ActiveRecord::Base
  has_one :hat
  accepts_nested_attributes_for :hat
end
```
```ruby
=begin
  Hat Database Information:
    id:integer
    color:string
    created_at:datetime
    updated_at:datetime
=end
class Hat < ActiveRecord::Base
	belongs_to :person
end
```

### 2.在 Controller 中指定接收的 Attributes
由於我們在 People Controller 內的 Strong Parameters 並不包含 color 這個 Attributes，所以在新增 Hat 的時候就無法把 color 寫進資料庫，這時候需要加上 `hats_attributes: []` 這個 Attributes，並且將要傳的 Hat Attributes 寫進 Array 中：

``` ruby
class PeopleController < ActionController::Base
  def update
    person.update_attributes!(person_params)
    redirect_to :back
  end

  private
    def person_params
      params.require(:person).permit(:name, :age, hats_attributes: [:color])
    end
end
```

這樣就可以通過 People Controller 的驗證了。
