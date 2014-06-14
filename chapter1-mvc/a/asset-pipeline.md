# Asset Pipeline
Asset Pipeline 是一套讓開發者很方便能夠削減 (minify) 以及 壓縮 (compress) Javascript / CSS 檔案的框架。它同時也提供你直接利用其他語言如 CoffeeScript / SASS / ERB ，直接撰寫這些 assets 的可能性。

(assets 指的是 stylesheets / javascripts / images 這些靜態檔案。)

## 提升前端速度的優勢

一般在做前端提速時，我們通常會依據 Yahoo 提供的 [Best Practices for Speeding Up Your Web Site](http://developer.yahoo.com/performance/rules.html) 這篇文章提及的一些技巧對網站優化，諸如：

* Minimize HTTP Requests
* Use a CDN
* Split Components Across Domains
* Gzip Components
* Minify JavaScript and CSS
* CSS Sprites

在很久之前的版本，能夠使用 Rails 內建機制達成的只有這三項：

### Minimize HTTP Requests

``` erb
<%= stylesheets_include_tag "aaa", "bbb", :cache => true %>
<%= javascrupt_link_tag "ccc", "ddd", :cache => "customized-functions" %>

```

將數支檔案打包成一支，降低 HTTP requests。

### Use a CDN + Split Components Across Domains

`config/enviroments/production.rb`

```
 config.asset_host = "cdn%d.example.org"
```

使網站的靜態檔案從以下網址

* http://cdn0.example.org
* http://cdn1.example.org
* http://cdn2.example.org
* http://cdn3.example.org

平均動態提供，達到網頁高速載入的效果。


## 滿足實戰需求

但雖然已內建這些機制，但是對於一般有較大吞吐量的網站，還是不敷使用。

### 不只打包，更需壓縮

現在的網站設計師，多半會使用一些現成的 CSS 框架，如 [Bootstrap](http://getbootstrap.com/) 來做快速 prototyping。而網站逐漸擴充功能，一個網站的靜態檔案數量與所佔容量也會隨著水漲船高。有時候光 CSS 與 JavaScript 的檔案，加起來就足足有 1MB 以上的 size。

Rails 原先內建的功能，充其量只有將這些檔案「打包」，並沒有將檔案「壓縮」的作用。

若要談加速下載，唯有進行「壓縮」(trim / uglify / gzip) 才能達到真正減肥提升速度的目標。

字面上的「壓縮」其實還分幾種作法:

* 把不要的空白 / 不必要的注釋 去掉 (trim)
* 把檔案的變數以單個字母取代 ( uglify )
* 將檔案壓成 gz

### 滿足主流 CDN invalid cache 需求

舊有的 Rails asset 是採用 query string 的方式，來達到 invalid browser cache 的作用。如：

```erb
 <%= image_tag("example.gif") %>
```

會生成

``` html
<img src="/example.gif?1234567" />

```

query string 數字的演算法，是根據該 assets 更新的時間去定義。這樣每次 deploy 網站時，可以保證： assets 只要被更動過，query string 都會不一樣，而 browser 就將之視為不同的 URI，重新下載。

不過相當不幸運的，不是每一家 CDN 都支援 query string。

再者，stylesheets 內的 images，並不在 query string 的守備範圍內，也就是如果開發者使用了

``` css
background: url("logo-bg.gif");
```

當替換了 CSS 內的背景圖原始圖檔，或者是 CDN 不支援 query string。通常每 deploy 一次，你就必須上 CDN panel 去手動 invalid assets，並沒有辦法讓使用者的 browser 自動清除。


## Fast by Default

這些都是相當難處理的問題。因此 Rails 在版本 3.1 後開發了 Asset Pipeline 架構來自動解決這些實際會發生的問題：

* 壓縮提速
* Fingerprinting Assets 

並且倡導使用先進的 Asset 語言和框架，如 SCSS / Compass / CoffeeScript 結合 Rails 做更有效率的開發。




