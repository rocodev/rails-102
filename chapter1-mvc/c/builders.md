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

