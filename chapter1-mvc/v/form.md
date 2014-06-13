# form

Form 表單是給使用者輸入資料的地方，預設是使用 `POST` 方法送出資料，再由 Rails 決定是新增或是修改。

Rails內最常見的表單 helper 就是`form_for`，可以幫我們針對特定model以及model內的欄位送出資料。

```erb
<%= form_for @topic do |f| %>
	<%= f.label :name %>
	<%= f.text_field :name %>
	<%= f.submit %>
<% end %>
```

其中如`label`、`text_field`和`submit`也是 form 的 helper，幫助產生對應的 HTML tag。

