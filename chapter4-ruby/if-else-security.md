# if / else 的 Fail Close 安全觀念


在撰寫安全性程式碼時，使用 if 和 unless，也會產生截然不同的差別。在 Security on Rails 中有介紹 Fail open 與 Fail close 兩種觀念：

### "Fail open" way, it’s bad

``` ruby
def show
  @invoice = Invoice.find(params[:id])
  unless @user.validate_code( @invoice.code )
    redirect_to :action => 'not_authorized'
  end
end
```

### "Fail close" way

``` ruby
def show
  @invoice = Invoice.find(params[:id])
  if @user.validate_code( @invoice.code )
    redirect_to :action => 'authorized
  else
    redirect_to :action => 'not_authorized'
   end
end
```

使用 Fail open：「條件不成功，才不允許，不然就允許。」出包的機率遠比 Fail close：「如果條件成功，才允許進行，不然就不允許。」高的許多，這也是值得注意的地方。
