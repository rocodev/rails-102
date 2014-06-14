# CoffeeScript

CoffeeScript 本身也是一種程式語言，開發者可以透過撰寫 CoffeeScript，編譯產生 JavaScript。它的語法有點像是 Ruby 與 Python 的混合體。

不得不坦承，當初 Rails 3.1 選擇同時納入 SCSS 以及 CoffeeScript 作為預設支援時，開發者是一半歡欣一半困惑的。歡欣的是納入 SCSS，困惑的是引入 CoffeeScript。

SCSS 讓撰寫 CSS 變得無比的直觀，並藉由 Compass 引入了不少 killer features。但使用 CoffeeScript 卻沒有這麼多壓倒的好處，有些人也形容，撰寫 CoffeeScript 需要腦袋內建 compiler …

好像用 Python 在寫 Ruby，但實際上寫的是 JavaScript

這是 CoffeeScript 的一段範例

``` coffee
name = "Rails";
greeting_words = "Hi, #{name}"
say_hi = (name) ->
  if name
    "Hello, #{name}"
  else
    greeting_words

```
編譯之後會變成

``` javascript
var greeting_words, name, say_hi;
name = "Rails";
greeting_words = "Hi, " + name;
say_hi = function(name) {
  if (name) {
    return "Hello, " + name;
  } else {
    return greeting_words;
  }
};

```

greeting_words 用的是 Ruby 語法

``` ruby
greeting_words = "Hi, #{name}"
```

say_hi 內的 if / else 則使用 Python 縮排

``` python
  if name
    "Hello, #{name}"
  else
    greeting_words
```

這是 CoffeeScript 的另外一段範例

``` coffee
jQuery ->
  $('#content').focus
```

編譯之後會變成

``` javascript
jQuery(function() {
  return $('#content').focus;
});
```

## 目的：The beautiful way to write JavaScript

乍看之下，CoffeeScript 給人一種詭異感覺：它讓寫 JavaScript 這件事變得更複雜？但也更簡單？…似乎有點矛盾。

Plurk 前創辦人 amix 曾寫過一篇這樣的 post：[「CoffeeScript: The beautiful way to write Javascript」](http://amix.dk/blog/post/19612)來這樣形容 CoffeeScript：「以更漂亮的方式撰寫 JavaScript」。

他認為目前 JavaScript 存在幾種問題：

* JavaScript 是 functional language
* 雖然是 OOP，但卻是 prototype-based 的
* JavaScript 是 dynamic language，更像 Lisp 而不是 C/Java，但卻用了 C/Java 的語法。
* 名字裡面有 Java，但卻和 Java 沒什麼關係。
* 明明是 functional & dynamic laungaue，更偏向 Ruby / Python，卻使用了 C / Java 的 syntax，原本可以是一門很美的語言，卻活生生的變成了悲劇。

而 CoffeeScript 的誕生，原因就是就是為了扭正這樣的局面，重新讓寫 JavaScript 這件事也可以變得「很美」。

CoffeeScript 做了幾項努力：

### 改善 Syntax

JavaScript 目前使用的是與本身型態不搭嘎的 C / Java 語法。CoffeeScript 改採用了深受 Lisp 影響的 Ruby + Python 的混合語法。

### 借鑑其他語言的好處

CoffeeScript 從其他語言借了不少好處，寫起來更方便。

#### Array ( From Python )

``` coffee
# Array
list = [1, 2, 3, 4, 5]
# list comprehensions 
cubes = (math.cube num for num in list)
# array slicing
copy = list[0...list.length]
# array generators
countdown = (num for num in [10..1])
```

#### String (From Ruby)

``` coffee
author = "Wittgenstein"
quote  = "A picture is a fact. -- #{ author }"
```
生成

``` javascript
var author, quote;
author = "Wittgenstein";
quote = "A picture is a fact. -- " + author;

```

多行 String 也沒問題

``` coffee
mobyDick = "Call me Ishmael. Some years ago -
never mind how long precisely -- having little
or no money in my purse, and nothing particular..."
```

這些例子若是直接使用 JavaScript 實作，肯定痛苦個半死…

### Good Parts

CoffeeScript 留下了 JavaScript 的 Good Parts，而在設計上極力消除 JavaScript 原生特性會產生的缺點，例如：

#### 消除到處污染的全域變數

開發者在寫 JavaScript 時，常不自覺的使用全域變數，導致很多污染問題。而透過 CoffeeScript 生出來的 JavaScript，變數一律為區域變數（ 以 var 開頭）

#### Protected code

使用 CoffeeScript 撰寫 function，產生出來的 JavaScript 必以一個 anonymous function: function(){}(); 自我包裹，獨立運作不干擾到其他 function。

#### 使用 -> 和 indent(縮排) 讓撰寫 function 更不容易出錯

在撰寫 JavaScript 時，最令人不爽的莫過於 function(){}();，這些複雜的括號和分號稍微一漏，程式就不知道死在哪裡了….

CoffeeScript 自動產生出來的 JavaScript 能夠確保括號們絕對不會被漏掉。

#### 更容易偵測 syntax error 並攔阻

JavaScript 在 syntax error 時，非常難以偵測錯誤，幾乎是每個程式設計師的夢靨。而 CoffeeScript 是一門需要 compile 的語言，可以藉由這樣的特性擋掉 syntax error 的機會。

#### 實作物件導向變簡單了

Javascript 是一種物件導向語言，裡面所有東西幾乎都是物件。但 JavaScript 又不是一種真正的物件導向語言，因為它的語法裡面沒有 class（類別）。

在 JavaScript 中，我們要實作 OOP 有很多種方式，你可以使用 prototype、function 或者是 Object。但無論是哪一種途徑，其實都「不簡單」。

但 CoffeeScript 讓這件事變簡單了，比如以官網的這個例子：

``` coffee
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."

class Snake extends Animal
  move: ->
    alert "Slithering..."
    super 5

class Horse extends Animal
  move: ->
    alert "Galloping..."
    super 45

sam = new Snake "Sammy the Python"
tom = new Horse "Tommy the Palomino"

sam.move()
tom.move()

```

#### 容易建構 class，也很 Ruby Way

``` coffee
class Animal
  constructor: (@name) ->
```

自動生成

``` javascript
var Animal;
Animal = (function() {
  function Animal(name) {
    this.name = name;
  }
  return Animal;
})();

```

#### 易於在 class 內增添function

``` coffee
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."
```

自動生成

``` javascript
var Animal;
Animal = (function() {
  function Animal(name) {
    this.name = name;
  }
  Animal.prototype.move = function(meters) {
    return alert(this.name + (" moved " + meters + "m."));
  };
  return Animal;
})();

```

#### 實作繼承

``` coffee
class Animal
  constructor: (@name) ->

  move: (meters) ->
    alert @name + " moved #{meters}m."

class Snake extends Animal
  move: ->
    alert "Slithering..."
    super 5
```

自動生成

``` javascript

var Animal, Snake;
var __hasProp = Object.prototype.hasOwnProperty, __extends = function(child, parent) {
  for (var key in parent) { if (__hasProp.call(parent, key)) child[key] = parent[key]; }
  function ctor() { this.constructor = child; }
  ctor.prototype = parent.prototype;
  child.prototype = new ctor;
  child.__super__ = parent.prototype;
  return child;
};
Animal = (function() {
  function Animal(name) {
    this.name = name;
  }
  Animal.prototype.move = function(meters) {
    return alert(this.name + (" moved " + meters + "m."));
  };
  return Animal;
})();
Snake = (function() {
  __extends(Snake, Animal);
  function Snake() {
    Snake.__super__.constructor.apply(this, arguments);
  }
  Snake.prototype.move = function() {
    alert("Slithering...");
    return Snake.__super__.move.call(this, 5);
  };
  return Snake;
})();

```

#### 更容易撰寫測試

因為實作物件導向非常容易，所以撰寫測試這件事也更容易了。所以不少 Node.js 的套件或者是 JavaScript 的 Library 後來都改以 CoffeeScript 去實作。