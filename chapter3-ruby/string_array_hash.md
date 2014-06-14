# String / Array / Hash

在Ruby裡面，String / Array / Hash都是類別
```
"".class #=> String
"".class.class # => Class
[].class #=> Array
[].class.class # => Class
{}.class #=> Hash
{}.class.class # => Class
```

因此我們可以呼叫各別的class method，例如：

* String：字串
```ruby
"hello world".capitalize # => "Hello World"
```
* Array：陣列
```ruby
[ "a", "b" ] << [ "c", "d", "e" ] # => [ "a", "b", "c", "d", "e" ]
```
* Hash：由key-value鍵組成的檔案形態
```ruby
{:name => "hello"}.empty?   #=> false
{}.empty?   #=> true
```

可再參考 http://www.ruby-doc.org/ 獲得更多資訊。
