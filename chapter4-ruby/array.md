# Array 慣例

#### 當要宣告一個擁有多字串的 Array 陣列時，偏好使用 %w 

``` ruby
array = ["A", "B", "C", "D"]

# better
array = %w(A B C D)
```

### Hash 慣例

使用 `:symbool` 而非 `"string"` 作為 Hash 的 key

``` ruby
# bad
{ "foo" => "bar" }

# good
{ :foo => "bar" }

```

原因：若使用 `"string"`，Ruby 每次都會為 key 在不同的記憶體位置再產生一個新 string object 。

使用 `"string"` :

``` ruby
string1 = { "foo" => "bar" }
string2 = { "foo" => "rab" }
string1.each_key {|key| puts key.object_id.to_s}
# => 2191071500
string2.each_key {|key| puts key.object_id.to_s}
# => 2191041700
```
改採用 `:symbol` :

``` ruby
string1 = { :foo => "bar" }
string2 = { :foo => "rab" }
string1.each_key {|key| puts key.object_id.to_s}
# => 304828
string2.each_key {|key| puts key.object_id.to_s}
# => 304828
```

這就是鼓勵使用 `[:symbol]` 而非`"string"` 作為 Hash 中的key的原因，在很多記憶體使用量的膨脹和浪費的 case 中，多數都是因為產生了過多不必要的 object 所造成的問題。










