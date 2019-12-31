# Association

## blongs_to, has_many について

Rails のアソシエーションは主従関係が成り立っている。 Active Record でアソシエーションを参照したい場合、下記の通りにする。

Good

```rb
# model/book.rb

Book belongs_to User
```

```rb
Book.where(user: user)
```

Better

```rb
# model/user.rb

User has_many Books
```

```rb
books = user.books
```
