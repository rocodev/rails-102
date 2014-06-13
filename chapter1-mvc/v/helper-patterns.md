# Helper Patterns


Helper 是以 module 的形態存在的，在 Rails內 負責寫 View 要用到的method。

所以設計時能夠保持「簡單」且「可重複使用」是最重要的。

通常我們要使用 Helper 的時機是 View 有太多髒亂的code的時候，所以有時候會想把所有的髒 code 都寫進同一個 helper method裡面，這是不對的。

比較好的做法是應該把這些髒 code 拆成很多不同的小部分，再針對不同的部分判斷是要放在 partial 還是 helper。

我們也可以在 partial 內搭配 helper，這也是讓 view 變乾淨的好方法。

由於要讓 helper 保持「簡單」且「可重副使用」，在設計 helper 時應該讓h elper只「做一件事情」。（例如:判斷是否能編輯文章、回傳文章的連結按鈕）

這樣做的好處是這個 helper就會變得重複使用性很高（畢竟很多地方都需要判斷是否能編輯文章），就不會變成為了某個特定的 view 寫了一個 helper 卻只能用到一次，落實 Don't Repeat Yourself 的 Rails精神。

以下一些常見的 helper 設計方法舉例：

#### 1.儘量避免太多html code（無論ruby的或純html）

#### 2.View裡面有太多讓人難以理解的判斷時，裝在helper裡面並語意命名，讓view更能理解

```ruby
<% if current_user && current_user = @topic.user_id %>
	#show shomething
<% end %>
```

可以改成

```ruby
<% if editable?(current_user) %>
	#show shomething
<% end %>
```

推薦參考文章：

* http://blog.xdite.net/posts/2011/12/09/how-to-design-helpers
* http://blog.xdite.net/posts/2011/12/10/how-to-design-helpers-2
* http://blog.xdite.net/posts/2012/01/16/how-to-design-helper-3
