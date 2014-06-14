# 括號慣例


#### 定義 method 要加括號。除非沒有參數。

``` ruby

# 有括號
def find_book(author,title, options={})
  # ....
end

# 無括號
def word_count
  # ....
end

```

#### 使用 method 要加括號。除非是 statement 或 command

``` ruby

# 有括號

link_to("Back", post_path(post))

# 無括號

redirect_to post_path(post)

```

#### statement 多數時候要加括號，但如果狀況單純可不加括號

``` ruby

# 無括號

if post.content_size > 100
  # ....
end

# 有括號

if (post.content.size > 100) && post.is_promotion?
  # ....
end
```

### 「使用括號」是一個相對比較好的習慣

看到這裡都開始讓人搞迷糊了。到底是什麼樣的情況要加括號？什麼樣的情況不加括號？筆者的建議是，一旦沾到相當較複雜的陳述句時，儘量加上括號。Ruby 雖然是一個相當自由的語言，可以用空格(space)或是括號(parentheses)傳入參數。但濫用空格可能造成 Ruby 在 parsing 陳述句的時候解讀異常，產出非正確的結果，這就是大家所不願意樂見的狀況了。

### 括號的唯一例外：super 與 super()

在 Ruby 中，唯一加括號和不加括號會有別的是 super 與 super()。它們代表了不同的意思：


#### super 不加括號表示呼叫父類別的同名函式，並且將本函式的所有參數傳入父類別的同名函式。


``` ruby
class Foo
  def initialize(*args)
     args.each {|arg| puts arg}
  end
end

class Bar < Foo
  def initialize( a, b, c)
    super
  end
end

```
如果執行 

``` ruby
> a, b, c = *%W[a b c]
> Bar.new a, b, c
```

將會印出 `a` `b` `c`

#### super() 帶括號則表示呼叫父類別的同名函式，但是不傳入任何參數。

但如果是

``` ruby
class Foo
  def initialize(*args)
     args.each {|arg| puts arg}
  end
end

class Bar < Foo
  def initialize( a, b, c)
    super()
  end
end

```

執行 

``` ruby
> a, b, c = *%W[a b c]
> Bar.new a, b, c
```

則不會印出任何東西。

