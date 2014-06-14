# RESTful on Rails

## RESTful

Representational State Transfer，簡稱 REST。是 Roy Fielding 博士在2000年他的博士論文中提出來的一種軟體架構風格。目前是一種相當風行的 Web Services 實現手法，因為 REST 風格的 Web Services 遠比傳統的 SOAP 與 XML-RPC 來的簡潔。在近年，幾乎所有各大主流網站的 API 都已採用此種風格進行設計。

### What is REST?

REST 提出了一些設計概念和準則：

1. 網路上的所有事物都被將被抽象成資源 (resource)
2. 每個資源對應一個唯一的 resource identifier
3. 通過通用的介面 (generic connector interface) 對資源進行操作
4. 對資源的各種操作不會改變 resource idetifier
5. 所有的操作都是無態 (stateless) 的

對照到 web services 上來說：

* resource indentifier 是 URI
* generic connector interface 是 HTTP

### RESTful Web Services

RESTful Web Services 是使用 HTTP 並遵循 REST 設計原則的 Web Services。它從以下三個方面資源進行定義：

* URI，比如：http://example.com/resources/。
* Web Services accept 與 return 的 media type，如：JSON，XML ，YAML 等。
* Web Services 在該 resources 所支援的一系列 request methid : 如：POST，GET，PUT 或 DELETE。

以下列出在實現 RESTful Web 服務時HTTP請求方法的典型用途。

#### GET

|資源                | GET       |
|-------------------|-----------|
|一組資源的URI，比如http://example.com/resources/    | 使用給定的一組資源替換當前整組資源。|
|單個資源的URI，比如http://example.com/resources/142 | 獲取 指定的資源的詳細信息，格式可以自選一個合適的 media type（如：XML、JSON等）|

#### PUT

|資源                |  PUT|
|-------------------|-----------|
|一組資源的URI，比如http://example.com/resources/    | 列出 URI，以及該資源組中每個資源的詳細信息（後者可選）。|
|單個資源的URI，比如http://example.com/resources/142 | 替換/創建 指定的資源。並將其追加到相應的資源組中。|

#### POST

|資源                | POST|
|-------------------|-----------|
|一組資源的URI，比如http://example.com/resources/    | 在本組資源中創建/追加一個新的資源。 該操作往往返回新資源的URL。|
|單個資源的URI，比如http://example.com/resources/142 | 把指定的資源當做一個資源組，並在其下創建/追加一個新的元素，使其隸屬於當前資源。|

{::pagebreak :/}

#### DELETE

|資源                |  DELETE|
|-------------------|-----------|
|一組資源的URI，比如http://example.com/resources/    | 刪除 整組資源。|
|單個資源的URI，比如http://example.com/resources/142 | 刪除 指定的元素。|


### 制約即解放

DHH 在 [Discovering a world of Resources on Rails](http://www.slideshare.net/vishnu/discovering-a-world-of-resources-on-rails) 提到一個核心概念：Constraints are liberating 。

很多剛踏入 Rails 這個生態圈的開發者，對於 REST 總有股強烈的反抗心態，認為 REST 是一個討厭的限制。但事實上，DHH 卻認為引入 REST 的制約卻反為 Rais 開發帶來了更大的解放，而這也是他引入這個設計的初衷。

#### 維護性：解決了程式碼上的風格不一

在傳統的開發方式中，對於有效組織網頁應用中的程式碼，大家並沒有什麼共識。所以很可能在專案中會出現這種風格不一致的程式碼：

``` ruby
def add_friend
end

def remove_friend
end

def create_post
end

def delete_post
end

```
透過 REST 的包裝（對於 resource 的操作），可以變得更簡潔直觀，且具有統一的寫法。

``` ruby
class FriendShipController
   def create
   end

   def destroy
   end
end

class PostController
  def create
  end

  def destroy
  end
end

```

### 介面統一：Action as Resource

大眾最常對 REST 產生的一個誤解，就是以為 resource 只有指的是 data。其實 resource 指的是：data + representation (表現形式，如 html, xml, json 等)。

在網頁開發中，網站所需要的表現格式，不只有 HTML 而已，有時候也需要提供 json 或者 xml。Rails 透過 responder 實現了

在 Resource Oriented Architecture (ROA，一組 REST 架構實現 guideline) 中有一條： 「A resource can use file extension in the URI, instead of Content-Type negotiation 」。

Rails 透過 responder 的設計，讓一個 action 可以以 file extension ( .json, .xml, .csv ...etc.) 的形式，提供不同類型的 representation。

``` ruby
class PostsController < ApplicationController
  # GET /posts
  # GET /posts.xml
  def index
    @posts = Post.all

    respond_to do |format|
      format.html # index.html.erb
      format.xml  { render :xml => @posts }
    end
  end

```



### 開發速度：透過 CRUD 七個 action + HTTP 四個 verb + 表單 Helper 與 URL Helper 達到高速開發

REST 之所以能簡化開發，是因為其所引入的架構約束。Rails 中的 REST implementation 將 controller 的 method 限制在七個：

* index
* show
* new
* edit
* create
* update
* destroy

實際上就是整個 CRUD。而在實務上，web services 的需要的操作行為，其實也不脫這七種。Rails 透過 HTTP 作為 generic connector interface，使用 HTTP 的四種 verb ： GET、POST、PUT、DELETE 對資源進行操作。


#### GET

``` ruby
<%= link_to("List", posts_path) %>
<%= link_to("Show", post_path(post)) %>
<%= link_to("New", new_post_path) %>
<%= link_to("Edit", edit_post_path(post)) %>
```

#### POST
``` ruby
  <%= form_for @post , :url => posts_path , :html => {:method => :post} do |f| %>
```

#### PUT
``` ruby
  <%= form_for @post , :url => post_path(@post) , :html => {:method => :put} do |f| %>
```

#### Destroy
``` ruby
  <%= link_to("Destroy", post_path(@post), :method => :delete )
```

{::pagebreak :/}

#### Form 綁定 Model Attribute 的設計

Rails 的表單欄位，是對應 Model Attribute 的：

``` ruby
<h1>New post</h1>

<%= form_for @post , :url => posts_path do |f| %>
    <%= f.error_messages %>
    <div><label>subject</label><%= f.text_field :subject %></div>
    <div><label>content</label><%= f.text_area :content %> </div>
    <%= f.submit "Submit", :disable_with => 'Submiting...' %>
<% end -%>


<%= link_to 'Back', posts_path %>
```

透過 form_for 傳送出來的表單，會被壓縮包裝成一個 parameter: params[:post]，

``` ruby
def create
  @post = Post.new(params[:post])
  if @post.save
    flash[:notice] = 'Post was successfully created.'
    redirect_to post_path(@post)
  else
    render :action => "new"
  end
end
```

如此一來，原本創造新資源的一連串繁複動作就可以大幅的被簡化，開發速度達到令人驚艷的地步。




