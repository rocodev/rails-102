# 邏輯慣例

## if / unless 的寫作觀念

Ruby 在邏輯控制的部份，除了提供 if 還提供了 unless。

unless 等於 「if not something 」等於 「if !something」。

不過雖說 Ruby 提供了 unless 這個用法，但在實務上來說，一般還是不太推薦使用 unless。除了以下幾種狀況：

### 當語意較適合時，使用 unless

``` ruby
unless content.blank?
  # ....
end
```

### 沒有 else 的時候，使用 unless

當沒有 else 的時候，看起來還算 OK

``` ruby
unless foo?
  # ....
end
```

但加上一個 else，看起來就不是那麼直觀了

``` ruby
unless foo?
  # ....
else
  # ....
end  
```

如果專案當中有這樣的 code，相信我，換成 if 的陳述會直觀許多。

``` ruby
if !foo?
  # ....
else
  # ....
end  
```

### 當只有一個條件時，使用 unless 很適合。但多個條件時，使用 unless 很糟糕。

``` ruby
unless foo? && baz?
  # ....
end
```

相同的，改成 if 也會直觀許多

``` ruby
if !foo? || !baz?
  # ...
end
```
