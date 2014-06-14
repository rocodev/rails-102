# 字串慣例

#### 使用 `"#{}"` 而非 `+` 串接字串。

``` ruby
# bad
full_name = first_name + ' <' + last_name + '>'

# good
full_name = "#{first_name} <#{last_name}>"

```
原因：使用 string interpolation 可以讓程式顯得更直觀。而且 `+`會產生一堆不必要的 new object。

#### 使用 `<<` 而非 `+` 串接字串

``` ruby
html << "<h2>Post Title </h2>"
```

原因：`String#<<` 比 `String#+` 速度快的多。而且 `+`會產生一堆不必要的 new object。

#### 偏好使用 `" "`(double quote) 而非`' '`(single quote) 包覆字串

```
name = "foobar"
string = "#{name}"

# => foobar

string = '#{name}'

# => #{name}

```
原因： 雖然 `' '` 和 `" "` 都可以用來宣告字串。但`" "` 才有 string interpolation (double quote)效果。

#### 使用 `%()` 處理需要 string interpolation 但同時也需要 `" "`(double quote) 的狀況

有時候我們不避免的需要寫出這樣的 code

``` ruby
<%= "<div class=\"name\"> #{name} </div>" %>
```

雖然可以透過將 `" "` 換成 `' '` 讓 code 不那麼粘膩。

``` ruby
<%= "<div class='name'> #{name} </div>" %>
```

但其實還有這一招使用 `%()`，可以確保事情不會變得更加複雜。

``` ruby
<%= %(<div class="name">#{name}</div>) %>
```