# Active Record

## Boolean 値の保存について

例えば `JavaScript` で `POST` されたパラメータで、 `hasBooks` という `Boolean` 型の値があった場合、例え `JavaScript` で `Boolean` 型であっても、 `Rails Controller` に投げらると `String` 型になることがある。

```javascript
hasBooks = true | false
```

その場合、例えばユーザーモデルの `has_books` column にアサインしたい場合、 `has_books` column が `Boolean` 型であれば、わざわざ `String -> Boolean` という変換を行わなくて良い。

```rb:Bad
has_books = params[:hasBooks]

if has_books == "true"
  has_books = true
elsif has_books == "false"
  has_books = false
end

user.update(has_book: has_books)
```

```rb:Good
user.update(has_book: params[:hasBooks])
```
