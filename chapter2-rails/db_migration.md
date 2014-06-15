# DB migration

在 Rails 的開發流程，我們會使用 `rails g model post` 產生所需要的 model 檔案。這個指令會在 `app/model/` 下產生 post.rb，這是 model 檔案。此指令另外也會在 `db/migration/` 下產生 `(time_stamp)_create_post.rb`，這是連帶產生的 db migration 檔。

在傳統的 web application 開發流程中，並不存在 db migration 機制。開發者多半使用 phpmyadmin 開設所需要的 db 欄位。

db migration 檔的格式如下：

``` ruby
class CreatePosts < ActiveRecord::Migration
  def self.up
    create_table :posts do |t|
      t.string :title
      t.text :excerpt
      t.text :content
      t.timestamps
    end

  end

  def self.down
    drop_table :posts
  end
end
```

Rails 開發者將所需要開設的欄位加進 migration 檔案，執行 `rake db:migrate`，即可完成新增資料庫以及資料欄位的新增。

同樣的，若要對資料庫欄位進行更動，也是一樣透過 migration。`rails g migration add_user_id_to_post` 會產生一個空 migration 檔，再將所需變更寫入檔案，再次執行 `rake db:migrate` 即可：

``` ruby
class AddUserIdToPost < ActiveRecord::Migration

   def change
     add_column :users, :user_id, :integer
   end

end

```

## 資料庫欄位變更在協同開發以及佈署上所造成的問題

由其他語言剛轉換過來的開發者，對於這樣的設計通常會感覺到不習慣。透過 phyMyAdmin 就可以進行的操作，為什麼要繞了一個圈？透過 rake 和 migration 對資料庫進行操作。

在傳統開發流程中，當一個人獨自進行開發且未進行至部署階段時，開發者都不會感覺到有什麼問題。

### 問題 1: 協同開發中，程式碼與 db 欄位的不一致

但若專案陸續加入了第二位、第三位開發者，就會陷入極大的麻煩：沒有人知道現在的 db schema 長成什麼樣子。當 A 決定將 post 的 title 改成 subject 時，僅透過 phyMyAdmin 改變了 db schema，而忘了告訴 B，就將 code push 到了程式版本控制系統。而 B 根本不曉得了這一個變更，於是 B 的開發端就爆炸了，這樣的事件層出不窮。

### 問題 2: 沒有 automation 與 rollback 機制

若沒有使用 db migration 機制，在佈署時開發者必須要自己手動輸入 SQL 或透過 phpMyAdmin 變更資料欄位。而這樣的動作在程式碼與 production 環境且 db schema 差異過大時，是非常危險的：

1. 開發者可能會因為手動操作的關係打錯字，而讓線上程式炸掉
2. 因為差異過大，網站可能會有 downtime。
3. 當變更資料庫欄位後，之後發現程式其實有問題，無法輕易的恢復剛剛所作的變更。


## 對 database 進行版本控制，流程自動化且可回復

DB schema 難道是不可能被版本控制的嗎？ Rails 解決了這樣的難題：db migration 正是因此誕生的的 best practices。

透過 db migration 檔，可以紀錄資料庫每一次的欄位變遷，並且可以被版本控制。而協同開發者，在 checkout 程式碼下來之後，看到欄位發生變更，只要執行 `rake db:migration` 就可以追上資料庫最新的進度。

同時，`rake db:migrate` 的動作是全自動化的，如果在開發端能夠執行，在 production 環境上也可以重製。而 db migration 檔也提供了回復的機制，如果程式碼哪邊出現了問題，導致對應的資料庫欄位可能也要暫時改回去，只要執行 `rake db:rollback` 就可以回復到上一次變更前的狀態。


