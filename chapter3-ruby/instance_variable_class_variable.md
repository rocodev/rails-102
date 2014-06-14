# instance variable / class variable


簡單來說，class variable跟著class走，instance variable跟著實例走
class variable跟instance variable都可以被繼承
但只要是在class底下的任何實例改變了class變數，其他同個class的實例的class變數也會被改變
class variable例子：

```ruby
class Earth
	# class variable用@@定義
  @@pollution = "low"
end

class HumanBorn < Earth
	@@pollution = "high"
end
```
讓我們查看這時Earth的變數`@@pollution`就變成了`"high"`，因為是class variable所以被HumanBorn更改了。


但若class底下的實例是改變實例變數，那麼就只會在實例中被改變，不會影響到其他實例
instance variable例子：

```ruby
class Kid
	@age = 1
  def grow_up
  	@age = @age +1
  end

  def show_age
  	@age
  end
end

wayne = Kid.new
wayne.show_age # => 1
wayne.grow_up
wayne.show_age # => 2

jason = Kid.new
# wayne.grow_up改變的是wayne這個實例內的instance variable，所以不影響jason這個實例
jason.show_age # => 1
```
