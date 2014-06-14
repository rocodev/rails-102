# 什麼是 partial

Partial 簡單說就是程式碼中的一小段，通常使用在 HTML 中讓 View的Code 可以更乾淨，將重複使用到的區塊切成獨立的 Partial，比方說頁首頁尾、表單、社群插件等等，讓任何一個頁面都可以讀取這段Partial而不用重複寫一次一模一樣的Code。

## 使用情境

什麼時候應該將把程式碼搬到 Partial 呢？

＊long template | 如果當檔 HTML 超過兩頁
＊highly duplicated | HTML 內容高度重複
＊independent blocks | 可獨立作為功能區塊

## 使用範例

假設我們常常需要在頁面產生 topics 的列表，就可以考慮將列表包裝成 partial，這樣每個頁面需要時只要 render 這個 partial 就可以了。

`_topic_list.html.erb`

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

`index.html.erb`

```erb
...
<%= render "topic_list" %>
...
```
