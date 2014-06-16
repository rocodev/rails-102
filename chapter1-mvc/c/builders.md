# builders

builders是一種Template Handler，跟erb是很像的東西，erb會幫我們把內容轉化為瀏覽器看得懂的html或js等，而builder也是做一樣的事情，只是大家習慣使用erb作為html和js的handler，使用builder作為xml、rss、atom的handler。

補充：
>Builder templates are a more programmatic alternative to ERB. They are especially useful for generating XML content. An XmlMarkup object named xml is automatically made available to templates with a .builder extension.

所謂的more programmatic alternative to ERB應該是指它是以更程式的邏輯去generate出xml file，所以更能展現tag間彼此的相對關係的意思，見下方例子：

 app/views/topics/show.xml.builder
```builder
xml.topic do |t|
  t.title @topic.title
  t.content @topic.content
end
```
會產出這樣的xml
```xml
<topic>
  <title>Topic Title</title>
  <content>Topic Content Here</content>
</topic>
```

## JSON builder

可以參考 [jbuilder](https://github.com/rails/jbuilder) 生成 JSON 格式的資料。

## RSS Builder

RSS、ATOM 跟 Xml 是很像的東西，因為 RSS 、 ATOM 都是基於 Xml 格式的延伸應用，所以 Build 的方式跟 Xml 一樣，唯一需要注意的就是一些 RSS 規範中需要有的 Tag ，例如要有 rss version 的 tag ，並把要呈現的內容放在  channel tag 中：

app/views/topics/index.rss.builder
```builder
xml.instruct! :xml, :version => "1.0"
xml.rss :version => "2.0" do
  xml.channel do
    xml.title "Rails102"
    xml.description "Intermediate to Rails"
    xml.link root_url
    for topic in @topics
      xml.item do
        xml.title topic.title
        xml.description topic.content
        xml.pubDate topic.created_at.to_s(:rfc822)
        xml.link board_topic_url(topic.board_id, topic)
        xml.guid board_topic_url(topic.board_id, topic)
      end
    end
  end
end
```

####補充：Generate RSS URI 的方法

首先要讓 controller 可以 respond_to rss ，並且將 layout 預設為 false
```ruby
class TopicsController < ApplicationController
  def index
    @topcis = Topic.all
    respond_to do |format|
      format.html
      format.rss { render :layout => false }
    end
  end
end
```
之後再 html view 內加上 RSS 連結就完成了。
```erb
<%= link_to "+RSS", posts_url(format: "rss") %>
```
