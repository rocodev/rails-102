# 不應該放在 view 裡的東西

### 邏輯判斷

```erb
<% if topic.present? %>
	<%= @topic.title %>
<% else %>
	Unknown
<% end %>
```

ruby block
```ruby
<% @topics.each do |topic| %>
	#content
<% end %>
```

### 撈 Model資料的code

```erb
<%= Topic.find(params[:id]).title %>
```


