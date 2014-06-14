# 布林慣例

### 布林邏輯使用 && 與 || ，而非 and 和 or

不少人在寫邏輯判段式時，會誤以為 && 和 || 與 and / or 是等價的，因此產出不少 bug。其實 and 和 or 跟 if / else 是等價的。所以請千萬不要在 boolean 邏輯內使用 and / or。 

* 被判斷為 foo = ( 42 && foo ) / 2

``` ruby

foo = 42 && foo / 2  
=> NoMethodError: undefined method '/' for nil:NilClass

``` 

#### 使用 and

``` ruby

food = 42 and foo / 2
=> 21

```

### and 與 or 真正的用法

#### and 的用法

``` ruby
next if widget = widgets.pop  
```

相當於

``` ruby 
widget = widgets.pop and next  

```

#### or 的用法

``` ruby
raise "Not ready!" unless ready_to_rock?   
```
相當於

``` ruby
ready_to_rock? or raise "Not ready!"  
```

## 參考資料

* Avdi 的 [Using “and” and “or” in Ruby](http://avdi.org/devblog/2010/08/02/using-and-and-or-in-ruby)
