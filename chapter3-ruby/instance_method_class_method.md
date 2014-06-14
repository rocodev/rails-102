# instance method / class method

class method就是給class層級呼叫的method
instance method則是給class的實例呼叫的method

舉例說明，假設我們有一個class Test長這樣：
```ruby
class Test
# 在class內定義method時加上self代表要直接取用class
  def self.class_method
  	"class method"
  end

  def instance_method
 	 "instance method"
  end
end
```

呼叫class method時的情況：
```ruby
#class的呼叫
Test.class_method # => "class method"
Test.instance_method # => NoMethodError: undefined method `instance_method' for Test:Class
```
呼叫instance method時的情況：
```ruby
#class實例的呼叫
test = Test.new  # => #<Test:0x007fd103969840>
test.class_method # => undefined method `class_method' for #<Test:0x007fd103969840>
test.instance_method # => "instance method"
```
