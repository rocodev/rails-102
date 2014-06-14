# Mixin / Extend / Inheritance


在說明Mixin跟Extend之前我們必須先解釋何為Module，因為Mixin跟Extend是在引入module時會使用到的語法，而Inheritance則是繼承class時會用到的。

### Module
Module的好處就是可以選擇性的引用Module內的方法，不會讓Module內的變數或是Method與其他Class互相影響，有點類似class補充包的感覺。而引用Module的方式就是Mixin & Extend。

## Mixin

引用Module的方式有以下兩種
第一是可以在Class內include Module
```ruby
class Include < Example
	include module
end
```
使用include的方式可以讓module的method在class底下被取用
所以我們就可以使用這樣的方法：
```ruby
user.module_method
```

## Extend

另外一個引用Module方式是Extend
Extend的用法是讓Class可以直接取用Module內的Method
```ruby
class Extend < Example
	extend module
end
```
所以這樣這個時候我們就可以使用這樣的寫法：
```ruby
Extend.module_method
```


## Inheritance
Inheritance（繼承）的意思就是繼承者擁有被繼承者的特性，用於類別(class)的繼承，所以子類別可以呼叫父類別的方法

```ruby
class Parent
  @last_name = "james"
  def laugh
  	"heeeeeeeeha!"
  end
  def last_name
  	@last_name
  end
end

class Child < Parent
end

dad = Parent.new
son = Child.new
#Child可以呼叫Parent的method
papa.laugh # => "heeeeeeeeha!"
son.laugh # => "heeeeeeeeha!"
#Child也繼承了Parent的實例變數
son.last_name # => "james"
```

## 參考資源

* http://railstips.org/blog/archives/2009/05/15/include-vs-extend-in-ruby/