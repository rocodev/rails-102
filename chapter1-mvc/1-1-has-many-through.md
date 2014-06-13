# has_many :through

`has_many :through`主要是在建立多對多關聯資料庫的時候使用。

例如一個「球隊」可以有很多「球員」，一個「球員」可以參加很多「球隊」，這個就是多對多關係。

在這裏球員跟球隊都是一個 Model，要建立多對多關係時我們會需要第三個 Model扮演連接的橋樑。

第三個 Model 就是「體育協會」，負責登記每個球員所屬的球隊以及球隊目前的成員。如此一來我們就可以從體育協會得知每個球隊和球員的狀況（所以叫作「through」）。


所以「球員」throuth「體育協會」has_many「球隊」，舉例：

### models/player.rb

```ruby
class Player < ActiveRecord::Base
	# 先告訴model我們在體育協會有很多筆資料
	has_many :sports_associations
  # 這些資料是要拿來判斷這個球員有參與多少球隊
	has_many :teams, :through => :sports_associations
end
```

### models/team.rb

```ruby
class Team < ActiveRecord::Base
	has_many :sports_associations
	has_many :players, :through => :sports_associations
end
```

### models/sports_associations.rb

```ruby
class SportsAssociations < ActiveRecord::Base
	#體育協會要對球員和球隊負責，所以體育球隊belongs_to球員和球隊
	belongs_to :team
	belongs_to :player
end
```

