# 常見 Helper

Rails 最令其他 Ruby Web Framework 羨慕的就是內建的很多方便 Helper。舉幾個省下很多重造輪子功夫的 Helper ：

#### simple_format

可以處理使用者的內容中 \r\n 自動轉 br 和 p 的工作

#### auto_link

可以處理使用者的內容中若有連結就自動 link 的工作。（ Rails 4 已移除內建）

#### truncate

使用者輸入的內容若過長可以指定多少字後就自動砍掉並加入 “....” 

#### html_escape

使用者輸入的內容若有 html tag為了怕使用者輸入惡意 tag 進行 hack。會進行自動過濾。

(Rails 3 之前要手動加 h 過濾，在 3.0.0+ 後預設 escap，不想被 escape 可以用 `raw` unescape)

這些東西若自己寫 parser 處理不知道要花費多少精力還不一定濾的徹底。卻都是 Rails 預設內建 Helper。

## 基礎建設 Helper

Rails 內建的某些 Helper 是為了與其他更棒的基礎建設整合：

### stylesheet_link_tag 與 image_tag

有些開發者覺得，這東西還要用 Helper 嗎？直接貼 HTML 不是也一樣會動嗎? 有什麼差別。差別可大了。

``` rthml
<%= stylesheet_link_tag "abc","def",:cache => true %>
```

這一個 Helper可以在 production 環境時自動幫你將兩支 CSS 自動壓縮成 一支 applicatiion.css。直接實現了 Yahoo Best Practices for Speeding Up Your Web Site中minify HTTP reqesut 的建議。而在 Rails 3.1 之後甚至還會自動幫你 trim 與 gzip。

完全不需要去在 deploy process 中 hook 另外的 compressor 就可以達到。

### image_tag

至於 image_tag 有什麼特別的地方?

``` rhtml
<%= image_tag("xxx.jpg") %>
```

Rails 可以幫忙在 asset 自動在後面上 query string。若網站有整合 CDN 架構時，以自動處理 invalid cache 的問題。而 Rails 也有選項可以實作 asset parallel download 的機制，一旦打開，站上 的 asset 也會配合設定，亂數吐不同來源的 asset host 實做平行下載。

輕鬆就可以把網站 Scale 上去。


### form_for

form_for 也是 Rails 相當為人稱讚的一個利器。Rails 的表單欄位是綁 model(db 欄位)。（解決資料庫映射問題)

開發方便( `Post.new(params[:post]` 直接收參數做 mapping)之外，也內建了防 CSRF (protect_from_forgery)的防禦措施。

