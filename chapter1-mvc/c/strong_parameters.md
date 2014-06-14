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

TBD