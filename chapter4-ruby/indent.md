# 縮排慣例


Ruby 的縮排是 2 個空格。不是 3，也不是 4。

``` ruby
# good
def hello
  "Hello World"
end

# bad
def hello
    "Hello World"
end
```

###  編輯器的自動縮排功能

Sublime Text2 設定, Settings Default =>


```
// The number of spaces a tab is considered equal to
"tab_size": 2,

// Set to true to insert spaces when tab is pressed
"translate_tabs_to_spaces": true,
```

### 必裝 Submlime Text2 套件

* [BeautifyRuby](https://github.com/CraigWilliams/BeautifyRuby)

`Ctrl` + `Cmd` + `k` 自動對 Ruby 縮排