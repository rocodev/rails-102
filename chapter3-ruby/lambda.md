# lambda


要解釋 lambda 必須先解釋 Proc，Proc就是把block存成實例的方式，呼叫前加上`&`就可以轉回block：

```ruby
p = Proc.new { |x| puts x * 2 }   # 也可以寫成 p = proc { |x| puts x * 2 }
# => #<Proc:0x007ffb8c250488@(irb):66>   存成Proc的實例
# 要用時加上&
[1,2,3].each(&p)
# => 2
# => 4
# => 6
p.class
# => Proc
```

lambda 基本上也是 Proc 的實例，只是它的形態叫做lambda。

```ruby
lam = lambda { |x| puts x * 2 }
# => #<Proc:0x007ffb8c230408@(irb):5 (lambda)>  也是存成Proc的實例，但是存成lambda的形態
[1,2,3].each(&lam)
# => 2
# => 4
# => 6
lam.class
# => Proc
```

lambda 和 proc的主要差別有兩個

### 1. lambda會check參數數量，proc不會

```ruby
# lambda
lam = lambda { |x| puts x }
lam.call(2) #=> 2
lam.call(2,3) #=> ArgumentError: wrong number of arguments (2 for 1)

# proc
proc = Proc.new { |x| puts x }
proc.call(2) #=> 2
proc.call(2,3) #=> 2    proc忽略了其他參數，只傳第一個
```

### 2. `return`的處理不同，lambda的`return`只會跳出lambda，proc的`return`會跳出整個method


```ruby
def lambda_test
  lam = lambda { return }
  lam.call
  puts "Haha! after lam call, i survived!"
end
def proc_test
  p = Proc.new { return }
  p.call
  puts "after proc call, i survived!"
end

lambda_test # => "Haha! after lam call, i survived!"
proc_test # => #沒東西，因為在執行到puts前就跳出proc_test這個method了
```

## 參考資料

* http://augustl.com/blog/2008/procs_blocks_and_anonymous_functions/
* http://awaxman11.github.io/blog/2013/08/05/what-is-the-difference-between-a-block/

