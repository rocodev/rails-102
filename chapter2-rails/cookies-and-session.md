# Cookies & Session


## Cookies

看演唱會或是去遊樂園玩常常會發生一種情況，就是入場以後要暫時出場，這時候工作人員通常會給你蓋個手章，用來註記你曾經入場過，基本上 Cookies 的功用就是這個手章，只要使用者進到我們的網站，我們就幫他儲存一個 Cookies ，下次當使用者再度造訪時我們就可以由 Cookies 得知使用者的資訊。

有些遊樂園的手章上會標記當天的入園時間，以免有人回家不洗澡隔天又來玩一次，而 cookies 記錄這個時間的方法就是以 key/value 的形式儲存在使用者的瀏覽器中，例如：
```
{"login_time": "1990/2/1"}
```
但 Cookies 屬於沒有加密的公開檔案，所以不建議儲存敏感資料。

## Session

 相較於 Cookies 存在 Client 端， Session 則是存在 Server 的資料，通常與 Cookies 相呼應。

 當使用者造訪我們的網站時，我們由伺服器產生 session id (32 byte long MD5 hash value)，並傳送存有這個 session id 的 cookie 給瀏覽器儲存，之後使用者造訪我們網站時，只需要比對 cookies 上的 session id 和 session 裡的 session id 就可以知道使用者身份，大部份的網站也是運用此原理實作儲存 User 登入狀態的機制。

 這樣做的好處是若有人劫取到使用者的 Cookies 資料也無法得知資料內容，但是仍有 Hijacking 攻擊的疑慮，可以參考 Rails Guide 的 [Security章節](http://guides.rubyonrails.org/security.html)。

## Rails session

在 rails 中只要使用`session[:session_name]` 的 instance method 就可以在 controller 拿取 Session 的資料，例如以下的購物車功能：
```ruby
class ApplicationController < ActionController::Base
  def find_cart
    @cart = Cart.find_by(id: session[:cart_id])
  end
end
```
同理我們也可以將資料儲存或刪除 Session：
```ruby
class ApplicationController < ActionController::Base
  def store_cart
    session[:cart_id] = cart.id
  end
  def reset_cart
    session.delete(:cart_id)
  end
end
```



## 延伸閱讀-Authenticity Token

所謂的 `authenticity_token` 就是一串隨機生成的 string ，在我們建立 rails 的表單時， rails 將會隨機生成一個 `authenticity_token` 存在 session 中，並且在表單的 hidden field 中也加入一樣的 `authenticity_token` ，當我們送出表單（post request）時， rails 會驗證表單的 `authenticity_token` 和 session 中的 `authenticity_token` 是否一樣，一樣才可以成功送出。
 
這樣做的好處是可以避免所謂的跨站請求偽造 (Cross-site Request Forgery) ，又稱 ＣＳＲＦ。
 ＣＳＲＦ 攻擊的原理是偽造一個 form 送 post 給伺服器，所以很有可能發生的情況是你在Ａ網站有登入使用者，但是在Ｂ網站點了帶有 ＣＳＲＦ code的連結，內容是要重新設定Ａ網站的使用者密碼為 12345678，此時Ａ網站以為是你自己送出的請求，那麼你的密碼就被換掉了。
 
而 rails 加上了 `authenticity_token` 這樣的機制就是為了阻擋ＣＳＲＦ，因為Ｂ網站不會知道你的 `authenticity_token` 是什麼，送出的 post request 就會被擋下來。在 rails 中預設會檢查 POST, PUT, DELETE requests 的 authenticity_token。
 

參考資料：
* http://guides.rubyonrails.org/security.html#sessions
* http://guides.rubyonrails.org/action_controller_overview.html#session
* http://andikan.github.io/blog/2012/10/03/cookie-and-session/
* http://stackoverflow.com/questions/941594/understand-rails-authenticity-token