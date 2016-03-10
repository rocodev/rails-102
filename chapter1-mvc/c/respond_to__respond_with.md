# respond_to 與 respond_with

respond_to可以用來回應不同的資料格式，如果使用者要get www.example.com/ex.xml，rails會先尋找`ex.xml.erb`和`ex.xml.builder`，最後會找`ex.html.erb`的檔案。

```ruby
def index
    @topics = Topic.all
    respond_to do |format|
        format.html
        format.xml { render :xml => @topics }
        format.json { render :json => @topics }
    end
end
```

respond_with則是rails3之後才有的做法，可以先告知controller respond_to支援哪幾種檔案形態，如此一來在action內只要寫respond_with就可以了，因此可將上方的例子寫成下面的樣子：

```ruby
respond_to :html, :xml, :json
def index
    @topics = Topic.all
    respond_with(@topics)
end
```

respond_with也可以寫成block，並在block內重新定義預設的render行為：
```ruby
respond_to :html, :xml, :json
def index
    @topics = Topic.all
    respond_with(@topics) do |format|
    	format.html { redirect_to root_path }
    end
end
```

