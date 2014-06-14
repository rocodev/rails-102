# 三重運算子簡化 if / else

比較簡單的 if / else statement

如:

``` ruby
if some_condition
  something 
else 
  something_else 
end
```

其實可以簡化成 : 

``` ruby
some_condition ? something : something_else
```

#### 不要濫用三重運算子

雖說 Ruby 提供這樣的簡化方式，但儘量還是不要濫用。如果超過兩層還是要將之拆開

``` ruby
# bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# good
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```

