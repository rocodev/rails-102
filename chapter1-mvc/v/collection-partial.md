# 什麼是 collection partial

正常的 Partial 只會將內容 render出來一次，collection partial 則會自動 count 我們給予的物件，並render count的次數，可以省去在 partial 內再寫 block 或 helper的繁瑣，讓 partial 更簡潔。

延續[上一題](partial.md)的例子，我們可以改寫成：

`_topic_list.html.erb
`
```erb
<li># <%= topic.id %></li>
<li>Topic Name: <%= link_to(topic.title, topic_path(topic)) %></li>
<li>Description: <%= topic.content %></li>
```
然後這樣render：

`index.html.erb`

```erb
...
<ul><%= render :partial => "topic_list", :collection => @topics, :as => :topic %></ul>
...
```
如此一來就不用在view裡面包block了。


