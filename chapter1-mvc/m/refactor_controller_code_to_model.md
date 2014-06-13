# Refactor controller code to model


我們應該儘量把跟資料庫有關的操作都搬回model，例如以下幾個情況：


## 1.把應該是在model內的邏輯搬回去


當 User 發佈 posts 時可以根據內容多寡得到虛擬幣，最多500元，controller 中寫法如下：

#### Refactor 前：

`post_controller.rb`

```ruby
def publish
  @post = Post.find(params[:id])
  @post.update(:is_published => true)
  if @post.content.size < 500
    @post.owner.money += @post.content.size
  else
    @post.owner.money += 500
  end
  redirect_to post_path(@post)
end
```
#### Refactor 後：

`post_controller.rb`

```ruby
def publish
  @post = Post.find(params[:id])
  @post.publish
  redirect_to post_path(@post)
end
```

`model/post.rb`

```ruby
def publish
  self.update(:is_published => true)
  if self.content.size < 500
    self.owner.money += self.content.size
  else
    self.owner.money += 500
  end
end
```


## 2.利用scope，把 ORM 的邏輯都整理 Model 

見 [scope介紹](scope.md)


## 3.讓 ActiveRecord 建立關聯而不是自己土法煉鋼，直接看範例：

#### Refactor 前：

```ruby
class PostsController < ApplicationController
  def create
    @post = Post.new(params[:post])
    @post.user_id = current_user
    @post.save
  end
end
```

#### Refactor 後：

```ruby
class PostsController < ApplicationController
  def create
    @post = current_user.posts.build(params[:post])
    @post.save
  end
end

class User < ActiveRecord::Base
  has_many :posts
end
```

#### 參考資料

* http://rails-bestpractices.com/posts/2-use-model-association


## 4.Use scope access

scope access可以讓我們避免掉許多不必要的判斷，請直接看例子，此例使用current_user就可以省去判斷user的情況。

#### Refactor前：

```ruby
class PostsController < ApplicationController
  def edit
    @post = Post.find(params[:id])
    if @post.user != current_user
      flash[:warning] = 'Access denied'
      redirect_to posts_url
    end
  end
end
```

#### Refactor後：

```ruby
class PostsController < ApplicationController
  def edit
    @post = current_user.posts.find(params[:id])
  end
end
```

#### 參考資料

* http://rails-bestpractices.com/posts/3-use-scope-access


## 5. use Model virtual attribute

有時候由於表單的設計方式與 Model 內的 attribute 不同，我們會需要將表單的資料拆解後再送給資料庫，例如資料庫內有 `first_name`和`last_name`但是表單只有`full_name`。

#### Refactor前：

（不好的寫法）

在 controller 裡面將 params 的資料切開，並存進資料庫：

```ruby

<% form_for @user do |f| %>
  <%= text_field_tag :full_name %>
<% end %>

class UsersController < ApplicationController
  def create
    @user = User.new(params[:user])
    @user.first_name = params([:full_name]).split(' ', 2).first
    @user.last_name = params([:full_name]).split(' ', 2).last
    @user.save
  end
end
```

#### Refactor後：

（比較好的寫法）

```ruby
class User < ActiveRecord::Base

  # 這個method可以讓表單以後要讀取full_name的attribute時可以拿到資料
  def full_name
    [first_name, last_name].join(' ')
  end
  # 這個method讓post回來的full_name拆解成first_name和last_name儲存
  def full_name=(name)
    split = name.split(' ', 2)
    self.first_name = split.first
    self.last_name = split.last
  end
end

<% form_for @user do |f| %>
  <%= f.text_field :full_name %>
<% end %>

class UsersController < ApplicationController
  def create
    @user = User.create(params[:user])
  end
end
```

如此一來 Controller 將變得超乾淨

#### 參考資料

* http://rails-bestpractices.com/posts/4-add-model-virtual-attribute

[]()

<hr>

## TODO：

6.Use model callback

[參考資料](http://rails-bestpractices.com/posts/5-use-model-callback)

7.Replace Complex Creation with Factory Method

[參考資料](http://rails-bestpractices.com/posts/6-replace-complex-creation-with-factory-method)

8.Nested Model Forms

TO BE MOVE http://waynechu.logdown.com/posts/201843-nested-model-form

[參考資料](http://rails-bestpractices.com/posts/9-nested-model-forms)
