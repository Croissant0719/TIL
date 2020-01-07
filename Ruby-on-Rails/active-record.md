# Active Record

## クエリの発行

Arel を用いると、 SQL 文を Active Record のメソッドのように生成することができる。
また、簡単な `where` 句などを発行する場合などは関係ないが、テーブルを `join` したり複雑な DB 操作をする場合は、モデルのスコープに定義すると良い。

[Railsの複雑な検索はスコープを使おう](https://qiita.com/okamos/items/724a4a162dfa9e27754a)

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
