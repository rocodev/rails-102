# begin rescue

Ruby 中例外的處理方式是靠 begin-end block 的 rescue 判斷並執行。

```ruby
begin
  # 可能會發生例外的 code
rescue AExceptionClass => some_variable
  # 屬於 AExceptionClass 的例外發生時 run 這段 code
rescue BExceptionClass => some_other_variable
  # 屬於 BExceptionClass 的例外發生時 run 這段 code
else
  # 都沒有例外發生時 run 這段 code
ensure
  # 無論有沒有發生例外，都會 run 這段 code
end
```
例外的子類別可以參考 http://www.ruby-doc.org/core-2.1.2/Exception.html

另外也可以寫成這樣：
```ruby
def foo
  # 正常時的處理
rescue
  # 發生例外時的處理
end
```


##rails中的使用

在 rails 中最常會使用到的情況是 `save!`, `create!` 這兩種指令，一般我們使用 `save` 和 `create` 只會回傳 boolean 值，但是使用 `save!` 和 `create!` 則會觸發 `ActiveRecord::RecordInvalid` 並拋出例外訊息。

ActiveRecord::RecordInvalid
```
begin
  complex_operation_that_calls_save!_internally
rescue ActiveRecord::RecordInvalid => invalid
  puts invalid.record.errors
end
```