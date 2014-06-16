# helper_method 與 view_context

## helper_method
在 controller 裡面的 method 不能在 view 裡面用。

也就是在
```ruby
class ProductsController
  def find_cart
    @cart = Cart.find(session[:cart_id])
  end
end
```
View 裡面不能用
```ruby
<%= find_cart.items %>
```
拉這個 cart 出來直接用。

如果你要在 controller 和 view 都能拉現在的購物車，必須要用 helper_method 宣告這是一個 controller 級的 helper。
```ruby
class ApplicationController
  helper_method :current_cart
  def current_cart
    cart = Cart.find(session[:cart_id])
    return cart
  end
end
```
這樣你就能在 View 裡面用 current_cart。
```ruby
<%= find_cart.items %>
```
或者是 Controller 裡面也能用 current_cart。
```ruby
class ProductsController
  def add_to_cart
    current_cart.items << @product
  end
end
```

##view_context
在 helper 裡面的 method 不能在 controller 裡面用。
也就是在
```ruby
class ProductsController
  def show
    @page_description = truncate(@product.desc, :lenght => 50 )
  end
end
```
是不會動的。

如果要在 controller 裡面取用系統內建的 Rails View Helper，或自定義的 View Helper。
必須要用 view_context 去調用。
```ruby
class ProductsController
  def show
    @page_description =  view_context.truncate(@product.desc, :lenght => 50 )
  end
end
```
##小結
但基本上還是建議在 View Helper 與 Controller 的 code 不要互相混來呼叫來呼叫去。讓 View 歸 View，Controller 歸 Controller。若真有業務上的需求需要「到處都可以用」。建議寫 Module 掛在 lib 用 mixin 技巧混入。

