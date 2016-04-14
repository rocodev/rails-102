# self

self指的就是我們物件本身

舉例說明，假設我們有一個class Foo：
```ruby
class Foo
  def self.foo
  	"class method"
  end
  def foo
 	 "instance method"
  end
  def foobar
  	self.foo
  end
end
```
我們可以用class呼叫method，self現在是Foo class：
```ruby
Foo.foo # => "class method"
```
或是讓Foo class生成一個實例，再用實例呼叫method：
```
# 產生Foo class 的 object
f = Foo.new  # => #<Foo:0x007fd103969840>
f.foo # => "instance method"
# foobar method 裡面的 self 就是 f 這個實例
f.foobar # => "instance method"
```

此章節建議搭配[instance method / class method](instance_method_class_method.md)和[instance variable / class variable](instance_variable_class_variable.md)一起觀看。
