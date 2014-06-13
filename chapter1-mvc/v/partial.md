# 什麼是 partial

Partial簡單說就是程式碼中的一小段，通常使用在HTML中讓View的Code可以更乾淨，將重複使用到的區塊切成獨立的Partial，比方說頁首頁尾、表單、社群插件等等，讓任何一個頁面都可以讀取這段Partial而不用重複寫一次一模一樣的Code。

假設我們常常需要在頁面產生topics的列表，就可以考慮將列表包裝成partial，這樣每個頁面需要時只要render這個partial就可以了。

_topic_list.html.erb
```erb
<ul>
<% @topics.each do |topic| %>
  <li># <%= topic.id %></li>
  <li>Topic Name: <%= link_to(topic.title, topic_path(topic)) %></li>
  <li>Description: <%= topic.content %></li>
<% end %>
</ul>
```
這樣頁面就會變得很簡單：

 index.html.erb
```erb
...
<%= render "topic_list" %>
...
```
