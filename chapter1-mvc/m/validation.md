# validation

validation是在 Model 內驗證資料的方法，用以確保資料符合我們的要求。

validation 運作的時機是在 SQL 指令執行之前，所以當 ActiveRecord 認為這筆資料未通過驗證，就不會將 Ruby 轉換為 SQL 語言寫入，而是傳回錯誤訊息。

validation常見的寫法有：

```ruby
class Topic < ActiveRecord::Base
  # presence: true代表這個資料必須有值
  validates :title, presence: true
  # content最多只能200字
  validates :content, length: { maxmum: 200 }
end
```

會引發驗證機制的method有`create`、`save`、`update`等。

正常情況若validate fail時 create 會把object丟回來，update和save則是會回傳false，倘若想知道錯誤原因，可以在method後加上驚嘆號`save!`

```ruby
topic.save
# => false
topic.save!
# => ActiveRecord::RecordInvalid: Validation failed: Title can't be blank
```

## 參考資料

除了上述兩種驗證方式，尚有驗證文字格式、數字、唯一等等，可以查看 [Rails Guide](http://guides.rubyonrails.org/active_record_validations.html) 得到更多資訊。


