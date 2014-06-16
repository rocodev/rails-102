# Nested form

Nested form 可以將有關聯的 model attribute 放在同一個 form 裡面一起建立或更新。


例如這次的實作是一個商品有很多種規格，我希望在新增商品的時候就可以同時新增完規格（ product has_many specs ），Controller相關的設定解說可以參考 [Strong Parameters](../c/strong_parameters.md) 章節的相關解說。

Model如下：
```ruby
class Product < ActiveRecord::Base
  has_many :specs, :dependent => :destroy
  accepts_nested_attributes_for :specs
```

```ruby
class Spec < ActiveRecord::Base
  belongs_to :product
end
```

如此一來後端的設定就算是OK了，接下來是前端form的部分，在此用simple_form作為例子，rails guide內也有原生form的教學可以 [參考此連結](http://guides.rubyonrails.org/form_helpers.html#nested-forms)

如果是用 simple_form 就是使用 `simple_field_for` 的這個helper即可

view/admin/products/_form.html.erb
```erb
<%= simple_form_for [:admin, @product] do |f|  %>
  <%= f.input :name, :required => true %>
  <%= f.input :description, :required => true %>
  <%= f.input :price %>

  <!-- nested form從這裡開始 -->
  <%= f.simple_fields_for :specs do |spec| %>
    <%= spec.input :name %> <!-- spec的name欄位 -->
    <%= spec.input :detail %> <!-- spec的detail欄位 -->
  <% end %>
  <!-- nested form結束 -->

  <%= f.button :submit, "Submit", :disable_with => "Submiting..." %>
<% end %>
```

這樣就完成了最簡單的nested form了。


