# ids

collection_singular_ids是當我們做has_many時產生的method。

假設我們有`Drink`和`Material`兩個many-to-many的model
並希望使用者在新增Drink的時候可以同時選取Material做關聯


這時候的做法就是讓被選取的materials的id存成array，經由`params[:material_ids]`傳給drink controller
rails就會根據`material_ids`幫我們建立關聯。


補充：

記得要在`drink_controller.rb`的strong params內加上`material_ids: []`
使用simple_form時只要下`f.association`就可以了

```erb
<%=  simple_form_for @drink do |f| %>
  <%= f.association :materials, :as => :check_boxes %><br>
  <%= f.submit "Submit" %>
<% end %>
```

## 參考資料


* http://railscasts.com/episodes/17-habtm-checkboxes
* http://guides.rubyonrails.org/association_basics.html#has-many-association-reference

