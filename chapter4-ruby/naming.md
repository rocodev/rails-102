# 命名慣例


### 變數或者是 method 名稱，採用 snake_case

``` ruby
def credit_card_discount
  original_price * 0.9
end
```

###  Class 和 Module 名稱，採用 CamelCase

``` ruby
class UserProfile
  def initialize(name)
    @name = name
  end
end

```

###  CONSTANT 使用 SCREAMING_SNAKE_CASE

``` ruby
class Invoice
  CREDIT_CARD_TYPE = ["VISA","MASTER"]
end

```
