# form

Form表單是給使用者輸入資料的地方，預設是使用post方法送出資料，再由rails決定是新增或是修改。

Rails內最常見的表單helper就是`form_for`，可以幫我們針對特定model以及model內的欄位送出資料
```erb
<%= form_for @topic do |f| %>
	<%= f.label :name %>
	<%= f.text_field :name %>
	<%= f.submit %>
<% end %>
```
其中如label、text_field和submit也是form的helper，幫助產生對應的html tag。

