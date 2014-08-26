# Sass / SCSS

Asset Pipeline 提供了內建直接使用 Sass 撰寫 CSS 的功能。你也許會生出這樣的疑惑：什麼是 Sass？ Why should I care?

Sass (Syntactically Awesome Stylesheets) 原先是內建在 Haml 中的一個副功能。

## Haml

要談 Sass，就不得不先來談 Haml 這個 project。 Haml 全名為 HTML Abstract Markup Language，它是提供網頁設計師撰寫 HTML 的另外一條途徑。

透過 Haml，你可以很快的使用它的 syntax 寫出結構穩固的 HTML。

網頁設計師經常有一個煩惱：在撰寫 HTML 時要是忘記關一個 TAG，在瀏覽器中整個版面可能就會大爆炸，而這樣的 Bug 卻是很難被抓出來的。

Haml 主要就是讓開發者，能夠使用縮排的方式撰寫 HTML，輕鬆做到永不忘記關 Tag 的效果。以下是 Haml 範例：

``` haml
 %h1= "Hello World"
```

產生出來的 HTML 就會長這樣

``` html
 <h1>Hello World</h1>
```

而

``` haml
 %ul{:id => "list", :class => "menu"}
    %li= "Item 1"
    %li= "Item 2"
    %li= "Item 3"
```

會產生出來這樣的 HTML

``` html
 <ul id="list" class="menu">
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
  </ul>
```

### 使用 Haml 撰寫 HTML 的好處

Haml 是需要使用縮排撰寫，再行 compile 的 markup language。它可以讓你：

#### 阻絕撰寫出錯誤結構的 HTML TAG 的機會

只要 syntax 一錯誤，編譯就無法成功。利用這樣的特性，很容易阻絕寫出會在瀏覽器因為 TAG 結構錯誤而難以 debug 出的 HTML。

#### 輕鬆調整排版

在網頁設計開發階段，若要大幅調整 HTML 結構，對網頁設計師也是很傷腦筋的一件事。因為大幅的搬動 HTML，通常有時候會造成：「少剪到一個 TAG」或 「改了開頭 TAG ，卻忘了改關閉 TAG 」的憾事。

在 Haml 中，這些狀況都不會發生。因為 Haml 本身就屬於「塊狀結構」、「自我 close」。因此不論怎樣搬動和調整，只要符合縮排，幾乎都不會爆炸。

#### 使用 Haml 撰寫 HTML 的壞處

如此 powerful 的 markup language 為何沒有風行？反倒是原先屬於副功能的 Sass 大紅特紅。原因就在於 Haml 的特性：不只需要被機器 compile，它也需要被人腦 compile。

HTML 本身就是一門相當直觀的 markup language。在撰寫 Haml 時，排版雖然相當輕鬆。但接手維護 Haml 版面的人，卻通常痛苦不堪。因為「非常不直觀」。

這也是 Haml 的反對者，批評最力的地方。

多數人無法接受維護不直觀的「任何東西」，加上撰寫 Haml 需要另外學習特殊的 syntax。沒有壓倒性的好處，一般人是不會貿然進行技術投資的。這也是為什麼 Haml 始終處是小眾技術的主要原因。


## Sass / SCSS

拉回來談 Sass，Sass 原先是附屬在 Haml 裡面的一個副功能。這也是 sass-convert 這個指令必須要安裝 haml 這個 gem 才能使用的原因。

Sass 的原理，是讓開發者可以透過「縮排」的方式去撰寫維護 CSS，同樣可以避免忘記關 TAG 而大爆炸的糗事。

而因為 CSS 的結構特性，造成了 Sass 與 Haml 截然不同的命運。多數人反對 Haml，是因為 Haml 反而造成了 HTML 在閱讀上的不直觀。

而 Sass 的語法

``` sass
  .content
    margin: 2em 0
    h1
      font-size: 2em
```

產生出

``` css
   .content{
    margin: 2em 0;
   }
   .content h1{
      font-size: 2em;
   }
```

反倒讓 CSS 的維護變得直觀了。接觸 Sass / SCSS 後的不少開發者甚至認為，縮排 block 的撰寫方式才是 CSS 在被發明時應該被設計出來的樣子。

現在撰寫 CSS 的方式，有一個絕大缺點：只要在結構上涉及巢狀或多個 class，維護者就必須複製貼上 style。不少人認為這真是愚蠢至極且煩人透頂的設計。

### 其他便利功能

Sass 也提供了其他便利功能，如變數、函數、數學、繼承、mixin …等等功能。

在進行網頁 protyping 時，更改全站配色或者是直接提供兩個以上的設計，對設計師來說是家常便飯的事。

但更改全站配色卻是相當麻煩的一件事，因為「尋找 + 全數取代」，並不能保證最後會有正確的結果。很有可能：你更改了所有 CSS 中涉及連結的顏色，卻發現在全數取代的過程中，不小心也改到邊框的顏色。

若能使用變數去指定特定 style 的顏色，該有多好。

#### 變數 ( Variables )

``` sass
   $border-color: #3bbfce
   $link-color: #3bbfcf
   .content
      border-color: $border-color
      a
        color: $link-color
```

生成

``` css
   .content{ border-color: #3bbfce; }
   .content a{color: #3bbfcf; }
```

#### 數學

在調整區塊寬度時，你也希望：每次調整寬度時，可不可以不要每次都按計算機，再全數手動修改…

``` sass
   .content
      width: (500px/2);
```

生成

``` css
   .content { width: 250px; }
```

#### 內建函式

在調整顏色亮度時，你希望可否無需再開調色盤，直接改 CSS 就讓 style 暗一點？

``` sass
   $color = darken(#800, 20%)
   .content
      background-color: $color
```

生成

``` css
   .content{ background-color: #200; }
```

這都還只是 Sass 所提供的當中一小部分基礎功能而已，卻足以讓網頁設計師驚艷十足了。加上撰寫維護時十分直觀，這也難怪為何 Sass 只是 Haml 中的副功能，後繼的聲勢浪頭卻遠高於 Haml 本身。

## SCSS

那 SCSS 又與 Sass 有什麼差別，他們看起來好像是類似的東西？

是這樣的，Sass 原先使用的縮排，對於網頁設計師來說，還是相當不直觀。而且實務上也不能直接將舊有的 CSS 直接貼進 Sass 中。其實還是存在一定的不方便度。也因此 Sass 進行了進化，改良了 syntax，而 Sass 3 後來就被稱為 SCSS ( Sassy CSS)。

它的 syntax 與 CSS 原有的 syntax 完全 compatible，使用了 { } 去取代原先的縮排方式。

比如說原有的

``` sass
  .content
    margin: 2em 0
    h1
      font-size: 2em
```
在 SCSS 中變成了

``` scss
  .content{
    margin: 2em 0;
    h1 {font-size: 2em }
  }

```
在撰寫上，更加無比的直觀，同時也能將舊有的 CSS 直接貼進去，完全沒問題！SCSS 更新增了不少關於 CSS3 的 feature 函式。

就拿我最愛的背景漸變色來說好了，原先要做漸變色，CSS 必須要這樣寫：

``` scss
 #linear-gradient {
   background-image: -webkit-gradient(linear, 0% 0%, 100% 100%, color-stop(0%, #ffffff), color-stop(100%, #dddddd));
   background-image: -webkit-linear-gradient(left top, #ffffff, #dddddd);
   background-image: -moz-linear-gradient(left top, #ffffff, #dddddd);
   background-image: -o-linear-gradient(left top, #ffffff, #dddddd);
   background-image: -ms-linear-gradient(left top, #ffffff, #dddddd);
   background-image: linear-gradient(left top, #ffffff, #dddddd);
 }

```
因為你必須支援所有的 Browser。

但在 SCSS 中，一行就搞定了！

``` scss
 #linear-gradient { @include background-image(linear-gradient(left top, white, #dddddd)); }
```
