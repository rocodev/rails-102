# render options

Rails 接受以下四種 render options：

### :content_type

Rails預設會找 `text/html`類型的檔案（除非我們有下`:json`或`:xml`的選項）。

但我們也可以藉由`:content_type`設定其他的檔案形態，例如：
```ruby
render file: filename, content_type: "application/rss"
```

註記：content_type 類型可 Google `MIME搜尋`

#### Rails官方對content_type的說明

>By default, Rails will serve the results of a rendering operation with the MIME content-type of text/html (or application/json if you use the :json option, or application/xml for the :xml option.). There are times when you might like to change this, and you can do so by setting the :content_type option

### :layout

文章上方已解釋過，可參考[render :layout](render-layout.md)的部分

### :location

location header是HTTP通訊協定回應時幫client重新定位的方法，當client丟一個request到server，我們可以丟回location這個header將client導到別的地方，舉例：

```ruby
render xml: photo, location: photo_url(photo)
```

這段code的意思是告訴 client 端說 photo 的 xml檔要從`photo_url(photo)`這邊拿，所以假設我們有個 ajax script要來拿這個檔案，它就會跑到`photo_url(photo)`拿。

### :status

指定server要丟什麼樣的http request status給client

```ruby
# 以下兩種寫法都可以
render status: 500
render status: :forbidden
```

## 參考資源

* Rails Guides 內有一份[status列表](http://guides.rubyonrails.org/layouts_and_rendering.html#the-status-option)




