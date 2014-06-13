# View

##什麼是View

View基本上就是負責處理視覺呈現的地方，在rails的開發中view就是負責放html碼的地方，也就是前端呈現。

##什麼東西應該放在View

原則上View只應該出現跟前端呈現有關的東西，儘量不要把判斷以及邏輯相關的code放在View，例如以下的例子就是不好的做法：
```erb
<% if current_user %>
	<p><%= current_user.name %></p>
<% else %>
	<p>Not Logined</p>
<% end %>
```
這個例子中在view判斷使用者是否登入，且還對使用者讀取name的欄位
比較好的做法是將`if else`改寫在partial中，並把`current_user.name`用helper包起來。這樣html code的好讀性就可以大大提升。

請參考本章詳細介紹。

