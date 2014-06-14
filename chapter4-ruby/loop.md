# 迴圈慣例

####  單行的迴圈使用 { } ，多行的迴圈使用 do end

``` ruby
10.times {|n| puts "This is #{n}"}

10.times.do |n|
  puts "This is #{n}"
  puts "That is #{n*2}"
end

```

大師 Jim Weirich 在 [Braces VS DO/END](http://onestepback.org/index.cgi/Tech/Ruby/BraceVsDoEnd.rdoc) 這篇提出他的觀點：

* Use { } for blocks that return values
* Use do / end for blocks that are executed for side effects

``` ruby
# block used only for side effect
list.each do |item| puts item end

# Block used to return test value
list.find { |item| item > 10 }

# Block value used to build new value
list.collect { |item| "-r" + item  }
```

####  使用 each 而非 for

Ruby 中跑迴圈的方式可以有很多種，最常使用的是 for 和 each 

使用無窮迴圈測試四種常見迴圈寫法。

``` ruby

Benchmark.bm do |x|

  x.report('while1') do
    n = 0
    while 1 do
      break if n >= 1000000
      n += 1
    end
  end
 
  x.report('loop') do
    n = 0
    loop do
      break if n >= 1000000
      n += 1
    end
  end
 
  x.report('Infinite.each') do
    n = 0
    (0..(1/0.0)).each do
      break if n >= 1000000
      n += 1
    end
  end 
  
  x.report('for Infinite') do
    n = 0
    for i in (0..(1/0.0)) do
      break if n >= 1000000
      n += 1
    end
  end
  
end
```

跑出來的數值如下

```
                    user     system      total        real
while1          31.960000   0.150000  32.110000 ( 36.749597)
loop            42.240000   0.190000  42.430000 ( 45.533708)
Infinite.each  108.400000   0.970000 109.370000 (117.421059)
for Infinite   112.070000   1.010000 113.080000 (126.712828)
```

for 明顯比 each 慢上許多。

## 參考資料：

* <http://www.ruby-forum.com/topic/179264>