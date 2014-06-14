# Compass


## Sass : extend / mixin / import

在 Sass 一章，我們只提到了一些基礎的部分。更強大的其實是這些功能

* extend
* mixin
* include


### extend

extend 可以讓你將某些已經寫好的樣式，直接套入另外一組樣式中重複使用。

``` css
   .warning{
      border: 1px;
      color: red;
   }
   .serious-warning{
       border: 1px;
       color: red;
       font-weight: bold;
   }
```   
而使用 extend，只需這樣寫，就可生成上述 CSS 了：

``` scss
   .warning{
      border: 1px;
      color: red;
   }
   .serious-warning{
       @extend .warning;
       font-weight: bold;
   }
```

### mixin

可以預先寫好自定要被 mixin 的 function ，需要用時 include 進來

``` scss
 @mixin rounded-top {
   $side: top;
   $radius: 10px;
   border-#{$side}-radius: $radius;
   -moz-border-radius-#{$side}: $radius;
   -webkit-border-#{$side}-radius: $radius;
 }
```
要用時 include 進來

``` scss
   #navbar li { @include rounded-top; }
   #footer { @include rounded-top; }
```

### import

可以把太長的 SCSS 拆開成一個一個的 partial，要用時 import 進來。

`style.scss`

``` scss

   //需要被 import 的檔案必須以 _開頭命名，如 _rounded.scss
   @import "rounded";
```


有了 extend / mixin / import，加上 variable，加上支援部分 Ruby syntax。

聰明的你，應該想到這些元素集合起來可以作什麼？

沒錯，就是造 CSS Framework！

## Compass = Sass framework powered by community

Sass 提供了一堆基本武器可以讓許多開發者造出自己的最佳實踐，再讓其他人可以重複利用。而 Compass 就是這些實踐產物的集合體。

Compass 自己的 core 充滿了 killer features，比如說：

### CSS3 helpers 

http://compass-style.org/reference/compass/css3/

撰寫漸層色與圓角框不再是令人頭大的難事。

### 漸層色 Background Gradients 

http://compass-style.org/examples/compass/css3/gradient/


### 圓角框 Border radius: 

http://compass-style.org/examples/compass/css3/border_radius/

### CSS Pie

CSS3 Pie : http://compass-style.org/reference/compass/css3/pie/


### 不費吹灰之力實作 CSS Sprites

記得我們在 Asset Pipeline 中提到的 CSS Sprites 技巧嗎？它原是 Minimize HTTP Requests 中的一招，實作方式是將 CSS 中的小圖合併成較大的一張，再透過 CSS 定位的方式呼叫。比如說這個 CSS 中原先需要用到十張小圖，合併到只剩一張，就變得非常節省 HTTP requests（ 因為光是發出 requests 也相當耗時）。

問題是，負責 Scaling 的 server guy 很喜歡這招，但網頁設計師卻對這件事相當感冒。因為太麻煩了。試想，url(‘xxx.gif’) 到處貼多方便呀，誰喜歡合併成一張，然後仔細精算定位？後續維護又怎麼辦呢？

Well，Compass 幫你「自動解決了問題」！http://compass-style.org/help/tutorials/spriting/

你可以把原先所有要用的小圖，通通丟進同一個資料夾。讓 Compass 幫你自動合併並算出位置！

``` scss
@import "icon/*.png";
@include all-icon-sprites;
```

Compass 會幫你自動合併並算出位置：

``` scss
.icon-sprite,
.icon-delete,
.icon-edit,
.icon-new,
.icon-save   { background: url('/images/icon-s34fe0604ab.png') no-repeat; }
.icon-delete { background-position: 0 0; }
.icon-edit   { background-position: 0 -32px; }
.icon-new    { background-position: 0 -64px; }
.icon-save   { background-position: 0 -96px; }

```

毛骨悚然的強大呀！
