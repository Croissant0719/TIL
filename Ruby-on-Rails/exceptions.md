# 例外処理について

参考: [【Ruby】例外処理](https://qiita.com/tsubasakat/items/6825bcefcad26da3471b)

## begin ~ rescue ~ end

```rb
def hello
  File.open( "/hello/file" )
end

begin
  hello # エラーを起こす可能性のあるコード
rescue => error # 例外オブジェクトを変数 error に代入
  puts error # 変数の値を表示
end
```

### 特殊変数

エラー内容が「特殊変数」に代入される。

|特殊変数|説明|
|:-|:-|
|$!|例外が起こった時にその例外オブジェクト(`Exception`)が代入されます。もしも複数の例外があった場合は一番最後の例外オブジェクトが代入されることになります。例外が発生しなかった場合にアクセスすると `nil` が得られます。|
|$@|例外が起こったバックトレースを配列にして代入してくれます。バックトレースとは、例外を発生させたプログラム全体の流れを追って、原因となったコードの情報を示すものです。|

### 例外オブジェクトに関するメソッド

|メソッド|説明|
|:-|:-|
|Object#class|レシーバがどのクラスのインスタンスなのかを教えてくれる。例外オブジェクトをレシーバにすると `Exception` であることが分かる。|
|Kernel.#raise|例外を発生させるモジュール関数。 (Kernel は、クラス Object にインクルードされているので、全てのクラスから使用が可能です。)|
|Exception#message|エラーメッセージを返す。|
|Exception#backtrace|例外の原因となった箇所の情報を `Array` オブジェクトの `String` 要素にして返します。 `$@` は `p $!.backtrace` と同じ意味になります。|

## begin ~ rescue ~ ensure ~ end

例外が起こっても起こらなくても実行したい時のコードがある場合、 `ensure` を使う。

```rb
# メソッド定義 引数にコピー元とコピー先を指定
def copy(from, to)
  # 指定されたコピー元ファイルを開いて代入
  src = File.open(from)
  begin
    # 指定されたコピー先ファイルを書き込みモードで開いて代入
    dst = File.open(to, "w")
    # コピー元を全て読み込んで代入
    data = src.read
    # 読み込んだコピー元をコピー先に代入
    dst.write(data)
    # コピー先ファイルを閉じる。
    dst.close
  ensure
    # 例外が起こっても起こらなくても実行したい時のコード
    # コピー元ファイルをとにかく閉じる
    src.close
  end
end
```

## rescue 修飾子

`if` や `unless` のように `rescue` も一行で書ける。例えば以下のコードでは、モジュール関数 `Integer` がエラーを起こした時、代わりに `=` の右側を全体の式と見なして 0 を代入する。

```rb
default_num = Integer(val) rescue 0
```

## 制御構造 raise

上記でも使った `raise` ですが、このメソッドを使ってエラーをどのように起こすかをコントロールできます。自分が求める条件下でエラーを発生させたり、直前に対処したエラーを再度発生させたり、例外を呼び出し元に伝える為に使ったりします。

|エラータイプ|説明|
|:-|:-|
|raise message| `RuntimeError` を発生させ、メッセージを文字列として例外オブジェクトに格納します。|
|raise error_type|指定されたエラーが起こります。|
|raise Exception, message|上のふたつを行います。指定されたエラーが起こされ、メッセージを文字列として例外オブジェクトに格納します。|
|raise| `rescue` の外では `RuntimeError` を発生させます。 `rescue` の中では、最後に起こったエラー $1 を再度起こさせます。|

```rb
# RuntimeError を発生させて
# 例外オブジェクトにメッセージを格納。
raise "Invalid Error"

# SyntaxError を発生させる。
raise SyntaxError

# 引数に文字列オブジェクトを指定すると
# それをメッセージとする RuntimeError を発生させる。
raise SyntaxError.new( "Invalid Error" )

# 引数に例外オブジェクトを指定すると
# そのエラーを発生させる。
raise Exception.new( SyntaxError )

# rescue の外では RuntimeError、
# rescue の中では最後のエラーをもう一度発生。
raise
```

### Subclasses of Exception

例外処理のサブクラス

- NoMemoryError
- ScriptError
  - LoadError
  - NotImplementedError
  - SyntaxError
- SecurityError
- SignalException
  - Interrupt
- StandardError – default for rescue
  - ArgumentError
    - UncaughtThrowError
  - EncodingError
  - FiberError
  - IOError
    - EOFError
  - IndexError
    - KeyError
    - StopIteration
  - LocalJumpError
  - NameError
    - NoMethodError
  - RangeError
    - FloatDomainError
  - RegexpError
  - RuntimeError – default for raise
    - FrozenError
  - SystemCallError
    - Errno::*
  - ThreadError
  - TypeError
  - ZeroDivisionError
- SystemExit
- SystemStackError
- fatal – impossible to rescue
